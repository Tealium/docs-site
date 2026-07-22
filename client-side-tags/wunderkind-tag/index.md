---
title: Wunderkind Tag Setup Guide
description: This article describes how to set up the Wunderkind tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/wunderkind-tag/
---
## Tag tips

Use mappings to:

* Dynamically override `website_id`.
* Dynamically override the E-Commerce extension values listed below.
* Set values for other required and optional parameters.

Required parameters to trigger conversion events:

* Order ID 
* Customer ID/Email
* Goal
* Currency
* Tax Amount
* Shipping Amount
* Sub Total/Amount
* Product SKU

This tag supports the following E-Commerce extension values:

* Order ID (goes to `order_id`)
* Order Subtotal (goes to `amount`)
* Customer ID (goes to `email`)
* Currency
* Promo Code (goes to `coupon`)
* Product/Item IDs
* Product/Item SKUs
* Product/Item Quantities
* Product/Item Price
* Tax Amount
* Shipping Amount

If you are using the E-Commerce extension and have it configured to use the values above, you do not need to set up mappings for these parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Website ID**: Your Wunderkind Website ID. Sometimes referred to as Client ID.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| **Variable** | **Description** |
|:---------|:------------|
| `website_id` | Website ID |
| `phone` | Phone |
| `goal` | Goal |
| `transaction_origin` | Transaction origin |
| `total_discount` | Total discount |
| `pay_method` | Payment method |

### E-Commerce

| **Variable** | **Description** | **Data Type** |
|:---------|:------------|:------------|
| `order_id` | Order ID (overrides `_corder`) | String |
| `customer_id` | Customer ID (overrides `_ccustid`) | String |
| `order_subtotal` | Sub total (overrides `_csubtotal`) | Integer |
| `order_currency` | Currency (overrides `_ccurrency`) | String |
| `promo_code` | Promo code (overrides `_cpromo`) | String |
| `product_id` | List of product IDs (overrides `_cprod`) | Array |
| `product_sku` | List of SKUs (overrides `_csku`) | Array |
| `product_quantity` | List of quantities (overrides `_cquan`) | Array |
| `product_unit_price` | List of prices (overrides `_cprice`) | Array |
| `order_tax` | Tax amount (overrides `_ctax`) | Array |
| `shipping_amount` | Shipping amount (overrides `_cship`) | Array |
