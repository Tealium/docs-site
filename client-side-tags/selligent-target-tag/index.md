---
title: Selligent Target Tag Setup Guide
description: This article describes how to set up the Selligent Target tag.
url: https://docs.tealium.com/client-side-tags/selligent-target-tag/
---
Selligent is an international digital marketing campaign management solutions vendor with customers in Europe and the USA across industries as diverse as retail, travel and entertainment, media and publishing, and financial services.

## Tag tips

Use mapping to:
* Override the standard config value for Universe ID.
* Set optional config parameters.
* Set a Custom User Identifier.
* Pass tag name/value pairs.
* Specify a post-tracking callback function.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following setting:

* **Universe ID**: Your Selligent Universe ID. Provided by Selligent.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `universe_id` | Universe ID |
| `customIdentifier` | Custom user identifier |
| `tag.mytag` | Custom tag |
| `useConfig` | Use config |
| `finishedCallback` | Callback function |
| `async` | Async |
| `isEvent` | Is event |