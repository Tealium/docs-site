---
title: Freshdesk Connector Setup Guide
description: This article describes how to set up the Freshdesk connector.
url: https://docs.tealium.com/server-side-connectors/freshdesk-connector/
---
## Requirements

## Supported Actions

| **Action Name**              | **AudienceStream** | **EventStream** |
|:-----------------------------|:-------------------|:----------------|
| Create a Contact             | ✓                  | ✗               |
| Update a Contact             | ✓                  | ✗               |
| Soft Delete a Contact        | ✓                  | ✗               |
| Permanently Delete a Contact | ✓                  | ✗               |

## Configure Settings

Go to the Connector Marketplace and add a new Connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a Connector.

After adding the connector, configure the following settings:

* **Account Domain**: Provide your account's domain name. For example, enter `exampledomain` if your Freshdesk account API endpoint is: `https://exampledomain.freshdesk.com/api/v2/`.   
([Freshdesk API](https://developers.freshdesk.com/api/#getting-started))
* **Username**: For authentication, use the same username and password that you use when you log in to Freshdesk.
* **Password**: For authentication, use the same username and password that you use when you log in to Freshdesk.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create a Contact

#### Parameters

| **Parameter**      | **Description**                                                                                                                                                                                |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name               | Name of the contact. For more information on this endpoint, visit: [Freshdesk's documentation](https://developers.freshdesk.com/api/#create_contact).                                          |
| Email              | Primary email address of the contact. To associate additional emails with this contact, use the `other_emails` attribute.                                                                      |
| Phone              | Telephone number of the contact.                                                                                                                                                               |
| Mobile             | Mobile number of the contact.                                                                                                                                                                  |
| Twitter ID         | X handle of the contact.                                                                                                                                                                 |
| Unique External ID | External ID of the contact.                                                                                                                                                                    |
| Other Emails       | Additional emails associated with the contact. String or set of strings attribute.                                                                                                             |
| Company ID         | ID of the primary company to which this contact belongs.                                                                                                                                       |
| View All Tickets   | `True` or `false`. Set to `true` if the contact can see all the tickets that are associated with the company to which they belong.                                                             |
| Address            | Address of the contact.                                                                                                                                                                        |
| Custom Fields      | Key-value pairs containing the name and value of the custom field. Only dates in the format `YYYY-MM-DD` are accepted as input for custom date fields.                                         |
| Description        | A small description of the contact.                                                                                                                                                            |
| Job Title          | Job title of the contact.                                                                                                                                                                      |
| Language           | Language of the contact. Default language is `en`. This can only be set if the Multiple Language feature is enabled (Garden plan and above).                                                   |
| Tags               | Tags associated with this contact. Must be `set of strings` or `array of strings` attribute type. If only one item is needed here, it must first be formatted to one of those attribute types. |
| Time Zone          | Time zone of the contact. Default value is the time zone of the domain. This can only be set if the Multiple Time Zone feature is enabled (Garden plan and above).                             |

### Action - Update a Contact

#### Parameters

| **Parameter**      | **Description**                                                                                                                                                                                |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Contact ID         | The ID of the contact you want to update. For more information on this endpoint, visit: [Freshdesk's documentation](https://developers.freshdesk.com/api/#update_contact).                     |
| Name               | Name of the contact.                                                                                                                                                                           |
| Email              | Primary email address of the contact. To associate additional emails with this contact, use the `other_emails` attribute.                                                                      |
| Phone              | Telephone number of the contact.                                                                                                                                                               |
| Mobile             | Mobile number of the contact.                                                                                                                                                                  |
| Twitter ID         | X handle of the contact.                                                                                                                                                                 |
| Unique External ID | External ID of the contact.                                                                                                                                                                    |
| Other Emails       | Additional emails associated with the contact. String or set of strings attribute.                                                                                                             |
| Company ID         | ID of the primary company to which this contact belongs.                                                                                                                                       |
| View All Tickets   | `True` or `false`. Set to `true` if the contact can see all the tickets that are associated with the company to which they belong.                                                             |
| Address            | Address of the contact.                                                                                                                                                                        |
| Custom Fields      | Key-value pairs containing the name and value of the custom field. Only dates in the format `YYYY-MM-DD` are accepted as input for custom date fields.                                         |
| Description        | A small description of the contact.                                                                                                                                                            |
| Job Title          | Job title of the contact.                                                                                                                                                                      |
| Language           | Language of the contact. Default language is `en`. This can only be set if the Multiple Language feature is enabled (Garden plan and above).                                                   |
| Tags               | Tags associated with this contact. Must be `set of strings` or `array of strings` attribute type. If only one item is needed here, it must first be formatted to one of those attribute types. |
| Time Zone          | Time zone of the contact. Default value is the time zone of the domain. This can only be set if the Multiple Time Zone feature is enabled (Garden plan and above).                             |

### Action - Soft Delete a Contact

#### Parameters

| **Parameter** | **Description**                                                                                                                                                                 |
|:--------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Contact ID    | The ID of the contact you want to soft delete. For more information on this endpoint, visit: [Freshdesk's documentation](https://developers.freshdesk.com/api/#delete_contact). |

### Action - Permanently Delete a Contact

#### Parameters

| **Parameter** | **Description**                                                                                                                                                   |
|:--------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Contact ID    | ID of the contact you want to permanently delete. This action requires that either the contact is already soft deleted OR the `force` parameter is set to `true`. |
| Force         | `True` or `false`. Set as `true` to force hard delete of a contact that is not already soft deleted.                                                              |
