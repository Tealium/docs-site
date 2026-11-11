---
title: Google Ad Manager 360 Audience Pixel Tag Setup Guide
description: This article describes how to set up the Google Ad Manager 360 Audience Pixel tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-ad-manager-360-audience-pixel-tag/
---
Build first-party audience segments in Google Ad Manager 360 without serving any ads by adding the Audience Pixel tag to your site or mobile app. You can use the pixel tag at no extra cost, without being charged for serving an Ad Manager impression. This tag also lets you use a publisher provided identifier (PPID) for audience segmentation in place of a Google Marketing Platform cookie or mobile advertising ID.

## Tag tips

* Use mappings to override or dynamically set the tag configurations.
* Publisher Provided ID (PPID) should only be added to the URL if a mapped value is populated for it.
* The PPID value requirements are:
    * Alphanumeric (`[0-9 a-z A-Z]`) or UUID HEX representation (`8-4-4-4-12`). (Hyphens are permitted)
    * The following regex can be used to enforce the value: `^([0-9a-zA-Z]{32,150})$|^([0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12})$`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Network Code**: The publisher’s Google Ad Manager network identifier. Found under **Admin > Global Settings** or in the Ad Manager URL.
* **Segment ID**: Segment Identifier (`dc_seg`).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| Network Code (`network_code`) | String |
| Segment ID (`segment_id`) | String |
| Publisher Provided ID (`publisher_provided_id`) | String |