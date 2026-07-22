---
title: Glassbox Detector Tag Setup Guide
description: This article describes how to set up the Glassbox Detector tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/glassbox-detector-tag/
---## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).


## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`src_link`|  <ul><li>Source Link</li><li>Link to Glassbox JavaScript</li></ul> |
|`data-clsconfig`|  <ul><li>`data-clsconfig` must contain `reportURI`.</li><li>Can also include additional optional parameters.</li></ul> |
