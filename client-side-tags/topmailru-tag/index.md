---
title: Top.Mail.ru Tag Setup Guide
description: This article describes how to set up the Top.Mail.ru tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/topmailru-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Counter ID**: (Required) Your Top Mail.ru Counter ID.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `base_url`  | String | Base URL |
|  `id`  | String | Counter ID |

### E-commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `productid`  | String | Product ID |
|  `value`  | String | Value |
|  `pagetype`  | String | Page type |
|  `list`  | String | List |
|  `userid`  | String | User ID |
|  `totalvalue`  | Number or String | Total value |

### Events

To map events, see [Create an Event Mapping]()

| Variable | Type | Description |
|:---------|:------------|:------------|
| `pageView` | String | Page view |
| `viewProduct` | String | View product |
| `addToCart` | String | Add To cart |
| `purchase` | String | Purchase |
| `itemView` | String | Item view |
| `custom` | String | Custom |

### Event-specific Parameters

To map events, see [Create an Event Mapping]()

| Variable | Type | Description |
|:---------|:------------|:------------|
| `productid` | String | Product ID |
| `value` | String | Value |
| `pagetype` | String | Page type |
| `list` | String | List |
| `userid` | String | User ID |
| `totalvalue` | Number or String | Total value |
| `custom_parameter` | String | Custom parameter |
| `pageView` | String | Page view |
| `viewProduct` | String | View product |
| `addToCart` | String | Add To cart |
| `purchase` | String | Purchase |
| `custom_event` | String | Custom event |
