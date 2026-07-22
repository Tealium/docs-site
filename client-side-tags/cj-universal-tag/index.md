---
title: CJ Universal Tag Setup Guide
description: This article describes how to set up the CJ Universal tag.
url: https://docs.tealium.com/client-side-tags/cj-universal-tag/
---
The CJ Universal Tag provides complete tracking protection and maintains program integrity across browsers with tracking restrictions, including Chrome, Safari, and Firefox. This next-generation tag helps you succeed in the CJ network by enabling advanced tracking features, such as Vertical Attributes for Situational Commissioning and transaction-level insights. The Universal Tag also serves as the foundation for future enhancements, including Affiliate Incrementality and Cross-Channel Customer Journey reporting.

## Tag Tips

* Conversion Tag is present when Order ID is set.
* CJ's Client Integration Team recommends this tag not be bundled.
* Supports these E-Commerce extension parameters:
    * Order ID (`_corder`)
    * Sub Total (`_csubtotal`)
    * Currency (`_ccurrency`)
    * Customer ID (`_ccustid`)
    * List of Product IDs (`_cprod`)
    * List of Quantities (`_cquan`)
    * List of Prices (`_cprice`)
    * List of Discounts (`_cpdisc`)
* Use mappings to override or dynamically set the tag configurations.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Proxy Path**:  
Configure a reverse proxy to CJ’s servers to receive the full benefits of this integration. Example: `//yourdomain.com/proxydir/tags/<YOUR_TAG_ID>/tag.js`.
* **CJ Hosted Tag ID**:  
If you are unable set up a reverse proxy, enter your CJ Hosted Tag ID to use the CJ Hosted Tag. CJ’s Client Integration team provides this value.
Example: `//www.mczbf.com/tags/<TAG_ID>/tag.js`.
* **Action Tracker Id**:  
Static value provided by CJ’s Client Integration team.
* **CJ Enterprise Id**:  
Static value provided by CJ’s Client Integration team.
* **Enable Page Visits**:  
Enables the CJ page visit tag on all pages except the conversion page. 

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `proxyPath` | Proxy path. |
| `tagId` | CJ hosted tag ID. |
| `actionTrackerId` | Action tracker ID. |
| `enterpriseId` | CJ enterprise ID. |
| `enablePageVisit` | Boolean. Enables the page visit tag. |
| `bypassChannel.name` | Bypass channel name. |
| `bypassChannel.timestamp` | Bypass channel timestamp. |

### Page Visit

| Variable | Description |
|:---------|:------------|
| `pageType` | Page type. |
| `emailHash` | SHA-256 hash of the email address. |
| `referringChannel` |  Referring channel. |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` | Order ID (overrides `_corder`). |
| `order_subtotal` | Sub total (overrides `_csubtotal`). |
| `order_currency` | Currency (overrides `_ccurrency`). |
| `order_coupon_code` | Promo code (overrides `_cpromo`). |
| `order_discount` | Discount. |
| `customer_id` | User ID or customer ID (overrides `_ccustid`). |
| `product_id` | Array of product IDs (overrides `_cprod`). |
| `product_quantity` | Array of product quantities (overrides `_cquan`). |
| `product_unit_price` | Array of product unit prices (overrides `_cprice`). |
| `product_discount` | Array of product discounts (overrides `_cpdisc`). |
| `brand` | Brand of items purchased. |
| `brandId` | Brand identifier. |
| `category` | Category of items purchased. |
| `customerStatus` | Customer status. |
| `delivery` | Method of delivery. |
| `marketingChannel` | Marketing channel. |

### Loyalty

| Variable | Description |
|:---------|:------------|
| `loyaltyEarned` | Loyalty points earned. |
| `loyaltyFirstTimeSignup` | Loyalty first time sign up. |
| `loyaltyLevel` | Loyalty level. |
| `loyaltyRedeemed` | Loyalty points redeemed. |
| `loyaltyStatus` | Loyalty status. |
