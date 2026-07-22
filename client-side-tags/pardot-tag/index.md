---
title: Pardot Tag Set Up Guide
description: This article describes how to set up the Pardot tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pardot-tag/
---
## Tag tips

* Use mapping to override the standard config values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Account ID**: An integer value. For example: `123456`.
* **Campaign ID**: An integer value. For example: `123456`.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|piAId| Sets your pardot account ID|
|piCId| Sets your pardot campaign ID|
