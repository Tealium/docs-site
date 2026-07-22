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

* Tag Documentation: [iSpot TV Cookie Matching Service Tag Setup Guide](https://docs.tealium.com/ispot-tv-cookie-matching-service-tag/).

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Pixel      | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Site ID**
  * The tracking code requires a unique Site ID for each unique web site or app, which will be provided by iSpot.
  * The format for Site ID is `TC-1234-1`, where:
    * `TC` represents the tracking code.
    * `1234` is the client's account ID.
    * `-1` is the site identifier, which increments per site.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

| **Parameter** | **Description**        |
|:--------------|:-----------------------|
| IP Address    | <ul><li>IP address should be IPv4 only.</li><li>For example: `192.168.0.1`</li><li>Tealium passes the value in the `X-Forwarded-For` request header.</li></ul>           |
| User Agent    | <ul><li>The user agent of the original client device.</li><li>Tealium passes the `User-Agent` in the request header.</li></ul>          |
| User Agent    | <ul><li>Set to User Agent to the user agent of the original client device.</li><li>Tealium passes the `User-Agent` in the request header.</li></ul>          |
| Cookies       | <ul><li>The iSpot cookie is sent as part of the Cookie request header.</li><li>The value of this cookie can be derived from the original client-side browser through a JSON response from the service.</li><li>For example: `https://ps.ispot.tv/v2/your-site-id.gif`</li></ul>     |
| Referrer      | <ul><li>Referrer of the original visit, which is sent in the referrer request header.</li></ul>         |
| Event Time    | <ul><li>If the time difference between the client visit and server-side request is greater than a few minutes, set Event Time to the original UTC time of the client visit in `yyyy-MM-dd hh:mm:ss` format</li><li>If you do not specify an Event Time, the connector generates one at execution time.</li></ul> |
| Custom Data   | <ul><li>The iSpot Tracking Code supports passing custom data for your business goals.</li><li>Pass individual attributes in this section, and the connector combines them into a URL-encoded JSON object.</li></ul>                                                                                         |