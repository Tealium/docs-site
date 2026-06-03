---
title: MediaMath Tag Setup Guide
description: This article describes how to set up the MediaMath tag.
url: https://docs.tealium.com/client-side-tags/mediamath-tag-basic-configuration/
---
## Prerequisites

* MediaMath Account

## Tag Configuration

First, go to the tag marketplace and add the MediaMath (Adroit Digital) Tag to your profile (See [Add a tag]()).

After adding the Tag, configure the below settings:

1. **Title**: Enter a descriptive title to identify the Tag instance.
1. **Advertiser ID**: Enter the advertiser identifier you received from MediaMath.
1. **Pixel ID**(formerly Event ID): Enter the pixel identifier you received from MediaMath.
1. **Tag Type**: Choose the type of MediaMath pixel you are loading. The default selection is Image.

Use Data Mappings (listed below) if you prefer to set these values dynamically. But remember, mapping will take precedence over the values supplied in the Tag fields.

### Load Rules

[Load Rules]() determine when and where to load an instance of this Tag on your site. You may load this on all pages of your site using the default **All Pages** rule. Or create and apply custom Load Rules if you want to load it on specific pages only.

### Data Mappings

Mapping is the process of sending data from a [Data Layer Variable]() to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the MediaMath Tag are built into its Data Mapping tab. Available categories are:

#### Standard

|Tag Destination| Description|
|---| ---|
|Tag Type| Type of MediaMath pixel you are loading. |
|Pixel ID (formerly Event ID)| Pixel identifier you received from MediaMath|
|Advertising ID| Advertiser identifier you received from MediaMath|
|Hashed Customer Email| Hashed email address of the customer|
|Hashed User/Customer ID| Hashed identifier assigned to the customer |
|v1 through v3| Map additional data to these destinations|
|v.n| Use this for mapping to v4 and higher. Replace `n` with any number above 3.|
|s1 through s3| Map additional data to these destinations. If you&#39;re using MediaMath for conversion tracking, you can map e-commerce data to these destinations|
|s.n| Use this for mapping to s4 and higher. Replace `n` with any number above 3.|
