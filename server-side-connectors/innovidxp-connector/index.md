---
title: InnovidXP Connector Setup Guide
description: This article describes how to set up the InnovidXP connector.
url: https://docs.tealium.com/server-side-connectors/innovidxp-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client Host**
  * Client-specific collector hostname.
  * A static value supplied by InnovidXP.
  * For example, `collector-1233.tvsquared.com`.

* **Site ID**
  * Client-specific collector site ID.
  * A static value supplied by InnovidXP.
  * For example, `TV1234-1`.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Track Event| ✓| ✓|

### Track Event

#### URL Parameters

The following table lists URL parameter to be encoded in the server-to-server request:


<blockquote>
The `servertrack` and `RAND` parameters are automatically set by Tealium.
</blockquote>


|**Parameter**| **Description**|
|---| ---|
|Visitor ID (`VISITORID`)|  <ul><li>(Required) Unique ID for the visitor.</li><li>URL parameters to be encoded in the server-to-server request.</li><li>For example, `0123456789ABCDEF`.</li></ul> |
|User Agent (`UA`)|  <ul><li>User agent, if applicable.</li><li>For example, `Mozilla/5.0`.</li></ul> |
|Browser Language (`LANG`)|  <ul><li>Browser language, if applicable.</li><li>For example, `en`.</li></ul> |

#### Session Parameters (`_cvar`)

The following table lists the fine-grained session-level tracking information:

|**Parameter**| **Description**|
|---| ---|
|`appid`|  <ul><li>ID of the app.</li><li>For example, `com.myapp.appster`.</li></ul> |
|`appname`|  <ul><li>Name of the app.</li><li>For example, My Application.</li></ul> |
|`country`|  <ul><li>Country.</li><li>For example, `US`.</li></ul> |
|`deviceid`|  <ul><li>Device ID.</li><li>For example, `e3f5536a141811db40efd6400f1d0a4e`.</li></ul> |
|`deviceidtype`|  <ul><li>Device ID type.</li><li>For example, `AAID` or `IDFA`.</li></ul> |
|`ip`|  <ul><li>(Required) The IP address of the mobile device.</li><li>For example, `8.8.8.8`.</li></ul> |
|`lang`|  <ul><li>User language.</li><li>For example, `en`.</li></ul> |
|`medium`|  <ul><li>(Required) Set to `app` for mobile app.</li><li>For example, `app`.</li></ul> |
|`os`|  <ul><li>Operating system.</li><li>For example, `ANDROID`.</li></ul> |
|`source`|  <ul><li>(Required) Identifies the name of the partner supplying the data.</li><li>For example, `myApplication`</li></ul> |
|`ua`|  <ul><li>User Agent.</li><li>For example, `Mozilla/5.0`.</li></ul> |
|`user`|  <ul><li>User ID.</li><li>Client-supplied private unique user identifier, such as an internal ID from a billing system.</li><li>For example, `U1234`.</li></ul> |

#### Action Parameters (`cvar`)

The following table lists the fine-grained per-action tracking information:

|**Parameter**| **Description**|
|---| ---|
|Action Name|  <ul><li>(Required) Name of the action being performed.</li><li>For example, `INSTALL`.</li></ul> |
|`adchannel`|  <ul><li>Advertising channel name.</li><li>For example, `Social`.</li></ul> |
|`campaign`|  <ul><li>Campaign name.</li><li>For example, `NY_Acquisition`.</li></ul> |
|`currency`|  <ul><li>Currency of revenue.</li><li>For example, `USD`.</li></ul> |
|`id`|  <ul><li>Action ID of an individual user action, such as an order ID.</li><li>For example, `42342`.</li></ul> |
|`preattributed`|  <ul><li>Whether the event has already been attributed.</li><li>For example, `1`.</li></ul> |
|`prod`|  <ul><li>Product name.</li><li>For example, `angry birds`.</li></ul> |
|`promo`|  <ul><li>The promo code, if the user used one.</li><li>For example, `ABCD`.</li></ul> |
|`rev`|  <ul><li>Revenue amount.</li><li>If not specified, is supplied by default.</li><li>For example, `12`.</li></ul> |
|`ts`|  <ul><li>Exact Unix timestamp of event, in UTC format.</li><li>If not provided, will be provided by default.</li><li>For example, `1538996046`.</li></ul> |
