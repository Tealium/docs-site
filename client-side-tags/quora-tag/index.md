---
title: Quora Tag Setup Guide
description: This article describes how to set up the Quora tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/quora-tag/
---
## Tag Tips

* Use mappings to:
  * Override standard configuration values
  * Set up event triggers

## Tag Configuration

First, go to Tealium's tag marketplace and add the Quora tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* `pixel_id`
A Quora-provided alphanumeric string uniquely identifying the pixel

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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
