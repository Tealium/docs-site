---
title: Decibel Insight Tag Setup Guide
description: This article describes how to set up the Decibel Insight tag.
url: https://docs.tealium.com/client-side-tags/decibel-insight-tag.md/
---
## Tag tips

Use mapping to dynamically override the Account ID value or to set additional parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Account ID**: : The Decibel account ID.
* **Property ID**: (Optional) The unique property ID of selected website. 

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
|  `da_accountId` |Account ID  |
|  `da_propertyId` |Property ID  |
|  `collectionRemember` |Collection remember  |
|  `collectionStatus` |Collection status  |
|  `customer_id` |Customer ID  |
|  `order_currency` |Order currency  |
|  `errorMessage` |Error message  |
| `errorMessageCssSelector` |Error message CSS selector  | 
| `goalName` |Goal name  | 
|  `goalValue` |Goal value  |
|  `httpErrorCode` |HTTP error code  |
|  `pageRole` |Page role  |
|  `retentionStatus` |Retention status  |
| `retentionRemember` |Retention remember  | 

### Page View

| Variable | Description |
|:---------|:------------|
| `pageName` | Page mame| 
| `pageViewParams.title` | Title| 
| `pageViewParams.queryString` | Query string| 
| `pageViewParams.fragment` | Fragment| 
| `pageViewParams.waitTime` | Wait time| 

### Events

For more information on mapping events, see [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `sendApplicationError` | Send application error |
| `sendGoal` | Send goal |
| `sendHTTPError` | Send HTTP error |
| `setCollection` | Set collection |
| `setRetention` | Set retention |
| `trackPageView` | Track page view |
| `updateUserId` | Update user ID |

### E-Commerce

|  Variable |Description |
|:---------|:------------|
|  `customer_id` (Overrides `_ccustid`) |Customer ID  |

