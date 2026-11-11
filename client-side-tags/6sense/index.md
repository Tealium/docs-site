---
title: 6sense Tag
description: This article describes how to set up the 6sense tag.
url: https://docs.tealium.com/client-side-tags/6sense/
---
6sense empowers marketing and sales teams with 100 percent visibility into their buyers' identities, needs, and timing.

## Tag tips

Use mapping to:

* Override standard config values.
* Set custom parameters and attributes.
* To track events for only specific tags, map **Manually Tracked Tags** (for example, `['A', 'BUTTON']`).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Event Tracking Customer Token**: Enables Auto Event Tracking. Provided by your 6sense customer success manager.
* **Identity API Organization Token**: Enables the Company Identity API. Provided by your 6sense customer success manager.
* **Trigger Event On Detect**: If you select `Yes`, a callback function will be called upon tag detection. Trigger `utag.link` that passes in the JSON object returned.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|   `customer_token` | String | Event Tracking Customer Token |
|   `org_token` | String | Identity API Organization Token |
|  `trackedTags`  | Array | Manually Tracked Tags|
| `setEndpoint` | String | Endpoint |
|  `setWhitelistFields`  | Array | Whitelist Fields|
|  `setCustomMetatags`  | Array | Custom Metatags|
| `setPageAttributes.param` | String | Page Attributes |
|   `setThirdPartyValues.vendor` | String | Third Party Analytics|
| `enableCompanyDetails`  | Boolean | Enable Data Retrieval|
|  `enableEventTracking`  | Boolean | Enable Event Tracking |
|  `triggerEvent`  | Boolean | Trigger Event on Detect |