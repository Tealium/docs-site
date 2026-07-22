---
title: Glance Cobrowse Tag Setup Guide
description: This article describes how to set up the Glance Cobrowse tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/glance-cobrowse-tag/
---
Enable co-browsing capabilities to instantly join customers in viewing your app or website without requiring the customer to download or install a screen sharing app.

## Tag tips

* Use mapping to dynamically override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Group ID**: The assigned group ID number provided by Glance.
* **Website Stage**: The website environment that this tag will be deployed to.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
| `group_id`  | String | Group ID  |
|  `website_stage`  | String | Website stage |

