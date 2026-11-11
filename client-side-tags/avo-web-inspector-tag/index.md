---
title: Avo Web Inspector tag
description: This article describes how to set up the Avo Web Inspector tag.
url: https://docs.tealium.com/client-side-tags/avo-web-inspector-tag/
---
Avo Web Inspector analyzes the analytics events sent from your website, without collecting the actual data. Based on that analysis Avo automatically builds a single source of truth tracking plan, covering all your products and platforms, giving you a complete overview of which is tracking what, and which is not.

## Tag tips

* Use mapping to override the standard config values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **API Key**: The API key obtained from the **Sources** tab in your Avo.app workspace.
* **Environment**: The environment to use: **prod**, **qa**, or **staging**.
* **Version**: The Avo app version. Many Avo Inspector features rely on a specific version.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
|`api_key`  | String |  API Key  |
|  `environment`  | String | Environment |
|  `version`  | String | Version |

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `appName`  | String | App Name |

### Event-specific Parameters
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `allEvents` | All Events |
| `custom` | Custom Events |

    