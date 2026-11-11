---
title: Lytics Tag Setup Guide
description: This article describes how to set up the Lytics tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/lytics-tag/
---

## Tag tips

* Use mapping to override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Collection ID**: Your Lytics supplied Collection ID (`cid`/`account id`)

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`cid`| Collection ID|
