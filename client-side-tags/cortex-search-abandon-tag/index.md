---
title: Cortex Search Abandon Tag Setup Guide
description: This article describes how to set up the Cortex Search Abandon tag.
url: https://docs.tealium.com/client-side-tags/cortex-search-abandon-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the Cortex Search Abandon Tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the rag, configure the below settings:

* **Site ID:** Enter the unique site identifier you received from Cortex.

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: Set up custom rule(s) to load this tag on specific pages where you want to track search activity.

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a Variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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
