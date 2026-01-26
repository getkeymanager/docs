---
title: API Documentation
weight: 1
---

# API Documentation

## Introduction

This API documentation is **generated directly from the Postman collection** and represents the
canonical source of truth for all API endpoints.

## API Fundamentals

- **Base URL:** `https://your-domain.com/api/v1`
- **Authentication:** API Key (Bearer token or form parameter)
- **Response Format:** JSON
- **API Version:** v1

## Authentication

All API requests require authentication using an API key. You can provide the API key in two ways:

1. **Authorization Header (Recommended):**
   ```
   Authorization: Bearer YOUR_API_KEY
   ```

2. **Request Parameter:**
   ```
   api_key=YOUR_API_KEY
   ```

## API Endpoints Overview

**Total Endpoints:** 39

### API Key Related Errors (1 endpoints)

- ✓ [Response Examples](errors/response-examples) - `POST /api/v1/verify` (4 examples)

### Access Restrictions (1 endpoints)

- ✓ [Blocked IP or identifier - Access denied](errors/blocked-ip-or-identifier-access-denied) - `POST /api/v1/verify` (1 examples)

### Endpoints (36 endpoints)

- ✓ [Send Telemetry](endpoints/send-telemetry) - `POST /api/v1/send-telemetry-data` (2 examples)
- ✓ [Get Telemetry](endpoints/get-telemetry) - `GET /api/v1/get-telemetry-data` (1 examples)
- ✓ [Verify  License Key](endpoints/verify-license-key) - `POST /api/v1/verify` (2 examples)
- ✓ [Activate  License Key](endpoints/activate-license-key) - `POST /api/v1/activate` (3 examples)
- ✓ [Assign License Key](endpoints/assign-license-key) - `POST /api/v1/assign-license-key` (2 examples)
- ✓ [Assign And Activate License Key](endpoints/assign-and-activate-license-key) - `POST /api/v1/assign-and-activate-license-key` (1 examples)
- ✓ [Random Assign License Keys](endpoints/random-assign-license-keys) - `POST /api/v1/random-assign-license-keys` (4 examples)
- ✓ [Random Assign License Keys Queued](endpoints/random-assign-license-keys-queued) - `POST /api/v1/random-assign-license-keys-queued` (1 examples)
- ✓ [Deactivate  License Key](endpoints/deactivate-license-key) - `POST /api/v1/deactivate` (2 examples)
- ✓ [Get License Key Details](endpoints/get-license-key-details) - `POST /api/v1/get-license-key-details` (2 examples)
- ✓ [Access Downloadables](endpoints/access-downloadables) - `POST /api/v1/access-downloadables` (1 examples)
- ✓ [Create License Keys](endpoints/create-license-keys) - `POST /api/v1/create-license-keys` (1 examples)
- ✓ [Update License Key](endpoints/update-license-key) - `POST /api/v1/update-license-key` (1 examples)
- ✓ [Delete License Key](endpoints/delete-license-key) - `POST /api/v1/delete-license-key` (1 examples)
- ✓ [Create Product](endpoints/create-product) - `POST /api/v1/create-product` (3 examples)
- ✓ [Update Product](endpoints/update-product) - `POST /api/v1/update-product` (2 examples)
- ✓ [Delete Product](endpoints/delete-product) - `POST /api/v1/delete-product` (1 examples)
- ✓ [Create License Key Meta](endpoints/create-license-key-meta) - `POST /api/v1/create-license-key-meta` (2 examples)
- ✓ [Update License Key Meta](endpoints/update-license-key-meta) - `POST /api/v1/update-license-key-meta` (2 examples)
- ✓ [Delete License Key Meta](endpoints/delete-license-key-meta) - `POST /api/v1/delete-license-key-meta` (1 examples)
- ✓ [Create Product Meta](endpoints/create-product-meta) - `POST /api/v1/create-product-meta` (2 examples)
- ✓ [Update Product Meta](endpoints/update-product-meta) - `POST /api/v1/update-product-meta` (2 examples)
- ✓ [Delete Product Meta](endpoints/delete-product-meta) - `POST /api/v1/delete-product-meta` (1 examples)
- ✓ [Get All Products](endpoints/get-all-products) - `GET /api/v1/get-all-products` (1 examples)
- ✓ [Get All Generators](endpoints/get-all-generators) - `GET /api/v1/get-all-generators` (1 examples)
- ✓ [Generate](endpoints/generate) - `POST /api/v1/generate` (1 examples)
- ✓ [Get License Keys](endpoints/get-license-keys) - `GET /api/v1/get-license-keys` (1 examples)
- ✓ [Get Available License Keys Count](endpoints/get-available-license-keys-count) - `GET /api/v1/get-available-license-keys-count` (2 examples)
- ✓ [Get All Contracts](endpoints/get-all-contracts) - `GET /api/v1/get-all-contracts` (2 examples)
- ✓ [Create Contract](endpoints/create-contract) - `POST /api/v1/create-contract` (2 examples)
- ✓ [Update Contract](endpoints/update-contract) - `POST /api/v1/update-contract` (2 examples)
- ✓ [Delete Contract](endpoints/delete-contract) - `POST /api/v1/delete-contract` (2 examples)
- ⚠️ [Get Contract Info (Legacy)](endpoints/get-contract-info-legacy) - `GET /api/v1/contracts/get-info` (0 examples)
- ⚠️ [Generate Contract Licenses (Legacy)](endpoints/generate-contract-licenses-legacy) - `POST /api/v1/contracts/generate` (0 examples)
- ⚠️ [Destroy Contract License (Legacy)](endpoints/destroy-contract-license-legacy) - `POST /api/v1/contracts/destroy` (0 examples)
- ⚠️ [Destroy All Contract Licenses (Legacy)](endpoints/destroy-all-contract-licenses-legacy) - `POST /api/v1/contracts/destroy-all` (0 examples)

### Public Endpoints (1 endpoints)

- ⚠️ [Get Product Changelog](public/get-product-changelog) - `GET /api/v1/products/:slug/changelog` (0 examples)
