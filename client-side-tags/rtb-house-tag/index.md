---
title: RTB House Retargeting Tag Setup Guide
description: This article describes how to set up the RTB House Retargeting tag.
url: https://docs.tealium.com/client-side-tags/rtb-house-tag/
---
## Tag tips

* Supports the following [E-Commerce extension]() parameters:
    * Offer ID (`_cprod`)
    * Conversion ID (`_corder`)
    * Conversion Value (`_ctotal`)
    * Category ID (`_ccat`)
* UID should be an anonymized user ID (for example, based on the user email or login). If none is provided, the tag will send the value `unknown`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tagging Hash**: Your RTB House Tagging Hash.
* **Region Subdomain**: Your RTB House Region Subdomain.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `eventType`  | String | Event Type |
|  `size`  | String | Size |
|  `uid`  | String | UID |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `offerId`  | String | Offer ID
|  `offerIds` (Overrides `_cprod`)  | Array of Strings | Offer IDs|
|  `conversionClass`  | String | Conversion Class | 
|  `conversionSubClass`  | String | Conversion Sub Class |
|  `conversionId` (Overrides `_corder`)  | String | Conversion ID |
|  `conversionValue` (Overrides `_ctotal`)  | String | Conversion Value |
| `categoryId`  | String | Category ID  |

### Events

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Description |
|:---------|:------------|
| `home` | Home | 
| `category` | Category | 
| `sales` | Sale or Promo | 
|  `newoffers` | New products |
| `offer` | Product | 
| `wishlist` | Add to wish list or favourites | 
| `size` | Product Size Selection | 
| `offlinecheck` | Offline Store Checking | 
|  `listing` | Search Result |
| `basketadd` | Shopping Cart - Add To Cart | 
| `basketstatus` | Shopping Cart - Status | 
| `startorder` | Order Process Start | 
|  `conversion` |Order Confirmation |
|  `custom` |Custom |

### Event-specific Parameters

Use this category to map parameters only for the selected event.

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

