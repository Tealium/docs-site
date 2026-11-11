---
title: Medallia Digital Tag Setup Guide
description: This article describes how to set up the Medallia Digital tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/medallia-digital-tag/
---
Medallia gives you the customer experience management tools to create beautifully branded and highly targeted dialogues, with more than 25 specific ways to engage during web, mobile web, or in-app interactions.

## Tag tips

* Use mapping to override standard configuration values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Website ID**: Numeric value for site ID. For example, `https://resources.digital-cloud-west.medallia.com/{Path}/{WebSiteID}/onsite/embed.js`.
* **Path**: A string found in your Medallia Digital URL. For example, `https://resources.digital-cloud-west.medallia.com/{Path}/{WebSiteID}/onsite/embed.js`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------| ---| :------------|
| Website ID | Number | Numeric value for site ID. |
| Path | String | A string found in your Medallia Digital URL. |

    