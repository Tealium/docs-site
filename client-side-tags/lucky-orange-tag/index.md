---
title: Lucky Orange Tag Setup Guide
description: This article describes how to set up the Lucky Orange Tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/lucky-orange-tag/
---
## Tag tips

*   Use mappings to override and dynamically set the tag configuration.
*   Use Custom event to enter the name of the event you need.
*   You can use as many custom parameters as you need.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Site ID**: (Required) The unique identifier for the client’s site.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `site_id` | Site ID |
| `customer_id` | A visitor ID to identify the customer |
| `email` | Customer email address |
| `phone` | Customer phone number |
| `name` | Customer name |