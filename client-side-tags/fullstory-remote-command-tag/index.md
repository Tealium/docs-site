---
title: FullStory Remote Command Tag Setup Guide
description: This article describes how to set up the FullStory Remote Command tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/fullstory-remote-command-tag/
---
FullStory captures all your customer experience data in one powerful, easy-to-use platform. FullStory's tiny script unlocks pixel-perfect session playback, automatic insights, funnel analytics, and robust search and segmentation, empowering everyone in your organization to help build the best online experience for your customers.

## Tag tips

* Use mappings to trigger events.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `uid`  | String | UID |
|  `user_variables.email_str`  | String | Email |
|  `user_variables.phone_str`  | String | Phone |
|  `tealium_event`  | String | Tealium Event |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `event.cart_id_str`  | String | Cart ID |
| `event.product_id_str`  | String | Product ID  |
|  `event.price_real`  | Number |Price Real|
|  `event.name_str`  | String | Name|
|  `event.categoryProperties`  | String | Category Properties |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|  `identify` | identify |
| `setuservariables` | setuservariables |
| `logevent` | logevent |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|  `identify` | Identify |
|  `setuservariables` | Set User Variables |
|  `logevent` | Log Event |