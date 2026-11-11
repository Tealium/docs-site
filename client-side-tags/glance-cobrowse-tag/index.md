---
title: Glance Cobrowse Tag Setup Guide
description: This article describes how to set up the Glance Cobrowse tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/glance-cobrowse-tag/
---
Enable co-browsing capabilities to instantly join customers in viewing your app or website without requiring the customer to download or install a screen sharing app.

## Tag tips

* Use mapping to dynamically override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Group ID**: The assigned group ID number provided by Glance.
* **Website Stage**: The website environment that this tag will be deployed to.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
| `group_id`  | String | Group ID  |
|  `website_stage`  | String | Website stage |

