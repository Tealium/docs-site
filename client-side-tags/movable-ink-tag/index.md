---
title: Movable Ink Studio Tag Setup Guide
description: This article describes how to configure the Movable Ink Studio tag in your iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/movable-ink-tag/
---
The tracking implementation involves two complementary scripts:

* **Behavior Tracking Script**: Loads on every tracked page.
* **Conversion Tracking Script**: Loads only on order confirmation or conversion pages. This happens automatically when an order ID is set.

Both scripts are asynchronous and don&#39;t impact site performance.

### Behavior tracking

The Studio behavior script sends a pageview event on every page where it is installed. You do not need to map event parameters for page views. The beacon includes the page URL and links activity to the visitor profile.

Conversions use the E-commerce extension to trigger `addProduct`, `addPromo`, and conversion events. Studio does not support event-specific parameter mapping. This differs from the Movable Ink Da Vinci tag, which uses an explicit event model.

## Requirements

The Movable Ink Studio tag requires the following:

* Your tracking subdomain from your Movable Ink account configuration.
* Merge tags in your email service provider (ESP) for a unique user ID and a campaign ID.

## Validate and test

Use the [Movable Ink Behavior Tracking Chrome extension](https://chromewebstore.google.com/detail/movable-ink-behavior-trac/icfallhogjlkfkcojmplakniiofcllgi?hl=en-US) to validate behavior tracking and sitemap configuration.

In the Movable Ink Studio analytics dashboard, verify conversions and product parameters are received and processed correctly.

## Tag tips

* Conversion tracking occurs automatically when an order ID is provided.
* Supports the E-Commerce extension for:  
    * Order ID (`identifier`)  
    * Order total (`revenue`)  
    * List of product SKUs (`sku`)  
    * List of product names (`name`)  
    * List of product quantities (`quantity`)  
    * List of product prices (`price`)
* Use mappings to:  
    * Pass array of promo codes (`promo_code`)  
    * Pass array of promo descriptions (`promo_description`)  
    * Pass array of other product data (`other_product_data`)  
    * Dynamically override the E-Commerce extension and tracking subdomain values

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags]().

When adding the tag, configure the following settings:

* **Tracking Subdomain**: The tracking subdomain for your Movable Ink account.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `tracking_subdomain` | Tracking subdomain. |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_id` | `String` | Order ID (Overrides `_corder`). |
| `order_total` | `Number` | Order total (Overrides `_ctotal`). |
| `product_name` | `Array` | List of product names (Overrides `_cprodname`). |
| `product_sku` | `Array` | List of product SKUs (Overrides `_csku`). |
| `product_quantity` | `Array` | List of product quantities (Overrides `_cquan`). |
| `product_price` | `Array` | List of product prices (Overrides `_cprice`). |
| `other_product_data` | `Array` | Other product data. |
| `promo_code` | `Array` | List of promo codes. |
| `promo_description` | `Array` | List of promo descriptions. |