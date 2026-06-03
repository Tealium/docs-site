---
title: ROKT Connector Setup Guide
description: This article describes how to set up the ROKT connector (formerly ROKT Events connector).
url: https://docs.tealium.com/server-side-connectors/rokt/
---
## API information

This connector uses the following vendor APIs:

* API Name: ROKT API
* API Endpoints: 
  * API Endpoint: `https://api.rokt.com`
  * V1: `https://api.rokt.com/v1/events`
  * V2: `https://api.rokt.com/v2/events`
  * Custom Audience Import: `https://data.rokt.com/v3/import/suppression`
* Documentation: 
  * [Custom Audience Import API](https://docs.rokt.com/developers/api-reference/custom-audience-import/)
  * [Event API](https://docs.rokt.com/developers/api-reference/event-api/)

 The send event actions support both v1 and v2 authentication methods. You can specify the API to use at the action level. However, the Update custom audience actions only support the v2 authentication method. For more information, see the [Rokt: Event API v1](https://docs.rokt.com/developers/api-reference/event-api#generating-app-id-and-app-secret) or [Rokt: Event API v2](https://docs.rokt.com/developers/api-reference/event-api/#authentication-v2) documentation. 

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](/server-side/connectors/manage/).

After adding the connector, configure the following settings:

* **Client ID**  
  * (Required) Provide your App ID or Public Key. 
* **Client Secret**  
  * (Required) Provide your App Secret or Secret Key.
* **Account ID**  
  * (Required) Provide your Account ID.

Click **Done** when you have finished configuring the connector.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send event | ✓ | ✓ |
| Send event (Batch) | ✓ | ✓ |
| Update custom audience | ✓ | ✗|
| Update custom audience (Batch) | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send event

#### Conversion Data

| **Parameter** | **Description** |
| --- | --- |
| Event ID | If not mapped, Tealium generates a UUID for this value. |
| Event Time | If not mapped, is set to the current timestamp in RFC 3339 format. |
| Meta Data | Non-business critical information about the event. |
| Version | `V2` is the default. Set to `V1` to send events to the V1 endpoint using the **App ID** and **App Secret** keys. Set to `V2` to send events to the V2 endpoint using the `rpub` and `rsec` keys. |

### Send event (Batch)

#### Conversion Data

| **Parameter** | **Description** |
| --- | --- |
| Event ID | If not mapped, Tealium generates a UUID for this value. |
| Event Time | If not mapped, is set to the current timestamp in RFC b3339 format. |
| Meta Data | Non-business critical information about the event. |
| Version | `V1` is the default. Set to `V1` to send events to the V1 endpoint using the **App ID** and **App Secret** keys. Set to `V2` to send events to the V2 endpoint using the `rpub` and `rsec` keys.|

### Update custom audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Action | Set to `include` to add a visitor to the specified list, which can then be used for targeting or suppression. Set to `exclude` to remove a visitor from the specified list.|
| Email | An email address. |
| List | The name of the custom audience list to use. If no list value is provided, the email address is imported into the AdvertiserDatabase list by default. |
| SHA-256 Hashed |  Select this checkbox if you want Tealium to SHA-256 hash the raw email addresses provided in the email field. |

### Update custom audience (Batch)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Action | Set to `include` to add a visitor to the specified list, which can then be used for targeting or suppression. Set to `exclude` to remove a visitor from the specified list. |
| Email | An email address. |
| List | The name of the custom audience list to use. If no list value is provided, the email address is imported into the AdvertiserDatabase list by default. |
| SHA-256 Hashed |  Select this checkbox if you want Tealium to SHA-256 hash the raw email addresses provided in the email field. |