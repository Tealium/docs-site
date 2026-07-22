---
title: Google Ad Manager 360 Audience Pixel Tag Setup Guide
description: This article describes how to set up the Google Ad Manager 360 Audience Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-ad-manager-360-audience-pixel-tag/
---
Build first-party audience segments in Google Ad Manager 360 without serving any ads by adding the Audience Pixel tag to your site or mobile app. You can use the pixel tag at no extra cost, without being charged for serving an Ad Manager impression. This tag also lets you use a publisher provided identifier (PPID) for audience segmentation in place of a Google Marketing Platform cookie or mobile advertising ID.

## Tag Tips

* Use mappings to override or dynamically set the tag configurations.
* Publisher Provided ID (PPID) should only be added to the URL if a mapped value is populated for it.
* The PPID value requirements are:
    * Alphanumeric (`[0-9 a-z A-Z]`) or UUID HEX representation (`8-4-4-4-12`). (Hyphens are permitted)
    * The following regex can be used to enforce the value: `^([0-9a-zA-Z]{32,150})$|^([0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12})$`

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Network Code**: The publisher’s Google Ad Manager network identifier. Found under **Admin > Global Settings** or in the Ad Manager URL.
* **Segment ID**: Segment Identifier (`dc_seg`).

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| Network Code (`network_code`) | String |
| Segment ID (`segment_id`) | String |
| Publisher Provided ID (`publisher_provided_id`) | String |