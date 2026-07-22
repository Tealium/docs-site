---
title: Spotify Pixel Tag Setup Guide
description: This article describes how to set up the Spotify Pixel Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/spotify-pixel-tag/
---
This article describes how to set up the Spotify Pixel tag.

Spotify provides transparent impression reporting in real-time across hosting providers so advertisers can understand how their campaigns are pacing and the number of households they are reaching. Spotify connects podcast downloads to on-site activity, giving advertisers and publishers unprecedented insights into the effectiveness of their podcast advertising campaigns.

## Tag tips

* Use mappings to override Standard parameters.
* Supported E-Commerce extension parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Spotify Pixel ID**: Spotify Pixel ID that is unique to each client

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `spotify_id`  | String | Spotify Pixel ID |
|  `value`  | Number | Value |
|  `discount_code`  | String | Discount code | 
|  `category`  | String | Category |
|  `type`  | String | Type |
|  `id`  | String | Hashed internal ID | 

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `order_id` (Overrides `_corder`)  | String | Order ID |
|  `order_subtotal` (Overrides `_csubtotal`)  | String | Order sub total |
|  `currency` (Overrides `_ccurrency`)  | String | Order currency |
|  `order_coupon_code` (Overrides `_cpromo`)  | String | Discount code |
|  `order_total` (Overrides `_ctotal`)  | String | Order total |
|  `is_new_customer`  | Boolean | Is new customer |
|  `product_unit_price`  | Array of numbers | Product unit price |
|  `quantity`  | Array of numbers | Product quantity |
|  `product_id`  | Array | Product ID |
|  `product_name`  | Array | Product name |
|  `product_type`  | Array | Product type |
|  `product_vendor`  | Array | Product vendor |
|  `variant_id`  | Array | Variant ID |
|  `variant_name`  | Array | Variant name |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|  `alias` | Alias |
|  `lead` | Lead |
|  `product` | Product |
|  `addtocart` | Add to cart |
|  `checkout` | Check out |
|  `purchase` | Purchase |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `spotify_id` | Spotify Pixel ID  |
| `value` | Value (`value`) |
| `discount_code` | Discount code  |
| `category` | Category |
| `type` | Type | 
| `id` | Hashed internal ID  |
| `order_id` | Order ID  |
| `order_subtotal` | Order Sub Total  | 
| `currency` | Order currency  |
| `order_coupon_code` |  Discount code  |
| `order_total` | Order total  |
| `is_new_customer` | Is new customer  |
| `product_unit_price` | Product unit price  |
| `quantity` | Product quantity  | 
| `product_id` | Product ID |
| `product_name` | Product name  |
| `product_type` | Product type  |
| `product_vendor` | Product vendor  |
| `variant_id` | Variant ID | 
| `variant_name` |  Variant name |
| `alias` | Alias | 
| `lead` | Lead | 
| `product` | Product | 
| `addtocart` | Add to cart |
| `checkout` | Check out |
| `purchase` | Purchase |