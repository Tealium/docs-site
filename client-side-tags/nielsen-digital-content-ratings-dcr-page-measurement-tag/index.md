---
title: Nielsen Digital Content Ratings (DCR) - Page Measurement Tag Setup Guide
description: This article describes how to configure the Nielsen Digital Content Ratings (DCR) - Page Measurement tag in your iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/nielsen-digital-content-ratings-dcr-page-measurement-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the Nielsen Digital Content Ratings (DCR) - Page Measurement Tag to your profile (See [Add a tag]()).

After adding the Tag, configure the below settings:

1. **Client ID**: Your Nielsen client identifier. This is passed to Nielsen in the `nol_ci` key.
1. **Sub-brand ID**: Your Nielsen Sub-brand ID. This is passed to Nielsen in the `nol_vc` key.
1. **App ID**: Unique Nielsen ID assigned to player/site. This is passed to Nielsen in the `nol_apid` key.
1. **Publisher Name**: User-defined string value for identifying your player/site. This is passed to Nielsen in the `nol_apn` key.
1. **Collection Environment**: Location of Nielsen Collection Environment. This is passed to Nielsen in the `nol_sfcode` key.
1. **Use Path for Site Section**: When set to `yes`, the first folder in the web page&#39;s path is used for Site Section. If the first folder is absent or not available, the **Site Section** value will default to `home`. The **Site Section** value can also be configured through Data Mappings (see below).

Site Section reporting is limited to a maximum of 25 unique values.

## Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **Load on all pages**.

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Nielsen Digital Content Ratings (DCR) - Page Measurement Tag are built into its Data Mapping tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Client ID| Nielsen Client ID. Overrides the value set in the Vendor Configuration. See Tag Configuration above for details.|
|Sub-brand ID| Nielsen Sub-brand ID. Overrides the value set in the Vendor Configuration. See Tag Configuration above for details.|
|Site Section| Lets you send custom site sections (limited to a maximum of 25 unique values). This is passed to Nielsen in the `nol_assetname` key. If the mapping returns an empty value, then **Site Section** will be set to the default value of `home`. **NOTE**: If you are mapping to this destination, be sure to turn off the **Use Path for Site Section** toggle in the **Tag** settings.|
|Custom Segment A| Custom Segment reporting is limited to a maximum of 25 unique values across custom segments A, B, and C (`nol_segA &#43; nol_segB &#43; nol_segC &lt;= 25`). This passed to Nielsen in the `nol_segA` key.|
|Custom Segment B| Custom Segment reporting is limited to a maximum of 25 unique values across custom segments A, B, and C (`nol_segA &#43; nol_segB &#43; nol_segC &lt;= 25`). This passed to Nielsen in the `nol_segB` key.|
|Custom Segment C| Custom Segment reporting is limited to a maximum of 25 unique values across custom segments A, B, and C (`nol_segA &#43; nol_segB &#43; nol_segC &lt;= 25`). This passed to Nielsen in the `nol_segC` key.|

## Vendor Documentation

* [Static Page Measurement - Implementation Guide](https://engineeringforum.nielsen.com/sdk/developers/product-dcr-implementation-static-bsdk.php)
* [Static Lite Page Measurement - Implementation Guide](https://engineeringforum.nielsen.com/sdk/developers/product-dcr-implementation-static-lite-bsdk.php)
