---
title: BlueKai Tag Setup Guide
description: This article describes how to set up the BlueKai tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/bluekai-tag/
---
## Tag tips

Use mapping to override the standard configuration values or to pass additional parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Site ID**: Unique number that identifies a pixel as belonging to a certain DMP Partner.
* **Limit**: Maximum number of media partner segment pixels that will be fired by BlueKai.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The following variables are available for the BlueKai tag:

### Standard

|Variable| Description|
|---| ---|
|Site ID| (siteid)|
|Limit| (limit)|
|Allow Multiple Calls (`allow_multiple_calls`)| [boolean]|
|show| |
|tod| |
|lv| |
|ss| |
|top| |
|sub1| |
|sub2| |
|sub3| |
|ref| |
|srch| |
