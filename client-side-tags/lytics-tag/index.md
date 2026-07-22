---
title: Lytics Tag Setup Guide
description: This article describes how to set up the Lytics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/lytics-tag/
---

## Tag Tips

* Use mapping to override the standard config values.

## Tag Configuration

First, go to the tag marketplace and add the Lytics tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Collection ID**: Your Lytics supplied Collection ID (`cid`/`account id`)

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`cid`| Collection ID|
