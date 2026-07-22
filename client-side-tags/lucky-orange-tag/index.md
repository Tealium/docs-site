---
title: Lucky Orange Tag Setup Guide
description: This article describes how to set up the Lucky Orange Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/lucky-orange-tag/
---
## Tag Tips

*   Use mappings to override and dynamically set the tag configuration.
*   Use Custom event to enter the name of the event you need.
*   You can use as many custom parameters as you need.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Site ID**: (Required) The unique identifier for the client’s site.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `site_id` | `String` | Site ID |
| `customer_id` | `String` | A visitor ID to identify the customer |
| `email` | `String` | Customer email address |
| `phone` | `String` | Customer phone number |
| `name` | `String` | Customer name |
| `identify.custom` | `String` | Custom identify field |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `site_id` | Site ID |
| `customer_id` | A visitor ID to identify the customer |
| `email` | Customer email address |
| `phone` | Customer phone number |
| `name` | Customer name |