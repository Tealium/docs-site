---
title: Schema App Tag Setup Guide
description: This article describes how to set up the Schema App tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/schema-app-tag/
---
## Tag tips

* The account ID can be found in the application under **Integrations > JavaScript**.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**: Your Schema App account ID.
* **Output Cache**: Enable output caching. The default value is `False`.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Type | Description|
|---| ---| ---|
| `account_id` | String | Account ID.|
| `output_cache` | Boolean | Enable output caching. |
| `base_url` | String | Base URL/API endpoint. |