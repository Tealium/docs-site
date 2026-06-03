---
title: InnovidXP Connector Setup Guide
description: This article describes how to set up the InnovidXP connector.
url: https://docs.tealium.com/server-side-connectors/innovidxp-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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

The `servertrack` and `RAND` parameters are automatically set by Tealium.

|**Parameter**| **Description**|
|---| ---|
|Visitor ID (`VISITORID`)|  &lt;ul&gt;&lt;li&gt;(Required) Unique ID for the visitor.&lt;/li&gt;&lt;li&gt;URL parameters to be encoded in the server-to-server request.&lt;/li&gt;&lt;li&gt;For example, `0123456789ABCDEF`.&lt;/li&gt;&lt;/ul&gt; |
|User Agent (`UA`)|  &lt;ul&gt;&lt;li&gt;User agent, if applicable.&lt;/li&gt;&lt;li&gt;For example, `Mozilla/5.0`.&lt;/li&gt;&lt;/ul&gt; |
|Browser Language (`LANG`)|  &lt;ul&gt;&lt;li&gt;Browser language, if applicable.&lt;/li&gt;&lt;li&gt;For example, `en`.&lt;/li&gt;&lt;/ul&gt; |

#### Session Parameters (`_cvar`)

The following table lists the fine-grained session-level tracking information:

|**Parameter**| **Description**|
|---| ---|
|`appid`|  &lt;ul&gt;&lt;li&gt;ID of the app.&lt;/li&gt;&lt;li&gt;For example, `com.myapp.appster`.&lt;/li&gt;&lt;/ul&gt; |
|`appname`|  &lt;ul&gt;&lt;li&gt;Name of the app.&lt;/li&gt;&lt;li&gt;For example, My Application.&lt;/li&gt;&lt;/ul&gt; |
|`country`|  &lt;ul&gt;&lt;li&gt;Country.&lt;/li&gt;&lt;li&gt;For example, `US`.&lt;/li&gt;&lt;/ul&gt; |
|`deviceid`|  &lt;ul&gt;&lt;li&gt;Device ID.&lt;/li&gt;&lt;li&gt;For example, `e3f5536a141811db40efd6400f1d0a4e`.&lt;/li&gt;&lt;/ul&gt; |
|`deviceidtype`|  &lt;ul&gt;&lt;li&gt;Device ID type.&lt;/li&gt;&lt;li&gt;For example, `AAID` or `IDFA`.&lt;/li&gt;&lt;/ul&gt; |
|`ip`|  &lt;ul&gt;&lt;li&gt;(Required) The IP address of the mobile device.&lt;/li&gt;&lt;li&gt;For example, `8.8.8.8`.&lt;/li&gt;&lt;/ul&gt; |
|`lang`|  &lt;ul&gt;&lt;li&gt;User language.&lt;/li&gt;&lt;li&gt;For example, `en`.&lt;/li&gt;&lt;/ul&gt; |
|`medium`|  &lt;ul&gt;&lt;li&gt;(Required) Set to `app` for mobile app.&lt;/li&gt;&lt;li&gt;For example, `app`.&lt;/li&gt;&lt;/ul&gt; |
|`os`|  &lt;ul&gt;&lt;li&gt;Operating system.&lt;/li&gt;&lt;li&gt;For example, `ANDROID`.&lt;/li&gt;&lt;/ul&gt; |
|`source`|  &lt;ul&gt;&lt;li&gt;(Required) Identifies the name of the partner supplying the data.&lt;/li&gt;&lt;li&gt;For example, `myApplication`&lt;/li&gt;&lt;/ul&gt; |
|`ua`|  &lt;ul&gt;&lt;li&gt;User Agent.&lt;/li&gt;&lt;li&gt;For example, `Mozilla/5.0`.&lt;/li&gt;&lt;/ul&gt; |
|`user`|  &lt;ul&gt;&lt;li&gt;User ID.&lt;/li&gt;&lt;li&gt;Client-supplied private unique user identifier, such as an internal ID from a billing system.&lt;/li&gt;&lt;li&gt;For example, `U1234`.&lt;/li&gt;&lt;/ul&gt; |

#### Action Parameters (`cvar`)

The following table lists the fine-grained per-action tracking information:

|**Parameter**| **Description**|
|---| ---|
|Action Name|  &lt;ul&gt;&lt;li&gt;(Required) Name of the action being performed.&lt;/li&gt;&lt;li&gt;For example, `INSTALL`.&lt;/li&gt;&lt;/ul&gt; |
|`adchannel`|  &lt;ul&gt;&lt;li&gt;Advertising channel name.&lt;/li&gt;&lt;li&gt;For example, `Social`.&lt;/li&gt;&lt;/ul&gt; |
|`campaign`|  &lt;ul&gt;&lt;li&gt;Campaign name.&lt;/li&gt;&lt;li&gt;For example, `NY_Acquisition`.&lt;/li&gt;&lt;/ul&gt; |
|`currency`|  &lt;ul&gt;&lt;li&gt;Currency of revenue.&lt;/li&gt;&lt;li&gt;For example, `USD`.&lt;/li&gt;&lt;/ul&gt; |
|`id`|  &lt;ul&gt;&lt;li&gt;Action ID of an individual user action, such as an order ID.&lt;/li&gt;&lt;li&gt;For example, `42342`.&lt;/li&gt;&lt;/ul&gt; |
|`preattributed`|  &lt;ul&gt;&lt;li&gt;Whether the event has already been attributed.&lt;/li&gt;&lt;li&gt;For example, `1`.&lt;/li&gt;&lt;/ul&gt; |
|`prod`|  &lt;ul&gt;&lt;li&gt;Product name.&lt;/li&gt;&lt;li&gt;For example, `angry birds`.&lt;/li&gt;&lt;/ul&gt; |
|`promo`|  &lt;ul&gt;&lt;li&gt;The promo code, if the user used one.&lt;/li&gt;&lt;li&gt;For example, `ABCD`.&lt;/li&gt;&lt;/ul&gt; |
|`rev`|  &lt;ul&gt;&lt;li&gt;Revenue amount.&lt;/li&gt;&lt;li&gt;If not specified, is supplied by default.&lt;/li&gt;&lt;li&gt;For example, `12`.&lt;/li&gt;&lt;/ul&gt; |
|`ts`|  &lt;ul&gt;&lt;li&gt;Exact Unix timestamp of event, in UTC format.&lt;/li&gt;&lt;li&gt;If not provided, will be provided by default.&lt;/li&gt;&lt;li&gt;For example, `1538996046`.&lt;/li&gt;&lt;/ul&gt; |
