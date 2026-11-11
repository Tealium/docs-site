---
title: Catchpoint Real User Monitoring (RUM) Tag Setup Guide
description: This article describes how to set up the Catchpoint Real User Monitoring tag.
url: https://docs.tealium.com/client-side-tags/catchpoint-real-user-monitoring-rum-tag/
---
## Tag tips

* Use mappings to set Page Groups, Variations, Insight Indicators, and Tracepoints.
* Both the value and the token for Insight Indicator and Tracepoint must be mapped with populated variables to capture this data.
* Conversion fires automatically when an Order ID is present.
* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * List of Quantities (`_cquan`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **REST URL**
  * The URL provided in your tag snippet.
  * Example: `g.3gl.net/jp/xxx/v3/M`

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `pageGroup_token` |  <ul><li>Page Group Token.</li></ul> |
| `variation_token` |  <ul><li>Variation Tag Token.</li></ul> |
| `indicator_token` |  <ul><li>Indicator Tag Token.</li></ul> |
| `indicator_value` |  <ul><li>Indicator Value.</li></ul> |
| `tracepoint_token` |  <ul><li>Tracepoint Token.</li></ul> |
|`tracepoint_value`|  <ul><li>Tracepoint Value.</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
| `order_id` |  <ul><li>Order ID.</li><li>Overrides `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Subtotal.</li><li>Overrides `_csubtotal`.</li></ul> |
|`product_quantity`|  <ul><li>Array.</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li></ul> |
