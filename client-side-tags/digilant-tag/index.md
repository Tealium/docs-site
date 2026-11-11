---
title: Digilant Tag Setup Guide
description: This article describes how to set up the Digilant tag.
url: https://docs.tealium.com/client-side-tags/digilant-tag/
---
## Tag tips

* Specify a Pixel ID in the standard configuration.
* Override the Pixel ID in the standard configuration with a mapping.
* Set the **Synchronous Load Type** in **Advanced Settings** when the library needs to be loaded synchronously.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag Version**
* **Pixel ID**:

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`id`| Pixel ID|
