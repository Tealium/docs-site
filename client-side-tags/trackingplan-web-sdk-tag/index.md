---
title: Trackingplan Web SDK Tag Setup Guide
description: This article describes how to set up the Trackingplan Web SDK tag.
url: https://docs.tealium.com/client-side-tags/trackingplan-web-sdk-tag/
---
Trackingplan automatically monitors data quality across analytics, pixels, consent signals, and campaign tracking to detect missing events, broken pixels, and privacy compliance risks in real time.

## Tag tips

* Use mapping to override configuration settings.
* Use the **Tags** mapping tab to attach custom metadata to the Trackingplan initialization.
* The Trackingplan SDK loads once per page and initialises with the configuration from the first tag fire.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Trackingplan ID**: (Required) Your Trackingplan account identifier (`TP_ID`), found in the Trackingplan panel.
* **Encrypt personal data**: When enabled, Trackingplan automatically encrypts detected personal data in privacy reports. Enabled by default.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `tp_id` | String | (Required) Trackingplan account identifier (`TP_ID`). |
| `usePrivacy` | Boolean | Encrypts detected personal data in privacy reports. Defaults to `true`. |

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `environment` | String | Deployment environment. Defaults to `PRODUCTION`. |
| `tracksEndPoint` | String | Custom tracking endpoint URL. Only applied when set. |
| `debug` | Boolean | Enables debug logging. Only applied when set. |

### Tags

Enter a tag key name to map a data layer variable to `tags.{key_name}` in the Trackingplan initialization.
