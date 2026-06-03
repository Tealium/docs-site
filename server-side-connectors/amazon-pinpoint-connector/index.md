---
title: Amazon Pinpoint Connector Setup Guide
description: This article describes how to set up the Amazon Pinpoint connector.
url: https://docs.tealium.com/server-side-connectors/amazon-pinpoint-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Amazon Pinpoint API
* API Version: v1
* API Endpoint: `https://pinpoint.us-east-1.amazonaws.com`
* Documentation: [Amazon Pinpoint Documentation](https://docs.aws.amazon.com/pinpoint/latest/apireference/welcome.html)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Message| ✓| ✓|
|Send Push Notification| ✓| ✓|
|Send Template| ✓| ✓|
|Put Event| ✓| ✓|
|Update Endpoint| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Access Key**
  * (Required) Provide your IAM User&#39;s access key
  * Associated IAM policy (for either IAM User or Assumed Role) must grant `mobiletargeting:*`, `ses:*`, `sms-voice:\*` permissions.
  * For additional information, see: [Amazon Pinpoint](https://docs.aws.amazon.com/pinpoint/latest/developerguide/security_iam_service-with-iam.html).

* **Secret Key**
  * (Required) Provide your IAM User&#39;s secret key

* **Region**
  * (Required) Select region.

* **Assume Role: ARN**
  * (Optional) Provide Amazon Resource Name (ARN) of role to assume.
  * Example: `arn:aws:iam::222222222222:role/myrole`
  * For additional information, see: [Switching to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).

* **Assume Role: Session Name**
  * (Optional) Provide identifier for assumed role session.

* **Assume Role: External ID**
  * (Optional) Provide external identifier.
  * For more information, see: [How to Use an External ID](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Message

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  &lt;ul&gt;&lt;li&gt;(Required) The unique identifier for the application.&lt;/li&gt;&lt;li&gt;This identifier is displayed as the Project ID on the Amazon Pinpoint console.&lt;/li&gt;&lt;/ul&gt; |
|Message Type|  &lt;ul&gt;&lt;li&gt;Message Type&lt;/li&gt;&lt;li&gt;Options are **Email**, **SMS**, or **Voice**.  &lt;ul&gt;&lt;li&gt;Addresses (Template), Endpoints (Template) or Destination is required and only one of each is permitted.&lt;/li&gt;&lt;li&gt;The fields Destination, Body, and Title are used to build an Addresses (Template).&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;SMS  &lt;ul&gt;&lt;li&gt;Body for the SMS message type is required.&lt;/li&gt;&lt;li&gt;Valid values for Message type are `TRANSACTIONAL` or `PROMOTIONAL`.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |
|Charset|  &lt;ul&gt;&lt;li&gt;Character set mapping for the message content.&lt;/li&gt;&lt;/ul&gt; |
|Html Part|  &lt;ul&gt;&lt;li&gt;Only one of Text Part or HTML part is permitted.&lt;/li&gt;&lt;/ul&gt; |
|Subject|  &lt;ul&gt;&lt;li&gt;(Required) Subject of the email.&lt;/li&gt;&lt;/ul&gt; |
|Text Part|  &lt;ul&gt;&lt;li&gt;Text or HTML.&lt;/li&gt;&lt;li&gt;Use all text or all HTML.&lt;/li&gt;&lt;/ul&gt; |
|Raw Email|  &lt;ul&gt;&lt;li&gt;Used only when Type=Email is selected.&lt;/li&gt;&lt;li&gt;The email message, represented as a raw MIME message.&lt;/li&gt;&lt;li&gt;The entire message must be base64-encoded.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Push Notification

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application ID|  &lt;ul&gt;&lt;li&gt;The unique identifier for the application.&lt;/li&gt;&lt;li&gt;This identifier is displayed as the Project ID on the Amazon Pinpoint console.&lt;/li&gt;&lt;/ul&gt; |
|Push Notification Type|  &lt;ul&gt;&lt;li&gt;Push Notification Type.&lt;/li&gt;&lt;li&gt;Type in custom or select **ADM**, **AMPS**, **BAIDU**, or **GCM**.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;O(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Template

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  &lt;ul&gt;&lt;li&gt;The unique identifier for the application.&lt;/li&gt;&lt;li&gt;This identifier is displayed as the Project ID on the Amazon Pinpoint console.&lt;/li&gt;&lt;/ul&gt; |
|Template Type|  &lt;ul&gt;&lt;li&gt;Template Type&lt;/li&gt;&lt;li&gt;Options are **Email**, **Push**, **SMS**, **Voice**, or **Custom**.&lt;/li&gt;&lt;/ul&gt; |
|Addresses (Template)|  &lt;ul&gt;&lt;li&gt;Addresses (Template), Endpoints (Template) or Destination is required.&lt;/li&gt;&lt;li&gt;Only one of Addresses (Template), Endpoint (Template) or Destination is permitted.&lt;/li&gt;&lt;li&gt;The fields Destination, Body and Title are used to build an Addresses (Template).&lt;/li&gt;&lt;/ul&gt; |
|Context (Template)|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;An object that maps custom attributes to attributes for the address and is attached to the message.&lt;/li&gt;&lt;li&gt;Attributes are case-sensitive.&lt;/li&gt;&lt;li&gt;For a push notification, this payload is added to the `data.pinpoint` object.&lt;/li&gt;&lt;li&gt;For an email or text message, this payload is added to email/SMS delivery receipt event attributes.&lt;/li&gt;&lt;/ul&gt; |
|Destination|  &lt;ul&gt;&lt;li&gt;Addresses (Template), Endpoints (Template) or Destination is required.&lt;/li&gt;&lt;li&gt;Only one of Addresses (Template), Endpoint (Template) or Destination is permitted.&lt;/li&gt;&lt;li&gt;The fields Destination, Body and Title are used to build an Addresses (Template).&lt;/li&gt;&lt;/ul&gt; |
|Endpoints (Template)|  &lt;ul&gt;&lt;li&gt;Addresses (Template), Endpoints (Template) or Destination is required.&lt;/li&gt;&lt;li&gt;Only one of Addresses (Template), Endpoint (Template) or Destination is permitted.&lt;/li&gt;&lt;li&gt;The fields Destination, Body and Title are used to build an Addresses (Template).&lt;/li&gt;&lt;/ul&gt; |
|Name|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The name of the message template to use for the message.&lt;/li&gt;&lt;li&gt;If specified, this value must match the name of an existing message template.&lt;/li&gt;&lt;/ul&gt; |
|TraceId|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for tracing the message.&lt;/li&gt;&lt;li&gt;This identifier is visible in message events.&lt;/li&gt;&lt;/ul&gt; |
|Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the version of the message template to use for the message.&lt;/li&gt;&lt;li&gt;If specified, this value must match the identifier for an existing template version.&lt;/li&gt;&lt;li&gt;To retrieve a list of version and version identifiers for a template, use the [Template Versions](https://docs.aws.amazon.com/pinpoint/latest/apireference/templates-template-name-template-type-versions.html) resource.&lt;/li&gt;&lt;li&gt;If you do not specify a value for this property, Amazon Pinpoint uses the active version of the template.&lt;/li&gt;&lt;li&gt;The active version is typically the version of the template most recently reviewed and approved for use, which is not always the latest version.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header. or Body Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Action - Put Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  &lt;ul&gt;&lt;li&gt;The unique identifier for the application.&lt;/li&gt;&lt;li&gt;This identifier is displayed as the Project ID on the Amazon Pinpoint console.&lt;/li&gt;&lt;/ul&gt; |
|App Package Name|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The package name of the app recording the event.&lt;/li&gt;&lt;/ul&gt; |
|App Title|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The title of the app recording the event.&lt;/li&gt;&lt;/ul&gt; |
|App Version Code|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The version number of the app recording the event.&lt;/li&gt;&lt;/ul&gt; |
|Client Sdk Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The version of the SDK running on the client device.&lt;/li&gt;&lt;/ul&gt; |
|Event Type|  &lt;ul&gt;&lt;li&gt;(Required) String&lt;/li&gt;&lt;li&gt;The name of the event.&lt;/li&gt;&lt;/ul&gt; |
|Sdk Name|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The name of the SDK being used to record the event.&lt;/li&gt;&lt;/ul&gt; |
|Timestamp|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The date and time when the event occurred, in ISO 8601 format.&lt;/li&gt;&lt;/ul&gt; |
|Event Attributes|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;One or more custom attributes associated with the event.&lt;/li&gt;&lt;/ul&gt; |
|Event Metrics|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;One or more custom metrics associated with the event.&lt;/li&gt;&lt;/ul&gt; |
|Duration|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;The duration of the session, in milliseconds.&lt;/li&gt;&lt;/ul&gt; |
|Id|  &lt;ul&gt;&lt;li&gt;(Required) String&lt;/li&gt;&lt;li&gt;The unique identifier for the session.&lt;/li&gt;&lt;/ul&gt; |
|Start Timestamp|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The date and time the session began.&lt;/li&gt;&lt;/ul&gt; |
|Stop Timestamp|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The date and time the session ended.&lt;/li&gt;&lt;/ul&gt; |
|Address|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the recipient, such as a device token, email address, or mobile phone number.&lt;/li&gt;&lt;/ul&gt; |
|Demographic App Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The version of the app associated with the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Locale|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The locale of the endpoint.&lt;/li&gt;&lt;li&gt;Format is the ISO 639-1 alpha-2 code, followed by an underscore (\_), followed by an ISO 3166-1 alpha-2 value.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Make|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The manufacturer of the endpoint device.&lt;/li&gt;&lt;li&gt;Example: **Apple**, **Samsung**&lt;/li&gt;&lt;/ul&gt; |
|Demographic Model|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The model name or number of the endpoint device.&lt;/li&gt;&lt;li&gt;Example: **iPhone**, **SM-G900F**&lt;/li&gt;&lt;/ul&gt; |
|Demographic Model Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The model version of the endpoint device.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Platform|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The platform of the endpoint device.&lt;/li&gt;&lt;li&gt;Example: **ios**&lt;/li&gt;&lt;/ul&gt; |
|Demographic Platform Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The platform version of the endpoint device.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Timezone|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The time zone of the endpoint.&lt;/li&gt;&lt;li&gt;Specified as a `tz` database name value, such as **America/Los\_Angeles**.&lt;/li&gt;&lt;/ul&gt; |
|Effective Date|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The date and time when the endpoint was last updated, in ISO 8601 UTC format.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint ID|  &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Status|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Specifies whether to send messages or push notification to the endpoint.&lt;/li&gt;&lt;li&gt;Valid values are:  &lt;ul&gt;&lt;li&gt;**ACTIVE**: Messages are sent to the endpoint.&lt;/li&gt;&lt;li&gt;**INACTIVE**: Messages are not sent to the endpoint.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Amazon Pinpoint automatically sets this value to **ACTIVE** when you create an endpoint or update and existing endpoint.&lt;/li&gt;&lt;li&gt;Amazon Pinpoint automatically sets this value to **INACTIVE** if you update another endpoint that has the same address, as specified by the `address` property.&lt;/li&gt;&lt;/ul&gt; |
|Location City|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The name of the city where the endpoint is located.&lt;/li&gt;&lt;/ul&gt; |
|Location Country|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Country is the two-character code for the country or region where the endpoint is located, in ISO 3166-1 alpha-2 format.&lt;/li&gt;&lt;li&gt;Example: **en\_US** for the United States&lt;/li&gt;&lt;/ul&gt; |
|Location Latitude|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;li&gt;The latitude coordinate for the endpoint location, rounded to one decimal place.&lt;/li&gt;&lt;/ul&gt; |
|Location Longitude|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;li&gt;The longitude coordinate for the endpoint location, rounded to one decimal place.&lt;/li&gt;&lt;/ul&gt; |
|Location Postal Code|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The postal or zip code for the area where the endpoint is located.&lt;/li&gt;&lt;/ul&gt; |
|Location Region|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The name of the region where the endpoint is located.&lt;/li&gt;&lt;li&gt;For locations in the United States, the value is the name of a state.&lt;/li&gt;&lt;/ul&gt; |
|Request Id|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the request to create or update the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|User Id|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the user.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Attributes|  &lt;ul&gt;&lt;li&gt;One or more custom attributes that describe the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Metrics|  &lt;ul&gt;&lt;li&gt;One or more custom metrics that your app reports to Amazon Pinpoint for the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint User Attributes|  &lt;ul&gt;&lt;li&gt;One or more custom attributes that describe the user by associating a name with an array of values.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Channel Type|  &lt;ul&gt;&lt;li&gt;The channel used when sending messages or push notifications to the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint OptOut|  &lt;ul&gt;&lt;li&gt;Specifies whether the user associated with the endpoint has opted out of receiving messages and push notifications from you.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Endpoint

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  &lt;ul&gt;&lt;li&gt;The unique identifier for the application.&lt;/li&gt;&lt;li&gt;This identifier is displayed as the Project ID on the Amazon Pinpoint console.&lt;/li&gt;&lt;/ul&gt; |
|Address|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the recipient, such as a device token, email address, or mobile phone number.&lt;/li&gt;&lt;/ul&gt; |
|Demographic App Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The version of the app associated with the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Locale|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The locale of the endpoint.&lt;/li&gt;&lt;li&gt;Format is the ISO 639-1 alpha-2 code, followed by an underscore (\_), followed by an ISO 3166-1 alpha-2 value.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Make|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The manufacturer of the endpoint device.&lt;/li&gt;&lt;li&gt;Example: **Apple**, **Samsung**&lt;/li&gt;&lt;/ul&gt; |
|Demographic Model|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The model name or number of the endpoint device.&lt;/li&gt;&lt;li&gt;Example: **iPhone**, **SM-G900F**&lt;/li&gt;&lt;/ul&gt; |
|Demographic Model Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The model version of the endpoint device.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Platform|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The platform of the endpoint device.&lt;/li&gt;&lt;li&gt;Example: **ios**&lt;/li&gt;&lt;/ul&gt; |
|Demographic Platform Version|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The platform version of the endpoint device.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Timezone|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The time zone of the endpoint.&lt;/li&gt;&lt;li&gt;Specified as a `tz` database name value, such as **America/Los\_Angeles**.&lt;/li&gt;&lt;/ul&gt; |
|Effective Date|  &lt;ul&gt;&lt;li&gt;Effective date in ISO 8601 UTC format.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Status|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Specifies whether to send messages or push notification to the endpoint.&lt;/li&gt;&lt;li&gt;Valid values are:  &lt;ul&gt;&lt;li&gt;**ACTIVE**: Messages are sent to the endpoint.&lt;/li&gt;&lt;li&gt;**INACTIVE**: Messages are not sent to the endpoint.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Amazon Pinpoint automatically sets this value to **ACTIVE** when you create an endpoint or update and existing endpoint.&lt;/li&gt;&lt;li&gt;Amazon Pinpoint automatically sets this value to **INACTIVE** if you update another endpoint that has the same address, as specified by the `address` property.&lt;/li&gt;&lt;/ul&gt; |
|Id|  &lt;ul&gt;&lt;li&gt;(Required) String&lt;/li&gt;&lt;li&gt;The unique identifier for the session.&lt;/li&gt;&lt;/ul&gt; |
|Location City|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The name of the city where the endpoint is located.&lt;/li&gt;&lt;/ul&gt; |
|Location Country|  &lt;ul&gt;&lt;li&gt;Location country&lt;/li&gt;&lt;li&gt;Country is the two-character code, in ISO 369-1 alpha-2 code, followed by an underscore (\_), followed by an ISO 3166-1 alpha-2 value.&lt;/li&gt;&lt;li&gt;Example: **en\_US** for the United States&lt;/li&gt;&lt;/ul&gt; |
|Location Latitude|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;li&gt;The latitude coordinate for the endpoint location, rounded to one decimal place.&lt;/li&gt;&lt;/ul&gt; |
|Location Longitude|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;li&gt;The longitude coordinate for the endpoint location, rounded to one decimal place.&lt;/li&gt;&lt;/ul&gt; |
|Location Postal Code|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The postal or zip code for the area where the endpoint is located.&lt;/li&gt;&lt;/ul&gt; |
|Location Region|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The name of the region where the endpoint is located.&lt;/li&gt;&lt;li&gt;For locations in the United States, the value is the name of a state.&lt;/li&gt;&lt;/ul&gt; |
|Request Id|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the request or response.&lt;/li&gt;&lt;/ul&gt; |
|User Id|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The unique identifier for the user.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Attributes|  &lt;ul&gt;&lt;li&gt;One or more custom attributes that describe the endpoint by associating a name with an array of values.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Metrics|  &lt;ul&gt;&lt;li&gt;One or more custom metrics that your app reports to Amazon Pinpoint for the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint User Attributes|  &lt;ul&gt;&lt;li&gt;One or more custom attributes that describe the user by associating a name with an array of values.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint Channel Type|  &lt;ul&gt;&lt;li&gt;The channel used when sending messages or push notifications to the endpoint.&lt;/li&gt;&lt;/ul&gt; |
|Endpoint OptOut|  &lt;ul&gt;&lt;li&gt;Specifies whether the user associated with the endpoint has opted out of receiving messages and push notifications from you.&lt;/li&gt;&lt;li&gt;Valid values are **ALL** or **NONE**.&lt;/li&gt;&lt;/ul&gt; |