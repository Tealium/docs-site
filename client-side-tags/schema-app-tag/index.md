---
title: Schema App Tag Setup Guide
description: This article describes how to set up the Schema App tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/schema-app-tag/
---
## Tag tips

* The account ID can be found in the application under **Integrations > JavaScript**.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

After adding the tag, configure the following settings:

* **Account ID**: Your Schema App account ID.
* **Output Cache**: Enable output caching. The default value is `False`.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Type | Description|
|---| ---| ---|
| `account_id` | String | Account ID.|
| `output_cache` | Boolean | Enable output caching. |
| `base_url` | String | Base URL/API endpoint. |