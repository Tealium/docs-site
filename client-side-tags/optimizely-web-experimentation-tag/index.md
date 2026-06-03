---
title: Optimizely Web Experimentation Tag Setup Guide
description: This article describes how to set up the Optimizely Web Experimentation tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/optimizely-web-experimentation-tag/
---
## Tag tips

*   Use mapping to override the standard configuration value for Project ID.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Project ID**: Project ID is the number part of the path to the `.js` file (for example, `1234567` in `//cdn.optimizely.com/js/1234567.js`).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pid` | String | Project ID. |

### Event-Specific Tags

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event    | Description          |
|:---------|:---------------------|
| `revenue`| Revenue in cents.    |
| `value`  | Value.               |
| `custom` | Custom value.        |

### Event-Specific Properties

To map properties for specific events, first select the property, then enter the event name for which this mapping will occur. If using a custom property, select the **Custom** option and enter the name in the field that appears.

| Property    | Description            |
|:------------|:-----------------------|
| Category    | Category.              |
| Subcategory | Subcategory.           |
| Text        | Text.                  |
| URL         | URL.                   |
| SKU         | SKU.                   |
| Custom      | Custom property.       |