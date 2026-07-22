---
title: Pixibo FYF Tag Setup Guide
description: This article describes how to set up the "Find your Fit" pixibo.fyf tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pixibo-fyf-tag/
---## Tag tips

* Use mappings to dynamically override the standard config values.
* SKU ID in mapping is required for the tag to fire.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Client Name**
* **Client ID**
* **Environment**
  * Used to specify the environment of the script.
* **Language**
  * Optional
  * Language in which to load the widget.
  * The default value is English (`en`).

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`clientName`|  <ul><li>Client Name</li></ul> |
|`clientId`|  <ul><li>Client ID</li></ul> |
|`environment`|  <ul><li>Environment</li></ul> |
|`skuId`|  <ul><li>SKU ID</li></ul> |
|`lang`|  <ul><li>Language</li></ul> |
