---
title: Products
weight: 20
---

# Products

![Admin Portal Products Screenshot](placeholder-products-overview.png)
*Screenshot will be added showing the main interface*

---

## What Is This Page?

Manage all licensable products in your platform. Each product represents software, services, or digital goods that can be licensed to customers. This is where you configure product identity, cryptography, and basic settings.

---

## When to Use This Page

Use this page to create new products before generating licenses, edit product details, configure cryptographic signing keys, upload product images for branding, manage product status, or handle product-specific settings.

---

## Key Features

- Create and manage products
- Configure RSA-4096 cryptographic keys
- Upload product images to S3
- Manage product status and environments
- Set Envato integration settings

---

## Detailed Guide

### Product List

View and manage all products in a sortable, filterable table.

![Product List Screenshot](placeholder-products-product-list.png)
*Screenshot will be added*

#### What This Shows

- **Product Name**: Display name of the product
- **Slug**: URL-friendly identifier used in APIs and URLs
- **Source**: Internal (managed in platform) or Envato (synced from Envato marketplace)
- **Status**: Active (licenses can be created) or Inactive (paused)
- **Require License**: Toggle indicating if license verification is enforced
- **Environment**: production, staging, or development
- **Created Date**: When product was added to system
- **Actions**: Edit, View, Delete buttons

#### 💡 Tips & Tricks

- Use search to quickly find products by name or slug
- Filter by environment to work on staging without affecting production
- Sort by created date to find newest products
- Bulk actions available for status changes
- Product slugs cannot be changed after creation - choose wisely!

---

### Create/Edit Product

Comprehensive form for configuring all aspects of a product.

![Create/Edit Product Screenshot](placeholder-products-create-edit-product.png)
*Screenshot will be added*

#### What This Shows

- **Basic Info**: Name, slug, description
- **Source**: Internal or Envato marketplace
- **Status**: Active or Inactive
- **Require License Toggle**: Enforce verification or allow permissive mode
- **Environment**: Isolate by development stage
- **Product Image**: Logo or branding image (stored in S3)
- **Cryptographic Settings**: Private key, passphrase, hashing algorithm
- **Metadata**: Custom key-value pairs (JSON)

#### 💡 Tips & Tricks

- Choose descriptive product names that customers will recognize
- Use kebab-case for slugs: "my-awesome-product"
- Always start in staging environment, test thoroughly, then move to production
- Keep product descriptions clear and concise
- Generate strong RSA-4096 keys - they cannot be changed easily later
- Store private key passphrase in a secure password manager
- Upload high-resolution product images (recommended: 400x400px minimum)

---

### Cryptographic Configuration

Security settings that control how licenses are signed and verified.

![Cryptographic Configuration Screenshot](placeholder-products-cryptographic-configuration.png)
*Screenshot will be added*

#### What This Shows

- **Private Key**: RSA-4096 private key for signing licenses (never shared)
- **Public Key**: Corresponding public key (embedded in your product)
- **Passphrase**: Encryption passphrase for private key storage
- **Hashing Algorithm**: SHA-256, SHA-384, or SHA-512
- **Key Rotation**: Emergency key rotation for compromised keys

#### 💡 Tips & Tricks

- Use RSA-4096 for maximum security
- Store private keys securely - they should NEVER leave this system
- Use SHA-512 for strongest hashing (SHA-256 acceptable for compatibility)
- Implement key rotation only in emergency - requires product updates
- Test key configuration in staging before deploying to production
- Keep backup of public key in version control with your product code

---

### Product Images & Branding

Upload and manage product images used throughout the platform.

![Product Images & Branding Screenshot](placeholder-products-product-images-&-branding.png)
*Screenshot will be added*

#### What This Shows

- Current product image preview
- Upload button for new image
- Image dimensions and file size
- CDN URL for image

#### 💡 Tips & Tricks

- Use PNG or JPG format
- Recommended size: 400x400px or larger
- Keep file size under 2MB
- Use transparent backgrounds for PNG
- Images are stored in S3 and served via CDN
- Images appear in: Admin UI, Client Portal, Public Changelog, Email Templates

---

## Common Tasks

Here are the most frequent operations you'll perform on this page:

1. Create a new product before generating licenses
2. Update product descriptions for customer-facing displays
3. Upload or replace product images
4. Toggle product status for maintenance
5. Rotate cryptographic keys in emergency situations
6. Configure Envato sync for marketplace products

---

## ✅ Best Practices

- Create products in staging first, verify everything works, then create in production
- Use consistent naming conventions across products
- Document your cryptographic keys in a secure location
- Test license verification with every new product before going live
- Keep product images consistent in size and style
- Use inactive status instead of deleting products
- Enable "Require License" toggle only after testing

---

## ❗ Troubleshooting

### Cannot create license for product

**Solution**: Verify product status is Active. Check that a generator is configured for this product. Ensure you're in the correct environment.

### Image upload fails

**Solution**: Check S3 credentials in Settings > S3. Verify file size is under 2MB. Ensure S3 bucket has write permissions. Try different image format.

### License verification fails after key change

**Solution**: Key changes require product update. All existing licenses use old key. Create new licenses with new key. Consider key rotation strategy.

---

## Related Documentation

- See [License Generators](../generators) to configure how licenses are created
- See [Settings](../settings) for S3 configuration
- See [Downloadables](../downloadables) to add product files

---

## How to Access

1. Log in to the Admin Portal with your admin credentials
2. Click **Products** in the main navigation menu
3. The page will load showing the main interface

**Keyboard Shortcut**: Press `Ctrl+K` (Windows) or `Cmd+K` (Mac) to open Global Search, then type the page name.

---

## Related Pages

- [Dashboard](../dashboard) - Main overview and KPIs
- [Settings](../settings) - System configuration
- [Profile](../profile) - Your admin profile and security
