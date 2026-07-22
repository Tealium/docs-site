---
title: Quantcast Easy Tag for Measure Setup Guide
description: This article describes how to set up the Quantcast Easy Tag for Measure in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/quantcast-easy-tag-for-measure/
---
## Tag Tips

* Use mappings to dynamically override the standard configuration value for account.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Quantcast Easy Tag for Measure tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Account Code**
  * Account Code (P-code).
  * A 13-character, case sensitive, alpha-numeric code that begins with `p-`.
  * Contact your Quantcast representative if you have questions.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`qacct`|  <ul><li>Account Code (P-code).</li><li>A 13-character, case sensitive, alpha-numeric code that begins with `p-`.</li></ul> |
