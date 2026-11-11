---
title: Amobee Pixel Tag Setup Guide
description: This article describes how to set up the Amobee Pixel tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/amobee-pixel-tag/
---
## Tag tips

Use Mapping Toolbox to see sample values for mapping

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **ID**
  * For the Image pixel, this is the `b2= value` in the URL.
  * For the Script pixel, this is the long string of letters and numbers after `/id/` where `id` is the Amobee-provided ID.
* **Tag Type**
  * Select **r.turn.com (Image pixel**) or **d.turn.com (Script pixel)**
* **Campaign ID**
  * Image pixel only.
  * This is the `cid= value` in the URL.
  * Override this value using mapping.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Account ID/b2 Parameter| (acct)|
|Search Destination| (SearchDest)|
|Search Results Number| (SearchNum)|
|Search Date| (SearchDate)|
|Property Date| (PropDate)|
|Property Destination| (PropDest)|
|Property Number| (PropNum)|
|Property Rating| (PropRating)|
|Campaign ID for image tag| (cid)|
