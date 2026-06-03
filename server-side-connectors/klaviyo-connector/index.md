---
title: Klaviyo Connector Setup Guide
description: This article describes how to set up the Klaviyo connector.
url: https://docs.tealium.com/server-side-connectors/klaviyo-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Klaviyo API
* API Version: 2025-01-15
* API Endpoint: `https://a.klaviyo.com/api/`
* Documentation: [Klaviyo API Reference](https://developers.klaviyo.com/en/reference/api_overview)

## Configure Settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Private API Key**  

(Required) Private API Key. For more information, see [Obtain API credentials](https://developers.klaviyo.com/en/docs/retrieve_api_credentials).

### Create a list

If you do not already have a list at Klaviyo or you need to create a new one, use the following steps to create a list:

1. In the **Connector Configuration** window, click **Create List**. The **Create List** window is displayed..
2. Under **List Name**, enter the list name.
3. Click **Create** and then click **Done**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Update User Attributes | ✓ | ✗ |
| Add User to List (Real-Time) | ✓ | ✗ |
| Add User to List (Batched) | ✓ | ✗ |
| Remove User from List (Real-Time) | ✓ | ✗ |
| Remove User from List (Batched) | ✓ | ✗ |
| Create Profile | ✓ | ✗ |
| Create/Update Profile | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Update User Attributes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Profile ID | The primary identifier that Klaviyo assigns to each user profile. |
| External ID | A unique identifier used to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. Format varies based on the external system. |
| Email | The email address associated with a user profile. |
| Phone Number | The phone number associated with a user profile. |

#### User Attributes

Optional parameters: 

| **Parameter** | **Description** |
| --- | --- |
| Email | The individual&#39;s email address. |
| Phone Number | The individual&#39;s phone number in [E.164](https://en.wikipedia.org/wiki/E.164) format. |
| External ID | A unique identifier used to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. Format varies based on the external system. |
| Anonymous ID | For mobile app profiles, if Klaviyo cannot associate the user with an email address, an anonymous mobile app ID will represent the iOS profile. |
| First Name | Individual&#39;s first name. |
| Last Name | Individual&#39;s last name. |
| Organization | Name of the company or organization within the company for whom the individual works. |
| Title | Individual&#39;s job title. |
| Image | URL pointing to the location of a profile image. |
| Address 1 | First line of street address. |
| Address 2 | Second line of street address. |
| City | City name. |
| Country | Country name. |
| Latitude | Latitude coordinate. We recommend a precision of four decimal places. |
| Longitude | Longitude coordinate. We recommend a precision of four decimal places. | 
| Region | Region within a country, such as a state or province. |
| Zip | Zip code. |
| Timezone | Time zone name. We recommend time zones from the [IANA Time Zone Database](https://www.iana.org/time-zones). |
| Custom Properties | Map any custom properties assigned to this profile. Date attributes will be converted to ISO 8601 format. For example: `2021-09-15 13:34:08&#43;00:00`.|

### Action - Add User to List (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| List | Select the list to add the user to. |

#### User Identifier

Select one of the following identifiers to look up the user:

| **Parameter** | **Description** |
| --- | --- |
| Profile ID | The primary identifier that Klaviyo assigns to each user profile. |
| External ID | A unique identifier used by customers to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. The format varies based on the external system. |
| Email | The email address associated with a user profile. |
| Phone Number | The phone number associated with a user profile. |

### Action - Add User to List (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 1000
* Maximum time since oldest request: 10 minutes
* Maximum size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| List | Select the list to add the user to. |

#### User Identifier

Select one of the following identifiers to look up the user:

| **Parameter** | **Description** |
| --- | --- |
| Profile ID | The primary identifier that Klaviyo assigns to each user profile. |
| External ID | A unique identifier used by customers to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. The format varies based on the external system. |
| Email | The email address associated with a user profile. |
| Phone Number | The phone number associated with a user profile. |

### Action - Remove User from List (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| List | Select the list to add the user to. |

#### User Identifier

Select one of the following identifiers to look up the user:

| **Parameter** | **Description** |
| --- | --- |
| Profile ID | The primary identifier that Klaviyo assigns to each user profile. |
| External ID | A unique identifier used by customers to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. The format varies based on the external system. |
| Email | The email address associated with a user profile. |
| Phone Number | The phone number associated with a user profile. |

### Action - Remove User from List (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 1000
* Maximum time since oldest request: 10 minutes
* Maximum size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| List | Select the list to add the user to. |

#### User Identifier

Select one of the following identifiers to look up the user:

| **Parameter** | **Description** |
| --- | --- |
| Profile ID | The primary identifier that Klaviyo assigns to each user profile. |
| External ID | A unique identifier used by customers to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. The format varies based on the external system. |
| Email | The email address associated with a user profile. |
| Phone Number | The phone number associated with a user profile. |

### Action - Create Profile

#### Profile Attributes

| **Parameter** | **Description** |
| --- | --- |
| Email | The individual&#39;s email address. |
| Phone Number | The individual&#39;s phone number in [E.164](https://en.wikipedia.org/wiki/E.164) format. |
| External ID | A unique identifier used to associate Klaviyo user profiles with user profiles in an external system, such as a point-of-sale system. The format varies based on the external system. |
| Anonymous ID | For mobile app profiles. If Klaviyo cannot associate the user with an email address, an anonymous mobile app ID represents the iOS profile. |
| First Name | Individual&#39;s first name. |
| Last Name | Individual&#39;s last name. |
| Organization | Name of the company or organization within the company for whom the individual works. |
| Title | Individual&#39;s job title. |
| Image | URL of a profile image. |
| Address 1 | First line of street address. |
| Address 2 | Second line of street address. |
| City | City name. |
| Country | Country name. |
| Latitude | Latitude coordinate. We recommend a precision of four decimal places. |
| Longitude | Longitude coordinate. We recommend a precision of four decimal places. | 
| Region | Region within a country, such as a state or province. |
| Zip | Zip code or postal code. |
| Timezone | Time zone name. We recommend using time zone names from the [IANA Time Zone Database](https://www.iana.org/time-zones). |
| Custom Properties | Map any custom properties assigned to this profile. Date attributes are converted to ISO 8601 format. For example: `2021-09-15 13:34:08&#43;00:00`.|

### Action - Create/Update Profile

#### Profile Attributes

| **Parameter** | **Description** |
| --- | --- |
| ID | Primary key that uniquely identifies this profile. Generated by Klaviyo. |
| Email Address | Individual&#39;s email address. |
| Phone Number |Individual&#39;s phone number in [E.164](https://en.wikipedia.org/wiki/E.164) format. |
| External ID | A unique identifier used to associate Klaviyo profiles with profiles in an external system, such as a point-of-sale system. Format varies based on the external system. | 
| Anonymous ID| An ID that can be used to identify a profile when other identifiers are not available. | 
| Exchange ID| Also known as the `exchange_id`, this is an encrypted identifier used for identifying a profile by Klaviyo&#39;s web tracking. You can use this field as a filter when retrieving profiles through the Get Profiles endpoint.| 
| First Name| Individual&#39;s first name. | 
| Last Name| Individual&#39;s last name. | 
| Organization | Name of the company or organization within the company for whom the individual works. | 
| Locale | The locale of the profile, in the [IETF BCP 47](https://en.wikipedia.org/wiki/IETF_language_tag) language tag format like (ISO 639-1/2)-(ISO 3166 alpha-2). | 
| Title | Individual&#39;s job title. | 
| Profile Image Address | URL pointing to the location of a profile image. | 
| Address Line 1 | First line of street address. | 
| Address Line 2 | Second line of street address. | 
| City | City name. | 
| Country | Country name. | 
| Latitude| Latitude coordinate. We recommend providing a precision of four decimal places. | 
| Longitude| Longitude coordinate. We recommend providing a precision of four decimal places. | 
| Region| Region within a country, such as state or province. | 
| Zip Code| Zip code. | 
| Timezone| Time zone name. We recommend using time zones from the [IANA Time Zone Database](https://www.iana.org/time-zones). | 
| IP Address | IP Address. |
| Custom Properties | Map any custom properties assigned to this profile. Date attributes are converted to ISO 8601 format. For example: `2021-09-1513:34:08&#43;00:00`. |
| Meta Append Properties | Select a simple value or values to append to this property array. |
| Meta Unappend Properties | Select a simple value or values to remove from this property array. |
| Meta Unset | Select a key or keys to completely remove from properties with their values. |