---
title: Quantcast Easy Tag for Measure Setup Guide
description: This article describes how to set up the Quantcast Easy Tag for Measure in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/quantcast-easy-tag-for-measure/
---
## Tag tips

* Use mappings to dynamically override the standard configuration value for account.

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
