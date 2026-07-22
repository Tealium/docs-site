---
title: Amplitude Connector Setup Guide
description: This article describes how to set up the Amplitude connector.
url: https://docs.tealium.com/server-side-connectors/amplitude-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Amplitude HTTP API
* API Version: v2
* API Endpoint: `https://api2.amplitude.com/2/httpapi`
* Documentation: [Amplitude HTTP API](https://developers.amplitude.com/docs/http-api-v2)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event| ✓| ✓|
|Send Event (Non-Batched)| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **API Key**  
Located under **Settings &rarr; Projects**.
* **Server Endpoint**  
Enter the Amplitude endpoint to use.  
    * Standard Server: `https://api2.amplitude.com/2/httpapi`  
    * EU Residency Server: `https://api.eu.amplitude.com/2/httpapi`  
If you do not enter a value, the connector uses the **Standard Server** endpoint by default.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Event (Batched)


<blockquote>
If real-time processing is required, do not use the Send Events (Batched) action.
</blockquote>


#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Type| (Required) A unique identifier for your event. Amplitude reserves the following event names for internal use: `[Amplitude] Start Session`, `[Amplitude] End Session`, `[Amplitude] Revenue`, `[Amplitude] Revenue (Verified)`, `[Amplitude] Revenue (Unverified)`, and `[Amplitude] Merged User`. |
|API Key Override|  Overrides the **API Key** configuration setting. |
|Server Endpoint Override| Overrides the **Server Endpoint** configuration setting.  |
|Android ID| The Android ID for Android devices (not the advertising ID).  |
|App Version|  The current version of your application. |
|Carrier|  The carrier that the user is on. |
|City| The city that the user is in.   |
|Country|  The country that the user is in. |
|Designated Market Area| The user's current Designated Market Area (DMA).  |
|Device Brand|  The device brand that the user is on.|
|Device ID| A device-specific identifier, such as the Identifier for Vendor on iOS. If a device ID isn't sent with the event, then the default value is a hashed version of the user ID.  |
|Device IP Address|   The user IP address. Amplitude uses the IP address to reverse lookup a user's location (city, country, region, and DMA).  |
|Device Manufacturer|  The device manufacturer that the user is on. |
|Device Model|  The device model that the user is on. |
|Event ID| An incrementing counter to distinguish events with the same user ID and timestamp from each other. Amplitude recommends you send an event ID that increases over time, especially if you expect events to occur simultaneously.  |
|Google Play Services Advertising ID| The Google Play Services advertising ID for Android devices. |
|iOS Identifier for Advertiser| The Identifier for Advertiser for iOS devices.  |
|iOS Identifier for Vendor|  The Identifier for Vendor for iOS devices. |
|Insert ID| A unique identifier for the event. Amplitude deduplicates subsequent events sent with the same device ID and insert ID within the past seven days. Amplitude recommends generating a UUID or using some combination of device ID, user ID, event type, event ID, and time.  |
|Language|  The language set by the user. Amplitude automatically converts ISO 639 language codes to human-friendly language names (for example, `en-US` to `English`). |
|Location Latitude| The current latitude of the user.  |
|Location Longitude| The current longitude of the user.  |
|OS Name| The name of the mobile operating system or browser that the user is on.  |
|OS Version| The version of the mobile operating system or browser that the user is on.  |
|Platform| The device platform sending the data.  |
|Price|  The item's purchase price. Required for revenue data if the revenue field isn't sent. Use negative values for refunds. |
|Product ID| An identifier for the item purchased. You must also include price and quantity or include revenue with this field.  |
|Quantity| The quantity of the item purchased. If not specified, the default value is `1`.  |
|Region| The current region of the user.  |
|Revenue| The revenue from the transaction, which is the product of price times quantity. If you send all three fields of price, quantity, and revenue, then the revenue value is the product of price times quantity. Use negative values for refunds.  |
|Revenue Type| The type of revenue for the item purchased. You must send values for price and quantity or send a value for revenue with this field.  |
|Session ID| The start time of the session in milliseconds since epoch. This parameter is necessary if you want to associate events with a particular system. A value of `-1` represents no value specified.  |
|Time| The timestamp of the event in milliseconds since epoch. If time isn't sent with the event, the default value is the request upload time.  |
|User ID| The ID of the user.  |
|Event Properties| A dictionary of key-value pairs that represent additional data to be sent along with the event.<br> Empty values are skipped and not included.|
|User Properties| A dictionary of key-value pairs that represent additional data tied to the user. Each distinct value will show up as a user segment on the Amplitude dashboard.<br> Empty values are skipped and not included.|
|Groups| Enterprise only.<br> A dictionary of key-value pairs that represent groups of users. For more information about groups, see [our JavaScript SDK excerpt](https://github.com/amplitude/Amplitude-Javascript#setting-groups).<br> Empty values are skipped and not included.|
|Template Variables| Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/)<br> Name nested template variables with the dot notation (Example: `items.name`).<br> Nested template variables are typically built from data layer list attributes.|
|Templates| Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).<br> Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

### Action — Send Event (Non-Batched)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Type| (Required) A unique identifier for your event. Amplitude reserves the following event names for internal use: `[Amplitude] Start Session`, `[Amplitude] End Session`, `[Amplitude] Revenue`, `[Amplitude] Revenue (Verified)`, `[Amplitude] Revenue (Unverified)`, and `[Amplitude] Merged User`. |
|API Key Override|  Overrides the **API Key** configuration setting. |
|Server Endpoint Override| Overrides the **Server Endpoint** configuration setting.  |
|Android ID| The Android ID for Android devices (not the advertising ID).  |
|App Version|  The current version of your application. |
|Carrier|  The carrier that the user is on. |
|City| The city that the user is in.   |
|Country|  The country that the user is in. |
|Designated Market Area| The user's current Designated Market Area (DMA).  |
|Device Brand|  The device brand that the user is on.|
|Device ID| A device-specific identifier, such as the Identifier for Vendor on iOS. If a device ID isn't sent with the event, then the default value is a hashed version of the user ID.  |
|Device IP Address|   The user IP address. Amplitude uses the IP address to reverse lookup a user's location (city, country, region, and DMA).  |
|Device Manufacturer|  The device manufacturer that the user is on. |
|Device Model|  The device model that the user is on. |
|Event ID| An incrementing counter to distinguish events with the same user ID and timestamp from each other. Amplitude recommends you send an event ID that increases over time, especially if you expect events to occur simultaneously.  |
|Google Play Services Advertising ID| The Google Play Services advertising ID for Android devices. |
|iOS Identifier for Advertiser| The Identifier for Advertiser for iOS devices.  |
|iOS Identifier for Vendor|  The Identifier for Vendor for iOS devices. |
|Insert ID| A unique identifier for the event. Amplitude deduplicates subsequent events sent with the same device ID and insert ID within the past seven days. Amplitude recommends generating a UUID or using some combination of device ID, user ID, event type, event ID, and time.  |
|Language|  The language set by the user. Amplitude automatically converts ISO 639 language codes to human-friendly language names (for example, `en-US` to `English`). |
|Location Latitude| The current latitude of the user.  |
|Location Longitude| The current longitude of the user.  |
|OS Name| The name of the mobile operating system or browser that the user is on.  |
|OS Version| The version of the mobile operating system or browser that the user is on.  |
|Platform| The device platform sending the data.  |
|Price|  The item's purchase price. Required for revenue data if the revenue field isn't sent. Use negative values for refunds. |
|Product ID| An identifier for the item purchased. You must also include price and quantity or include revenue with this field.  |
|Quantity| The quantity of the item purchased. If not specified, the default value is `1`.  |
|Region| The current region of the user.  |
|Revenue| The revenue from the transaction, which is the product of price times quantity. If you send all three fields of price, quantity, and revenue, then the revenue value is the product of price times quantity. Use negative values for refunds.  |
|Revenue Type| The type of revenue for the item purchased. You must send values for price and quantity or send a value for revenue with this field.  |
|Session ID| The start time of the session in milliseconds since epoch. This parameter is necessary if you want to associate events with a particular system. A value of `-1` represents no value specified.  |
|Time| The timestamp of the event in milliseconds since epoch. If time isn't sent with the event, the default value is the request upload time.  |
|User ID| The ID of the user.  |
|Event Properties| A dictionary of key-value pairs that represent additional data to be sent along with the event.<br> Empty values are skipped and not included.|
|User Properties| A dictionary of key-value pairs that represent additional data tied to the user. Each distinct value will show up as a user segment on the Amplitude dashboard.<br> Empty values are skipped and not included.|
|Groups| Enterprise only.<br> A dictionary of key-value pairs that represent groups of users. For more information about groups, see [our JavaScript SDK excerpt](https://github.com/amplitude/Amplitude-Javascript#setting-groups).<br> Empty values are skipped and not included.|
|Template Variables| Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).<br> Name nested template variables with the dot notation (Example: `items.name`).<br> Nested template variables are typically built from data layer list attributes.|
|Templates| Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).<br> Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|