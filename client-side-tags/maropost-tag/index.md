---
title: Maropost Tag Setup Guide
description: This article describes how to set up the Maropost tag.
url: https://docs.tealium.com/client-side-tags/maropost-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the Maropost Web Tracking tag to your profile (See [Add a tag]()).

After adding the tag, configure the below settings:

* Account ID: An integer corresponding to your Maropost account ID
* Website ID: An integer corresponding to your specific web site that is being tracked
* Tracking Script File Name: A secure scramble of the file name for the web tracking Javascript function. It is unique for each account and for each web site. Embedded in the file name is the version of the script.

## Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Maropost Web Tracking tag are built into its **Data Mapping** tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Account ID| Your Maropost account ID. Use this to override the configuration value.|
|Website ID| The ID for your website. Use this to dynamically override the vendor configuration value.|
|Tracking Script File Name| The secure scramble for your web tracking function&#39;s filename. Use this to dynamically override the configuration value.|
