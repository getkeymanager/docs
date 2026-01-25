# License Lifecycle & State Machine  
## Formal Specification – v1.0

> This document defines the ONLY valid lifecycle, transitions, invariants,
> and side-effects for license keys.
>
> Any implementation that violates this document is incorrect.

---

## 1. Purpose & Scope

This document specifies:

- License states
- Allowed transitions
- Forbidden transitions
- Preconditions & postconditions
- Side-effects (audits, events, jobs)
- Admin, API, and Client Portal behavior
- Explainability rules (“Why is this license invalid?”)

This specification applies to:
- Admin Dashboard
- Public API
- Client Self-Service Portal
- Offline validation logic
- SDK implementations

---

## 2. License as a State Machine (Foundational)

A license key is a **stateful entity**.

It MUST always be in exactly **one** of the following states.

```
→ available
→ assigned
→ active
→ suspended
→ expired
→ revoked
```

---

## 3. State Definitions (Authoritative)

### 3.1 AVAILABLE

**Meaning**
- License exists but is not owned or used.

**Characteristics**
- Not assigned to a customer
- No activations allowed
- No downloads allowed
- Can be deleted (soft delete only)

**Entry Conditions**
- Created manually
- Created via generator
- Created via contract

---

### 3.2 ASSIGNED

**Meaning**
- License is owned by a customer but not activated.

**Characteristics**
- Assigned to customer_id
- Zero activations
- Downloads MAY be allowed (product setting)
- Offline file MAY be generated (inactive)

**Entry Conditions**
- Manual assignment
- Random assignment
- Contract assignment

---

### 3.3 ACTIVE

**Meaning**
- License has at least one valid activation.

**Characteristics**
- ≥ 1 active activation
- Activation limit enforced
- Feature flags enforced
- Downloads allowed
- Telemetry accepted

**Entry Conditions**
- Successful activation request
- Idempotent activation replay

---

### 3.4 SUSPENDED

**Meaning**
- License temporarily disabled without destruction.

**Characteristics**
- Activations blocked
- Existing activations invalid
- Offline validation fails
- Used for:
  - Payment issues
  - Abuse
  - Manual admin intervention

**Entry Conditions**
- Manual admin action
- Automated abuse detection
- Contract suspension

---

### 3.5 EXPIRED

**Meaning**
- License validity period has ended.

**Characteristics**
- Activations blocked
- Offline validation fails
- Existing activations invalid
- Downloads blocked
- Telemetry accepted (flagged)

**Entry Conditions**
- Expiry date reached
- Grace period exceeded

---

### 3.6 REVOKED

**Meaning**
- License permanently invalidated.

**Characteristics**
- Irreversible
- Cannot be reactivated
- Offline validation fails permanently
- Used for:
  - Fraud
  - Refunds
  - Security compromise

**Entry Conditions**
- Manual admin action
- Contract termination
- Emergency revocation

---

## 4. Allowed Transitions (STRICT)

| From → To     | Allowed | Trigger |
|--------------|---------|--------|
| available → assigned | ✅ | Assign |
| assigned → active | ✅ | Activate |
| active → suspended | ✅ | Admin / System |
| suspended → expired | ✅ | Time-based |
| active → expired | ✅ | Time-based |
| expired → revoked | ✅ | Admin |
| suspended → revoked | ✅ | Admin |

---

## 5. Forbidden Transitions (MUST FAIL)

The following transitions MUST throw explicit errors:

- assigned → available
- active → assigned
- expired → active
- revoked → any
- suspended → active
- available → active (without assignment)

**Rule**
> No backward or skipping transitions are allowed.

---

## 6. Transition Preconditions & Side Effects

### 6.1 available → assigned

**Preconditions**
- License not deleted
- Product active
- Environment matches

**Side Effects**
- Set customer_id
- Audit trail created
- Optional email sent
- Webhook (license_assigned)

---

### 6.2 assigned → active

**Preconditions**
- Activation limit not exceeded
- Identifier present
- License not expired
- License not suspended or revoked

**Side Effects**
- Activation created
- Audit trail created
- Webhook (license_activated)
- Telemetry enabled

---

### 6.3 active → suspended

**Preconditions**
- Admin or automated system trigger

**Side Effects**
- All activations invalidated
- Audit trail created
- Webhook (license_suspended)

---

### 6.4 active → expired

**Preconditions**
- Expiry date reached

**Side Effects**
- Activations invalidated
- Audit trail created
- Webhook (license_expired)

---

### 6.5 expired → revoked

**Preconditions**
- Admin or system trigger

**Side Effects**
- Permanent invalidation
- Audit trail created
- Webhook (license_revoked)

---

## 7. Idempotency Rules

All transitions MUST be idempotent.

Examples:
- Re-activating an active license returns success without duplication
- Assigning an already assigned license returns stable response
- Re-suspending a suspended license returns stable response

**Implementation Rule**
> Same Idempotency-Key → Same result → No side effects duplicated

---

## 8. Activation-Level Rules

Activations are subordinate to license state.

| License State | Activation Allowed |
|-------------|-------------------|
| available | ❌ |
| assigned | ❌ |
| active | ✅ |
| suspended | ❌ |
| expired | ❌ |
| revoked | ❌ |

---

## 9. Offline Validation Rules

Offline validation MUST:

1. Verify RSA-4096 signature
2. Verify license state
3. Verify expiry (±24h tolerance)
4. Verify HWID / domain
5. Enforce feature flags

**If ANY check fails → INVALID**

---

## 10. Explainability (“Why Is This License Invalid?”)

Every invalid response MUST map to:

- Invalid state
- Failed rule
- Relevant timestamp
- Activation count
- Environment mismatch

This data powers:
- Admin UI explainability
- Support diagnostics
- SDK error messages

---

## 11. Role-Based Behavior

### Admin
- Can force any allowed transition
- Cannot bypass forbidden transitions
- All actions audited

### API
- Can only trigger transitions via valid endpoints
- Must obey idempotency
- Permission-scoped

### Client Portal
- Can only:
  - View state
  - Deactivate own activations
- Cannot change license state directly

---

## 12. Audit & Compliance (MANDATORY)

EVERY transition MUST generate:

- Audit record
- Before state snapshot
- After state snapshot
- Actor identity
- Request ID
- Timestamp

Audit trails are immutable.

---

## 13. Failure Handling Rules

Failures MUST:
- Be explicit
- Return deterministic error codes
- Leave license state unchanged
- Still generate audit logs if applicable

---

## 14. Invariants (MUST ALWAYS HOLD)

- A license has exactly one state
- A revoked license can never be reactivated
- Activations never outlive license validity
- Offline validation matches online behavior
- State machine is the single source of truth

---

## 15. Final Enforcement Rule

If any code:
- Skips a state
- Mutates state directly
- Bypasses audits
- Allows forbidden transitions

→ That code is INVALID.

END OF LICENSE LIFECYCLE SPECIFICATION
