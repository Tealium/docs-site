---
title: Teads Advertiser Tag Setup Guide
description: This article describes how to set up the Teads Advertiser tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/teads-advertiser-tag/
---
## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable         | Description                                                                                      |
|:-----------------|:-------------------------------------------------------------------------------------------------|
| `advertiserId`   | <ul><li>(Required) Your Teads-supplied Advertiser ID.</li><li>Example: `123456`</li></ul> |
| `conversionType` | <ul><li>(Optional) The name or type of conversion.</li></ul>                              |
| `name` | Name |
| `price` | Price |
| `currency` | Currency |

