---
title: Braze Connector Setup Guide
description: This article describes how to set up the Braze connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/braze-connector/
---
## Consent categories

* Analytics
* Mobile
* Personalization

## Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Endpoint**  
(Required) Select API endpoint for the instance your account is provisioned to.  
For more information, see [Braze API Endpoints](https://www.braze.com/docs/developer_guide/rest_api/basics/#endpoints).
* **API Key**  
(Required) Provide API key with permission enabled for `users.track` and `users.delete`.  
For more information, see [Braze App Group REST API Keys](https://www.braze.com/docs/api/basics/?redirected=true#app-group-rest-api-keys).

For additional information see Braze Documentation [Braze Technology Partners: Tealium](https://www.braze.com/docs/partners/data_and_infrastructure_agility/customer_data_platform/tealium/).

## Actions

This section describes how to set up parameters and options for each action.

The **Track User** action contains the same functionality for both AudienceStream and EventStream. As a best practice, set the user attribute mappings for the AudienceStream action and the event and purchase mappings for the EventStream action.

| **Action Name**                                   | **AudienceStream** | **EventStream** |
|:--------------------------------------------------|:-------------------|:----------------|
| Track User (Batch)                                | ✓                  | ✓               |
| Track User (Non-Batch)                            | ✓                  | ✓               |
| Delete User (Non-Batch)                           | ✓                  | ✓               |
| Update User Subscription Group Status (Non-Batch) | ✓                  | ✗               |
| Update User Subscription Group Status Across Multiple Subscription Groups (Non-Batch) | ✓ | ✗ |
| Send Campaign Message                             | ✓                  | ✓               |
| Send Canvas Message                               | ✓                  | ✓               |
| Send Transactional Email                          | ✓                  | ✓               |
| Identify User                                     | ✓                  | ✓               |

### Track User (Batch/Non-Batch)

We recommend mapping as many ID parameters as possible. When an action triggers with multiple IDs mapped, the first non-blank value is selected based on the following priority order:

* External ID
* Braze ID
* Alias Name/Alias Label

For more information, see [Braze API: User Track](https://www.braze.com/docs/api/endpoints/user_data/post_user_track/).

#### Batch vs. non-batch  

* **Batch**: Use for large user profile backfills and syncs.
* **Non-batch**: Use for real-time use cases.

During peak traffic conditions, Braze prioritizes non-batch requests over batch requests.

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 75
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### User ID

| **Parameter**    | **Description**                                                                       |
|:-----------------|:--------------------------------------------------------------------------------------|
| External ID      | External ID of the user.                                                              |
| Braze ID         | Braze ID of the user.                                                                 |
| User Alias Name  | The alias name of the user. When specifying a user alias, both `Alias Name` and `Alias Label` must be set.  |
| User Alias Label | The alias label of the user. When specifying a user alias, both `Alias Name` and `Alias Label` must be set. |
| Customer Email Address | The email address of the customer. |
| Customer Phone Number | The phone number of the customer. |

#### User Attributes

We recommend following the Braze best practice of only sending changed user attributes and avoiding sending unchanged attributes. To avoid sending unchanged attributes, use visit and visitor attribute enrichments and rules that recognize when an attribute has changed. For more information, see [Enrichment Rules]().

Empty values are converted to `null` and removed from the Braze user profile.

| **Parameter** | **Description** |
|:--------------|:----------------|
| Country                      | The country of the user.|
| Current Location - Latitude  | The current latitude for the user to be tracked|
| Current Location - Longitude | The current longitude for the user.|
| Date of First Session        | The date of the first session of the user.|
| Date of Last Session         | The date of the last session of the user.|
| Date of Birth                | The date of birth for the user.|
| Email Address                | The email address for the user.|
| Email Subscription Status    | The email subscription status for the user.|
| Facebook                     | The hash containing any of `id` (string), `likes` (array of strings), `num_friends` (integer).|
| First Name                   | The first name of the user.|
| Gender                       | The gender of the user. `M`, `F`, `O` (other), `N` (not applicable), `P` (prefer not to say), or nil (unknown).|
| Home City                    | The home city for the user.|
| Image URL                    | The URL of an image to be associated with user profile.|
| Language                     | The language preference of the user in ISO 639-1 format. For more information, see [Braze: List of accepted language codes](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/language_codes/).|
| Last Name                    | The last name of the user.|
| Marked Email As Spam At      | Date at which the user’s email was marked as spam. Appears in ISO 8601 format or in `yyyy-MM-dd’T’HH:mm:ss:SSSZ` format.|
| Phone Number                 | The telephone number of the user.|
| Push Subscription Status     | Set to `opt_in` (explicitly registered to receive push messages), `unsubscribed` (explicitly opted out of push messages), or `subscribed` (neither opted in nor out).|
| Push Tokens ID Array         | An array of app ID&#39;s to use with push token migration. For more information, see [Braze API: Migration via API](https://www.braze.com/docs/help/help_articles/push/push_token_migration/#migration-via-api).|
| Push Tokens Array            | An array of push tokens.|
| Push Tokens Device ID Array  | An array of device ID&#39;s to use with push token migration. For more information, see [Braze API: Migration via API](https://www.braze.com/docs/help/help_articles/push/push_token_migration/#migration-via-api).     |
| Time Zone                    | The time zone name from [IANA Time Zone Database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). Example: `America/New_York` or `Eastern Time (US &amp; Canada)`. Invalid time zone values are ignored. |
| Twitter                      | Hash containing any of ID (integer), screen name (string, X handle), followers count (integer), friends count (integer), and statuses count (integer).|
| Update Existing Only (Users) | Set to `true` or `false`. If no user value exists, one is created by default. If set to **true**, only existing users are updated and new users are not created.|

#### Modify User Attributes

Modify numeric user attributes with the following operations:

* Increment (accepts positive or negative values)
* Decrement
* Add

Modify array attributes by adding or removing values from existing arrays.

#### Events

An event name must be mapped to **Name**.

Map array attributes of equal length to send multiple events. Single value attributes can be used and will apply to each event.

| **Parameter** | **Description** |
|:--------------|:----------------|
| App ID | The App Identifier API key or `app_id` associated with a specific app in your app group. For more information, see [Braze API: App Identifier API key](https://www.braze.com/docs/api/api_key/#the-app-identifier-api-key). |
| Name | (Required) The name of the event.|
| Time | The time of the event. Automatically set to `now` unless a value is mapped.|
| Update Existing Only (Events) | Set to **true** or **false**. If no event value exists, one is created by default. If set to **true**, only existing events are updated and no new events are created|

#### Event Template Variables

Provide template variables as data input. For more information, see .

Name nested template variables with the dot notation (Example: `items.name`).

Nested template variables are typically built from data layer list attributes.

#### Event Templates

Provide templates to be referenced in Body Data. For more information, see .

Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.

#### Purchases

To map data for purchases, you must map the values for Product ID, Currency, and Price. Map array attributes of equal length to send multiple events. Single value attributes can be used and will apply to each event.

The following code sample shows a Braze best practice example for receiving a single event containing purchases for multiple products:

```json
// event to Tealium:
{
  [...]
  &#34;tealium_event&#34;: &#34;purchase&#34;,
  &#34;product_name&#34;: [&#34;Backpack&#34;, &#34;Pencil&#34;, &#34;Notebook&#34;],
  &#34;product_quantity&#34;: [1, 5, 3],
  &#34;product_category&#34;: [&#34;Travel&#34;, &#34;Office&#34;, &#34;Office&#34;],
  &#34;product_price&#34;: [39.95, 1.99, 3.99],
  &#34;order_currency&#34;: &#34;USD&#34;
}
```

Map the corresponding product array attributes to the Braze parameters:

* `product_name` &amp;gt; Product ID
* `product_quantity` &amp;gt; Quantity
* `product_price` &amp;gt; Price

The results of this example sends the following purchases object to Braze, representing each product accordingly:

```json
// payload to Braze through Tealium Connector:
{
  &#34;purchases&#34;: [
    {
      &#34;external_id&#34; : &#34;user1&#34;,
      &#34;app_id&#34; : &#34;11ae5b4b-2445-4440-a04f-bf537764c9ad&#34;,
      &#34;product_id&#34; : &#34;Backpack&#34;,
      &#34;currency&#34; : &#34;USD&#34;,
      &#34;price&#34; : 39.95,
      &#34;time&#34; : &#34;2013-07-16T19:20:30&#43;01:00&#34;,
    },
    {
      &#34;external_id&#34; : &#34;user1&#34;,
      &#34;app_id&#34; : &#34;11ae5b4b-2445-4440-a04f-bf537764c9ad&#34;,
      &#34;product_id&#34; : &#34;Pencil&#34;,
      &#34;currency&#34; : &#34;USD&#34;,
      &#34;price&#34; : 1.99,
      &#34;time&#34; : &#34;2013-07-16T19:20:30&#43;01:00&#34;,
    },
    {
      &#34;external_id&#34; : &#34;user1&#34;,
      &#34;app_id&#34; : &#34;11ae5b4b-2445-4440-a04f-bf537764c9ad&#34;,
      &#34;product_id&#34; : &#34;Backpack&#34;,
      &#34;currency&#34; : &#34;USD&#34;,
      &#34;price&#34; : 3.99,
      &#34;time&#34; : &#34;2013-07-16T19:20:30&#43;01:00&#34;,
    }
  ]
}
```

| **Parameter**| **Description**|
|:-------------|:-----------------|
| App ID | The Event Application ID.|
| Product ID | An array of product IDs.&lt;br&gt; Required for purchase events.|
| Currency | The ISO 4217 alphabetic currency code of the purchase.&lt;br&gt; Required for purchase events.|
| Price | An array of product prices.&lt;br&gt; Required for purchase events.|
| Quantity | An array of product quantities.|
| Purchase Time | The time of the purchase in ISO 8601 format. Automatically set to `now` unless explicitly mapped.|
| Update Existing Only (Purchases) | (Optional) Values are `true` or `false`. By default, if a purchase value exists, one is created by default. If set to `true`, only existing purchases are updated and no new purchases are created. |

#### Purchase Template Variables

Provide template variables as data input. For more information, see .

Name nested template variables with the dot notation (Example: `items.name`).

Nested template variables are typically built from data layer list attributes.

#### Purchase Templates

Define a template to send nested objects.

When a template is defined, the mappings from the **Purchases** section are ignored.

Provide templates to be referenced in Body Data. For more information, see .

Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.

### Delete User (Non-Batch)

Only one of External ID, Braze ID, and User Alias is needed in each action, but we recommend mapping as many attributes as you can. When IDs are mapped, the first non-blank value is selected based on the following priority order:

* External ID
* Braze ID
* Alias Name
* Alias Label

For more information, see [Braze API: User Delete Endpoint](https://www.braze.com/docs/api/endpoints/user_data/post_user_delete/).

#### Parameters

| **Parameter**    | **Description**|
|:-----------------|:---------------|
| External ID      | External ID of the user to delete.|
| Braze ID         | Braze ID of the user to delete.|
| User Alias Name  | The alias name of the user to be deleted. When specifying a user alias, Alias Name and Alias Label should both be set.  |
| User Alias Label | The alias label of the user to be deleted. When specifying a user alias, Alias Name and Alias Label should both be set. |
| Customer Email Address | The email address of the user. |
| Customer Phone Number | The phone number of the user in E.164 format. |
| Deletion Prioritization | Required if **Customer Email Address** is the parameter used to identify the user to delete. An array that lists the prioritization of the deletion request. Allowed values are `most_recently_updated` and either `identified` (users with an External ID) or `unidentified` (users without an External ID). |

### Update User Subscription Group Status (Non-Batch)

For more information, see [Braze API: Subscription Groups Endpoints](https://www.braze.com/docs/api/endpoints/subscription_groups/).

#### Parameters

| **Parameter**| **Description**|
|:-------------|:---------------|
| Group Type | (Required) The subscription group type to manage (`SMS` or `EMAIL`).|
| Update Type | (Required) The subscription state to set (`SUBSCRIBE` or `UNSUBSCRIBE`).|
| Subscription Group ID  | (Required) The ID of the subscription group.|
| External ID | The external ID of the user or users.|
| Email | (Used with EMAIL subscription groups.)&lt;br&gt; The email address of the user.&lt;br&gt; Email is required if External ID is not set for an `EMAIL` group.|
| Phone | (Used with SMS subscription groups.)&lt;br&gt; The phone number in E.164 format.&lt;br&gt; Example: `&#43;1415555371`&lt;br&gt; Phone is required if External ID is not set for an `SMS` group. |

### Update User Subscription Group Status Across Multiple Subscription Groups (Non-Batch)

#### Parameters

| **Parameter** | **Description** |
|:--------------|:----------------|
| Group Type | (Required) The subscription group type to manage (`SMS`, `EMAIL`, or  both `SMS` and `EMAIL`).|
| Update Type | (Required) The subscription state to set (`SUBSCRIBE` or `UNSUBSCRIBE`).  |
| Subscription Group ID  | (Required) The ID of the subscription groups. Map array type attributes to update the user&#39;s status in multiple subscription groups at the same time.|
| External ID | The external ID of the user.&lt;br&gt; External ID is required if Email is not set.|
| Email | (Used with EMAIL subscription groups.)&lt;br&gt; The email address of the user.&lt;br&gt; Email is required if External ID is not set for an `EMAIL` group.|
| Phone | (Used with SMS subscription groups.)&lt;br&gt; The phone number in E.164 format.&lt;br&gt; Example: `&#43;1415555371`&lt;br&gt; Phone is required if External ID is not set for an `SMS` group. |

### Send Campaign Message

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Campaign ID | (Required) The campaign ID. |
| Send ID | Key either generated by Braze or created by you for a given message send under which the analytics should be tracked. |
| Alias Name | The value of the alias. |
| Alias Label | The key of the alias. |
| External User ID | A value used to identify the same user profile across multiple devices. |
| Send to Existing Only | The default value is `true`. If `false`, an attributes object must also be included. |
| Trigger Properties | Personalization key-value pairs that can be referenced in your message template.&lt;br&gt;Use templating for nested objects. |
| Recipient Attributes | Create or update a recipient attribute. |
| Template Variables | Provide template variables as data input for &lt;b&gt;Templates&lt;/b&gt;.&lt;br&gt;For more information and usage examples, see .&lt;br&gt;Name nested template variables with the dot notation. Example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Trigger Properties. For more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Send Canvas Message

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Canvas Data | &lt;b&gt;Canvas ID&lt;/b&gt; - Random key generated by Braze for a given Canvas within the Braze dashboard. |
| Alias Name | The alias value. |
| Alias Label | The alias key. |
| External User ID | A value used to identify the same user profile across multiple devices. |
| Send to Existing Only | The default value is `true`. If `false`, an attributes object must also be included. |
| Trigger Properties | Personalization key-value pairs that can be referenced in your message template.&lt;br&gt;Use templating for nested objects. |
| Recipient Attributes | Create or update a recipient attribute. |
| Canvas Entry Properties | Personalization key-value pairs that can be referenced in your message template.&lt;br&gt;Use templating for nested objects. |
| Template Variables | Provide template variables as data input for &lt;b&gt;Templates&lt;/b&gt;.&lt;br&gt;For more information and usage examples, see .&lt;br&gt;Name nested template variables with the dot notation. Example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Trigger Properties. For more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Send Transactional Email

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Campaign ID | (Required) The campaign ID. |
| External Send ID | Identifier for a particular send. When passed, this identifier will also be used as a deduplication key, which Braze will store for 24 hours. |
| Alias Name | The alias value. |
| Alias Label | The alias key. |
| External User ID | A value used to identify the same user profile across multiple devices. |
| Trigger Properties | Personalization key-value pairs that can be referenced in your message template.&lt;br&gt;Use templating for nested objects. |
| Recipient Attributes | Create or update a recipient attribute. |
| Template Variables | Provide template variables as data input for &lt;b&gt;Templates&lt;/b&gt;.&lt;br&gt;For more information and usage examples, see .&lt;br&gt;Name nested template variables with the dot notation. Example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Trigger Properties. For more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Identify User

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| External ID | Select an attribute to map to an external ID in Braze. |
| Alias Name | (Required) The alias name. |
| Alias Label | (Required) The alias label. |

## Frequently Asked Questions

### How does this connector work with other Braze integrations?

In addition to the Track User API, Braze has additional data collection methods, both of which support mapping of user attributes in Braze. Tealium supports Braze SDKs for Web and Native Mobile in the following two independent, but similar integrations:

* [Braze Web SDK Tag Setup](), [Braze Initial SDK Setup](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)
* Tealium Remote Command for Braze on Android and iOS/Swift ([Learn more](https://docs.tealium.com/platforms/remote-commands/integrations/braze/))

These integrations are alternative methods used for Braze to collect user behavior data that is similar to the data collected in the event and purchase actions of the connector.
