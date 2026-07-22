---
title: Contentsquare UX Analytics Tag Setup Guide
description: This article describes how to set up the Contentsquare UX Analytics tag.
url: https://docs.tealium.com/client-side-tags/contentsquare-ux-analytics-tag/
---
## Tag tips
*   The `ecommerce:addTransaction` event is tracked when an order ID is set.
*   When mapping a badge, enter the name that should appear in Contentsquare.
*   Set **Send All Audiences** to `true` to send each audience to Contentsquare in the format `_uxa.push(["trackDynamicVariable", {key: "CDP_TL_Audience ID : AUDIENCE_ID", value: "AUDIENCE_NAME"}]);`.
*   Supported E-Commerce extension parameters (\*required for transactions):
    *   Order ID (`_corder`) \*
    *   Order Total (`_ctotal`) \*
    *   Shipping Amount (`_cship`)
    *   Tax Amount (`_ctax`)
    *   Order Currency (`_ccurrency`)
    *   List of Product IDs (`_cprod`)
    *   List of Names (`_cprodname`) \*
    *   List of SKUs (`_csku`) \*
    *   List of Categories (`_ccat`)
    *   List of Quantities (`_cquan`) \*
    *   List of Prices (`_cprice`) \*

## Tag configuration

Navigate to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Main Tag ID**: The Main Tag ID specific to your website.
* **WebView Tag ID**: The Tag WebView ID specific to your website.
* **Send All Audiences**: Select `True` to send each audience to Contentsquare in the format `_uxa.push(["trackDynamicVariable", {key: "Tealium Audience AUDIENCE ID", value: "AUDIENCE NAME"}]);`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `id_project` | `String` | Main Tag ID |
| `webview_id_project` | `String` | WebView Tag ID |
| `send_audiences` | `String` | Send All Audiences |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_id` | `String` | Order ID (Overrides `_corder`) |
| `order_total` | `Number`  | Order Total (Overrides `_ctotal`) |
| `order_currency` | `String` | Currency (Overrides `_ccurrency`) |
| `product_id` | `Array` | List of Product IDs (Overrides `_cprod`) |
| `product_name` | `Array` | List of Names (Overrides `_cprodname`) |
| `product_sku` | `Array` | List of SKUs (Overrides `_csku`) |
| `product_category` | `Array` | List of Categories (Overrides `_ccat`) |
| `product_quantity` | `Array` | List of Quantities (Overrides `_cquan`) |
| `product_unit_price` | `Array` | List of Prices (Overrides `_cprice`) |

### Badges

To map a badge, enter the name that should appear in Contentsquare. The name is used in the `key` when calling `_uxa.push(["trackDynamicVariable", { "key" : "CDP_TL_Badge ID : BADGE_NAME", "value" : BADGE_VALUE`.

### Dynamic variables

To map a dynamic variable, enter the name of the variable expected by Contentsquare. The variable name is used as the `key` when calling `_uxa.push(["trackDynamicVariable", { "key": "my_key", "value": my_value }]);`.