---
title: Parse.ly Tag Set Up Guide
description: This article describes how to set up the Parse.ly tag.
url: https://docs.tealium.com/client-side-tags/parsely-tag/
---
## Tag tips

* No configuration parameters are required for this tag.
* Override `site_id` if you have a Parse.ly-given API key.
* The standard version requires that you place the parsely div id `parsely-root` on your web page which contains an anchor with parameter `data-parsely-site`. This parameter contains your Parse.ly Site ID.
* The DOM-Free version uses the domain that the tag is running on as your Site ID. You can override this value with mapping.
* If you switch between tag versions, you must delete your Parse.ly template for the change to take effect.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag Version**: Choose between the Standard version (requires the `parsely-root` div and anchor with `data-parsely-site`) or the DOM-Free version (uses the domain as Site ID; can be overridden with mapping).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable  | Description |
|:----------|:------------|
| `site_id` | Site ID     |