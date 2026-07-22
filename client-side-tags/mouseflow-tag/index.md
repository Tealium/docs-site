---
title: Mouseflow Tag Setup Guide
description: This article describes how to configure the Mouseflow tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/mouseflow-tag/
---
Mouseflow lets you record website visitors and generate instant heatmaps showing where they click, scroll, and even pay attention.

## Tag tips

Use mapping to:
* Override the default Account ID.
* Push key-value pairs into the `_mfq` array. Replace `myvar` with your variable name to use this feature.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Account ID**: A long string of letters and numbers in the path to the js file. For example: `758f91b4-27bd-3d5e-9596-9c4b152c25f8`.
* **Disable Key Logging**: Select to enable or disable key logging.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| **Variable** | **Description** |
|:---------|:------------|
| `account` | Account ID |
| `page_url` | Page URL (override `dom.url`) |
| `mouseflowPath` | Mouse flow path |
| `mouseflow_disable_key_log` | Disable key logging (JSON) |
| `myvar` | Custom |

    