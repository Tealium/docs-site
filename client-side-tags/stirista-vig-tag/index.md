---
title: Stirista VIG Tag Setup Guide
description: This article describes how to set up the Stirista VIG tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/stirista-vig-tag/
---
## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Stirista VIG tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Field i**
  * An alphanumeric value found in your generated code snippet.
  * Example: `i=000a000b123c`

* **Field s**
  * An alphanumeric value found in your generated code snippet.
  * Example: `s=000a000b123c`

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`i`| Must be mapped.|
|`t`| Must be mapped.|
|`p`| Must be mapped.|
|`s`| Must be mapped.|
|`r`| Must be mapped.|
|`u`| Must be mapped.|
