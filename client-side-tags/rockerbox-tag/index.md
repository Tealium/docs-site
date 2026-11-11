---
title: Rockerbox Tag Setup Guide
description: This article describes how to set up the Rockerbox tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/rockerbox-tag/
---

Rockerbox is the leading attribution provider for digital companies. Rockerbox provides one source of truth across all of your marketing, enabling companies to quickly uncover the effectiveness of all of their marketing.

## Tag tips

* Use mappings to:
  * Override standard config values and set custom parameters
  * Trigger standard and custom events
  * Supports the following E-Commerce extension values:
    * Order Id (`_corder`)
    * Revenue (`_ctotal`)
    * Coupon (`_cpromo`)
    * Products (`_cprod`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client Auth**: Client Auth ID
* **Allow automatic page view**:

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Base Url (`base_url`)| [String]|
|Client Auth (`client_auth`)| [String]|
|Automatic Page View (`automatic_pageview`)| [Boolean]|
|Disable Push State (`disablePushState`)| [Boolean]|

### E-commerce

|Variable| Description|
|---| ---|
|External Id (`external_id`)| [String/Number]|
|Order Id (`order_id`) (override `_corder`)| [String/Number]|
|Revenue (`revenue`) (override `_ctotal`)| [String/Number]|
|Coupon (`coupon`) (override `_cpromo`)| [String]|
|Products (`products`) (override `_cprod`)| [Array]|
|Email (`email`)| [String]|

### Address

|Variable| Description|
|---| ---|
|Country (`rb_country`)| [String]|
|State (`rb_state`)| [String]|
|City (`rb_city`)| [String]|
|Address 1 (`rb_address_1`)| [String]|
|Address 2 (`rb_address_2`)| [String]|
|Zip Code (`rb_zip_code`)| [String]|

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|Page View (view)| `view`|
|Purchase (`conv.purchase`)| `conv.purchase`|
|Add To Cart (`conv.add_to_cart`)| `conv.add_to_cart`|
|Initiate Checkout (`conv.initiate_checkout`)| `conv.initiate_checkout`|
|Create Account (`conv.create_account`)| `conv.create_account`|
|Email Signup (`conv.email_signup`)| `conv.email_signup`|
|Enrollment (`conv.enrollment`)| `conv.enrollment`|
|Purchase Subscription (`conv.purchase.subscription`)| `conv.purchase.subscription`|
|Purchase One Time (`conv.purchase.one_time`)| `conv.purchase.one_time`|
|Custom| `custom`|

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|Page View (`view`)| `view`|
|Purchase (`conv.purchase`)| `conv.purchase`|
|Add To Cart (`conv.add_to_cart`)| `conv.add_to_cart`|
|Initiate Checkout (`conv.initiate_checkout`)| `conv.initiate_checkout`|
|Create Account (`conv.create_account`)| `conv.create_account`|
|Email Signup (`conv.email_signup`)| `conv.email_signup`|
|Enrollment (`conv.enrollment`)| `conv.enrollment`|
|Purchase Subscription (`conv.purchase.subscription`)| `conv.purchase.subscription`|
|Purchase One Time (`conv.purchase.one_time`)| `conv.purchase.one_time`|
|Custom| `custom`|
