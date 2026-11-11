---
title: ObservePoint Data Layer Validator Tag Setup Guide
description: This article describes how to configure the ObservePoint Data Layer Validator tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/observepoint-data-layer-validator-tag/
---
## How it works

Use the ObservePoint Mobile Data Layer to validate your data layer within ObservePoint. This enhances the ObservePoint mobile app testing to match the capabilities of the web testing in reviewing the data layer.

## Tag tips

* This tag should not be run in a production environment
* The ObservePoint object name defaults to the value `utagdata`.
* The Data Layer object defaults to the value `b`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **ObservePoint Object Name**  
This is the name that appears in the ObservePoint user interface.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `op_object_name` | ObservePoint Object Name|
| `op_object` | Data Layer Object|
