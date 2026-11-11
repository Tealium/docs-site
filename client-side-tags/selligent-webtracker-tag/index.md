---
title: Selligent Webtracker Tag Setup Guide
description: This article describes how to set up the Selligent Webtracker tag.
url: https://docs.tealium.com/client-side-tags/selligent-webtracker-tag/
---
With Selligent cross-channel campaign management, marketers manage interaction from a single solution.

## Tag tips

Use mapping and override `taxtags` to pass in taxonomy tags.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**: Your account ID provided by Selligent.
* **DLL Domain**: Your `.dll` domain. For example: `example.domain.com` in `https://example.domain.com/optiext/webtracker.dll`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `accountid` | Account ID |
| `dll_domain` | DLL domain |
| `taxtags` | Taxonomy tags |
| `nb_segments` | Number of segments |
| `from_airport` | Departure airport |
| `to_airport` | Destination airport |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` | Order `ID` (Overrides `_corder`) |
| `order_total` | Order total (Overrides `_ctotal`) |

## Debug the tag

To test the tag, use a campaign that adds the `m_i` query string parameter to the redirection URL. The `m_i` query string triggers tracking calls, which then create the `m_trk` first-party cookie in the browser and assigns a value to it.