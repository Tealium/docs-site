---
title: iSpot TV Conversion Tracking Connector Setup Guide
description: This article describes how to set up the iSpot TV Conversion Tracking connector.
url: https://docs.tealium.com/server-side-connectors/ispot-tv-conversion-tracking-connector/
---
## How it works

iSpot TV Conversion Analytics connects TV ad exposures across more than 17 million TVs with your first-party website and app data using a tracking code. Each TV set is connected to the home network, making the home IP address accessible to iSpot. This enables iSpot to connect TV ad exposures with your data sets that are associated with IP addresses. This results in powerful closed-loop analytics around how TV creative, media and frequency drives sales and other critical KPIs. The entire process is done in a Personally Identifiable Information (PII)-compliant manner. 

## Connector tips

We recommend a hybrid setup using both a tag and a connector. This configuration ensures maximum data resilience, improves event matching with server-side signals, and maintains data flow continuity while retaining real-time client-side signals.

## Tag documentation

* Tag Documentation: [iSpot TV Cookie Matching Service Tag Setup Guide]().

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Pixel      | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Site ID**
  * The tracking code requires a unique Site ID for each unique web site or app, which will be provided by iSpot.
  * The format for Site ID is `TC-1234-1`, where:
    * `TC` represents the tracking code.
    * `1234` is the client&#39;s account ID.
    * `-1` is the site identifier, which increments per site.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

| **Parameter** | **Description**        |
|:--------------|:-----------------------|
| IP Address    | &lt;ul&gt;&lt;li&gt;IP address should be IPv4 only.&lt;/li&gt;&lt;li&gt;For example: `192.168.0.1`&lt;/li&gt;&lt;li&gt;Tealium passes the value in the `X-Forwarded-For` request header.&lt;/li&gt;&lt;/ul&gt;           |
| User Agent    | &lt;ul&gt;&lt;li&gt;The user agent of the original client device.&lt;/li&gt;&lt;li&gt;Tealium passes the `User-Agent` in the request header.&lt;/li&gt;&lt;/ul&gt;          |
| User Agent    | &lt;ul&gt;&lt;li&gt;Set to User Agent to the user agent of the original client device.&lt;/li&gt;&lt;li&gt;Tealium passes the `User-Agent` in the request header.&lt;/li&gt;&lt;/ul&gt;          |
| Cookies       | &lt;ul&gt;&lt;li&gt;The iSpot cookie is sent as part of the Cookie request header.&lt;/li&gt;&lt;li&gt;The value of this cookie can be derived from the original client-side browser through a JSON response from the service.&lt;/li&gt;&lt;li&gt;For example: `https://ps.ispot.tv/v2/your-site-id.gif`&lt;/li&gt;&lt;/ul&gt;     |
| Referrer      | &lt;ul&gt;&lt;li&gt;Referrer of the original visit, which is sent in the referrer request header.&lt;/li&gt;&lt;/ul&gt;         |
| Event Time    | &lt;ul&gt;&lt;li&gt;If the time difference between the client visit and server-side request is greater than a few minutes, set Event Time to the original UTC time of the client visit in `yyyy-MM-dd hh:mm:ss` format&lt;/li&gt;&lt;li&gt;If you do not specify an Event Time, the connector generates one at execution time.&lt;/li&gt;&lt;/ul&gt; |
| Custom Data   | &lt;ul&gt;&lt;li&gt;The iSpot Tracking Code supports passing custom data for your business goals.&lt;/li&gt;&lt;li&gt;Pass individual attributes in this section, and the connector combines them into a URL-encoded JSON object.&lt;/li&gt;&lt;/ul&gt;                                                                                         |