---
title: Impact Universal Tracking Tag Setup Guide
description: This article describes how to set up the Impact Universal Tracking tag.
url: https://docs.tealium.com/client-side-tags/impact-universal-tracking-tag/
---
## Tag tips

* Map the variable that contains the SHA1 hash of the customer&#39;s email to `customerEmail`. Unhashed email addresses are removed from Impact tracking calls.
* Custom mappings pass in the properties object of the Impact tracking call.
* This tag supports the following E-Commerce extension parameters:
    * Order ID (`_corder`)
    * Order subtotal (`_csubtotal`)
    * Order shipping (`_cship`)
    * Order tax (`_ctax`)
    * Order currency (`_ccurrency`)
    * Order promo code (`_cpromo`)
    * Customer ID (`_ccustid`)
    * Customer city (`_ccity`)
    * Customer state (`_cstate`)
    * Customer zip code (`_czip`)
    * Customer country (`_ccountry`)
    * List of product names (`_cprodname`)
    * List of product SKUs (`_csku`)
    * List of product brands (`_cbrand`)
    * List of product categories (`_ccat`)
    * List of product subcategories (`_ccat2`)
    * List of product quantities (`_cquan`)
    * List of product prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Unique ID**: Your Impact Unique ID.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `acid` | Unique ID |
| `actionTrackerId` | Action Tracker ID |

### E-commerce properties

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `currencyCode` | String | Currency code (Overrides `_ccurrency`). |
| `orderDiscount` | String | Order discount. |
| `orderId` | String | Order ID (Overrides `_corder`). |
| `orderPromoCode` | String | Order promo code (Overrides `_cpromo`). |
| `orderPromoCodeDesc` | String | Order promo code description. |
| `orderRebate` | String | Order rebate. |
| `orderShipping` | String | Order shipping (Overrides `_cship`). |
| `orderSubTotalPostDiscount` | String | Order subtotal post discount. |
| `orderSubTotalPreDiscount` | String | Order subtotal pre discount (Overrides `_csubtotal`). |
| `orderTax` | String | Order tax (Overrides `_ctax`). |
| `paymentType` | String | Payment type. |
| `product_brand` | `Array` | List of product brands (Overrides `_cbrand`). |
| `product_category` | `Array` | List of product categories (Overrides `_ccat`). |
| `product_deliveryType` | `Array` | List of product delivery types. |
| `product_discount` | `Array` | List of product discounts. |
| `product_mpn` | `Array` | List of product MPNs. |
| `product_name` | `Array` | List of product names (Overrides `_cprodname`). |
| `product_quantity` | `Array` | List of product quantities (Overrides `_cquan`). |
| `product_referenceId` | `Array` | List of product reference IDs. |
| `product_sku` | `Array` | List of product SKUs (Overrides `_csku`). |
| `product_subcategory` | `Array` | List of product subcategories (Overrides `_ccat2`). |
| `product_subTotal` | `Array` | List of product subtotals/prices (Overrides `_cprice`). |
| `product_promoCode` | `Array` | List of product promo codes. |
| `product_promoCodeDesc` | `Array` | List of product promo code descriptions. |
| `product_totalDiscount` | `Array` | List of product total discounts. |
| `product_totalRebate` | `Array` | List of product total rebates. |

### General properties

| Variable | Description |
|:---------|:------------|
| `callerId` | Caller ID. |
| `clickId` | Click ID. |
| `customerCity` | Customer city (Overrides `_ccity`). |
| `customerCountry` | Customer country (Overrides `_ccountry`). |
| `customerEmail` | Customer email. |
| `customerId` | Customer ID (Overrides `_ccustid`). |
| `customerPostCode` | Customer post code (Overrides `_czip`). |
| `customerRegion` | Customer region (Overrides `_cstate`). |
| `customerStatus` | Customer status. |
| `date1` | Date parameter 1. |
| `date2` | Date parameter 2. |
| `date3` | Date parameter 3. |
| `dispositionCode` | Disposition code. |
| `giftPurchase` | Gift purchase. |
| `hearAboutUs` | Hear about us. |
| `locationName` | Location name. |
| `locationType` | Location type. |
| `money1` | Money parameter 1. |
| `money2` | Money parameter 2. |
| `money3` | Money parameter 3. |
| `note` | Note. |
| `numeric1` | Numeric parameter 1. |
| `numeric2` | Numeric parameter 2. |
| `numeric3` | Numeric parameter 3. |
| `phoneNumber` | Phone number. |
| `referenceId` | Reference ID. |
| `siteCategory` | Site category. |
| `siteVersion` | Site version. |
| `test` | Test flag. |
| `text1` | Text parameter 1. |
| `text2` | Text parameter 2. |
| `text3` | Text parameter 3. |
### Options

| Variable | Description |
|:---------|:------------|
| `domReady` | DOM ready. |
| `tag` | Tag. |