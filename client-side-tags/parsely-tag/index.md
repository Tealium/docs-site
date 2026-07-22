---
title: Parse.ly Tag Set Up Guide
description: This article describes how to set up the Parse.ly tag.
url: https://docs.tealium.com/client-side-tags/parsely-tag/
---
## Tag Tips

* No configuration parameters are required for this tag.
* Override `site_id` if you have a Parse.ly-given API key.
* The standard version requires that you place the parsely div id `parsely-root` on your web page which contains an anchor with parameter `data-parsely-site`. This parameter contains your Parse.ly Site ID.
* The DOM-Free version uses the domain that the tag is running on as your Site ID. You can override this value with mapping.
* If you switch between tag versions, you must delete your Parse.ly template for the change to take effect.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tag Version**: Choose between the Standard version (requires the `parsely-root` div and anchor with `data-parsely-site`) or the DOM-Free version (uses the domain as Site ID; can be overridden with mapping).

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable  | Description |
|:----------|:------------|
| `site_id` | Site ID     |