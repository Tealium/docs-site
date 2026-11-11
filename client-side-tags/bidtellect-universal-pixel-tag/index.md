---
title: Bidtellect Universal Pixel Tag Setup Guide
description: This article describes how to set up the Bidtellect Universal Pixel tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/bidtellect-universal-pixel-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Customer Brand ID**: An integer value provided by Bidtellect that identifies your brand.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are as follows:

### Standard

| Variable | Description |
|:---------|:------------|
| Customer Brand ID | The brand ID provided by Bidtellect. |
| URL | If provided, overwrites the Page URL. |

    