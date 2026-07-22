---
title: Bloomreach Connector Setup Guide
description: This article describes how to set up the Bloomreach connector.
url: https://docs.tealium.com/server-side-connectors/bloomreach-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Bloomreach API
* API Version: v2.0
* API Endpoint: `https://api-engagement.bloomreach.com`
* Documentation: [Bloomreach API](https://documentation.bloomreach.com/engagement/reference/about)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **API Key**  
The API key.
* **API Secret**  
The API secret.
* **Project token**  
Your project token. You can find this in the Engagement web app under **Project settings > Access management > API**.
* **API Domain**  
Your Bloomreach API domain. The default value is `https://api-engagement.bloomreach.com`.

## Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see Batched Actions. Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 5 minutes
* Max size of requests: 30 MB

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Update Customer Properties | ✓ | ✗ |
| Update Customer Properties Batch | ✓ | ✗ |
| Add Event | ✓ | ✓ |
| Add Event Batch | ✓ | ✓ |
| Trigger Transactional Email | ✓ | ✓ |
| Trigger Transactional SMS | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Update Customer Properties

#### Customer IDs

| **Parameter** | **Description** |
| --- | --- |
| Registered | (Required) Hard or soft IDs. |

#### Properties

(Required) Customer properties to update.

| **Parameter** | **Description** |
| --- | --- |
| Email | The customer's email address. |
| First Name | The customer's first name. |
| Last Name | The customer's last name. |

#### Optional

| **Parameter** | **Description** |
| --- | --- |
| Update Timestamp | Unix timestamp in seconds. Only properties with an older update time are updated. |

### Update Customer Properties Batch

#### Customer IDs

| **Parameter** | **Description** |
| --- | --- |
| Registered | (Required) Hard or soft IDs. |

#### Properties

(Required) Customer properties to update.

| **Parameter** | **Description** |
| --- | --- |
| Email | The customer's email address. |
| First Name | The customer's first name. |
| Last Name | The customer's last name. |

#### Optional

| **Parameter** | **Description** |
| --- | --- |
| Update Timestamp | Unix timestamp in seconds. Only properties with an older update time are updated. |

### Add Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | Type of the event. The event type based on the filled properties triggers as many events as needed based on the property categories selected.<ul><li>Purchase</li><li>Purchase Item</li><li>Cart Update</li><li>Checkout</li><li>View Item</li><li>View Category</li><li>Consent</li><li>Banner</li><li>Recommendation</li></ul> |

#### Customer IDs

| **Parameter** | **Description** |
| --- | --- |
| Registered | (Required) Hard or soft IDs. |

#### Properties

| **Parameter** | **Description** |
| --- | --- |
| Timestamp | UNIX timestamp of when the event was created (seconds). If not provided, the current time is used. Timestamp supports a date-time in an ISO 8601 format. The value should be in seconds as there is no automatic recognition of milliseconds based on character number. |

### Add Event Batch

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | Type of the event. The event type based on the filled properties triggers as many events as needed based on the property categories selected.<ul><li>Purchase</li><li>Purchase Item</li><li>Cart Update</li><li>Checkout</li><li>View Item</li><li>View Category</li><li>Consent</li><li>Banner</li><li>Recommendation</li></ul> |

#### Customer IDs

| **Parameter** | **Description** |
| --- | --- |
| Registered | (Required) Hard or soft IDs. |

#### Properties

| **Parameter** | **Description** |
| --- | --- |
| Timestamp | UNIX timestamp of when the event was created (seconds). If not provided, the current time is used. Timestamp supports a date-time in an ISO 8601 format. The value should be in seconds as there is no automatic recognition of milliseconds based on character number. |

### Trigger Transactional Email

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Integration ID | The ID of your email service provider integration. This can be found in the URL of the selected integration. |

#### Integrations

| **Parameter** | **Description** |
| --- | --- |
| ID | (Required) The ID of the email service provider integration. |
| Sender Address | (Required) Email address that will be used as the email’s sender for this integration, overriding any other ways of supplying this parameter. |

#### Email Content

| **Parameter** | **Description** |
| --- | --- |
| Template ID | The ID of the email template that you want to send out. This can be found in the URL in the selected predefined template. |
| Subject | Define the email subject. Jinja is not evaluated in this field. |
| Sender Address | The email address of the sender. |
| Sender Name | This is usually a first name of the sender. |
| Attachments Filename | The name of the attachment. |
| Attachments Content | Base64 encoded content of your file. |
| Attachments Content Type | The format of your attachments. |
| Html | Define the content of the email between the `<html>` and `</html>` tags. You can include CSS content. is also accepted. Jinja is not evaluated in this field. |
| Email Content Parameters | Provide all the required data for email personalization used in the template. Format: `param_name`:"value". For example: `first_name`:"Marian" |
| Campaign Name | The name of the email campaign. |

#### Recipient

| **Parameter** | **Description** |
| --- | --- |
| Email | Specify the email of the customer. If the email is not provided, it is taken from the customer profile in Bloomreach Engagement based on the customer ID. |
| Language | Language version of your template. If the template has several language versions created, you can choose which one to use for this email. |

#### Recipient Customer IDs

| **Parameter** | **Description** |
| --- | --- |
| Transfer Identity | Whether link transfer ability should be enabled. Possible values:<ul><li>`Enabled` - default value, appends `iitt` parameter, which identifies on all clicks.</li><li>`Disabled` - appends nothing to the links, no identity transfer.</li><li>`First Click` - appends `xnpe_tifc`, which identifies on first click only.</li></ul> |

#### Email Template Settings

| **Parameter** | **Description** |
| --- | --- |
| Transfer User Identity | Whether link transfer ability should be enabled. Possible values:<ul><li>`enabled` (default value)</li><li>`disabled`</li><li>`iitt` - do not transfer identity into the link.</li></ul> This setting is the same as the `transferidentity` parameter directly in the body of the request. Note that only one can be specified. Specifying transfer identity as part of the settings as well as alone will result in an error. |
| Consent Category | To respect the consent in the Engagement platform, specify the consent category of the customer. |
| Consent Category Tracking | To respect the tracking consent in the Engagement platform, specify the tracking consent category of the customer. |
| Email Template Custom Event Properties | Custom attributes. |
| Email Template Custom Headers | Request headers to send to the email provider. |
| Email Template URL Parameters | URL parameters used for tracking in session start events. |

### Trigger Transactional SMS

#### SmsContent

| **Parameter** | **Description** |
| --- | --- |
| Template ID | The ID of the SMS template you want to send. This can be found in the URL in the selected predefined template. |
| Message | Content of the SMS message. |
| Max Message Parts | The maximum allowed number of message parts. If exceeded, the SMS message is not sent. Minimum value: `1`, Maximum value: `8`, Default value: `8`. |
| Sender | Your sender phone number. |
| Sms Content Parameters | Provide all the required data for SMS personalization used in the template. Format: `param_name`:"value". For example: `first_name`:"Marian". |
| Campaign Name | Name of the SMS campaign. |

#### Recipient

| **Parameter** | **Description** |
| --- | --- |
| Phone | Specify the phone number of the customer. If the phone number is not provided, it is taken from the customer profile in Bloomreach Engagement based on the customer ID. |
| Language | Language version of your template. If the template has several language versions created, you can choose which one to use for this SMS. |

#### Recipient Customer IDs

| **Parameter** | **Description** |
| --- | --- |

#### SMS Template Settings

| **Parameter** | **Description** |
| --- | --- |
| Transfer User Identity | Whether link transfer ability should be enabled. Possible values:<ul><li>`enabled` (default value)</li><li>`disabled`</li><li>`iitt` - do not transfer identity into the link.</li></ul> This setting is the same as the `transferidentity` parameter directly in the body of the request. Note that only one can be specified. Specifying transfer identity as part of the settings as well as alone will result in an error. |
| Consent Category | To respect the consent in the Engagement platform, specify the consent category of the customer. |
| Consent Category Tracking | To respect the tracking consent in the Engagement platform, specify the tracking consent category of the customer. |
| SMS Template Custom Event Properties | Custom attributes. |
| SMS Template Custom Headers | Request headers to send to the SMS provider. |
| SMS Template URL Parameters | URL parameters used for tracking in session start events. |