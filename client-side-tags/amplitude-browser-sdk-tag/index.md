---
title: Amplitude Browser SDK Tag Setup Guide
description: This article describes how to set up the Amplitude Browser SDK tag in your Tealium account.
url: https://docs.tealium.com/client-side-tags/amplitude-browser-sdk-tag/
---
Amplitude is a leading digital analytics platform that helps companies unlock the power of their products. The Browser SDK lets you send events to Amplitude.

## Vendor information

This tag implements the following vendor API:

* [Amplitude Browser SDK 2](https://amplitude.com/docs/sdks/analytics/browser/browser-sdk-2)
* [Amplitude: Migrate from Javascript SDK to Browser SDK 1.0](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-javascript-sdk-to-browser-sdk-1-0)
* [Amplitude: Migrate from Javascript SDK 1.0 to Browser SDK 2.0](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-browser-sdk-1-0-to-2-0)

## Tag tips

* Conversion fires when Order ID is set.
* The Customer ID is sent as the `userId` with the `amplitude.init()` call if populated.
* Supports these E-Commerce extension parameters:
    * Order ID (`_corder`)
    * Cart or Order Type (`_ctype`)
    * Customer ID (`_ccustid`)
    * List of Product IDs (`_cprod`)
    * List of Quantities (`_cquan`)
    * List of Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **API Key**: Your Amplitude project&#39;s API key.
* **SDK Version**: The version of the library to load. The default is version 2.6.0.
* **Session Replay**: Enable or disable session replay.
* **Session Replay Version**: The version of the library to load. The default value is 1.13.9.
* **Enable Guides and Surveys**: Enable or disable guides and surveys.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `api_key`  | String | API key |
| `sdk_version`  | String | SDK version |
| `defaultTracking`  | Boolean | Default tracking|
| `deviceId`  | String | Device ID |
| `flushIntervalMillis`  | Number | Flush interval in milliseconds |
| `flushQueueSize`  | Number | Flush queue size |
| `flushMaxRetries`  | Number | Flush maximum retries |
| `identityStorage`  | String | Identity storage |
| `logLevel`  | String | Log level |
| `optOut`  | Boolean | Opt out |
| `serverUrl`  | String | Server URL |
| `serverZone`  | String | Sever zone |
| `transport`  | String | Transport |
| `useBatch`  | Boolean | Use batch |
| `userId`  | Number | User ID |
| `session_replay` | Boolean | Enable session replay |
| `session_replay_version` | String | Session replay version |
| `guides_and_surveys` | Boolean | Enable guides and surveys |

### User Properties

| Variable | Description |
|:---------|:------------|
| `add.custom` | Increment the numerical value by a specified number |
| `append.custom` | Append the value to the property array |
| `prepend.custom` | Prepend the value to the property array |
| `set.custom` | Set or overwrite the property value |
| `setOnce.custom` | Set the value, and once set these values cannot be overwritten |
| `unset.custom` | Unset the value to null |

### Events

| Variable | Description |
|:---------|:------------|
| `event_type` | Event type |
| `eventProperties.custom` | Event properties  |
| `groups.custom` | Groups |

### Revenue Tracking/E-Commerce

| Variable | Type | Description |
|:---------|:-----|:------------|
| `order_id`  | String | Order ID (overrides `_corder`) | 
| `order_type`  | String | Cart or order type (overrides `_ctype`) |
| `customer_id`  | String | Customer ID (overrides `_ccustid`) |
| `product_id`  | Array | List of product IDs (overrides `_cprod`) |
| `product_quantity`  | Array | List of product quantities (overrides `_cquan`) |
| `product_unit_price`  | Array | List of product prices (overrides `_cprice`) |

### User Groups

| Variable | Description |
|:---------|:------------|
| `group.custom`  |  |

### Default Tracking

| Variable | Type |
|:---------|:-----|
| `attribution`  | Boolean |
| `pageViews`  | Boolean |
| `sessions`  | Boolean |
| `formInteractions`  | Boolean |
| `fileDownloads`  | Boolean |

### Tracking Options

| Variable | Type |
|:---------|:-----|
| `ipAddress`  | Boolean |
| `language`  | Boolean |
| `platform`  | Boolean |

### Cookie Options

| Variable | Type |
|:---------|:-----|
| `domain`  | String |
| `expiration`  | Number |
| `sameSite`  | String |
| `secure`  | Boolean |
| `upgrade`  | Boolean |

    