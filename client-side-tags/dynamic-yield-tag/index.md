---
title: Dynamic Yield Tag Setup Guide
description: This article describes how to set up the Dynamic Yield tag.
url: https://docs.tealium.com/client-side-tags/dynamic-yield-tag/
---
## Tag Tips

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

## Tag Configuration

First, go to Tealium's tag marketplace and add the Dynamic Yield tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Site ID**: Your Dynamic Yield-supplied Site ID or Site ID (`scsec`).
* **Dynamic Yield data center**: Select your Dynamic Yield data center.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|   `scsec` | String | Site ID | 
|   `cdn` | String | Your Dynamic Yield data center | 
|  `evt_list`  | [CSV/Array] | List of Events to fire | 
|   `context.type` | String | Context type | 
|  `context.data`  | Array | Context data | 

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
| `Custom`         | Custom         |

### Parameters

| Variable                     | Description              |
|:-----------------------------|:-------------------------|
| Size (`size`)                | `properties.size`        |
| Search Keywords (`keywords`) | `properties.keywords`    |
| Hashed Email (`hashedEmail`) | `properties.hashedEmail` |
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
