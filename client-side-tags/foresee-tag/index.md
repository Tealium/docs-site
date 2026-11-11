---
title: Foresee Tag Setup Guide
description: This article describes how to set up the Foresee Tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/foresee-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Title**: The default is "Foresee". You may replace it with a custom name of choice.
* **File Path**: The URL where your Foresee files/configurations are hosted.   
 For example, `//gateway.foresee.com/sites/XXX/XXX/gateway.min.js`

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the Foresee Tag are built into its Data Mapping tab. Available categories are:

### Standard

|Tag Destination| Description|
|---| ---|
|File Path| The URL where your Foresee snippet is hosted|

## Vendor Documentation

[Foresee Developer Portal](https://developer.foresee.com/v1.0/)
