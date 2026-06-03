---
title: Optimise Media Conversion Tag Setup Guide
description: This article describes how to set up the Optimise Media Conversion Tag tag.
url: https://docs.tealium.com/client-side-tags/optimise-media-conversion-tag/
---
## Tag tips
* Use mappings to:
    * Dynamically override the standard config values
    * Dynamically override the E-Commerce extension values
    * Add additional query string parameters
* Map extended data values to `ex1-ex11`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Merchant Identifier (MID)**: An numeric value.
* **Product Identifier (PID)**: An numeric value.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `mid` | Merchant identifier |
| `pid` | Product identifier |
| `channel` | Channel |
| `cust_type` | Customer type |
| `action` | Action |
| `ex1-ex11` | Extended data values |
    