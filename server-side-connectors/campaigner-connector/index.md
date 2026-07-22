---
title: Campaigner Connector Setup Guide
description: This article describes how to set up the Campaigner connector.
url: https://docs.tealium.com/server-side-connectors/campaigner-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **API Key**  
  * The Campaigner API key. Required to add, update, or remove subscribers.
* **Integration Key**  
  * The Campaigner integration key. Required for the Upsert contact action.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upsert contact | ✓ | ✗ |
| Add a subscriber | ✓ | ✗ |
| Update subscriber | ✓ | ✗ |
| Remove a subscriber | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Upsert contact

#### Contact

| **Parameter** | **Description** |
| --- | --- |
| Resubscribe | Set to `true` to resubscribe the contact to the email, SMS channel, or both. |
| Contact Id | The contact ID assigned by Campaigner. If provided, the information is updated for this contact. If omitted, the primary key field determines whether to update or insert. |

#### Custom Fields

Map an array of strings for the following fields. If a string is mapped, it is treated as an array of size 1.

| **Parameter** | **Description** |
| --- | --- |
| Field IDs | The unique identifier for the custom fields. |
| Values | The values of the custom fields for the contact. |
| List IDs | List IDs to be associated with this subscriber. Select the checkbox to assign a list. |

#### Static fields

| **Parameter** | **Description** |
| --- | --- |
| Email | The contact's email address. |
| First Name | The contact's first name. |
| Last Name | The contact's last name. |
| Phone | The contact's phone number. |
| Mobile Phone | The contact's mobile number. |
| Fax | The contact's fax number. |
| Email Message Format | The contact's preferred email message format. |
| Email Status | The contact's email status. |
| Sms Status | The contact's SMS status. |
| Is Test Contact | Whether this contact is marked as a test contact. |
| Owner Email | The contact owner's email address. |
| Owner First Name | The contact owner's first name. |
| Owner Last Name | The contact owner's last name. |

#### Trigger Workflows

| **Parameter** | **Description** |
| --- | --- |
| Trigger All Workflows | Set to `true` if Campaigner should trigger all applicable workflows after this contact is created or updated. Default is `false`.  |
| Trigger Specific Workflows | An array of workflow IDs to trigger for this contact's creation or update. Raises an error if `triggerAllWorkflows` is set to `true` and `triggerSpecificWorkflows` have values specified. |

### Add a subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Email Address | The subscriber's email address. |

#### Custom Fields

Map an array of strings for the following fields. If a string is mapped, it is treated as an array of size 1.

| **Parameter** | **Description** |
| --- | --- |
| Field Names | The database column names. |
| Values | The database column values. |
| Source ID | The ID of the source to associate with this subscriber. If not provided, the first source is used. |
| Publications | Publication IDs to associate with the subscriber. If no publications are specified, the subscriber will be inactive and will not receive campaigns. If the subscriber was previously removed from a publication, they will not be re-added unless Force publications is set to `true`. |
| List IDs | List IDs to associate with this subscriber. |

#### Order Data

| **Parameter** | **Description** |
| --- | --- |
| SKUs | The Product SKUs. |
| Quantities | The number of items purchased. Default is `1`. |
| Weights | The total weight of the order item. Default is `0`. |
| Statuses | The status of the order item. |
| Order Number | The order number. |
| Purchase Date | The date order was placed in `YYYY-MM-DD` format (UTC). Defaults to the current date if not provided. |
| Product Names | The name of the product. |
| Unit Prices | The price per unit. Default is `0`. |

#### Force

| **Parameter** | **Description** |
| --- | --- |
| Force | 	Set to `true` to add subscribers previously removed or bounced. If `false` or not provided, the subscriber will not be added and an `HTTP 400 Bad Request `error will be returned. Use this option carefully to avoid adding subscribers who have opted out. |
| Force Publications | Set to `true` to force this subscriber back into a publication they previously requested removal from. |

### Update subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Email Address | The subscriber's email address. |

#### Custom Fields

Map an array of strings for the following fields. If a string is mapped, it will be treated as an array of size 1.

| **Parameter** | **Description** |
| --- | --- |
| Field Names | The database column names. |
| Values | The database column values. |
| Source ID | The ID of the source to associate with this subscriber. If not provided, the first source is used. |
| Publications | Publication IDs to associate with the subscriber. If no publications are specified, the subscriber will be inactive and will not receive campaigns. If the subscriber was previously removed from a publication, they will not be re-added unless Force publications is set to `true`. |
| List IDs | List IDs to associate with this subscriber. |

#### Order Data

| **Parameter** | **Description** |
| --- | --- |
| SKUs | The Product SKUs. |
| Quantities | The number of items purchased. Default is `1`. |
| Weights | The total weight of the order item. Default is `0`. |
| Statuses | The status of the order item. |
| Order Number | The order number. |
| Purchase Date | The date order was placed in `YYYY-MM-DD` format (UTC). Defaults to the current date if not provided. |
| Product Names | The name of the product. |
| Unit Prices | The price per unit. Default is `0`. |

#### Force

| **Parameter** | **Description** |
| --- | --- |
| Force | Set to `true` to add subscribers previously removed or bounced. If `false` or not provided, the subscriber will not be added and an `HTTP 400 Bad Request `error will be returned. Use this option carefully to avoid adding subscribers who have opted out. |
| Force Publications | Set to `true` to force this subscriber back into a publication they previously requested removal from. |

### Remove a subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Email Address | The subscriber's email address. |

