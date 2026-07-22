---
title: Cordial Connector Setup Guide
description: This article describes how to set up the Cordial connector.
url: https://docs.tealium.com/server-side-connectors/cordial-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Cordial API
* API Version: v1.0
* Documentation: [Cordial API](https://support.cordial.com/hc/en-us/categories/12092749097741-Developer-resources)

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**  
Cordial uses HTTP Basic Authentication (BA). From within the Cordial platform, you can generate an encoded API key for your account. This key is then used as the `username` for your BA credentials. For more information, see [RESTful API Summary and Usage](https://support.cordial.com/hc/en-us/articles/203885498-RESTful-API-summary-and-usage). 
<blockquote>
You must add the [Tealium IP addresses]() to your `API_KEY` whitelist in Cordial.
</blockquote>

* **Path-URL**  
Select one of the following Path URLs or type it manually.
  * `https://api.cordial.io/v2/` - Use this URL if your admin panel URL is `https://admin.cordial.io/`.
  * `https://api.usw2.cordial.io/v2/` - Use this URL if your admin panel URL is `https://usw2.admin.cordial.io/`.

Click **Done** when you are finished configuring the connector.

## Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Upsert contact | ✓ | ✓ |
| Add cart to contact | ✗ | ✓ |
| Record contact activity (event) | ✓  | ✓ |
| Add or delete a contact from an account list | ✓ | ✓ |
| Create a new order | ✗ | ✓ |
| Send notification | ✓ | ✓ |
| Record contact activity (batch) | ✓ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Upsert contact

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact Identifier Key | The contact identifier key. For example, `email`, `cID`. |
| Contact Identifier Value | The contact identifier value. |
| Email Address | Unique channel address to identify and reference the contact. |
| Subscribe Status | Promotional messages will not be sent unless set to `subscribed`. Default is `none`. Possible values: `none`, `subscribed` or `unsubscribed`. |
| Suppress Triggers | If `true`, suppresses message triggers that are based on updates to contact attribute values. Default is `true`. |
| Force Subscribe | If unsubscribed, this key must be used to update subscribe status to subscribed. Possible values: `true`, `false`. |
| Invalid | No email message will be sent unless set to `false`. Default is `false`. Possible values: `true`, `false`. |

#### Optional Parameters

| **Parameter** | **Description** |
| --- | --- |
| Account Lists | Adds or removes the contact from a list. Possible values: true, false. |
| String Parameters | Adds a string attribute value when the attribute type is set as string. |
| Number Parameters | Adds a number attribute value when the attribute type is set as number. |
| Date Parameters | Adds a date attribute value when the attribute type is set as date. |
| Geo Parameters | Adds a geo attribute value when the attribute type is set as geo. Note that geo attributes contain following set schema of key names: <ul><li>Street Address</li><li>Street Address 2</li><li>City</li><li>State</li><li>Postal Code</li><li>Country ISO</li><li>Time Zone</li><li>Location</li><ul><li>Latitude</li><li>Longitude</li></ul></ul> |
| Array Parameters | Adds array attribute values when the attribute type is set as array. The default behavior is to replace the array value with the provided one. An object specifying add/remove behavior can be specified to override the default. If the max items limit is exceeded (default is 25), newer values will replace the oldest values. |

### Add cart to contact

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact Identifier Key | The contact identifier key. For example, `email`, `cID`. |
| Contact Identifier Value | The contact identifier value. |
| Message Contact ID | The message contact ID. |
| Customer ID | The customer ID. |
| Link ID | The link ID. |
| Cart URL | The cart URL. |

#### Cart Item Parameters

| **Parameter** | **Description** |
| --- | --- |
| Product ID | The item identifier. |
| Name | The item name. |
| SKU | The item number. |
| Category | The item category. |
| Quantity | The quantity in the cart. |
| Images | The image names or paths. If item has more than one image the provided value will be split by comma (`,`). |
| Item Price | The price per item. |
| Description | The item description. |
| URL | The link to the item. |

### Record contact activity (event)

#### Parameters


| **Parameter** | **Description** |
| --- | --- |
| Contact Identifier Key | The contact identifier key. For example, `email`, `cID`. |
| Contact Identifier Value | The contact identifier value. |
| Action | Defines a custom action to create, such as browse, order, cart, or any other custom action. The maximum length of the parameter is `40` characters. Note that reserved actions cannot be added through the `POST` method. For more information, see [Contact activities (events) API](https://support.cordial.com/hc/en-us/articles/203885968-Contact-activities-events-API#reservedEvents) |
| Action Timestamp | Action timestamp. If undefined, the current date and time will be used. Date format is `ISO 8601` standard. |
| Properties | An object of additional event attributes. The default maximum number of properties an event can have is `1,000`. Note that property keys consisting of numeric-only values (such as `57`) or keys containing a `dot` (such as `shoes.color`) are stripped. |

### Add or delete a contact from an account list

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Account List | Select account list or enter a list ID. |
| Action | Choose action `Add` or `Delete`. |
| Contact Identifier Key | The contact identifier key. For example, `email`, `cID`. |
| Contact Identifier Value | The contact identifier value. |

### Create a new order

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact Identifier Key | The contact identifier key. For example, `email`, `cID`. |
| Contact Identifier Value | The contact identifier value. |
| Order ID | Unique identifier assigned for the order. |
| Purchase Date | A date value signifying the purchase data and time. Date format is `ISO 8601`. |
| mcID | Cordial ID that represents the account, contact and the message. Required to track revenue attribution to an email. |
| msID | Cordial ID that represents the message. |
| Customer ID | An ID value assigned by the eCommerce or CRM system. |
| Link ID | Cordial ID that represents the message and link. Required to track revenue attribution to a specific link. |
| Total Amount | Auto-calculated as the sum of each `item.amount`. |
| Tax | The amount of the tax. |
| Shipping and Handling | The amount charged for shipping and handling. |
| Properties | key-value pairs describing the properties of the order. |

#### Shipping Address

| **Parameter** | **Description** |
| --- | --- |
| Address | The address. |
| City | The city. |
| Country | The country. |
| Name | The name. |
| Postal Code | The postal code. |
| State | The state. |

#### Billing Address

| **Parameter** | **Description** |
| --- | --- |
| Address | The address. |
| City | The city. |
| Country | The country. |
| Name | The name. |
| Postal Code | The postal code. |
| State | The state. |

#### Item Parameters

| **Parameter** | **Description** |
| --- | --- |
| Product ID | The item identifier. |
| Name | The item name. |
| SKU | The item number. |
| Category | The item category. |
| Quantity | The number of items purchased. Defaults to `1` if not passed. |
| Images | The image names or paths. If item has more than one image the provided value will be split by comma (`,`). |
| Item Price | The price per item. |
| Description | The item description. |
| URL | The link to the item. |
| Amount | Auto-calculated as `qty` x `itemPrice`. If a value not equal to `qty` x `itemPrice` is passed, it is overwritten. |
| Tags | A comma separated array of values to describe the product. Only accepts alphanumeric characters or dashes. |

### Send notification

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Automation Template | Select template or provide template ID. |
| Email | The email. |
| CID | The contact ID. |
| Identify By | Specifies which identifier key in the request body should be used to look up the contact. |
| External Variables | The external variables. Supports templates. |
| Template Variables | <ul><li>Provide template variables as external variables input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation (For example, `items.name`).</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates | <ul><li>Provide templates to be referenced in parameters. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul> |

### Record contact activity (batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 99
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Host | Specify your Cordial region:<ul><li>usw1: `https://integrations-ingest-svc.cordial.com`</li><li>usw2: `https://integrations-ingest-svc.usw2.cordial.com`</li><li>use1: `https://integrations-ingest-svc.use1.cordial.com`</li></ul> |
| Source | Data source. The default value is `TEALIUM`. |

#### Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | Contact ID. |
| Email | Contact email address. |
| Phone | Contact phone number. |
| Custom ID | Primary or secondary keys set up in your account. For more information, see [Cordial: Primary v. secondary keys](https://support.cordial.com/hc/en-us/articles/13084804213517-Primary-v-secondary-keys). |
| Identifiers Priority | The order in which identifiers are used when searching for a contact. |

#### Contact Activity

| **Parameter** | **Description** |
| --- | --- |
| Name | Event name. |
| Time | Action timestamp. If undefined, the current date and time is used. Date format is `ISO 8601` standard. |
| City | Name of the city. |
| Country | Name of the country. |
| Latitude | Latitude coordinate. |
| Longitude | Longitude coordinate. |
| Device | Specific device model. |
| Platform | Operating system of the device. |
| Browser | Browser used on the device. |
| IP | IP address of the device. |
| Robot | Indicates whether the device is operated by a bot. |
| Device Type | Type of device, such as mobile or desktop. |
| Contact Activity Properties | Additional event attributes. By default, each event can have up to 1,000 properties. Property keys that are numeric-only (for example, `57`) or contain a dot (for example, `shoes.color`) are stripped. |
| Contact Attributes | The attributes to set if a contact doesn't exist and should be created. |

#### Contact Options

| **Parameter** | **Description** |
| --- | --- |
| Force subscribe | Force subscribe. |
| Merge allowed | Merge allowed. |
| Mergeable secondary keys | Secondary keys, such as `email`, that can be used to merge contact records. |
| Can be created | (Optional) The default value is `false`. Creates a new contact if it doesn't already exist. |
| Can be updated | (Optional) The default value is `false`. Updates the contact if it already exists. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between 1 and 60 minutes. The default value is 10 minutes. |
