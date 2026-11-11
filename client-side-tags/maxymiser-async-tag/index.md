---
title: Maxymiser (Async) Tag Setup Guide
description: This article describes how to set up the Maxymiser (Async) tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/maxymiser-async-tag/
---
Maxymiser empowers brands to transform every digital interaction into seamless, relevant and engaging customer experiences with its cloud-based testing, personalization and cross-channel optimization solutions.

## Tag tips

* Contact Maxymiser before using this tag to confirm that your Maxymiser library is set up to be loaded asynchronously.
* If you need to load Maxymiser synchronously, paste the Maxymiser code into `utag.sync.js` or use the Maxymiser (Sync) tag instead of this one.
* For best performance:
  * Advanced Settings: Set **Tag Timing** to **Prioritized**.
  * Move this tag to the top of your list of tags (so that it loads first).
  * Publish Settings: Enable Bundling
  * Move `utag.js` to the top of the body

* Use mapping to:
  * Disable the tag on a page-by-page basis.
  * Pass additional data to Maxymiser (must be enabled on your Maxymiser account).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Library URL**: The `mmcore.js` library URL provided by Maxymiser.  
Example:  
`//service.maxymiser.net/cdn/tealium/js/mmcore.js`  
This should start with `//`. Do not include `http:` or `https:`.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable                         | Description                                |
|:---------------------------------|:-------------------------------------------|
| Library URL                      | (`library_url`)                            |
| Disable Maxymiser                | (`mm_disable`)                             |
| Load Test Content Asynchronously | (`mm_async`) (Overrides default of `true`) |
| Custom                           | (`custom.myvar`)                           |
