---
title: Singular Connector Setup Guide
description: This article describes how to set up the Singular connector.
url: https://docs.tealium.com/server-side-connectors/singular-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Singular API
* API Version: v1
* API Endpoint: `https://s2s.singular.net/api/v1`
* Documentation: [Singular API](https://support.singular.net/hc/en-us/articles/31394799175963-Server-to-Server-SESSION-Endpoint-API-Reference#Session_API_Endpoint)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **SDK API Key**
    * (Required) The SDK Key is passed as the `a` parameter in the API request.
    * Retrieve the SDK Key from the Singular UI, under [Developer Tools](https://app.singular.net/?#/react/sdk_integration) in the Main Menu.
    * Do not use the reporting API Key as this will result in rejected data.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Session Data | ✗ | ✓ |
| Send Event Data | ✗ | ✓ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Send Session Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Platform | The app platform. Available values are: `Android`, `iOS`, `PC`, `Xbox`, `Playstation`, `Nintendo`, `MetaQuest`, and `CTV`. |

#### Session Data Parameters

All parameters will be URL-unencoded.

| Parameter | Description |
| --- | --- |
| IPv4 Address | (Required) The public IPv4 address of the device. |
| OS Version | (Required) The OS version of the device at session time. |
| App Identifier | (Required) The app identifier. |
| Application Version | (Required) Thhe application version. |
| Install | (Required) This parameter indicates whether this session is the first after an install or re-install. |
| Client Defined Identifier | The client-defined identifier for special cases where all other identifiers are not available. |
| Timestamp | The time of the session in UNIX time (seconds). |
| Timestamp (Milliseconds) | The time of the session in 13-digit UNIX time (milliseconds). |
| Global Properties | A JSON object with up to five key-value pairs. |
| Use IP | This parameter signals Singular to extract the IP address from the HTTP request instead of the IPv4 Address parameter. |
| Country | The ISO 3166-1 alpha-2 two-letter country code of the user at the time of the session. |
| User Agent | The User Agent of the device. |
| Data Sharing Options | The end-user consent to share information. |
| Internal User ID | The internal User ID. |

#### Platform Specific Data Parameters

Select event attributes to map to platform-specific parameters at the vendor.

### Send Event Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Platform | The app platform. Available values are: `Android`, `iOS`, `PC`, `Xbox`, `Playstation`, `Nintendo`, `MetaQuest`, and `CTV`. |

#### Event Data Parameters

All parameters will be URL-unencoded.

| Parameter | Description |
| --- | --- |
| IPv4 Address | (Required) The public IPv4 address of the device. |
| OS Version | (Required) The OS version of the device at session time. |
| App Identifier | (Required) The app identifier. |
| Name of Event | (Required) The name of the event being tracked. |
| Custom Event Attributes | Custom event attributes in JSON format. |
| Timestamp | The time of the session in UNIX time (seconds). |
| Timestamp (Milliseconds) | The time of the session in 13-digit UNIX time (milliseconds). |
| Global Properties | A JSON object with up to five key-value pairs. |
| Use IP | This parameter signals Singular to extract the IP address from the HTTP request instead of the IPv4 Address parameter. |
| Country | The ISO 3166-1 alpha-2 two-letter country code of the user at the time of the session. |
| Currency Amount | The currency amount. |
| Currency Code | The uppercase ISO 4217 three-letter currency code. |
| SKU Identifier | The product SKU identifier. |
| Transaction Identifier | The transaction identifier. |
| Data Sharing Options | The end-user consent to share information. |
| Internal User ID | The internal User ID. |
| Revenue Event? | This boolean parameter specifies whether the event is a revenue event (`true` or `false`). |

#### Platform Specific Data Parameters

Select event attributes to map to platform-specific parameters at the vendor.