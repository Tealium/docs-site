---
title: Mouseflow Tag Setup Guide
description: This article describes how to configure the Mouseflow tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/mouseflow-tag/
---
Mouseflow lets you record website visitors and generate instant heatmaps showing where they click, scroll, and even pay attention.

## Tag tips

Use mapping to:
* Override the default Account ID.
* Push key-value pairs into the `_mfq` array. Replace `myvar` with your variable name to use this feature.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**: A long string of letters and numbers in the path to the js file. For example: `758f91b4-27bd-3d5e-9596-9c4b152c25f8`.
* **Disable Key Logging**: Select to enable or disable key logging.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| **Variable** | **Description** |
|:---------|:------------|
| `account` | Account ID |
| `page_url` | Page URL (override `dom.url`) |
| `mouseflowPath` | Mouse flow path |
| `mouseflow_disable_key_log` | Disable key logging (JSON) |
| `myvar` | Custom |

    