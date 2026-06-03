---
title: Clinch Tag Setup Guide
description: This article describes how to set up the Clinch tag.
url: https://docs.tealium.com/client-side-tags/clinch-tag/
---
Clinch is a platform that uses creative automation tools, data access, and smart ad serving to optimize dynamic ads in real-time. It makes running hyper-personalized ads easy and effective, while offering true omnichannel personalization, dynamic video (DCO), and consumer intelligence. Use this tag to manage the clinch-sid cookie.

## Tag Tips

* Use mappings to override standard config values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Client encoded ID**: Specify the unique identifier for the client in an encoded format.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `encodedId` | `String` | The client encoded ID. |
