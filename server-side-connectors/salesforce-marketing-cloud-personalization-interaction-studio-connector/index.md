---
title: Salesforce Marketing Cloud Personalization (Interaction Studio) Connector Setup Guide
description: This article describes how to set up the Salesforce Marketing Cloud Personalization (Interaction Studio) connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-marketing-cloud-personalization-interaction-studio-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Personalization Event API
* API Version: v2
* Documentation: [Personalization Event API](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api.html)

## Connector Actions

| **Action Name**  | **AudienceStream** | **EventStream** |
|:-----------------|:-------------------|:----------------|
| Send Event Data via Trusted Channel (SalesforceInteractions Namespace) | ✓  | ✓ |
| Send Event Data via Trusted Channel (Evergage Namespace) | ✓  | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Account Name**  
(Required) Your Marketing Cloud Personalization account name.  
You can retrieve your account name by accessing **Gears** from the **Interaction Studio UI** in Salesforce and reviewing the URL. For example, if your Gears URL is `https://demo.us-1.evergage.com/`, then your account name is `demo`.
* **Instance Identifier**  
(Required) Your Marketing Cloud Personalization instance identifier.  
You can retrieve your instance identifier by accessing **Gears** from the **Interaction Studio UI** in Salesforce and reviewing the URL. For example, if your Gears URL is `https://demo.us-1.evergage.com/`, then your instance identifier is `us-1`.
* **Dataset Identifier**  
(Required) The name or identifier of the Marketing Cloud Personalization dataset you are sending data to.
* **API Key ID**  
(Required) Your API Key ID that will be used to generate an API Token.  
For more information about API tokens, see [Salesforce: Personalization API Tokens ](https://help.salesforce.com/s/articleView?id=mktg.mc_pers.htm&amp;type=5).
* **API Key Secret**  
(Required) Your API Key Secret that will be used to generate an API Token.  
For more information about API tokens, see [Salesforce: Personalization API Tokens ](https://help.salesforce.com/s/articleView?id=mktg.mc_pers.htm&amp;type=5).

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Event Data via Trusted Channel (SalesforceInteractions Namespace)

#### Event Data Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Explain | If `true`, return additional information in the response about why campaigns did or did not render.  |
| Page View | A value of `true` indicates that the event was triggered from a page load. |
| Time  | (Optional) The date and time of the event (in milliseconds) elapsed since the UNIX epoch. This field will be auto-populated with the current time if null. |

#### Interaction Type Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Interaction Type  | Select interaction type.&lt;br&gt; **Catalog Object Interaction**: Captures engagement data about catalog objects.&lt;br&gt; **Cart Interaction**: Captures engagement data about the contents of a user&#39;s cart.&lt;br&gt; **Order Interaction**: Captures engagement data about the items in a user&#39;s order. In Personalization, only the **PurchaseOrderInteraction** affects and updates a user&#39;s current order.  |

#### Interaction Name Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Interaction Name  | Select interaction name. Names are displayed according to the selected **Interaction Type**.  |

#### Catalog Object Data Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| ID  | A unique ID representing the catalog object.  |
| Type  | A type name representing the catalog object. |

#### Catalog Object Attributes Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Catalog Object Attributes | This section will be ignored if type selected in the **Interaction Type** section is not **Catalog Object Interaction**.&lt;br&gt; Key-value pairs are stored as metadata on the catalog object. These attributes must be defined in the platform.&lt;br&gt; For more information and usage examples, see [Salesforce: Marketing Cloud Personalization Event API](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api.html).&lt;br&gt; If you need nested objects support, you can use the **Templates** section to define a template. The template should be mapped by referencing its names with matching double curly braces: `{{template_name}}`.  |

#### Related Catalog Objects Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Related Catalog Objects | This section is ignored if the type selected in the **Interaction Type** section is not **Catalog Object Interaction**. Related catalog objects are provided as an array of key-value pair objects. These related catalog objects must be defined in the platform. For more information and usage examples, see [Salesforce: Marketing Cloud Personalization Event API](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api.html). |

#### Cart Data Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Cart Data | This section is ignored if the type selected in the **Interaction Type** section is not **Cart Interaction**. This type of Interaction captures engagement data about the contents of a user&#39;s cart. For more information and usage examples, see [Salesforce: Marketing Cloud Personalization Event API](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api.html). If you need nested objects support, you can use the **Templates** section to define a template. Reference the template by its name with matching double curly braces: `{{template_name}}`. |

#### Cart Data Line Items Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Catalog Object ID | A unique ID representing the catalog object. |
| Catalog Object Type | The type representing the catalog object. |
| Currency  | (Optional) The currency code of purchase. If the value is null, the default value is the dataset&#39;s configured currency. |
| Price | The price of the catalog object in the line item. |
| Quantity  | The number of catalog objects in the line item. |

#### Cart Line Items Attributes Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Cart Line Items Attributes  | This section will be ignored if type selected in the **Interaction Type** section is not **Cart Interaction**.&lt;br&gt; Key-value pairs are stored as metadata on the line item object. These attributes must be defined in the platform. For more information and object structure, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; Provide Array type attributes to add multiple items. Array type attributes must be of equal length.&lt;br&gt; **Cart Line Items Attributes** arrays and **Cart Line Items** arrays must be of equal length.&lt;br&gt; Single value attributes can be used and will apply to each item.  |

#### Cart Line Items Template Variables Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Cart Line Items Template Variables  | Provide template variables as data input for **Cart Line Items Template**.&lt;br&gt; For more information and usage examples, see .&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes. |

#### Cart Line Items Template Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Cart Line Items Template  | This section will be ignored if type selected in the **Interaction Type** section is not **Cart Interaction**.&lt;br&gt; If you need nested objects support, use this section to define a template.&lt;br&gt; The template expects a JSON object format if **Add To Cart** or **Remove From Cart** value is selected in the **Interaction Name** section. Otherwise the template expects a JSON array format.&lt;br&gt; When template is defined, then configuration from the **Cart Line Items** and **Cart Line Items Attributes** sections will be ignored.&lt;br&gt; You can use template variables mapped in the **Cart Line Items Template Variables** section.&lt;br&gt;For more information, see . |

#### Order Data Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Order ID  | The ID of the purchased order.  |
| Currency  | The purchase currency code.  |
| Total Value | Total value for purchase. |

#### Order Attributes Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Order Attributes  | This section will be ignored if type selected in the **Interaction Type** section is not **Order Interaction**.&lt;br&gt;Key-value pairs are stored as metadata on the order object. These attributes must be defined in the platform.&lt;br&gt; For more information and usage examples, see [Salesforce: Marketing Cloud Personalization Event API](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api.html).&lt;br&gt; If you need nested objects support, you can use the **Templates** section to define a template. The template should be mapped by referencing its names with matching double curly braces: `{{template_name}}`.  |

#### Order Line Items Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Catalog Object ID | A unique ID representing the catalog object.  |
| Catalog Object Type | The type representing the catalog object. |
| Currency  | (Optional) The currency code of purchase. If the value is null, the default value is the dataset&#39;s configured currency. |
| Price | The price of the catalog object in the line item. |
| Quantity  | The number of catalog objects in the line item. |

#### Order Line Items Attributes Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Order Line Items Attributes | This section will be ignored if type selected in the **Interaction Type** section is not **Order Interaction**.&lt;br&gt;Key-value pairs are stored as metadata on the line item object. These attributes must be defined in the platform. For more information and object structure, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; Provide Array type attributes to add multiple items. Array type attributes must be of equal length.&lt;br&gt; **Order Line Items Attributes** arrays and **Order Line Items** arrays must be of equal length.&lt;br&gt; Single value attributes can be used and will apply to each item.  |

#### Order Line Items Template Variables Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Order Line Items Template Variables | Provide template variables as data input for **Order Line Items Template**.&lt;br&gt; For more information and usage examples, see .&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.  |

#### Order Line Items Template Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Order Line Items Template | This section will be ignored if type selected in the **Interaction Type** section is not **Order Interaction**.&lt;br&gt; If you need nested objects support, use this section to define a template.&lt;br&gt; The template expects a JSON array format.&lt;br&gt; When template is defined, then configuration from the **Order Line Items** and **Order Line Items Attributes** sections will be ignored.&lt;br&gt; You can use template variables mapped in the **Order Line Items Template Variables** section.&lt;br&gt;For more information, see .  |

#### Consents Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Provider  | The consent provider. |
| Purpose | The purpose for the consent. For example, **Personalization**.  |
| Status  | The consent status. For example, **OptIn** or **OptOut**. |

#### Debug Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Test Messages | A comma-separated list of campaign experience IDs to be forced to return in the event, ignoring rules that would otherwise prevent the campaign from returning. Alternatively, you can use the string value true to return all campaigns in testing mode but all rules are respected. |

#### Flags Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| No Campaigns  | If `true`, do not return campaigns in the response. |
| Non Interactive | If `true`, a visit is not created (or updated) for the given user in the event. Additionally, no visit referrer nor originating referrer is created for the user. |

#### Source Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Application | The originating application level source of the event. For example, **ReactApp**, **3rdParty**, **ReactNative**.  |
| Channel | The originating source of the event. For example, **Web**, **MobileApp**, **CallCenter**. |
| Client IP | The IP Address sending the event. `clientIp` is populated automatically but can be overwritten if necessary.  |
| Config Version  | Version number of the configuration for the SDK.  |
| Content Zones | An array of content zones on the current page.  |
| Device  | Only applicable for mobile events.  |
| Locale  | The locale of the current page, as defined by ISO 639 alpha-2 language codes and ISO 3166 alpha-2 country codes. For example, **en_US** and **de_DE**. |
| Operating System  | Only applicable for mobile events.  |
| Operating System Version  | Only applicable for mobile events.  |
| Page Type | The type of page from which you are sending the event. For example, **PDP**, **Blog**, **Pricing**. |
| Survey ID | The ID of the survey being submitted. Set automatically for events sent through the Survey Gear.  |
| Survey Start Time | The start time of the survey being submitted. Set automatically for events sent through the Survey Gear.  |
| URL | The URL of the page from which you are sending the event. |
| URL Referrer  | The previous URL visited by the user. `urlReferrer` is populated from `document.referrer` by default on the web. It can be overwritten in the sitemap to any other value if necessary.  |
| User Agent  | The user agent for the event. `userAgent` is populated automatically but can be overwritten if necessary. |

#### User Data Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Anonymous ID  | The ID of an anonymous user.  |
| Encrypted ID  | The encrypted ID returned from an event that contains the ID field. Encrypted IDs are returned in the response to events that provide identities. |

#### User Identities Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| User Identities | Key-value pairs are stored as identity information of a user.&lt;br&gt; For more information and usage examples, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).  |

#### User Attributes Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| User Attributes | Key-value pairs are stored as metadata on the user. These attributes must be defined in the platform.&lt;br&gt;  For more information and usage examples, see [Salesforce: Marketing Cloud Personalization Event API](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api.html).&lt;br&gt; If you need nested objects support, you can use the **Templates** section to define a template. The template should be mapped by referencing its names with matching double curly braces: `{{template_name}}`. |

#### Profile Objects Template Variables Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Profile Objects Template Variables  | Provide template variables as data input for **Profile Objects Template**.&lt;br&gt; For more information and usage examples, see .&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes. |

#### Profile Objects Template Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Profile Objects Template  | Provide template to send key-value pairs of profile objects that are stored as metadata on the user.&lt;br&gt; Profile objects, their attributes, and related catalog objects must be defined in the platform. For more information and object structure, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; The template expects a valid JSON object format.&lt;br&gt; You can use template variables mapped in the **Profile Objects Template Variables** section.&lt;br&gt; For more information, see .  |

#### Account Data Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| ID  | The ID of an account. |

#### Account Attributes Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Account Attributes  |Key-value pairs are stored as metadata on the account. These attributes must be defined in the platform.&lt;br&gt; For more information and object structure, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; If you need nested objects support, you can use the **Templates** section to define a template. The template should be mapped by referencing its names with matching double curly braces: `{{template_name}}`.  |

#### Performance Metrics Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Network Time  | Time (in milliseconds) for the previous request to return.  |
| Page Load Time  | Time (in milliseconds) for the DOM to load. |
| SDK Load Time | Time (in milliseconds) for the network to load the web SDK. |
| SDK Parse Time  | Time (in milliseconds) for the beacon to be parsed during page load.  |

#### CampaignStat Array Template Variables Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| CampaignStat Array Template Variables | Provide template variables as data input for **CampaignStat Array Template**.&lt;br&gt; For more information and usage examples, see .&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes. |

#### CampaignStat Array Template Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| CampaignStat Array Template | Provide a template to send **campaignStats** array that is used to track campaign statistics for an associated event. For more information and object structure, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; The template expects a valid JSON array format.&lt;br&gt; You can use template variables mapped in the **CampaignStat Array Template Variables** section.&lt;br&gt; For more information about templates, see [Templates Guide](). |

#### Template Variables Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Template Variables  | Provide template variables as data input for **Templates**.&lt;br&gt; For usage examples, see [Template Variables Guide]().&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes. |

#### Templates Parameters

| **Parameter** | **Description**  |
|:------------------------|:-------------------|
| Templates | Provide templates to be referenced in **Event Data**, **Catalog Object Data**, **Catalog Object Attributes**, **Cart Data**, **Order Data**, **Order Attributes**, **Debug**, **Flags**, **Source**, **User Data**, **User Attributes**, **Account Data**, **Account Attributes** and **Performance Metrics** sections.&lt;br&gt; The template expects a valid JSON object format.&lt;br&gt; For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Action — Send Event Data via Trusted Channel (Evergage Namespace)

#### Item Action Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Item Action | Select the action taken on a catalog item.&lt;br&gt; For more information about supported item actions, see [Salesforce: Item Actions](https://developer.salesforce.com/docs/marketing/personalization/guide/item-actions.html?_ga=2.26533758.275889428.1751986406-534341303.1751986398). |

#### Event Data Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Action  | Name of the event. Used for segmentation, targeting, and reporting.  |

#### Catalog Data Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Item Type | (Required) Provide the type of the item to send `catalog` object. |

#### Order Data Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Item Type | (Required) Provide the type of the item to send `order` object. |
| Order ID  | ID of the purchased order. |
| Currency  | (Optional) The currency code of purchase. If the value is null, the default value is the dataset&#39;s configured currency. |
| Total Value | Total value for purchase. The default value is the sum of line items price multiplied by quantity. |

#### Order Line Items Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| ID  | The ID of the item.  |
| Price | The price of the item. |
| Quantity  | The number of items. |

#### Cart Data Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Item Type | (Required) Provide the type of the item to send `cart` object.  |

#### Cart Line Items Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| ID  | The ID of the item.  |
| Price | The price of the item. |
| Quantity  | The number of items. |

#### Consents Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Provider  | The consent provider.  |
| Purpose | The purpose for the consent. For example, **Personalization**. |
| Status  | The consent status. For example, **OptIn** or **OptOut**.  |

#### Debug Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Explanations  | If `true`, then return additional information in the response about why campaigns did or did not render. |
| Test Messages | A comma-separated list of campaign experience IDs to be forced to return in the event, ignoring rules that would otherwise prevent the campaign from returning. Alternatively, you can use the string value true to return all campaigns in testing mode but all rules are respected.  |

#### Flags Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Do Not Track  | If `true`, do not process the event once it is sent to the server.  |
| No Campaigns  | If `true`, do not return campaigns in the response.  |
| Non Interactive | If `true`, a visit is not created (or updated) for the given user in the event. Additionally, no visit referrer nor originating referrer is created for the user.  |
| Page View | If `true`, indicates that the event was triggered from a page load.  |

#### Source Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Application | The originating application level source of the event. For example, **ReactApp**, **3rdParty**, **ReactNative**. |
| Channel | The originating source of the event. For example, **Web**, **MobileApp**, **CallCenter**.  |
| Client IP | The IP Address sending the event. `clientIp` is populated automatically but can be overwritten if necessary. |
| Config Version  | Version number of the configuration for the SDK. |
| Content Zones | An array of content zones on the current page. |
| Device  | Only applicable for mobile events. |
| Locale  | The locale of the current page, as defined by ISO 639 alpha-2 language codes and ISO 3166 alpha-2 country codes. For example, **en\_US** and **de\_DE**. |
| Operating System  | Only applicable for mobile events. |
| Operating System Version  | Only applicable for mobile events. |
| Page Type | The type of page from which you are sending the event. For example, **PDP**, **Blog**, **Pricing**.  |
| Survey ID | The ID of the survey being submitted. Set automatically for events sent through the Survey Gear. |
| Survey Start Time | The start time of the survey being submitted. Set automatically for events sent through the Survey Gear. |
| Time  | (Optional) The date and time of the event (in milliseconds) elapsed since the UNIX epoch. This field will be auto-populated with the current time if null. |
| URL | The URL of the page from which you are sending the event.  |
| URL Referrer  | The previous URL visited by the user. `urlReferrer` is populated from `document.referrer` by default on the web. It can be overwritten in the sitemap to any other value if necessary. |
| User Agent  | The user agent for the event. `userAgent` is populated automatically but can be overwritten if necessary.  |

#### Encrypted ID Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Encrypted ID  | The encrypted ID returned from an event that contains the ID field. Encrypted IDs are returned in the response to events that provide a `user.id`. |
| ID  | The ID of a known user.  |

#### User Attributes Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| User Attributes | Key-value pairs are stored as metadata on the user. These attributes must be defined in the platform.&lt;br&gt;For more information and usage examples, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; If you need nested objects support, you can use the **Templates** section to define a template. The template should be mapped by referencing its names with matching double curly braces: `{{template_name}}`. |

#### Profile Objects Template Variables Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Profile Objects Template Variables  | Provide template variables as data input for **Profile Objects Template**.&lt;br&gt; For more information and usage examples, see .&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.  |

#### Profile Objects Template Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Profile Objects Template  | Provide template to send key-value pairs of profile objects are stored as metadata on the user.&lt;br&gt; Profile objects, their attributes, and related catalog objects must be defined in the platform. For more information and usage examples, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; The template expects a valid JSON object format.&lt;br&gt; You can use template variables mapped in the **Profile Objects Template Variables** section.&lt;br&gt; For more information, see . |

#### Account Data Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| ID  | The ID of an account.  |

#### Account Attributes Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Account Attributes  | Key-value pairs are stored as metadata on the account. These attributes must be defined in the platform.&lt;br&gt; For more information and usage examples, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; If you need nested objects support, you can use the **Templates** section to define a template. The template should be mapped by referencing its names with matching double curly braces: `{{template_name}}`.  |

#### Performance Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| DOM Load Time | Time (in milliseconds) for the DOM to finish loading.  |
| Event DNS Time  | Time (in milliseconds) to resolve account-specific domain. |
| Network Time  | Time (in milliseconds) for the previous request to return. |
| Page Load Time  | Time (in milliseconds) for the DOM to load.  |
| SDK DNS Time  | Time (in milliseconds) to perform resolution of SDK&#39;s CDN domain.  |
| SDK Load Time | Time (in milliseconds) for the network to load the web SDK.  |
| SDK Parse Time  | Time (in milliseconds) for the beacon to be parsed during page load. |

#### CampaignStat Array Template Variables Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| CampaignStat Array Template Variables | Provide template variables as data input for **CampaignStat Array Template**.&lt;br&gt; For more information and usage examples, see .&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes. |

#### CampaignStat Array Template Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| CampaignStat Array Template | Provide template to send **campaignStats** array that is used to track campaign statistics for an associated event. For more information and usage examples, see [Salesforce: Event API Requests](https://developer.salesforce.com/docs/marketing/personalization/guide/event-api-requests.html).&lt;br&gt; The template expects a valid JSON array format.&lt;br&gt; You can use template variables mapped in the **CampaignStat Array Template Variables** section.&lt;br&gt; For more information about templates, see [Templates Guide]().  |

#### Template Variables Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Template Variables  | Provide template variables as data input for **Templates**.&lt;br&gt; For usage examples, see [Template Variables Guide]().&lt;br&gt; Name nested template variables with the dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes. |

#### Templates Parameters

| **Parameter** | **Description**  |
|:--------------|:-----------------|
| Templates | Provide templates to be referenced in **Event Data**, **Catalog Data**, **Order Data**, **Cart Data**, **Debug**, **Flags**, **Source**, **User Data**, **User Attributes**, **Account Data**, **Account Attributes** and **Performance** sections.&lt;br&gt; The template expects a valid JSON object format.&lt;br&gt; For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |