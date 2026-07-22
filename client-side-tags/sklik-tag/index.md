---
title: Sklik Tag Setup Guide
description: This article describes how to set up the Sklik tag.
url: https://docs.tealium.com/client-side-tags/sklik-tag/
---
## Tag Tips

* Use mapping to dynamically override the standard config values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **C**: The Sklik conversion ID.
* **Color**: Hex color code to use for the background for the conversion iframe. For example, `#ffffff` for white.
* **V**: The conversion value.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `c` | The Sklik conversion ID. |
| `color` | Hex color code to use for the background for the conversion iframe. |
| `v` | The conversion value. |