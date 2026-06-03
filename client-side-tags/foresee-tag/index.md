---
title: Foresee Tag Setup Guide
description: This article describes how to set up the Foresee Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/foresee-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**: The default is &#34;Foresee&#34;. You may replace it with a custom name of choice.
* **File Path**: The URL where your Foresee files/configurations are hosted.   
 For example, `//gateway.foresee.com/sites/XXX/XXX/gateway.min.js`

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

Mapping is the process of sending data from a [Data Layer Variable]() to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Foresee Tag are built into its Data Mapping tab. Available categories are:

### Standard

|Tag Destination| Description|
|---| ---|
|File Path| The URL where your Foresee snippet is hosted|

## Vendor Documentation

[Foresee Developer Portal](https://developer.foresee.com/v1.0/)
