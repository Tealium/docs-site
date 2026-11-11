---
title: Bing Ads - Microsoft adCenter Tag Reference Guide
description: This article describes how to set up the Bing Ads - Microsoft adCenter tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/bing-ads-microsoft-adcenter-tag/
---


<blockquote>
Bing Ads has deprecated this tag and recommends replacing it with the [Bing Ads Universal Event Tracking Tag](https://docs.tealium.com/client-side-tags/microsoft-advertising-universal-event-tracking-uet-tag/).
</blockquote>


## Tag tips

* Analytics tag allows for additional variables to be mapped (`actionid`, `revenue`, `nonadvertisingcost`, `taxcost`, `shippingcost`)
* Use comma-separated lists in one or more of the following variables to send multiple tracking requests (iframe tag only):
  * `siteid`
  * `actionid`
  * `domainId`
  * `cp`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag**: Use default (script) if not sure.
* **Type**: Using the conversion type adds the `cp` value, but does not send revenue.
* **Site ID**: Site ID is a long string of letters and numbers following `flex.msn.com/mstag/site/` (for example, `d2c3d50f-6f6a-3f2c-a303-6f032aece46c`)
* **Action ID**: Default Action ID. Can be overwritten with a mapping.
* **Domain ID**: Default Domain ID. Can be overwritten with a mapping.
* **CP**: Used for conversion tag only (set to `5050` for default.)
* **Revenue**: Analytics tag only. Leave blank to automatically send the `_csubtotal` value

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable             | Description |
|:---------------------|:------------|
| Action ID            |             |
| Revenue              |             |
| Non Advertising Cost |             |
| Tax Cost             |             |
| Shipping Cost        |             |
| Site ID              |             |
| Domain ID            |             |
| cp                   |             |
