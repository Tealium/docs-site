---
title: Schema App Tag Setup Guide
description: This article describes how to set up the Schema App tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/schema-app-tag/
---
## Tag tips

* The account ID can be found in the application under **Integrations &gt; JavaScript**.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see .

After adding the tag, configure the following settings:

* **Account ID**: Your Schema App account ID.
* **Output Cache**: Enable output caching. The default value is `False`.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Type | Description|
|---| ---| ---|
| `account_id` | String | Account ID.|
| `output_cache` | Boolean | Enable output caching. |
| `base_url` | String | Base URL/API endpoint. |