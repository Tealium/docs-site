---
title: Amplitude Identify Connector Setup Guide
description: This article describes how to set up the Amplitude Identify connector.
url: https://docs.tealium.com/server-side-connectors/amplitude-identify-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Amplitude API
* API Version: v2
* API Endpoint: `https://api2.amplitude.com/identify`
* Documentation: [Amplitude Identify API](https://amplitude.com/docs/apis/analytics/identify)


## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **API Key**  
  * Your project API key. The API key is located in your Amplitude instance under **Settings > Projects**.
* **Endpoint**  
  * Select the endpoint or type the endpoint URL.
  * Standard Server: `https://api2.amplitude.com/identify`.
  * EU Residency Server: `https://api.eu.amplitude.com/identify`.
  * If not provided, Standard Server endpoint should be used by default.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Update User Properties | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Update User Properties

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| `user_id` | A `UUID` (unique user `ID`) that you specify. If you send a request with a `user_id` that is not in the Amplitude system yet, then the user tied to the `user_id` isn't marked new until their first event. |
| `device_id` | A device specific identifier, such as the Identifier for Vendor (`IDFV`) on iOS. |
| `app_version` | The version of the app the user is on. |
| `start_version` | The version of the app the user was on first. |
| `groups` | A dictionary of key-value pairs that represent groups of users. Setting groups lets you use account-level reporting. You can track up to `5` unique group types and `10` total groups. For more information, see [Account-level reporting in Amplitude](https://amplitude.com/docs/analytics/account-level-reporting). 
<blockquote>
This feature is only available to Enterprise customers who have purchased the accounts add-on.
</blockquote>
 |
| `language` | The language the user has set. |
| `paying` | Specify if the user is paying. |

#### Geographical Parameters


<blockquote>
You must update all of the following fields together. Setting any of these fields automatically resets the others if they aren't also explicitly set on the same identify call.
</blockquote>


| **Parameter** | **Description** |
| --- | --- |
| `country` | The country that the user is in. |
| `region` | The geographical region the user is in. |
| `city` | The city the user is in. |
| `DMA` | The designated market area of the user. |

#### Device Parameters

You must update the following fields together:
* `platform`
* `os_name`
* `os_version`
* `device_brand`
* `device_manufacturer`
* `device_model`
* `carrier`


<blockquote>
Setting any of the fields above resets all the other property values to null if they aren't explicitly set on the same identify call. All property values otherwise persist to later events if the values aren't changed to a different string or if all values are passed as `null`. Amplitude tries to use `device_brand`, `device_manufacturer`, and `device_model` to map the corresponding device type.
</blockquote>


| **Parameter** | **Description** |
| --- | --- |
| `platform` | The platform that's sending the data. |
| `os_name` | The mobile operating system or browser the user is on. |
| `os_version` | The version of the mobile operating system or browser the user is on. |
| `device_brand` | The device brand the user is on. |
| `device_manufacturer` | The device manufacturer of the device that the user is on. |
| `device_model` | The device model the user is on. |
| `carrier` | The carrier the user has. |
| `user_properties` | A dictionary of key-value pairs that represent data tied to the user. Each distinct value appears as a user segment on the Amplitude dashboard. Object depth may not exceed `40` layers. You can store property values in an array and date values are transformed into string values. |
