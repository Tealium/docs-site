---
title: SalesViewer tag setup guide
description: This article describes how to set up the SalesViewer tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/salesviewer-tag/
---
## Tag tips

* You can dynamically set your SalesViewer ID with mappings.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **SalesViewer ID**: Your SalesViewer-provided ID.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `salesviewer_id` | SalesViewer ID. |