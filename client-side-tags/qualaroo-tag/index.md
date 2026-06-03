---
title: Qualaroo Tag
description: This article describes how to set up the Qualaroo tag.
url: https://docs.tealium.com/client-side-tags/qualaroo-tag/
---
## Tag tips

* Use mapping to override the standard configuration values dynamically.
* To send an email address (or other identifier) for logged-in customers, assign that value to `identify` with a mapping.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **JavaScript File Path**: The path to the Qualaroo JavaScipt library file. For example, `s3.amazonaws.com/ki.js/12345/example.js`

## Load rules

Load the tag on all pages or set conditions for when the tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
| `jspath`| String | The path to the Qualaroo JavaScipt library file. For example, `s3.amazonaws.com/ki.js/12345/example.js`  |
|`identify`| String | The email address or other identifier parameter.  | 

    