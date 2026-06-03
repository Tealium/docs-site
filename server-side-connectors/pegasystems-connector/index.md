---
title: Pegasystems Connector Setup Guide
description: This article describes how to set up the Pegasystems connector.
url: https://docs.tealium.com/server-side-connectors/pegasystems-connector/
---
## Prerequisites

*   Tealium EventStream or AudienceStream
*   Pega Customer Decision Hub access to the following:
    * Client ID, Client Secret, Access Token URL
    * Implement the [Tealium Customer Data Connector](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/tealium-integration-component.html) component

## How it works

Accurate predictions of customer’s preferences and their next best actions rely on a good understanding of that customer and most recent interactions across all touchpoints. Tealium enhances Pega’s Customer Decision Hub by making it easy to connect this accurate and rich customer data to inform decisions and recommendations.

The Pegasystems connector connects valuable customer data in two ways: 

1.  Tealium and Pega share consolidated customer information based on a 360-degree view of the customer, aggregating all cross-channel signals in a standardized customer profile.
1.  Tealium streams customer interactions across web, app, call-center and other channels in real-time to Pega to provide in-the-moment context for decision making.

The Pegasystems connector supports both EventStream and AudienceStream actions and lets you track page views/interactions through EventStream. Using a customer identifier or cookie ID, you can configure and map differing page types to send interaction history to Pega.

Additionally, trigger next best actions within the Pega Customer Decision Hub by sending audience segments and statuses to Pega along with a customer identifier.

## Connector actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Update Segment Membership Data (Real-Time) | ✓ | ✗ |
| Update Segment Membership Data (Batched) | ✓ | ✗ |
| Send Custom Event Data (Real-Time) | ✗ | ✓ |
| Send Custom Event Data (Batched) | ✗ | ✓ |
| ID Merge | ✓ | ✗ |
| Send Customer Profile Data | ✓ | ✗ |

While Tealium supports batched actions to Pega, we recommend that you discuss your use case configuration and need for batching with your Pega account team.

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Client ID**: (Required) The unique ID that is assigned to the client.
* **Client Secret**: (Required) The password that the system assigns to the client to authenticate with the Pega Platform authorization module.
* **Access Token URL**: (Required) The request URL used to receive an access token for the client as a response after authentication.
* **Authentication method**: (Required) The authentication method used to access the Pega Platform. 
  * **POST**: Send the client credentials in the body of the POST request.
  * **BASIC**: Send the client credentials (Client ID and Client Secret) to the external application as a part of the authorization header.

The REST service authentication used by the client requires **Client ID** and **Client Secret** credentials.

Click **Done** when you are finished configuring the connector.

## Action settings — parameters and options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Update Segment Membership Data (Real-Time)

Use this action to send audience data to Pega to trigger next best action decisioning within the Pega Customer Decision Hub. Send audience data and additional parameters relevant to that visitor&#39;s profile for making a decision in real-time.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Service Endpoint URL | The Service Endpoint URL defined in your Pega system.&lt;br&gt;The **Service Endpoint URL** uses the following structure, but is customizable and may be provided by your Pega contact: `https://&lt;host&gt;:&lt;port&gt;/prweb/PRRestService/&lt;servicepackage&gt;/&lt;serviceclass&gt;/&lt;servicemethod&gt;` |
| Customer ID | (Required) The primary key for a Pega Customer Profile. |
| Name | (Required) The audience name to be sent to the Pega platform. We recommend configuring your audience name or similar value as a string to be passed to Pega. |
| Status | (Required) The audience trigger action to join or leave an audience. Based on the action you select, we recommend that you include mapping **Join** or **Leave** values to the Segment Status field. |
| Namespace | (Required) Any subcategory parameters used to supplement the audience data provided to Pega. |
| Last Qualification Time | (Required) The timestamp when the user joined the audience. Date attributes will be converted to the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format. If not mapped, this parameter will be initialized with the current timestamp in the ISO 8601 format. For example: `2022-08-30T01:13:16.081Z`. |

### Action — Update Segment Membership Data (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

Use this action to send audience data to Pega to trigger next best action decisioning within the Pega Customer Decision Hub. Send audience data and additional parameters relevant to that visitor&#39;s profile for making a decision in real-time.

While Tealium can support batched actions to Pega, we recommend that you discuss your use case configuration and need for batching with your Pega account team.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Service Endpoint URL | The Service Endpoint URL defined in your Pega system.&lt;br&gt;The **Service Endpoint URL** uses the following structure, but is customizable and may be provided by your Pega contact: `https://&lt;host&gt;:&lt;port&gt;/prweb/PRRestService/&lt;servicepackage&gt;/&lt;serviceclass&gt;/&lt;servicemethod&gt;` |
| Customer ID | (Required) The primary key for a Pega Customer Profile. |
| Name | (Required) The audience name to be sent to the Pega platform. We recommend configuring your audience name or similar value as a string to be passed to Pega. |
| Status | (Required) The audience trigger action to join or leave an audience. Based on the action you select, we recommend that you include mapping **Join** or **Leave** values to the Segment Status field. |
| Namespace | (Required) Any subcategory parameters used to supplement the audience data provided to Pega. |
| Last Qualification Time | (Required) The timestamp when the user joined the audience. Date attributes will be converted to the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format. If not mapped, this parameter will be initialized with the current timestamp in the ISO 8601 format. For example: `2022-08-30T01:13:16.081Z`. |

### Action — Send Custom Event Data (Real-Time)

Use this EventStream action to send real-time event data, primarily page views, to Pega for aggregation within the Pegasystems endpoint.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Service Endpoint URL | The value is the Service Endpoint URL defined in your Pega system.&lt;br&gt;The **Service Endpoint URL** uses the following structure, but is customizable and may be provided by your Pega contact: `https://&lt;host&gt;:&lt;port&gt;/prweb/PRRestService/&lt;servicepackage&gt;/&lt;serviceclass&gt;/&lt;servicemethod&gt;` |
| Page Type | (Required) The type of the page visited. |
| Device Type | (Required) The device used in event generation. |
| Event Type | (Required) The name of the event. Recommended to use your `tealium_event` value. |
| Customer ID | Primary key for Pega customer profile. Required if **Cookie ID** is not provided. |
| Cookie ID | Required if **Customer ID** is not provided. If both are provided, only **Customer ID** is used. |
| Event Timestamp | Time of the event generated. Date attributes will be converted to the ISO [8601](https://en.wikipedia.org/wiki/ISO_8601) format. If not mapped, it will be initialized with the current timestamp in the ISO 8601 format. For example: `2022-08-30T01:13:16.081Z`. |
| Page Location | Page URL is required when **PageView** event is provided. |
| Page View Active Time | The time in seconds the visitor spent on the page. |

### Action — Send Custom Event Data (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

Use this EventStream action to send batched event data, primarily page views, to Pega for aggregation within the Pegasystems endpoint.

While Tealium can support batched actions to Pega, we recommend that you discuss your use case configuration and need for batching with your Pega account team.

#### Parameters

| Parameter | Description |
| --- | --- |
| Service Endpoint URL | The value is the Service Endpoint URL defined in your Pega system.&lt;br&gt;The **Service Endpoint URL** uses the following structure, but is customizable and may be provided by your Pega contact: `https://&lt;host&gt;:&lt;port&gt;/prweb/PRRestService/&lt;servicepackage&gt;/&lt;serviceclass&gt;/&lt;servicemethod&gt;` |
| Page Type | (Required) The type of the page visited. |
| Device Type | (Required) The device used in event generation. |
| Event Type | (Required) The name of the event. Recommended to use your `tealium_event` value. |
| Customer ID | Primary key for Pega customer profile. Required if Cookie ID is not provided. |
| Cookie ID | Required if Customer ID is not provided. If both are provided, only Customer ID is used. |
| Event Timestamp | Time of the event generated. Date attributes will be converted to the ISO [8601](https://en.wikipedia.org/wiki/ISO_8601) format. If not mapped, it will be initialized with the current timestamp in the ISO 8601 format. For example: `2022-08-30T01:13:16.081Z`. |
| Page Location | Page URL is required when PageView event is provided. |
| Page View Active Time | The time in seconds the visitor spent on the page. |

### Action — ID Merge

Use this action to merge customer behavioral information to produce more accurate recommendations and next-best-action decisions based on cumulative behavioral data.

#### Suggested setup in Tealium

We recommend the following Pegasystems connector configuration:

1. Create the following attributes:
    * **Pega Customer ID**: (EventStream string) Inherited from the data layer.
    * **Pega Customer IDs**: (AudienceStream array of strings) The **Pega Customer ID**s stitched together by Tealium.
    * **Pega Customer IDs count**: (AudienceStream number) The length of the **Pega Customer IDs** set of strings.
1. Create an audience with the name **Pega match check**, where the condition is `Pega Customer IDs count &gt; 1`.
1. Add a **Merge customer behavioral data** action to the existing Pega connector, where:
    * **Trigger**: `In Audience at end of visit`.
    * **Uncheck**: `And was not a member of this Audience at start of visit`.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Primary ID / Secondary ID | (Required) An array of strings that contains the Primary ID and Secondary IDs. The first value is Primary ID, and subsequent values are Secondary IDs. For example: `[&#34;ID12345&#34;,&#34;ID12346&#34;,&#34;ID12347&#34;]`. |
| Application Name | The ID of the application in which the data of the known customer and unknown prospect is saved. If this value is not passed, the application ID is identified from the value of the application alias in the service URL. |
| Context Name | Select the context name or enter a custom context name: **Customer**, **Provider**, or **Subscriber**. |

## Vendor resources

* [Pega: Installing the Tealium Customer Data Connector](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/tealium-installation-guide.html#con-tealium-installation-guide)