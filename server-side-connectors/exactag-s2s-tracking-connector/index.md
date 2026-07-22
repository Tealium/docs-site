---
title: Exactag S2S Tracking Connector Setup Guide
description: This article describes how to set up the Exactag S2S Tracking connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/exactag-s2s-tracking-connector/
---
This article describes how to set up the Exactag S2S Tracking connector.

## API Information

This connector uses the following vendor API:

* API Name: Exactag S2S Tracking API
* API Version: v1.0
* API Endpoint: `https://m.exactag.com/s2s/pi.ashx`

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Page Impression Event | ✗ | ✓ |
| Send Onsite Conversion Request | ✗ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Campaign**  
The 32-byte encrypted brand specific campaign code.

## Actions

The following section lists the supported parameters for each action.

### Send Page Impression Event

#### Unique Identifier Attribute

| **Parameter** | **Description** |
| --- | --- |
| euk | A unique identifier to identify the person or device. Use this parameter when using Tealium Visitor ID. |
| mid | Use this parameter when the Mobile Device ID, such as IDFA or Google Play Store ID, is being used. It must be MD5 hashed and used as user key. |
| uk | A unique identifier to identify the person or device. This value must be MD5 hashed. Use this parameter if using an Exactag User ID. |
| gk | A unique identifier to identify an anonymous group of multiple users. This value must be MD5 hashed and combined with the group expire timestamp (urlEncoded or base64url). |


#### Event Attributes

| **Parameter** | **Description** |
| --- | --- |
| sitegroup | (Required) Configured event / sitegroup. Used to categorize the page impressions and to identify conversion events. |
| useragent | (Required) User agent of the client (encoded). |
| ipaddress | (Required) IP Address of the client used for geolocation (not stored). |
| referrer | (Required) Referrer URL, which must include the protocol. For example: `https://www.tealium.com` |
| sessionid | (Required) Value to identify a single user session. |
| host | (Required) Host (domain only without site and protocol). For example: `example.com` |
| site | (Required) Path part of requested URI. For example, `resources` is the path portion of  `https://tealium.com/resources/`.|
| search | (Required) Query part of requested URI. For example: `?utm_campaign=abc` |
| sescount | (Required) Session number, where 1 is a new visitor, and greater than 1 is a recurring visitor. |
| sesevent | (Required) Session number, where 1 is the first page impression in this session. |
| optout | Binary. If set to 1, the request is treated as if the customer has opted out. In this case, the user identifier is ignored and not stored. |
| consent | JSON object for type or partner based consent (URL encoded). For example: `{“comfort”:1,”analytics”:0,”marketing”:0}`. To create more complex data structures, provide the template name in the **Event Attributes Templates** section. |
| consent_string | IAB GDPR consent string. |
| protocol | Protocol. Either `http` or `https`. |
| params | A JSON object containing any additional parameters to send to Exactag. To create more complex data structures, provide the template name in the **Event Attributes Templates** section. |
| Event Attributes Template Variables | Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). Name nested template variables with the dot notation (for example: `items.name`). Nested template variables are typically built from data layer list attributes. |
| Event Attributes Templates | Provide templates to be referenced in **Event Attributes**. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`. |

### Send Onsite Conversion Request

#### Unique Identifier Attribute

| **Parameter** | **Description** |
| --- | --- |
| euk | A unique identifier to identify the person or device. Use this parameter if using Tealium Visitor ID. |
| mid | Use if the Mobile Device ID, such as IDFA or Google Play Store ID, is being used. It must be MD5 hashed and used as user key. |
| uk | A unique identifier to identify the person or device. This value must be MD5 hashed. Use this parameter if using a Exactag User ID. |
| gk | A unique identifier to identify an anonymous group of multiple users. This value must be MD5 hashed and combined with the group expire timestamp (urlEncoded or base64url). |

#### Request Attributes

| **Parameter** | **Description** |
| --- | --- |
| sitegroup | (Required) Configured event / sitegroup. Used to categorize the page impressions and to identify conversion events. |
| useragent | (Required) User agent of the client (encoded). |
| ipaddress | (Required) IP Address of the client used for geolocation (not stored). |
| referrer | (Required) Referrer URL, which must include the protocol. For example: `https://www.tealium.com`|
| sessionid | (Required) Value to identify a single user session. |
| host | (Required) Host (domain only without site and protocol). For example: `example.com` |
| site | (Required) Path part of requested URI. For example, `resources` is the path portion of  `https://tealium.com/resources/`.|
| search | (Required) Query part of requested URI. For example: `?utm_campaign=abc` |
| sescount | (Required) Session number, where 1 is a new visitor and greater than 1 is a recurring visitor. |
| sesevent | (Required) Session number, where 1 is the first page impression in this session. |
| optout | (Required) Binary. If set to 1, the request is treated as if the customer has opted out. In this case, the user identifier is ignored and not stored. |
| level | Recommended. Configured commission level. |
| orderid | Recommended. Order ID (Can be used for order deduplication). |
| customerid | Recommended. Customer ID (Can be used for cross device). |
| totalprice | Recommended. Total basket value. |
| consent | URL encoded JSON object for type or partner based consent (for example: `{“comfort”:1,”analytics”:0,”marketing”:0}`). To create more complex data structures, provide the template name in the **Request Attributes Templates** section. |
| protocol | Protocol `http` or `https`. |
| Request Attributes Template Variables | Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). Name nested template variables with the dot notation (for example: `items.name`). Nested template variables are typically built from data layer list attributes. |
| Request Attributes Templates | Provide templates to be referenced in **Request Attributes**. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`. |   