---
title: Glassbox Detector Tag Setup Guide
description: This article describes how to set up the Glassbox Detector tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/glassbox-detector-tag/
---## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).


## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`src_link`|  <ul><li>Source Link</li><li>Link to Glassbox JavaScript</li></ul> |
|`data-clsconfig`|  <ul><li>`data-clsconfig` must contain `reportURI`.</li><li>Can also include additional optional parameters.</li></ul> |
