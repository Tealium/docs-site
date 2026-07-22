---
title: FreakOut Tag Setup Guide
description: This article describes how to set up the FreakOut Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/freakout-tag/
---
## Tag tips

* Use mapping to override config values or set custom data.
* **Conversion Type** is only used when **Tag Type** is set to `conv`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**: Your FreakOut account ID.
* **Conversion Type**: Enter the exact, case-sensitive conversion action name from FreakOut (for example, `purchase`, `signup`, or `leadform`).
* **Tag Type**:
    * `segment`: Standard retargeting.
    * `conv`: Standard conversions.

## Best practices

* Before adding a new conversion action:
    1. Configure the conversion in FreakOut.
    1. Update your mapping table and tests within FreakOut.
    1. Deploy to QA.
    1. Validate payloads.
    1. Publish to prod with a short monitoring window.
* For single-page applications (SPA) or multi-step funnels, fire the tag only on the final success state, not intermediate steps.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable              | Type   | Description                                       |
|:----------------------|:-------|:--------------------------------------------------|
| `account_id`          | String | Account ID.                                       |
| `conversion_type`     | String | Conversion type.                                  |
| `segment_data.custom` | String | Additional custom data for segmentation purposes. |
