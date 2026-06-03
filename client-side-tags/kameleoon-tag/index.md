---
title: Kameleoon Tag Setup Guide
description: This article describes how to set up the Kameleoon tag.
url: https://docs.tealium.com/client-side-tags/kameleoon-tag/
---
## Tag Tips

* Events such as Track Product View and Track Add To Cart, which use a single item&#39;s information, pull the first available datapoint in e-commerce arrays if no mappings are present.
* Use mappings to:
  * Override standard config values and set parameters.
  * Trigger events.
  * Set event specific parameters.
* Supports the following E-Commerce extension values:
  * Order Total
  * List of SKUs
  * List of Product IDs
  * List of Names
  * List of Brands
  * List of Categories
  * List of Quantities
  * List of Prices

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Site Code**: Your unique site code provided by Kameleoon.
* **Iframe URL**: The URL to your self-hosted Iframe.
* **Use Cross Domain Tracking Iframe**: Use the cross-domain tracking Iframe.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable                | Description                             |
|:------------------------|:----------------------------------------|
| `site_code`             | Site code.                              |
| `use_iframe`            | Use cross domain tracking Iframe.       |
| `iframe_url`            | Iframe URL.                             |
| `eventName`             | Custom event name.                      |
| `redirectionURL`        | Redirection URL.                        |
| `goalNameOrID`          | Goal name or ID.                        |
| `revenue`               | Goal revenue.                           |
| `name`                  | Name.                                   |
| `value`                 | Custom data value.                      |
| `overwriteIfCollection` | Overwrite custom data if collection.    |
| `experimentID`          | Experiment ID.                          |
| `variationID`           | Variation ID.                           |
| `override`              | Override assigned variation.            |
| `productId`             | Product ID.                             |
| `productName`           | Product name.                           |
| `categoryId`            | Product category ID.                    |
| `category`              | Product category name.                  |
| `mainImageURL`          | Product main image URL.                 |
| `unitPrice`             | Product unit price.                     |
| `quantity`              | Product quantity.                       |
| `available`             | Product available.                      |
| `brand`                 | Product brand.                          |
| `child`                 | Product for child.                      |
| `gender`                | Product gender.                         |
| `type`                  | Product type.                           |
| `feature`               | Product feature.                        |
| `sku`                   | Product SKU.                            |

### E-Commerce

| Variable             | Type   | Description                                     |
|:---------------------|:-------|:------------------------------------------------|
| `order_total`        | Number | Order total (overrides `_ctotal`).              |
| `product_id`         | Array  | List of product IDs (overrides `_cprod`).       |
| `product_name`       | Array  | List of product names (overrides `_cprodname`). |
| `product_sku`        | Array  | List of SKUs (overrides `_csku`).               |
| `product_brand`      | Array  | List of brands (overrides `_cbrand`).           |
| `product_category`   | Array  | List of categories (overrides `_ccat`).         |
| `product_quantity`   | Array  | List of quantities (overrides `_cquan`).        |
| `product_unit_price` | Array  | List of prices (overrides `_cprice`).           |


### Event Parameters

| Variable                      | Description                 |
|:------------------------------|:----------------------------|
| `enable_legal_consent`        | Enable legal consent.       |
| `disable_legal_consent`       | Disable legal consent.      |
| `enable_single_page_support`  | Enable single page support. |
| `load`                        | Load.                       |
| `process_redirect`            | Process redirect.           |
| `cancel_conversion`           | Cancel conversion.          |
| `process_conversion`          | Process conversion.         |
| `reset_custom_data`           | Reset custom data.          |
| `set_custom_data`             | Set custom data.            |
| `trigger`                     | Trigger.                    |
| `track_add_to_cart`           | Track add to cart.          |
| `track_category_view`         | Track category view.        |
| `track_product_view`          | Track product view.         |
| `track_transaction`           | Track transaction.          |
| `assign_variation`            | Assign variation.           |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event                        | Description                          |
|:-----------------------------|:-------------------------------------|
| `eventName`                  | Custom event name.                   |
| `redirectionURL`             | Redirection URL.                     |
| `goalNameOrID`               | Goal name or ID.                     |
| `revenue`                    | Goal revenue.                        |
| `value`                      | Custom data value.                   |
| `overwriteIfCollection`      | Overwrite custom data if collection. |
| `experimentID`               | Experiment ID.                       |
| `variationID`                | Variation ID.                        |
| `override`                   | Override assigned variation.         |
| `productId`                  | Product ID.                          |
| `productName`                | Product name.                        |
| `categoryId`                 | Product category ID.                 |
| `category`                   | Product category name.               |
| `mainImageURL`               | Product main image URL.              |
| `unitPrice`                  | Product unit price.                  |
| `quantity`                   | Product quantity.                    |
| `available`                  | Product available.                   |
| `brand`                      | Product brand.                       |
| `child`                      | Product for child.                   |
| `gender`                     | Product gender.                      |
| `type`                       | Product type.                        |
| `feature`                    | Product feature.                     |
| `sku`                        | Product SKU.                         |