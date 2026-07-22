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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Access Key**
  * (Required) Provide your IAM User's access key
  * Associated IAM policy (for either IAM User or Assumed Role) must grant `mobiletargeting:*`, `ses:*`, `sms-voice:\*` permissions.
  * For additional information, see: [Amazon Pinpoint](https://docs.aws.amazon.com/pinpoint/latest/developerguide/security_iam_service-with-iam.html).

* **Secret Key**
  * (Required) Provide your IAM User's secret key

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
|Application Id|  <ul><li>(Required) The unique identifier for the application.</li><li>This identifier is displayed as the Project ID on the Amazon Pinpoint console.</li></ul> |
|Message Type|  <ul><li>Message Type</li><li>Options are **Email**, **SMS**, or **Voice**.  <ul><li>Addresses (Template), Endpoints (Template) or Destination is required and only one of each is permitted.</li><li>The fields Destination, Body, and Title are used to build an Addresses (Template).</li></ul> </li><li>SMS  <ul><li>Body for the SMS message type is required.</li><li>Valid values for Message type are `TRANSACTIONAL` or `PROMOTIONAL`.</li></ul> </li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables as data input for templates.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |
|Charset|  <ul><li>Character set mapping for the message content.</li></ul> |
|Html Part|  <ul><li>Only one of Text Part or HTML part is permitted.</li></ul> |
|Subject|  <ul><li>(Required) Subject of the email.</li></ul> |
|Text Part|  <ul><li>Text or HTML.</li><li>Use all text or all HTML.</li></ul> |
|Raw Email|  <ul><li>Used only when Type=Email is selected.</li><li>The email message, represented as a raw MIME message.</li><li>The entire message must be base64-encoded.</li></ul> |

### Action - Send Push Notification

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application ID|  <ul><li>The unique identifier for the application.</li><li>This identifier is displayed as the Project ID on the Amazon Pinpoint console.</li></ul> |
|Push Notification Type|  <ul><li>Push Notification Type.</li><li>Type in custom or select **ADM**, **AMPS**, **BAIDU**, or **GCM**.</li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables as data input for templates.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>O(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |

### Action - Send Template

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  <ul><li>The unique identifier for the application.</li><li>This identifier is displayed as the Project ID on the Amazon Pinpoint console.</li></ul> |
|Template Type|  <ul><li>Template Type</li><li>Options are **Email**, **Push**, **SMS**, **Voice**, or **Custom**.</li></ul> |
|Addresses (Template)|  <ul><li>Addresses (Template), Endpoints (Template) or Destination is required.</li><li>Only one of Addresses (Template), Endpoint (Template) or Destination is permitted.</li><li>The fields Destination, Body and Title are used to build an Addresses (Template).</li></ul> |
|Context (Template)|  <ul><li>Object</li><li>An object that maps custom attributes to attributes for the address and is attached to the message.</li><li>Attributes are case-sensitive.</li><li>For a push notification, this payload is added to the `data.pinpoint` object.</li><li>For an email or text message, this payload is added to email/SMS delivery receipt event attributes.</li></ul> |
|Destination|  <ul><li>Addresses (Template), Endpoints (Template) or Destination is required.</li><li>Only one of Addresses (Template), Endpoint (Template) or Destination is permitted.</li><li>The fields Destination, Body and Title are used to build an Addresses (Template).</li></ul> |
|Endpoints (Template)|  <ul><li>Addresses (Template), Endpoints (Template) or Destination is required.</li><li>Only one of Addresses (Template), Endpoint (Template) or Destination is permitted.</li><li>The fields Destination, Body and Title are used to build an Addresses (Template).</li></ul> |
|Name|  <ul><li>String</li><li>The name of the message template to use for the message.</li><li>If specified, this value must match the name of an existing message template.</li></ul> |
|TraceId|  <ul><li>String</li><li>The unique identifier for tracing the message.</li><li>This identifier is visible in message events.</li></ul> |
|Version|  <ul><li>String</li><li>The unique identifier for the version of the message template to use for the message.</li><li>If specified, this value must match the identifier for an existing template version.</li><li>To retrieve a list of version and version identifiers for a template, use the [Template Versions](https://docs.aws.amazon.com/pinpoint/latest/apireference/templates-template-name-template-type-versions.html) resource.</li><li>If you do not specify a value for this property, Amazon Pinpoint uses the active version of the template.</li><li>The active version is typically the version of the template most recently reviewed and approved for use, which is not always the latest version.</li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables as data input for templates.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
|Templates|  <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header. or Body Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |

### Action - Put Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  <ul><li>The unique identifier for the application.</li><li>This identifier is displayed as the Project ID on the Amazon Pinpoint console.</li></ul> |
|App Package Name|  <ul><li>String</li><li>The package name of the app recording the event.</li></ul> |
|App Title|  <ul><li>String</li><li>The title of the app recording the event.</li></ul> |
|App Version Code|  <ul><li>String</li><li>The version number of the app recording the event.</li></ul> |
|Client Sdk Version|  <ul><li>String</li><li>The version of the SDK running on the client device.</li></ul> |
|Event Type|  <ul><li>(Required) String</li><li>The name of the event.</li></ul> |
|Sdk Name|  <ul><li>String</li><li>The name of the SDK being used to record the event.</li></ul> |
|Timestamp|  <ul><li>String</li><li>The date and time when the event occurred, in ISO 8601 format.</li></ul> |
|Event Attributes|  <ul><li>Object</li><li>One or more custom attributes associated with the event.</li></ul> |
|Event Metrics|  <ul><li>Object</li><li>One or more custom metrics associated with the event.</li></ul> |
|Duration|  <ul><li>Integer</li><li>The duration of the session, in milliseconds.</li></ul> |
|Id|  <ul><li>(Required) String</li><li>The unique identifier for the session.</li></ul> |
|Start Timestamp|  <ul><li>String</li><li>The date and time the session began.</li></ul> |
|Stop Timestamp|  <ul><li>String</li><li>The date and time the session ended.</li></ul> |
|Address|  <ul><li>String</li><li>The unique identifier for the recipient, such as a device token, email address, or mobile phone number.</li></ul> |
|Demographic App Version|  <ul><li>String</li><li>The version of the app associated with the endpoint.</li></ul> |
|Demographic Locale|  <ul><li>String</li><li>The locale of the endpoint.</li><li>Format is the ISO 639-1 alpha-2 code, followed by an underscore (\_), followed by an ISO 3166-1 alpha-2 value.</li></ul> |
|Demographic Make|  <ul><li>String</li><li>The manufacturer of the endpoint device.</li><li>Example: **Apple**, **Samsung**</li></ul> |
|Demographic Model|  <ul><li>String</li><li>The model name or number of the endpoint device.</li><li>Example: **iPhone**, **SM-G900F**</li></ul> |
|Demographic Model Version|  <ul><li>String</li><li>The model version of the endpoint device.</li></ul> |
|Demographic Platform|  <ul><li>String</li><li>The platform of the endpoint device.</li><li>Example: **ios**</li></ul> |
|Demographic Platform Version|  <ul><li>String</li><li>The platform version of the endpoint device.</li></ul> |
|Demographic Timezone|  <ul><li>String</li><li>The time zone of the endpoint.</li><li>Specified as a `tz` database name value, such as **America/Los\_Angeles**.</li></ul> |
|Effective Date|  <ul><li>String</li><li>The date and time when the endpoint was last updated, in ISO 8601 UTC format.</li></ul> |
|Endpoint ID|  <ul><li>Required</li></ul> |
|Endpoint Status|  <ul><li>String</li><li>Specifies whether to send messages or push notification to the endpoint.</li><li>Valid values are:  <ul><li>**ACTIVE**: Messages are sent to the endpoint.</li><li>**INACTIVE**: Messages are not sent to the endpoint.</li></ul> </li><li>Amazon Pinpoint automatically sets this value to **ACTIVE** when you create an endpoint or update and existing endpoint.</li><li>Amazon Pinpoint automatically sets this value to **INACTIVE** if you update another endpoint that has the same address, as specified by the `address` property.</li></ul> |
|Location City|  <ul><li>String</li><li>The name of the city where the endpoint is located.</li></ul> |
|Location Country|  <ul><li>String</li><li>Country is the two-character code for the country or region where the endpoint is located, in ISO 3166-1 alpha-2 format.</li><li>Example: **en\_US** for the United States</li></ul> |
|Location Latitude|  <ul><li>Number</li><li>The latitude coordinate for the endpoint location, rounded to one decimal place.</li></ul> |
|Location Longitude|  <ul><li>Number</li><li>The longitude coordinate for the endpoint location, rounded to one decimal place.</li></ul> |
|Location Postal Code|  <ul><li>String</li><li>The postal or zip code for the area where the endpoint is located.</li></ul> |
|Location Region|  <ul><li>String</li><li>The name of the region where the endpoint is located.</li><li>For locations in the United States, the value is the name of a state.</li></ul> |
|Request Id|  <ul><li>String</li><li>The unique identifier for the request to create or update the endpoint.</li></ul> |
|User Id|  <ul><li>String</li><li>The unique identifier for the user.</li></ul> |
|Endpoint Attributes|  <ul><li>One or more custom attributes that describe the endpoint.</li></ul> |
|Endpoint Metrics|  <ul><li>One or more custom metrics that your app reports to Amazon Pinpoint for the endpoint.</li></ul> |
|Endpoint User Attributes|  <ul><li>One or more custom attributes that describe the user by associating a name with an array of values.</li></ul> |
|Endpoint Channel Type|  <ul><li>The channel used when sending messages or push notifications to the endpoint.</li></ul> |
|Endpoint OptOut|  <ul><li>Specifies whether the user associated with the endpoint has opted out of receiving messages and push notifications from you.</li></ul> |

### Action - Update Endpoint

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Application Id|  <ul><li>The unique identifier for the application.</li><li>This identifier is displayed as the Project ID on the Amazon Pinpoint console.</li></ul> |
|Address|  <ul><li>String</li><li>The unique identifier for the recipient, such as a device token, email address, or mobile phone number.</li></ul> |
|Demographic App Version|  <ul><li>String</li><li>The version of the app associated with the endpoint.</li></ul> |
|Demographic Locale|  <ul><li>String</li><li>The locale of the endpoint.</li><li>Format is the ISO 639-1 alpha-2 code, followed by an underscore (\_), followed by an ISO 3166-1 alpha-2 value.</li></ul> |
|Demographic Make|  <ul><li>String</li><li>The manufacturer of the endpoint device.</li><li>Example: **Apple**, **Samsung**</li></ul> |
|Demographic Model|  <ul><li>String</li><li>The model name or number of the endpoint device.</li><li>Example: **iPhone**, **SM-G900F**</li></ul> |
|Demographic Model Version|  <ul><li>String</li><li>The model version of the endpoint device.</li></ul> |
|Demographic Platform|  <ul><li>String</li><li>The platform of the endpoint device.</li><li>Example: **ios**</li></ul> |
|Demographic Platform Version|  <ul><li>String</li><li>The platform version of the endpoint device.</li></ul> |
|Demographic Timezone|  <ul><li>String</li><li>The time zone of the endpoint.</li><li>Specified as a `tz` database name value, such as **America/Los\_Angeles**.</li></ul> |
|Effective Date|  <ul><li>Effective date in ISO 8601 UTC format.</li></ul> |
|Endpoint Status|  <ul><li>String</li><li>Specifies whether to send messages or push notification to the endpoint.</li><li>Valid values are:  <ul><li>**ACTIVE**: Messages are sent to the endpoint.</li><li>**INACTIVE**: Messages are not sent to the endpoint.</li></ul> </li><li>Amazon Pinpoint automatically sets this value to **ACTIVE** when you create an endpoint or update and existing endpoint.</li><li>Amazon Pinpoint automatically sets this value to **INACTIVE** if you update another endpoint that has the same address, as specified by the `address` property.</li></ul> |
|Id|  <ul><li>(Required) String</li><li>The unique identifier for the session.</li></ul> |
|Location City|  <ul><li>String</li><li>The name of the city where the endpoint is located.</li></ul> |
|Location Country|  <ul><li>Location country</li><li>Country is the two-character code, in ISO 369-1 alpha-2 code, followed by an underscore (\_), followed by an ISO 3166-1 alpha-2 value.</li><li>Example: **en\_US** for the United States</li></ul> |
|Location Latitude|  <ul><li>Number</li><li>The latitude coordinate for the endpoint location, rounded to one decimal place.</li></ul> |
|Location Longitude|  <ul><li>Number</li><li>The longitude coordinate for the endpoint location, rounded to one decimal place.</li></ul> |
|Location Postal Code|  <ul><li>String</li><li>The postal or zip code for the area where the endpoint is located.</li></ul> |
|Location Region|  <ul><li>String</li><li>The name of the region where the endpoint is located.</li><li>For locations in the United States, the value is the name of a state.</li></ul> |
|Request Id|  <ul><li>String</li><li>The unique identifier for the request or response.</li></ul> |
|User Id|  <ul><li>String</li><li>The unique identifier for the user.</li></ul> |
|Endpoint Attributes|  <ul><li>One or more custom attributes that describe the endpoint by associating a name with an array of values.</li></ul> |
|Endpoint Metrics|  <ul><li>One or more custom metrics that your app reports to Amazon Pinpoint for the endpoint.</li></ul> |
|Endpoint User Attributes|  <ul><li>One or more custom attributes that describe the user by associating a name with an array of values.</li></ul> |
|Endpoint Channel Type|  <ul><li>The channel used when sending messages or push notifications to the endpoint.</li></ul> |
|Endpoint OptOut|  <ul><li>Specifies whether the user associated with the endpoint has opted out of receiving messages and push notifications from you.</li><li>Valid values are **ALL** or **NONE**.</li></ul> |