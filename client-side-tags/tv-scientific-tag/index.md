---
title: TV Scientific Tag Setup Guide
description: This article describes how to set up the TV Scientific tag.
url: https://docs.tealium.com/client-side-tags/tv-scientific-tag/
---
## Tag Tips

Use mappings to dynamically override standard config values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Pixel ID**: Specify the unique identifier for the pixel linked to your account.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pixelId` | `String` | Pixel ID |
| `eventId` | `String` | Event ID |
| `orderAmount` | `Number` | Order amount |
| `referrerUrl` | `String` | Referrer URL |
| `orderId` | `String` | Order ID |
| `lastTouchChannel` | `String` | Last touch channel |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `pixelId` | Pixel ID |
| `eventId` | Event ID |
| `orderAmount` | Order amount |
| `referrerUrl` | Referrer URL |
| `orderId` | Order ID |
| `lastTouchChannel` | Last touch channel |

