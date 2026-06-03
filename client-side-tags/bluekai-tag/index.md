---
title: BlueKai Tag Setup Guide
description: This article describes how to set up the BlueKai tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/bluekai-tag/
---
## Tag Tips

Use mapping to override the standard configuration values or to pass additional parameters.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

After adding the tag, configure the following variables:

* **Site ID**: Unique number that identifies a pixel as belonging to a certain DMP Partner.
* **Limit**: Maximum number of media partner segment pixels that will be fired by BlueKai.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The following variables are available for the BlueKai tag:

### Standard

|Variable| Description|
|---| ---|
|Site ID| (siteid)|
|Limit| (limit)|
|Allow Multiple Calls (`allow_multiple_calls`)| [boolean]|
|show| |
|tod| |
|lv| |
|ss| |
|top| |
|sub1| |
|sub2| |
|sub3| |
|ref| |
|srch| |
