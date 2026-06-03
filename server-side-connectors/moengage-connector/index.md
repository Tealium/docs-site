---
title: MoEngage Connector Setup Guide
description: This article describes how to set up the MoEngage connector.
url: https://docs.tealium.com/server-side-connectors/moengage-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add/Modify User Information (Real-Time)| ✓| ✓|
|Add/Modify User Information (Batched)| ✓| ✓|
|Track Event (Real-Time)| ✓| ✓|
|Track Event (Batched)| ✓| ✓|
|Add User to Audience/Cohort| ✓| ✓|
|Remove User from Audience/Cohort| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Username**
(Required) The username for your MoEngage account is available on the MoEngage Dashboard. For more information, see the [Moengage documentation](https://developers.moengage.com/hc/en-us/articles/4404674776724-Overview#01H815VFPB3Y06MX539856QSK4).

* **Password**
(Required) The password for your MoEngage account is available on the MoEngage Dashboard. For more information, see the [Moengage documentation](https://developers.moengage.com/hc/en-us/articles/4404674776724-Overview#01H815VFPB3Y06MX539856QSK4).

* **Data Center**
(Required) The Data Center used by your API. For more information see the [Moengage Data Center documentation](https://help.moengage.com/hc/en-us/articles/360057030512-Data-Centers-in-MoEngage#01G5DQVXGT2KZMXTJPF77QPJ25). Expected value: 0-4.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

This section describes how to set up parameters and options for each action.

### Add/Modify User Information (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer ID | (Required) The unique identifier which is set and passed on from MoEngage SDK. |
| Name | Full name of the user. |
| First Name | First name of the user. |
| Last Name | Last name of the user. |
| Email | Email address of the user. |
| Age | Age of the user. |
| Gender | Gender of the user. |
| Mobile Number | Mobile number of the user. Example: **918888444411**. |
| Latitude | Latitude of location of the user. |
| Longitude | Longitude of location of the user. |
| Publisher Name | This is the publisher name of install. Example: **Google Ads**. |
| First Seen | The time when the user was created in ISO 8601 format. Example: **2019-05-21T03:47:35Z**. |
| Last Seen | Last Seen Time of the user in ISO 8601 format. Example: **2020-05-01T03:52:35Z**. |
| Number of Conversions | A total number of conversions made by the user in a lifetime. |
| LTV | Lifetime value of the user. |
| Unsubscribe | Email unsubscribe attribute. Emails are not sent to the user when the set value is **true**. |
| Platform | Value is based on the active platforms of the user. Allowed values are **ANDROID**, **iOS**, or **web**. |
| Active | The platform status. |

### Add/Modify User Information (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 50
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer ID | (Required) The unique identifier which is set and passed on from MoEngage SDK. |
| Name | Full name of the user. |
| First Name | First name of the user. |
| Last Name | Last name of the user. |
| Email | Email address of the user. |
| Age | Age of the user. |
| Gender | Gender of the user. |
| Mobile Number | Mobile number of the user. Example: **918888444411**. |
| Latitude | Latitude of location of the user. |
| Longitude | Longitude of location of the user. |
| Publisher Name | This is the publisher name of install. Example: **Google Ads**. |
| First Seen | The time when the user was created in ISO 8601 format. Example: **2019-05-21T03:47:35Z**. |
| Last Seen | Last Seen Time of the user in ISO 8601 format. Example: **2020-05-01T03:52:35Z**. |
| Number of Conversions | A total number of conversions made by the user in a lifetime. |
| LTV | Lifetime value of the user. |
| Unsubscribe | Email unsubscribe attribute. Emails are not sent to the user when the set value is **true**. |
| Platform | Value is based on the active platforms of the user. Allowed values are **ANDROID**, **iOS**, or **web**. |
| Active | The platform status. |

### Track Event (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer ID | (Required) The unique identifier which is set and passed on from MoEngage SDK. |
| Action | (Required)  |
| Device ID | The default value is the **Customer ID** value. The value is used to map events to specific devices. |
| Platform | Used to identify the platform on which the event happened. Allowed values are **ANDROID**, **iOS**, **web**, or **unknown**. |
| App Version | App version of the app on which the event originated. |
| Local Time | Local time at which the event happened in seconds. |
| UTC Time | UTC time at which the event happened in seconds. |
| User Timezone Offset | Should have a value in seconds which can be between -54000 to 54000. For example, for IST (UTC&#43;0530), **User Timezone Offset** will be 19800. |

### Track Event (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 50
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer ID | (Required) The unique identifier which is set and passed on from MoEngage SDK. |
| Action | (Required)  |
| Device ID | The default value is the **Customer ID** value. The value is used to map events to specific devices. |
| Platform | Used to identify the platform on which the event happened. Allowed values are **ANDROID**, **iOS**, **web**, or **unknown**. |
| App Version | App version of the app on which the event originated. |
| Local Time | Local time at which the event happened in seconds. |
| UTC Time | UTC Time at which the event happened in seconds. |
| User Timezone Offset | Should have a value in seconds which can be between -54000 to 54000. For example, for IST (UTC&#43;0530), **User Timezone Offset** will be 19800. |

### Add User to Audience/Cohort

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | User ID of registered/logged-in users. Either **User ID** or **Anonymous ID** must be provided. If both are present, **User ID** will be used first to resolve a user and if not user is available, will try to resolve a user basis the **Anonymous ID**. |
| Anonymous ID | Identifier for unregistered/non-logged in users. |
| Timestamp | Timestamp of the request in ISO 8601. Example: **2019-05-21T03:47:35Z**. If not mapped, it will be initialized with the current timestamp. |
| Cohort Name | Name of the cohort. This setting overrides Tealium Audience name selected in the **Tealium Audience** section. |
| Cohort ID | ID of the cohort. This setting overrides Tealium Audience ID selected in the **Tealium Audience** section. |
| Cohort Description | Description of the cohort. |
| Tealium Audience | Select Tealium Audience to use Tealium Audience ID and Tealium Audience name as ID and name of the MoEngage cohort.&lt;br&gt; |

### Remove User from Audience/Cohort

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | User ID of registered/logged-in users. Either **User ID** or **Anonymous ID** must be provided. If both are present, **User ID** will be used first to resolve a user and if not user is available, will try to resolve a user basis the **Anonymous ID**. |
| Anonymous ID | Identifier for unregistered/non-logged in users. |
| Timestamp | Timestamp of the request in ISO 8601. Example: **2019-05-21T03:47:35Z**. If not mapped, it will be initialized with the current timestamp. |
| Cohort Name | Name of the cohort. This setting overrides Tealium Audience name selected in the **Tealium Audience** section. |
| Cohort ID | ID of the cohort. This setting overrides Tealium Audience ID selected in the **Tealium Audience** section. |
| Cohort Description | Description of the cohort. |
| Tealium Audience | Select Tealium Audience to use Tealium Audience ID and Tealium Audience name as ID and name of the MoEngage cohort. |

    