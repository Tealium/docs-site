---
title: The Trade Desk Real-Time Conversion Events Tag Setup Guide
description: This article describes how to set up the The Trade Desk Real-Time Conversion Events tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/the-trade-desk-real-time-conversion-events-tag/
---
## Tag tips

* Purchase tracking occurs automatically when an order ID is populated.
* You may enter a comma-separated list of Event Tracking IDs in the Event Tracking ID field.
* Use mapping to:
    * Dynamically set the tag configurations
    * Override the E-Commerce extension values
* Supports these E-Commerce extension parameters:
    * Order ID
    * Sub Total
    * Currency
    * List of product IDs
    * List of product categories
    * List of product prices
    * List of product quantities
    * List of product names

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags]().

When adding the tag, configure the following settings:

* **Merchant ID**: Your merchant ID is provided by The Trade Desk during the onboarding process.
* **Event Tracking ID**: An event tracking tag ID (or comma-separated list of IDs) configured in the platform UI (`pixel_id`). For more information, see [The Trade Desk: Real-Time Conversion Events](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Tag configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pixel_id` | String | Event tracking ID. |
| `merchant_id` | String | Merchant ID. |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_id` | String | Order ID (Overrides `_corder`). |
| `value` | String | Sub Total (Overrides `_csubtotal`). |
| `currency` | String | Currency (Overrides `_ccurrency`). |
| `items.cat` | Array | List of product categories (Overrides `_ccat`). |
| `items.item_code` | Array | List of product IDs (Overrides `_cprod`). |
| `items.name` | Array | List of product names (Overrides `_cprodname`). |
| `items.qty` | Array | List of product quantities (Overrides `_cquan`). |
| `items.price` | Array | List of product prices (Overrides `_cprice`). |

### User data

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `country` | String | Country. |
| `region` | String | Region. |
| `metro` | String | Metro. |
| `city` | String | City. |
| `zip` | String | Zip. |

### Events

For more information on how to map events, see [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `addtocart` | Add to cart. |
| `purchase` | Purchase. |
| `viewitem` | View item. |
| `searchitem` | Search item. |
| `searchcategory` | Search category. |
| `login` | Login. |
| `messagebusiness` | Message business. |
| `direction` | Direction. |
| `startcheckout` | Start checkout. |
| `viewcart` | View cart. |
| `sitevisit` | Site visit. |
| `wishlistitem` | Wish list item. |

### Event-specific parameters

For more information on how to map events, see [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `pixel_id` | Event tracking ID. |
| `merchant_id` | Merchant ID. |
| `order_id` | Order ID. |
| `value` | Sub Total. |
| `currency` | Currency. |
| `items.item_code` | List of product IDs. |
| `items.name` | List of product names. |
| `items.qty` | List of product quantities. |
| `items.price` | List of product prices. |
| `country` | Country. |
| `region` | Region. |
| `metro` | Metro. |
| `city` | City. |
| `zip` | Zip. |
| `td1` | Custom parameter td1. |
| `td2` | Custom parameter td2. |
| `td3` | Custom parameter td3. |
| `td4` | Custom parameter td4. |
| `td5` | Custom parameter td5. |
| `td6` | Custom parameter td6. |
| `td7` | Custom parameter td7. |
| `td8` | Custom parameter td8. |
| `td9` | Custom parameter td9. |
| `td10` | Custom parameter td10. |
| `addtocart` | Add to cart. |
| `purchase` | Purchase. |
| `viewitem` | View item. |
| `searchitem` | Search item. |
| `searchcategory` | Search category. |
| `login` | Login. |
| `messagebusiness` | Message business. |
| `direction` | Direction. |
| `startcheckout` | Start checkout. |
| `viewcart` | View cart. |
| `sitevisit` | Site visit. |
| `wishlistitem` | Wish list item. |

### Custom parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `td1` | String | Custom parameter td1. |
| `td2` | String | Custom parameter td2. |
| `td3` | String | Custom parameter td3. |
| `td4` | String | Custom parameter td4. |
| `td5` | String | Custom parameter td5. |
| `td6` | String | Custom parameter td6. |
| `td7` | String | Custom parameter td7. |
| `td8` | String | Custom parameter td8. |
| `td9` | String | Custom parameter td9. |
| `td10` | String | Custom parameter td10. |