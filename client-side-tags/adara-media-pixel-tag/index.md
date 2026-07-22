---
title: Adara Media Pixel Tag Setup Guide
description: This article describes how to set up the Adara Media Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adara-media-pixel-tag/
---
## Tag tips

There are several parameters that can be sent in the URL. Use the mapping toolbox to pass the dynamic variables.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Partner ID**: Your Adara Partner ID, as provided by Adara. 
* **Tag Type**: The type of tag to use. Possible values are:
    * `Image`: An image tag is used to send data to the vendor. This tag type does not support any additional parameters.
    * `Script`: A script tag is used to send data to the vendor. This tag type supports additional parameters that can be sent in the URL. For more information about the parameters, see the [Adara: SEM and YouTube Tracking with Impact](https://docs.adara.com/impact/sem-and-youtube-tracking-with-impact#step-3-add-url-tracking-template-to-sem-campaigns).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pid` | string | Partner ID. |