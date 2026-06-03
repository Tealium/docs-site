---
title: comScore Mobile JS Tracking Tag Setup Guide
description: This article describes how to set up the comScore Mobile JS Tracking tag.
url: https://docs.tealium.com/client-side-tags/comscore-mobile-js-tracking-tag/
---
## Tag tips

* This tag is for use within a native mobile app. It is not intended for use on mobile web site implementations.
* Use mapping to set additional parameters and to override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Client ID**
* **Publisher Secret Key**
* **Enable Auto Update**
* **Keep Alive Event**

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `clientID` | clientID  |
| `pub_key` | pub_key  |
| `appName` | appName  |
| `appVersion` | appVersion |
| `keepAliveEnabled` | keepAliveEnabled, true/false, default is true. |
| `enableAutoUpdate` | enableAutoUpdate, true/false, default is false. |
| `update_interval` | update_interval |
| `update_foregroundOnly` | update_foregroundOnly |
| `view_name` | Page View Name |

### Labels

| Variable | Description |
|:---------|:------------|
| `labels.ns_site` | comscore_site |
| `labels.####` | Custom Label |
| `autoStartLabels.####` | Auto Start Label |

### Events
To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Description |
|:---------|:------------|
| `active` | Active |
| `aggregate` | Aggregate |
| `close` | Close |
| `inactive` | Inactive |
| `hidden` | Hidden |
| `launch` | Launch |
| `sleep` | Sleep |
| `view` | View |
| `wake` | Wake |

### Platform

| Variable | Description |
|:---------|:------------|
| `plat.appName` | AppName |
| `plat.appVersion` | App Version |
| `plat.visitorId` | Visitor ID, overrides `_ccustid` |
| `plat.deviceName` | Device Name |
| `plat.version` | Platform Version |
| `plat.name` | Platform Name |
| `plat.runtime` | Runtime Version |
| `plat.os_version` | OS Version  |
| `plat.dev_resolution` | Device Resolution |
| `plat.dev_language` | Device Language |
| `plat.app_rdns` | Package Name |
| `plat.connection_type` | Connection Type |
| `plat.visitorIDSuffix` | Visitor ID Suffix |