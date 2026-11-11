---
title: Quora Tag Setup Guide
description: This article describes how to set up the Quora tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/quora-tag/
---
## Tag tips

* Use mappings to:
  * Override standard configuration values
  * Set up event triggers

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* `pixel_id`
A Quora-provided alphanumeric string uniquely identifying the pixel

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable   | Description                      |
|:-----------|:---------------------------------|
| `pixel_id` | <ul><li>Quora Pixel ID</li></ul> |

### Events

| Variable               | Description                                      |
|:-----------------------|:-------------------------------------------------|
| `ViewContent`          | <ul><li>Page View</li><li>View content</li></ul> |
| `Generic`              | <ul><li>Generic</li></ul>                        |
| `Purchase`             | <ul><li>Purchase</li></ul>                       |
| `GenerateLead`         | <ul><li>Generate lead</li></ul>                  |
| `CompleteRegistration` | <ul><li>Complete registration</li></ul>          |
| `AddPaymentInfo`       | <ul><li>Add payment Information</li></ul>        |
| `AddToCart`            | <ul><li>Add to cart</li></ul>                    |
| `AddToWishlist`        | <ul><li>Add to wish list</li></ul>               |
| `InitiateCheckout`     | <ul><li>Initiate checkout</li></ul>              |
| `Search`               | <ul><li>Search</li></ul>                         |
| `Custom`               | <ul><li>Custom</li></ul>                         |
