---
title: Leanplum Connector Setup Guide
description: This article describes how to set up the Leanplum connector.
url: https://docs.tealium.com/server-side-connectors/leanplum-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Leanplum API
* API Version: v1.0
* API Endpoint: `https://api.leanplum.com/api`
* Documentation: [Leanplum API](https://docs.leanplum.com/reference/overview#introduction)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Multi Request (Batched)| ✓| ✓|
|Set User Attributes| ✓| ✓|
|Send Message| ✓| ✓|
|Track Event| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **App ID**: The application ID. To find yours, select your app in the navigation column, and click Manage Apps. Then click Keys &amp; Settings.
* **API Version**: The version of the Leanplum API to use.
* **Client Key**: Production key for your Leanplum App.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

This section describes how to set up parameters and options for each action.

### Send Multi Request (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 50
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Action | API Action |
| Time | The time at which the request was issued (UNIX time). This is used to resolve the time difference between Leanplum and the API caller when computing the times of events. |
| User ID | The current user ID. You can set this to whatever your company uses for user IDs. Leave it blank to use the device ID. For more info, see &lt;a href=&#34;https://docs.leanplum.com/reference/selecting-a-user&#34; target=&#34;_blank&#34;&gt;selecting a user&lt;/a&gt;. |
| Device ID | The unique ID for the device. |
| App ID | The application ID. To find yours, select your app in the navigation column, and click **Manage Apps**. Then click **Keys &amp; Settings**. |
| API Version | The version of the Leanplum API to use. |
| Create Disposition | The policy that determines whether users are created by the API. The default value for this method is **CreateIfNeeded**.&lt;br&gt;&lt;br&gt;Possible values are:  &lt;ul&gt;&lt;li&gt;**CreateIfNeeded** Creates a user with the given IDs if one does not already exist.&lt;/li&gt;&lt;li&gt;**CreateNever** Requires that the user already exists, otherwise the API call is skipped and a warning will be returned.&lt;/ul&gt;&lt;/li&gt; |
| Dev Mode | Whether the user is in Development Mode (the user associated with the request is a developer and not a user). This is important for reporting purposes. Default value: `false`. |
| Event | The name of the event. Use &#34;Purchase&#34; to identify a monetization event, with the event value being the revenue. |
| Message ID | The message ID this event is associated with. Set this to track a user&#39;s interaction with a message. To track a message Send or a View, set the event argument to an empty string. |
| Disposition | Determines how tracked events affect sessions and user activity.&lt;br&gt;&lt;br&gt;If present, the disposition must have one of the following values:  &lt;ul&gt;&lt;li&gt;`active` &lt;ul&gt;&lt;li&gt;This is the default value.&lt;/li&gt;&lt;li&gt;Used for events reflect user activity.&lt;/li&gt;&lt;li&gt;Active events should mark the user as active and should be tracked within a session.&lt;/li&gt;&lt;li&gt;Replaces the deprecated option `allowOffline: false`.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;`passive` &lt;ul&gt;&lt;li&gt;Used for events that do not correspond to user activity.&lt;/li&gt;&lt;li&gt;These events do not need to occur within a session and do not mark a user as active.&lt;/li&gt;&lt;li&gt;Example: Sending a user a message would be tracked passively, since it affects a user, but does not represent user activity.&lt;/li&gt;&lt;li&gt;Replaces the deprecated option `allowOffline: true`.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;`requireActive` &lt;ul&gt;&lt;li&gt;Used for events that must only be tracked within a session.&lt;/li&gt;&lt;li&gt;These events are rejected and return a warning response with `ignored: true` if the user does not have an active session.&lt;/li&gt;&lt;li&gt;Clients should detect the warning by the ignored field, as warning messages may change.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt; |
| Force | Whether to send the message regardless of whether the user meets the targeting criteria. Default: `false`. |
| Created | The time at which the user was created, in seconds since midnight UTC on January 1, 1970. |
| Last Active | The time at which the user was last active, in seconds since midnight UTC on January 1, 1970. |
| Total Sessions | The total number of sessions that a user has had in their lifetime. |
| Time Spent In App | The total number of seconds spent in the app in the user&#39;s lifetime. |
| Locale | The current locale the user is in. Example: en_US. |
| Country | The country the user is in, specified by &lt;a href=&#34;http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2&#34; target=&#34;_blank&#34;&gt;&lt;u&gt;ISO 2-letter code&lt;/u&gt;&lt;/a&gt;. Example: US for United States. Set to (detect) to detect the country based on the IP address of the user. |
| Region | The region (state) the user is in. Example: ca for California. Set to (detect) to detect the region based on the IP address of the user. |
| City | The city the user is in. Example: San Francisco. Set to (detect) to detect the city based on the IP address of the user.  |
| Location | The location (latitude/longitude) of the user. Example: 37.775,-122.4183. Set to (detect) to detect the location based on the IP address of the user. |
| Location Accuracy Type | The type of location that is provided (IP, CELL, or GPS). Default: IP. |
| Timezone | The timezone abbreviation for the user. See list of timezone abbreviations. |
| Timezone Offset Seconds | The timezone offset from GMT in seconds. |
| User Attributes | A map of user attributes as key-value pairs. Each key must be a string. Attributes are saved across sessions. Only supplied attributes will be updated (for example, if you omit an existing attribute, it will be preserved). |
| User Attribute Values To Add | A map of values to add to existing user attribute sets. For example, supply {&#34;Interests&#34;:&#34;Sports&#34;} to add Sports to the existing set of Interests. |
| Value | The event value. For example, for a purchase event, this would be the purchase price. |
| Currency Code | The ISO 4217 currency code associated with value. Leanplum will automatically convert value into your preferred currency, while retaining the original price and currency code as event parameters localCurrency and localPrice. Currency conversion rates are updated every hour. |
| Time | Option to provide the UNIX timestamp for when the event occurred, which may be different from the current time. |
| Info | Any info attached to the event. |
| Parameters | A flat object of parameters as key-value pairs. Each key must be a string, and up to 50 parameters may be set. |
| Values | A JSON object of key-value pairs to override template variables used in the message. |

### Set User Attributes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | The current user ID. You can set this to whatever your company uses for user IDs. Leave it blank to use the device ID. For more info, see &lt;a href=&#34;https://docs.leanplum.com/reference/selecting-a-user&#34; target=&#34;_blank&#34;&gt;selecting a user&lt;/a&gt;. |
| Device ID | The unique ID for the device. |
| User Attributes | A map of user attributes as key-value pairs. Each key must be a string. Attributes are saved across sessions. Only supplied attributes will be updated (for example, if you omit an existing attribute, it will be preserved). |
| App ID | The application ID. To find yours, select your app in the navigation column, and click Manage Apps. Then click Keys &amp; Settings. |
| API Version | The version of the Leanplum API to use. |
| Create Disposition | The policy that determines whether users are created by the API. The default value for this method is **CreateIfNeeded**.&lt;br&gt;&lt;br&gt;Possible values are:  &lt;ul&gt;&lt;li&gt;**CreateIfNeeded** Creates a user with the given IDs if one does not already exist.&lt;/li&gt;&lt;li&gt;**CreateNever** Requires that the user already exists, otherwise the API call is skipped and a warning will be returned.&lt;/ul&gt;&lt;/li&gt; |
| User Attribute Values To Add | A map of values to add to existing user attribute sets. For example, supply {&#34;Interests&#34;:&#34;Sports&#34;} to add Sports to the existing set of Interests. |
| Dev Mode | Whether the user is in Development Mode, for example, the user associated with the request is a developer and not a user. This is important for reporting purposes. Default: `false`. |
| Created | The time at which the user was created, in seconds since midnight UTC on January 1, 1970. |
| Last Active | The time at which the user was last active, in seconds since midnight UTC on January 1, 1970. |
| Total Sessions | The total number of sessions that a user has had in their lifetime. |
| Time Spent In App | The total number of seconds spent in the app in the user&#39;s lifetime. |
| Locale | The current locale the user is in. Example: en_US. |
| Country | The country the user is in, specified by &lt;a href=&#34;http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2&#34; target=&#34;_blank&#34;&gt;&lt;u&gt;ISO 2-letter code&lt;/u&gt;&lt;/a&gt;. Example: US for United States. Set to (detect) to detect the country based on the IP address of the user. |
| Region | The region (state) the user is in. Example: ca for California. Set to (detect) to detect the region based on the IP address of the user. |
| City | The city the user is in. Example: San Francisco. Set to (detect) to detect the city based on the IP address of the user.  |
| Location | The location (latitude/longitude) of the user. Example: 37.775,-122.4183. Set to (detect) to detect the location based on the IP address of the user. |
| Location Accuracy Type | The type of location that is provided (IP, CELL, or GPS). Default: IP. |
| Timezone | The timezone abbreviation for the user. See list of timezone abbreviations. |
| Timezone Offset Seconds | The timezone offset from GMT in seconds. |

### Track Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | The current user ID. You can set this to whatever your company uses for user IDs. Leave it blank to use the device ID. For more info, see &lt;a href=&#34;https://docs.leanplum.com/reference/post_api-action-track#selecting-a-user&#34; target=&#34;_blank&#34;&gt;selecting a user&lt;/a&gt;. |
| Device ID | The unique ID for the device. |
| Event | The name of the event. Use &#34;Purchase&#34; to identify a monetization event, with the event value being the revenue. |
| App ID | The application ID. To find yours, select your app in the navigation column, and click Manage Apps. Then click Keys &amp; Settings. |
| API Version | The version of the Leanplum API to use. |
| Create Disposition | The policy that determines whether users are created by the API. The default value for this method is **CreateIfNeeded**.&lt;br&gt;&lt;br&gt;Possible values are:  &lt;ul&gt;&lt;li&gt;**CreateIfNeeded** Creates a user with the given IDs if one does not already exist.&lt;/li&gt;&lt;li&gt;**CreateNever** Requires that the user already exists, otherwise the API call is skipped and a warning will be returned.&lt;/ul&gt;&lt;/li&gt; |
| Dev Mode | Whether the user is in Development Mode, for example, the user associated with the request is a developer and not a user. This is important for reporting purposes. Default: `false`. |
| Value | The event value. For example, for a purchase event, this would be the purchase price. |
| Currency Code | The ISO 4217 currency code associated with value. Leanplum will automatically convert value into your preferred currency, while retaining the original price and currency code as event parameters localCurrency and localPrice. Currency conversion rates are updated every hour. |
| Time | Option to provide the UNIX timestamp for when the event occurred, which may be different from the current time. |
| Info | Any info attached to the event. |
| Parameters | A flat object of parameters as key-value pairs. Each key must be a string, and up to 50 parameters may be set. |
| Message ID | The message ID this event is associated with. Set this to track a user&#39;s interaction with a message. To track a message Send or a View, set the event argument to an empty string. |
| Disposition | Determines how tracked events affect sessions and user activity.&lt;br&gt;&lt;br&gt;If present, the disposition must have one of the following values:  &lt;ul&gt;&lt;li&gt;`active` &lt;ul&gt;&lt;li&gt;This is the default value.&lt;/li&gt;&lt;li&gt;Used for events reflect user activity.&lt;/li&gt;&lt;li&gt;Active events should mark the user as active and should be tracked within a session.&lt;/li&gt;&lt;li&gt;Replaces the deprecated option `allowOffline: false`.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;`passive` &lt;ul&gt;&lt;li&gt;Used for events that do not correspond to user activity.&lt;/li&gt;&lt;li&gt;These events do not need to occur within a session and do not mark a user as active.&lt;/li&gt;&lt;li&gt;Example: Sending a user a message would be tracked passively, since it affects a user, but does not represent user activity.&lt;/li&gt;&lt;li&gt;Replaces the deprecated option `allowOffline: true`.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;`requireActive` &lt;ul&gt;&lt;li&gt;Used for events that must only be tracked within a session.&lt;/li&gt;&lt;li&gt;These events are rejected and return a warning response with `ignored: true` if the user does not have an active session.&lt;/li&gt;&lt;li&gt;Clients should detect the warning by the ignored field, as warning messages may change.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt; |

### Send Message

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID | The current user ID. You can set this to whatever your company uses for user IDs. Leave it blank to use the device ID. For more info, see &lt;a href=&#34;https://docs.leanplum.com/reference/selecting-a-user&#34; target=&#34;_blank&#34;&gt;selecting a user&lt;/a&gt;. |
| Device ID | The unique ID for the device. |
| Message ID | The ID of the message, found in the URL when viewing a message (for example, `www.leanplum.com/dashboard#/{APP_ID}/messaging/{MESSAGE_ID}`). |
| App ID | The application ID. To find yours, select your app in the navigation column, and click Manage Apps. Then click Keys &amp; Settings. |
| API Version | The version of the Leanplum API to use. |
| Create Disposition | The policy that determines whether users are created by the API. The default value for this method is **CreateIfNeeded**.&lt;br&gt;&lt;br&gt;Possible values are:  &lt;ul&gt;&lt;li&gt;**CreateIfNeeded** Creates a user with the given IDs if one does not already exist.&lt;/li&gt;&lt;li&gt;**CreateNever** Requires that the user already exists, otherwise the API call is skipped and a warning will be returned.&lt;/ul&gt;&lt;/li&gt; |
| Dev Mode | Whether the user is in Development Mode, for example, the user associated with the request is a developer and not a user. This is important for reporting purposes. Default: `false`. |
| Values | A JSON object of key-value pairs to override template variables used in the message. |
| Force | Whether to send the message regardless of whether the user meets the targeting criteria. Default: `false`. |