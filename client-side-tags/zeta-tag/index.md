---
title: Zeta (Zync) Tag Setup Guide
description: This article describes how to set up the Zeta (Zync) Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/zeta-tag/
---
The Zeta Marketing Platform (ZMP) combines 2.4 billion unique data identities with industry-leading AI to create personalized, omnichannel experiences that exceed expectations and drive superior marketing results. Zeta can predict intent and engagement across every channel allowing you to give consumers the personalized experience they’re looking for and drive better performance for your brand.


## Tag tips

*  Use data mappings to:
    *   Dynamically override the standard config values
    *   Dynamically override E-Commerce extension values
* Supports the E-Commerce extension for:
  * Order ID
  * Order Total
  * Order Store
  * Order Currency
  * Order Promo Code&lt;
  * List of Product IDs
  * List of Categories
  * List of Quantities

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

*   **Client Hash Key**: The client hash key
*   **Partner Hash Key**: The partner hash key
*   **Tag Short Name**: The tag short name which defines the tag type within the Zeta Marketing Platform
*   **Client Site ID**: Defines the account in the Zeta Marketing Platform

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings]().
The available categories are:

### Standard Parameters

| Variable | Description |
| --- | --- |
| Base Url (base\_url) | \[String\] |
| Client Site ID (zmpID) | \[String\] |
| Client Hash Key (c) | \[String\] |
| Partner Hash Key (p) | \[String\] |
| Tag Short Name (k) | \[String\] |
| Customer ID (CustID) | \[String\] |
| Cache Buster (Cache\_buster) | \[String\] |
| MD5 Hashed Email (e\_md5) | \[String\] |
| SHA Hashed Email (e\_sha) | \[String\] |
| GDPR (gdpr) | \[Number\] |
| GDPR Consent (gdpr\_consent) | \[String\] |

### E-Commerce

| Variable | Description |
| --- | --- |
| Order ID (OrderID) (Overrides \_corder) | \[String\] |
| Order Amount (OrderAmount) (Overrides \_ctotal) | \[Number\] |
| Order Quantity (OrderQty) | \[Number\] |
| Currency (Currency) (Overrides \_ccurrency) | \[String\] |
| Store ID (StoreID) (Overrides \_cstore) | \[String\] |
| Promo Code (promoCode) (Overrides \_cpromo) | \[String\] |
| Product ID (ProductID) (Overrides \_cprod) | \[String\] |
| Category ID (CategoryID) (Overrides \_ccat) | \[String\] |
| Cart ID (cartID) | \[String\] |
| Cart Quantity (cartQty) (Overrides \_cquan) | \[String\] |
| Cart Total (cartTotal) | \[Number\] |

### Custom

| Variable | Description |
| --- | --- |
| Custom 1 | (custom1) |
| Custom 2 | (custom2) |
| Custom 3 | (custom3) |
| Custom 4 | (custom4) |
| Custom 5 | (custom5) |
| Custom 6 | (custom6) |
| Custom 7 | (custom7) |
| Custom 8 | (custom8) |
| Custom 9 | (custom9) |
| Custom 10 | (custom10) |
| Custom 11 | (custom11) |
| Custom 12 | (custom12) |
| Custom 13 | (custom13) |
| Custom 14 | (custom14) |
| Custom 15 | (custom15) |
| Custom 16 | (custom16) |
| Custom 17 | (custom17) |
| Custom 18 | (custom18) |
| Custom 19 | (custom19) |
| Custom 20 | (custom20) |