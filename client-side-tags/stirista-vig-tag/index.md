---
title: Stirista VIG Tag Setup Guide
description: This article describes how to set up the Stirista VIG tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/stirista-vig-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Field i**
  * An alphanumeric value found in your generated code snippet.
  * Example: `i=000a000b123c`

* **Field s**
  * An alphanumeric value found in your generated code snippet.
  * Example: `s=000a000b123c`

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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
