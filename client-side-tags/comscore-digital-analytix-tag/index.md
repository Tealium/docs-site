---
title: comScore Digital Analytix Tag Setup Guide
description: This article describes how to set up the comScore Digital Analytix tag.
url: https://docs.tealium.com/client-side-tags/comscore-digital-analytix-tag/
---
## Tag tips

* comScore is now GDPR-compliant. You can indicate a visitor's consent by setting the `cs_ucfr` parameter to 0 (no consent) or 1 (consent). By default the `cs_ucfr parameter` is set to 0. You can set this parameter with a mappings. You may have to update this tag's template to take advantage of this feature.
* Use mapping to add additional `c-parameters`.
* Order tracking is triggered automatically when an Order ID is set by the E-Commerce extension.
* Supports the following E-Commerce extension values:
    * Order ID
    * Shipping Amount
    * Customer ID
    * List of Product IDs
    * List of Brands
    * List of Categories
    * List of Categories 2
    * List of Quantities
    * List of Prices

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

Configure the following settings:

* **Client ID**: Your comScore Client ID (c2)
* **Stream Sense Video Tracking**: 
* **Form Identifier**: Enter a Form ID or Name to enable form measurements. Enter * to measure all forms. Use mapping to measure hidden form fields. Leave this field blank to disable form tracking.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `c1`  | <ul><li>C1</li><li>String</li></ul> |
| `c2`  | <ul><li>Client ID</li><li>String</li></ul> |
| `ns_type` | <ul><li>NS Type</li><li>String</li></ul> |
| `form` | <ul><li>Form identifier</li></ul> |
| `form_normal`  | <ul><li>Normal Form Fields</li><li>Array</li></ul> |
| `form_hidden`  | <ul><li>Hidden Form Fields</li><li> Array</li></ul> |
| `form_submit`  | <ul><li>Report Submit Events</li><li> Boolean</li></ul> |
| `form_abandon`  | <ul><li>Report Abandon Events</li><li>Boolean</li></ul> |
| `form_failure`  | <ul><li>Report Failure Events</li><li>Boolean</li></ul> |
| `cs_ucfr`  | <ul><li>Consent State</li><li>[0/1]</li></ul> |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` | <ul><li>Order ID</li><li>Overrides `_corder`</li></ul> |
| `order_shipping` | <ul><li>Shipping Amount</li><li>Overrides `_cship`</li></ul> |
| `customer_id` | <ul><li>Customer ID</li><li>Overrides `_ccustid`</li></ul> |
| `product_id` | <ul><li>List of Product IDs</li><li>Array</li><li>Overrides `_cprod`</li></ul> |
| `product_brand` | <ul><li>List of Brands</li><li>Array</li><li>Overrides `_cbrand`</li></ul> |
| `product_category` | <ul><li>List of Categories</li><li>Array</li><li>Overrides `_ccat`</li></ul> |
| `product_subcategory` | <ul><li>List of Sub Categories</li><li>Array</li><li>Overrides `_ccat`</li></ul> |
| `product_quantity` | <ul><li>List of Quantities</li><li>Array</li><li>Overrides `_cquan`</li></ul> |
| `product_unit_price` | <ul><li>List of Prices</li><li>Array</li><li>Overrides `_cprice`</li></ul> |   