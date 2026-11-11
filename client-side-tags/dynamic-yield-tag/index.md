---
title: Dynamic Yield Tag Setup Guide
description: This article describes how to set up the Dynamic Yield tag.
url: https://docs.tealium.com/client-side-tags/dynamic-yield-tag/
---
## Tag tips

* You can set the name and properties.
* Map parameters of a custom event in the Custom Event Data tab in the mappings toolbox.
* Conversion fires when Order ID is set.
* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Order Total (`_ctotal`)
  * Sub Total (`_csubtotal`)
  * Currency (`_ccurrency`)
  * List of Product IDs (`_cprod`)
  * List of Names `_cprodname`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)
* If the product lists contain more than one product, AddToCart and RemoveFromCart require the changed product. Map it to Product ID (`productId`) in the Parameters tab. Otherwise, the event is not sent.
* The hashed email value must be a SHA-256 hash. The tag sends it to Dynamic Yield as a customer ID of type `he`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Site ID**: Your Dynamic Yield-supplied Site ID or Site ID (`scsec`).
* **Dynamic Yield data center**: Select your Dynamic Yield data center.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|   `scsec` | String | Site ID | 
|   `cdn` | String | Your Dynamic Yield data center | 
|  `evt_list`  | [CSV/Array] | List of Events to fire | 
|   `context.type` | String | Context type | 
|  `context.data`  | Array | Context data | 
|  `context.lng`  | String | Context language, for example `en_GB` | 
|  `spa_mode`  | String | Set to `legacy` only for Dynamic Yield sections that use page-load or SPA-event detection | 

### E-Commerce

| Variable             | Type | Description |
|:-----------|:------------------------------------|:------------------------------------|
| `order_id`    | String |  Order ID (Overrides `_corder`)   | 
| `order_total`  |  Number |   Order total (Overrides `_ctotal`)     |
| `order_subtotal`     | Number |  Subtotal (Overrides `_csubtotal`)      |
| `order_currency`     | String | Currency (Overrides `_ccurrency`) |                       
| `product_id`         | Array | List of product IDs (Overrides `_cprod`) |
| `product_name`       | Array | List of names (Overrides `_cprodname`)   |
| `product_quantity`   | Array | List of quantities (Overrides `_cquan`) |
| `product_unit_price` |Array | List of prices (Overrides `_cprice`)    |

### Events

| Variable         | Description    |
|:-----------------|:---------------|
| `AddToCart`      | AddToCart      |
| `RemoveFromCart` | RemoveFromCart |
| `Search`         | Search         |
| `EmailSignup`    | EmailSignup    |
| `VideoWatch`     | VideoWatch     |
| `SyncCart`       | SyncCart       |
| `AddToWishlist`  | AddToWishlist  |
| `PromoCode`      | PromoCode      |
| `ChangeAttribute` | ChangeAttribute |
| `FilterItems`    | FilterItems    |
| `SortItems`      | SortItems      |
| `Login`          | Login          |
| `Signup`         | Signup         |
| `IdentifyUser`   | IdentifyUser   |
| `Custom`         | Custom         |

### Parameters

| Variable                     | Description              |
|:-----------------------------|:-------------------------|
| Size (`size`)                | `properties.size`        |
| Search Keywords (`keywords`) | `properties.keywords`    |
| Search Keywords (`searchKeywords`) | `properties.searchKeywords` |
| Hashed Email (`hashedEmail`) | `properties.hashedEmail` |
| Customer ID (`cuid`) | `properties.cuid` |
| Customer ID Type (`cuidType`) | `properties.cuidType` |
| Secondary Identifiers (`secondaryIdentifiers`) [Array] | `properties.secondaryIdentifiers` |
| Product ID (`productId`) | `properties.productId` |
| Quantity (`quantity`) | `properties.quantity` |
| Item Price (`itemPrice`) | `properties.itemPrice` |
| Value (`value`) | `properties.value` |
| Currency (`currency`) | `properties.currency` |
| Transaction ID (`uniqueTransactionId`) | `properties.uniqueTransactionId` |
| Promo Code (`code`) | `properties.code` |
| Attribute Type (`attributeType`) | `properties.attributeType` |
| Attribute Value (`attributeValue`) | `properties.attributeValue` |
| Filter Type (`filterType`) | `properties.filterType` |
| Filter Numeric Value (`filterNumericValue`) | `properties.filterNumericValue` |
| Filter String Value (`filterStringValue`) | `properties.filterStringValue` |
| Sort By (`sortBy`) | `properties.sortBy` |
| Sort Order (`sortOrder`) [`ASC`/`DESC`] | `properties.sortOrder` |
| Custom                       | Custom                   |

### Video Parameters

| Variable                               | Description                  |
|:---------------------------------------|:-----------------------------|
| Item ID                                | `properties.itemId`          |
| Categories (`categories`)              | `properties.categories`      |
| Autoplay (`autoplay`) [`true`/`false`] | `properties.autoplay`        |
| Progress (`progress`)                  | `properties.progress`        |
| Progress Percent (`progressPercent`)   | `properties.progressPercent` |
| Custom                                 | Custom                       |
