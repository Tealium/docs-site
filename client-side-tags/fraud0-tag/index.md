---
title: Fraud0 Tag Setup Guide
description: This article describes how to set up the Fraud0 tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/fraud0-tag/
---
## Tag tips

* Use data mappings to override standard tag configuration settings when needed.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag ID**: Your Fraud0 tag ID (`cid`).

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available category is:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `cid` | String | Tag ID. |
| `customer_id` | String | Customer ID. |
| `conversion_id` | String | Conversion ID. |
