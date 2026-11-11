---
title: Quantcast Easy Tag for Advertise Setup Guide
description: This article describes how to set up the Quantcast Easy Tag for Advertise in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/quantcast-easy-tag-for-advertise/
---
## Tag tips

* Use mappings to:
  * Dynamically override the standard configuration value for account.
  * Dynamically override the E-Commerce extension values.
  * Pass any `_fp` label as part of `_qevents`.
  * Pass any freeform label (`mylabel`).
  * Mapping arrays to freeform labels will be handled according to Quantcast documentation.

* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Order Subtotal (`_csubtotal`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account Code**
  * Account Code (P-code).
  * A 13-character, case sensitive, alpha-numeric code that begins with `p-`.
  * Contact your Quantcast representative if you have questions.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`qacct`|  <ul><li>Account Code (P-code).</li><li>A 13-character, case sensitive, alpha-numeric code that begins with `p-`.</li></ul> |
|`_fp.event`|  <ul><li>Event</li></ul> |
|`_fp.channel`|  <ul><li>Channel</li></ul> |
|`_fp.subchannel`|  <ul><li>Subchannel</li></ul> |
|`_fp.customer`|  <ul><li>Customer</li></ul> |
|`_fp.pcat`|  <ul><li>Product Category</li></ul> |
|`mylabel`|  <ul><li>Custom Label</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`orderid`|  <ul><li>Order ID.</li><li>Overrides E-Comm Order ID.</li></ul> |
|`revenue`|  <ul><li>Revenue.</li><li>Overrides E-Comm Order Subtotal.</li></ul> |
