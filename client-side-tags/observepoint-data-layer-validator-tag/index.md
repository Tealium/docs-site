---
title: ObservePoint Data Layer Validator Tag Setup Guide
description: This article describes how to configure the ObservePoint Data Layer Validator tag in your iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/observepoint-data-layer-validator-tag/
---
## How it works

Use the ObservePoint Mobile Data Layer to validate your data layer within ObservePoint. This enhances the ObservePoint mobile app testing to match the capabilities of the web testing in reviewing the data layer.

## Tag Tips

* This tag should not be run in a production environment
* The ObservePoint object name defaults to the value `utagdata`.
* The Data Layer object defaults to the value `b`.

## Tag Configuration

First, go to Tealium's tag marketplace and add the ObservePoint Data Layer Validator tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **ObservePoint Object Name**  
This is the name that appears in the ObservePoint user interface.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `op_object_name` | ObservePoint Object Name|
| `op_object` | Data Layer Object|
