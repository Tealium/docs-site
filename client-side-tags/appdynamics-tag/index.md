---
title: AppDynamics Tag Setup Guide
description: This article describes how to set up the AppDynamics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/appdynamics-tag/
---
AppDynamics is an Application Performance Management (APM) Platform that helps you understand and optimize your business performance, ranging from software to infrastructure and business journeys.

## Tag tips

* Use mapping to override the standard config values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **App Key**: Your EUM app key from your AppDynamics account.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
| App Key   | String | Your EUM app key from your AppDynamics account (overrides tag configiguration). |

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `xhr_url`  | String | Your XHR URL |
|  `error_msg`  | String | The error message | 
|  `error_line`  | Number | The line number in the source code where the error happened. |
|  `error_stack`  | String | The stack trace when the error occurred. |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `VPageView`  |Track the stages of a virtual page view. |
| `Ajax`| Track Ajax requests. |
| `Error` | Track errors. |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `xhr_url` | Your XHR URL.  |
| `error_msg` | Error Message. |
| `error_line` | The line number in source code where the error happened. |
| `error_stack` | The stack trace when the error occurred. |  |
| `VPageView` | Track the stages of a virtual page view. |
| `Ajax` | Track Ajax requests. |
| `Error`| Track errors. |

