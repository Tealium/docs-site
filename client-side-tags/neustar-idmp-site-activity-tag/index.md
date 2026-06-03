---
title: Neustar IDMP Site Activity Tag Setup Guide
description: This article describes how to set up the Neustar Identity Management Platform (IDMP) Site Activity tag.
url: https://docs.tealium.com/client-side-tags/neustar-idmp-site-activity-tag/
---
Use the Neustar IDMP Site Activity tag to track user behavior on your websites, such as conversion events.

## Tag tips

* Select the **Pixel Type** in the tag configuration to load the correct script type.
* Use mappings to override and dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Neustar Tag ID**: The numerical value of your Neustar IDMP tag.
* **Pixel Type**: Choose between generating an image or an iframe tag type.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `pixelId`  | String | Pixel ID |
|  `pixelType`  | String | Pixel type |

### Standard

|  Variable | Type | Description | 
|:---------|:------------|:------------|
| `che`  | String | Cache buster  |
|  `rev`  | Number | Revenue |
|  `cur`  | String | Currency code | 
|  `qty`  | Number | Order count |
|  `type`  | String | Type |
|  `ord`  | String | Order ID |
|  `uid`  | String | Third-party user ID |
|  `dedup`  | String | Deduplication ID |
|  `ip`  | String | IP Address |