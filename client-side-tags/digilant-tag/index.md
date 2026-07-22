---
title: Digilant Tag Setup Guide
description: This article describes how to set up the Digilant tag.
url: https://docs.tealium.com/client-side-tags/digilant-tag/
---
## Tag Tips

* Specify a Pixel ID in the standard configuration.
* Override the Pixel ID in the standard configuration with a mapping.
* Set the **Synchronous Load Type** in **Advanced Settings** when the library needs to be loaded synchronously.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Digilant tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Tag Version**
* **Pixel ID**:

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`id`| Pixel ID|
