---
title: Salecycle Tag Setup Guide
description: This article describes how to set up the Salecycle tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/salecycle-tag/
---
## Tag tips

*  Use mapping to override the standard configuration values or E-Commerce extension values.
*  Load this tag at the top or towards the top of the load order.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client ID**: The lowercase client ID provided by SaleCycle. This value replaces `clientID` in the script path (for example, `https://s.salecycle.com/clientID/bundle.js`). 
* **Pixel Type**: The type of tag to load. Possible values are `script` and `image`. If you are not sure which to use, use the `script` option.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).