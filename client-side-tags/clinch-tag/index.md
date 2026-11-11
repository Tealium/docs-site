---
title: Clinch Tag Setup Guide
description: This article describes how to set up the Clinch tag.
url: https://docs.tealium.com/client-side-tags/clinch-tag/
---
Clinch is a platform that uses creative automation tools, data access, and smart ad serving to optimize dynamic ads in real-time. It makes running hyper-personalized ads easy and effective, while offering true omnichannel personalization, dynamic video (DCO), and consumer intelligence. Use this tag to manage the clinch-sid cookie.

## Tag tips

* Use mappings to override standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client encoded ID**: Specify the unique identifier for the client in an encoded format.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `encodedId` | `String` | The client encoded ID. |
