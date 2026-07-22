---
title: Iterable Connector Setup Guide
description: This article describes how to set up the Iterable connector.
url: https://docs.tealium.com/server-side-connectors/iterable-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For more information, see [About connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Host**  
    * For EU-based API endpoints, select **https://app.eu.iterable.com**.
    * For US-based API endpoints, select **https://app.iterable.com**.
* **API Key**: Enter your Iterable API key.

To find your API Key, on the Iterable site, go to **Integrations > API Keys** in the **Iterable Connector** menu.

## Actions

|Action Name| AudienceStream| EventStream|
|---| ---| ---|
|Track Event (Batched)| ✗| ✓|
|Upsert User (Batched)| ✓| ✓|
|Forget a User in Compliance with GDPR| ✓| ✓|
|Send SMS Notification to User| ✓| ✓|
|Send an Email to an Email Address| ✓| ✓|
|Trigger Workflow| ✓| ✓|
|Add a User to a Subscription| ✓| ✗|
|Remove a User from a Subscription| ✓| ✗|
|Subscribe User to List| ✓| ✗|
|Unsubscribe User from List| ✓| ✗|
|Update User Email| ✓| ✓|
|Update Shopping Cart| ✓| ✓|
|Track Purchase| ✓| ✓|
|Merge Customer Data | ✓ | ✓ |

Click **Next** or go to the **Actions** tab.

The following section describes how to set up parameters and options for each action.

### Track Event (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 4 MB

#### Parameters

|Parameter| Description|
|---| ---|
|Event Name| (Required) Name of event.|
|Created At| The time the event occurred, as a Unix timestamp. If omitted, it uses the current processing time. |
|Email| User email. Either **Email** or **User ID** must be entered to identify the user. If both are entered, **Email** takes precedence.|
|Event ID| If an event exists with the entered ID, the event is updated. If none is specified, a new ID is automatically be generated and returned. Note that this ID cannot be longer than 512 bytes.|
|User ID| User ID that was passed into the `updateUser` call.|
|Campaign| <ul><li>Campaign tied to conversion.</li><li>For more information, see [Iterable: Introduction to Campaigns](https://support.iterable.com/hc/en-us/articles/360050203812-Introduction-to-Campaigns-).</li></ul>|
|Project Template| Template ID.  For more information, see [Iterable: Introduction to Templates](https://support.iterable.com/hc/en-us/articles/205480315-Introduction-to-Templates-).|
|Data Fields| Additional data associated with the event. For example: item amount or item quantity. For events of the same name, identically named data fields must be of the same type.|
|Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes</li></ul>|
|Templates| <ul><li>Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Upsert User (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 4 MB

#### Parameters

|Parameter| Description|
|---| ---|
|Email| User email. An email must be set unless a profile already exists with a user ID set. If a profile already exists, a lookup from the **User ID** to **Email** is performed.|
|Merge Nested Objects| Merge top level objects instead of overwriting. The default value is `False`. For example, if the user profile contains `{mySettings:{mobile:true}}` and the change contact field contains `{mySettings:{email:true}}`, the resulting profile would contain `{mySettings:{mobile:true,email:true}}`.|
|Prefer User ID| Create a new user with the specified User ID if the user does not exist yet.|
|User ID| The user ID. Either **Email** or **User ID** must be specified.|
|Data Fields| The data fields to store in the user profile.|
|Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>|
|Templates| <ul><li>Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Forget a User in Compliance with GDPR

#### Parameters

|Parameter| Description|
|---| ---|
|Email| User email. Provide user email if you want to delete the specified user's data from the Iterable project and prevent future data collection about them.|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Send SMS Notification to User

#### Parameters

|Parameter| Description|
|---| ---|
|Campaign| Campaign ID. For more information, see [Iterable: Introduction to Campaigns](https://support.iterable.com/hc/en-us/articles/360050203812-Introduction-to-Campaigns-).|
|Allow Repeat Marketing Sends| Defaults to True.|
|Recipient Email| Either **Email** or **User ID** must be entered to identify the user. If both are entered, **Email** takes precedence.|
|Recipient User ID| User ID that was passed into the `updateUser` call.|
|Send At|  Schedule the message for up to 365 days in the future. If set in the past, the message is sent immediately. Expected format is `YYYY-MM-DD HH:MM:SS`. Ensure data is properly formatted. If attribute of the **Date** type is provided, the connector converts the value to the appropriate date format, shown above. |
|Data Fields| Fields to merge into template.|
|Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`. Nested template variables are typically built from data layer list attributes.</li></ul>|
|Templates| <ul><li>Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Send an Email to an Email Address

#### Parameters

|Parameter| Description|
|---| ---|
|Campaign| Campaign ID. For more information, see [Iterable: Introduction to Campaigns](https://support.iterable.com/hc/en-us/articles/360050203812-Introduction-to-Campaigns-).|
|Allow Repeat Marketing Sends| Defaults to True.|
|Recipient Email| Either **Email** or **User ID** must be entered to identify the user. If both are entered, **Email** takes precedence.|
|Recipient User ID| User ID that was passed into the `updateUser` call.|
|Send At| Schedule the message for up to 365 days in the future. If set in the past, the message is sent immediately. Expected format is `YYYY-MM-DD HH:MM:SS`. Ensure data is properly formatted. If attribute of the **Date** type is provided, the connector converts the value to the appropriate date format, shown above. |
|Data Fields| Fields to merge into email template.|
|Metadata| Metadata to pass back through webhooks. Not used for rendering.|
|Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`. Nested template variables are typically built from data layer list attributes.</li></ul>|
|Templates| <ul><li>Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Trigger Workflow

#### Parameters

|Parameter| Description|
|---| ---|
|Workflow ID| ID of workflow to trigger. For more information, see [Iterable: Introduction to Workflows](https://support.iterable.com/hc/en-us/articles/205480265-Introduction-to-Workflows-).|
|List| Trigger the workflow for all users in a list.|
|Email| Trigger the workflow for the specified email address. Trigger only with **Email** or **List**.|
|Data Fields| Additional data associated with the triggering event.|
|Template Variables| <ul><li>Provide template variables as data input.  For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>|
|Templates| <ul><li>Provide templates to be referenced in Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Add a User to a Subscription

#### Parameters

|Parameter| Description|
|---| ---|
|Subscription Group| Select Subscription Group.|
|Subscription Group ID| Provide the ID of the message channel, message type, or email list to which you are subscribing the user.|
|Email| Provide the email address of the user for which you want to create a subscription. Either **Email** or **User ID** must be specified.|
|User ID| Provide the user ID of the user for which you want to create a subscription. Either **Email** or **User ID** must be specified.|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Remove a User from a Subscription

#### Parameters

|Parameter| Description|
|---| ---|
|Subscription Group| Select Subscription Group.|
|Subscription Group ID| Provide the ID of the message channel, message type, or email list from which you are unsubscribing the user.|
|Email| Provide the email address of the user that you are unsubscribing. Either **Email** or **User ID** must be specified.|
|User ID| Provide user ID of the user that you are unsubscribing. Either **Email** or **User ID** must be specified.|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Subscribe User to List

#### Parameters

|Parameter| Description|
|---| ---|
|List| Select list to subscribe user to.|
|Email| User email. An email must be set unless a profile already exists with a user ID set. In which case, a lookup from **User ID** to **Email** is performed. Either **Email** or **User ID** must be specified.|
|Merge Nested Objects| Merge top level objects instead of overwriting. The default value is `False`. For example, if the user profile contains `{mySettings:{mobile:true}}` and the change contact field contains `{mySettings:{email:true}}`, the resulting profile would contain `{mySettings:{mobile:true,email:true}}`.|
|Prefer User ID| Create a new user with the specified user ID if the user does not exist yet.|
|User ID| Typically your database generated ID. Either **Email** or **User ID** must be specified.|
|Data Fields| The data fields to store in the user profile.|
|Template Variables| <ul><li>Provide template variables as data input.  For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>|
|Templates| <ul><li>Provide templates to be referenced in Body Data.  For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Unsubscribe User from List

#### Parameters

|Parameter| Description|
|---| ---|
|List| Select list to unsubscribe user from.|
|Email| User email. Either **Email** or **User ID** must be specified.|
|User ID| The user ID. Either **Email** or **User ID** must be specified.|
|Campaign| Attribute unsubscribe to a campaign. For more information, see [Iterable: Introduction to Campaigns](https://support.iterable.com/hc/en-us/articles/360050203812-Introduction-to-Campaigns-).|
|Channel Unsubscribe| Unsubscribe email from list's associated channel.|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Update User Email

#### Parameters

|Parameter| Description|
|---| ---|
|New Email| (Required) New user email.|
|Current Email| Current user email. Either **Current Email** or **Current User ID** must be specified.|
|Current User ID| Typically your database generated ID. Either **Current Email** or **Current User ID** must be specified.|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Update Shopping Cart

#### Parameters

|Parameter| Description|
|---| ---|
|Email| User email. Either **Email** or **User ID** must be specified.|
|Merge Nested Objects| Merge top level objects instead of overwriting. The default value is `False`. For example, if the user profile contains `{mySettings:{mobile:true}}` and the change contact field contains `{mySettings:{email:true}}`, the resulting profile would contain `{mySettings:{mobile:true,email:true}}`.|
|Prefer User ID| Create a new user with the specified User ID if the user does not exist yet.|
|User ID| The user ID. Either **Email** or **User ID** must be specified.|
|User Data Fields| The data fields to store in the user profile.|
|User Data Fields Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>|
|User Data Fields Templates| <ul><li>Provide templates to be referenced in User Data Fields.  For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|

#### Item attributes

|Parameter| Description|
|---| ---|
|Item ID| Product item ID.|
|SKU| Product SKU.|
|Name| Product name.|
|Description| Product description.|
|Category| Product category.|
|Subcategory| Product subcategory.|
|Price| Product price.|
|Quantity| Product quantity.|
|Image URL| URL for product image.|
|URL| URL for product page.|
|Items Data Fields| <ul><li>Additional item properties.</li><li>Provide Array type attributes to add multiple items. Array type attributes must be of equal length.</li><li>Items Data Fields arrays and Items Attributes arrays must be of equal length.<br> Single value attributes can be used and are applied to each item.</li></ul>|
|Items Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.<br> Nested template variables are typically built from data layer list attributes.</li></ul>|
|Items Template| <ul><li>If you need nested objects support, use this section to define a template.</li><li>The template expects a JSON array format.</li><li>When template is defined, then configuration from the **Items Attributes** section are ignored.</li><li>Either **Items Template** or **Items Attributes** must be specified.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Track Purchase

#### Parameters

|Parameter| Description|
|---| ---|
|Total| (Required) Total order dollar amount. |
|Purchase ID| ID of purchase transaction.|
|Created At| The time the event occurred, as a Unix timestamp. If omitted, it uses the current processing time. |

#### User attributes

|Parameter| Description|
|---| ---|
|Email| User email. Either **Email** or **User ID** must be entered to identify the user. If both are entered, **Email** takes precedence.|
|Merge Nested Objects| Merge top level objects instead of overwriting. The default value is `False`. For example, if the user profile contains `{mySettings:{mobile:true}}` and the change contact field contains `{mySettings:{email:true}}`, the resulting profile would contain `{mySettings:{mobile:true,email:true}}`.|
|Prefer User ID| Create a new user with the specified User ID if the user does not exist yet.|
|User ID| The user ID. Either **Email** or **User ID** must be specified.|
|Campaign| Campaign ID. For more information, see [Iterable: Introduction to Campaigns](https://support.iterable.com/hc/en-us/articles/360050203812-Introduction-to-Campaigns-).|
|Project Template| <ul><li>Template ID.</li><li>For more information, see [Iterable: Introduction to Templates](https://support.iterable.com/hc/en-us/articles/205480315-Introduction-to-Templates-).</li></ul>|
|Data Fields| Additional fields to be tracked.|
|User Data Fields| The data fields to store in the user profile.|
|Data Fields Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>|
|Data Fields Templates| <ul><li>Provide templates to be referenced in Data Fields and User Data Fields. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul>|

#### Item attributes

|Parameter| Description|
|---| ---|
|Item ID| Product item ID.|
|SKU| Product SKU.|
|Name| Product name.|
|Description| Product description.|
|Category| Product category.|
|Subcategory| Product subcategory.|
|Price| Product price.|
|Quantity| Quantity of product purchased.|
|Image URL| URL for product image.|
|URL| URL for product page.|
|Items Data Fields| <ul><li>Additional item properties.</li><li>Provide Array type attributes to add multiple items. Array type attributes must be of equal length.</li><li>Items Data Fields arrays and Items Attributes arrays must be of equal length.</li><li>Single value attributes can be used and are applied to each item.</li></ul>|
|Items Template Variables| <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>|
|Items Template| <ul><li>If you need nested objects support, use this section to define a template.</li><li>The template expects a JSON array format.</li><li>When template is defined, then configuration from the **Items Attributes** section are ignored.</li><li>Either **Items Template** or **Items Attributes** must be specified.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li></ul>|
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |

### Merge Customer Data

#### Source User Parameters

|Parameter| Description|
| --- | --- |
| Source Email | Identify the source user profile by email. This parameter can be a string or an array. The array size limit is 10. |
| Source User ID | Identify the source user profile by user ID. This parameter can be a string or an array. The array size limit is 10. |

#### Destination User Parameters

|Parameter| Description|
| --- | --- |
| Destination Email | Identify the destination user profile by email. This parameter can be a string or an array. The array size limit is 10 and must be the same size as the source parameter. |
| Destination User ID | Identify the destination user profile by user ID. This parameter can be a string or an array. The array size limit is 10 and must be the same size as the source parameter. |
| API Key Override | Enter an API key or map an attribute for an API key to override the API key specified in the connector configuration. |