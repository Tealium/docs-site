---
title: Cortex Search Abandon Tag Setup Guide
description: This article describes how to set up the Cortex Search Abandon tag.
url: https://docs.tealium.com/client-side-tags/cortex-search-abandon-tag/
---
## Tag configuration

First, go to the tag marketplace and add the Cortex Search Abandon Tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the rag, configure the below settings:

* **Site ID:** Enter the unique site identifier you received from Cortex.

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: Set up custom rule(s) to load this tag on specific pages where you want to track search activity.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the Cortex Search Abandon Tag are built into its Data Mapping tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Site ID| site identifier provided by Cortex|
|User Email| visitor email|
|Search Term| search keyword used by visitor|

### E-Commerce

Since the Cortex Search Abandon Tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings
* an ecommerce variable you want is not offered in the extension

|**Destination Name**| **Description**|
|---| ---|
|User ID| unique visitor identifier|

## Vendor Documentation

* [Cortex Help Documentation](http://help.retentionscience.com/hc/en-us/articles/115000423328-Search-Abandon)
