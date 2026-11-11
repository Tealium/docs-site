---
title: Knotch Tag Setup Guide
description: This article describes how to configure the Knotch Tag.
url: https://docs.tealium.com/client-side-tags/knotch-tag/
---
## Tag tips

* Minimum utag.js Version: 4.36. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* Use mapping to dynamically override the standard configuration values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable          | Description                                                                                                                                  |
|:------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| `unit_id`         | <ul><li>Your Knotch Unit ID.</li><li>For example, `knotch_12ab3cd456ef789a0bc12345`</li></ul>                                                    |
| `tag_type`        | <ul><li>Values are `js` or `iframe`</li></ul>                                                                                                |
| `target_element`  | <ul><li>The DOM ID of the element (already on the page) where the Knotch widget should appear.</li></ul>                                     |
| `widget_position` | <ul><li>The position of the Knotch widget relative to the target element.</li><li>Values are `append_child`, `before`, or `after`.</li></ul> |
