---
title: ContentSquare Mobile Remote Command Tag
description: This article describes how to set up the ContentSquare Mobile Remote Command tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/contentsquare-mobile-remote-command-tag/
---
ContentSquare unlocks customer insights for your entire digital team. It&#39;s one platform that is powerful enough for every digital role, from marketers to product managers to IT.

## Tag Tips

* Use mappings to:   
  * Dynamically override config data   
  * Dynamically override the E-Commerce extension values   
  * Send additional data values   
  * Event Specific Parameters   
  * Event trigger

* Supports the following E-Commerce extension values:   
  * Order ID   
  * Product Price   
  * Currency

* This is a Mobile Remote Command companion tag for the native mobile app SDK.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags]().

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Settings

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `screen_name`   |  String | (Required) Screen name |
|   `dynamic_var` |  | (Required) Dynamic variable |

### E-Commerce

| Variable | Type |Description |
|:---------|:------------|:------------|
|  `purchase.price` (Overrides `_ctotal`)  | Array | (Required) Price |
|  `purchase.currency` (Overrides `_ccurrency`)  | String | (Required) Currency |
|  `purchase.transaction_id` (Overrides `_corder`)  | String | Transaction ID |

### Custom Variables

Custom variables are additional information about the page, user, or session sent along with screen views.

| Variable | Type |Description |
|:---------|:------------|:------------|
|  Index  | Number | The index position of the custom variable. Select a value between `1` and `20`. |
|  Name  | String | The name of the custom variable. |

### Events

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|  `sendscreenview` | Send screen view |
|  `sendtransaction` | Send transaction |
|  `senddynamicvar` | Send dynamic variable |
|  `stoptracking` | Stop tracking |
|  `resumeTracking` | Resume tracking |
|  `forgetme` | Forget me |
|  `optin` | Opt in |
|  `optout` | Opt out |
|  `custom` | Custom |

### Event Parameters

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|  `sendscreenview` | Send screen view |
|  `sendtransaction` | Send transaction |
|  `senddynamicvar` | Send dynamic variable |
|  `stoptracking` | Stop tracking |
|  `resumeTracking` | Resume tracking |
|  `forgetme` | Forget me |
|  `optin` | Opt in |
|  `optout` | Opt out |
|  `custom` | Custom |

