---
title: Maropost Tag Setup Guide
description: This article describes how to set up the Maropost tag.
url: https://docs.tealium.com/client-side-tags/maropost-tag/
---
## Tag configuration

First, go to the tag marketplace and add the Maropost Web Tracking tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

When adding the tag, configure the following settings:

* Account ID: An integer corresponding to your Maropost account ID
* Website ID: An integer corresponding to your specific web site that is being tracked
* Tracking Script File Name: A secure scramble of the file name for the web tracking Javascript function. It is unique for each account and for each web site. Embedded in the file name is the version of the script.

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the Maropost Web Tracking tag are built into its **Data Mapping** tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Account ID| Your Maropost account ID. Use this to override the configuration value.|
|Website ID| The ID for your website. Use this to dynamically override the vendor configuration value.|
|Tracking Script File Name| The secure scramble for your web tracking function's filename. Use this to dynamically override the configuration value.|
