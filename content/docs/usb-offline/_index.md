---
title: USB-Based Offline License Management
weight: 30
---

![USB Offline Placeholder Image](PLACEHOLDER_FOR_IMAGE)

---

## What is USB-Based License Management?

USB-based license management allows you to distribute and enforce licenses in environments without internet connectivity (air-gapped systems). The license is physically tied to a USB device, ensuring that the software can only run when the authorized physical key is present.

This is a specific implementation of [Offline Validation]({{< ref "/docs/license-lifecycle" >}}) that uses the USB drive as a hardware anchor.

---

## When to Use This

*   **Air-Gapped Systems**: High-security facilities or industrial environments with no network access.
*   **Industrial Control Systems**: PLCs, SCADA, or control terminals where stability is paramount.
*   **Field Deployments**: Research stations or remote sites where connectivity is unreliable.
*   **Portable Licenses**: Allowing users to take their software license from machine to machine on a physical key.
*   **Multi-Machine Licenses**: Managing several licenses across different machines via physical distribution.

---

## How It Works

The system relies on a cryptographically signed **Offline License File** (`.lic`) stored on a USB drive.

### 1. Hardware Anchor
The license file is typically bound to a unique identifier of the USB drive (e.g., Serial Number or UUID). The SDK verifies that the file is being read from the correct physical device.

### 2. Cryptographic Security
Every offline license uses **RSA-4096 signatures**. This ensures that the license data (expiry, features, status) cannot be modified by the user. If a single byte is changed, the validation will fail.

### 3. State Enforcement
Even without a connection, the [License State Machine]({{< ref "/docs/license-lifecycle" >}}) is enforced. The embedded `expires_at` and `status` fields determine whether the software continues to run.

---

## Key Benefits

*   **No Internet Required**: Total independence from network availability.
*   **Physical Control**: Hardware-level security through physical possession.
*   **Portable**: Easily move the license between different workstations.
*   **Secure**: Uses industry-standard RSA-4096-SHA256 signatures.
*   **Simple Deployment**: Just copy the license file to the root of the USB key.

---

## Implementation Steps

### 1. Create a Product
First, ensure your [Product]({{< ref "/docs/admin-portal/products" >}}) is configured in the Admin Portal with "Offline Support" enabled.

### 2. Generate the Offline License
Use the [Offline License Generator]({{< ref "/docs/admin-portal/generators" >}}) or the API to create a signed license file. You will need to provide the target Hardware ID (HWID) or USB identifier if binding is required.

### 3. Deploy to USB
Place the generated `.lic` file onto the authorized USB drive.

### 4. SDK Integration
Integrate one of our SDKs into your application. Configure the SDK to look for the license file on the mounted USB path.

---

## Related Pages

*   [License Lifecycle]({{< ref "/docs/license-lifecycle" >}}) — Understand the different states of a license.
*   [Generators]({{< ref "/docs/admin-portal/generators" >}}) — How to create offline licenses at scale.
*   [Products]({{< ref "/docs/admin-portal/products" >}}) — Configuring your products for offline use.
*   [Activations]({{< ref "/docs/admin-portal/activations" >}}) — Managing existing license activations.

---

## How to Access

**Navigation**: Admin Portal → **Products** → [Select Product] → **Generate Offline License**
**SDK Configuration**: Set the `public_key_file` path to the locally stored public key for verification.
