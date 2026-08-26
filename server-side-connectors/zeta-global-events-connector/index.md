---
title: Zeta Global Events Connector Setup Guide
description: Set up the Zeta Global Events connector to send behavioral events from Tealium EventStream to Zeta's Track Event REST API.
url: https://docs.tealium.com/server-side-connectors/zeta-global-events-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Zeta Global API
* API Version: ver2
* API Endpoint: `https://api.zetaglobal.net/`
* Documentation: [Zeta Global API](https://docs.zetaglobal.com/reference/track-an-event-rest)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Access Token**: Your ZMP (Zeta Marketing Platform) Access Token. The connector sends this value as the password of the HTTP Basic Authorization header. The username is fixed to `api`.
* **Site ID**: Your ZMP Site ID. The connector uses this value in a `POST` request to `https://api.zetaglobal.net/ver2/{site_id}/activities`.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Track Event | ✗ | ✓ |
| Track Events (Batch) | ✗ | ✓ |
| Track Event with Identify | ✗ | ✓ |

### Track Event

#### Activity data

Map Tealium attributes to the top-level fields of `activity`.

| Parameter | Description |
| --- | --- |
| Event | (Required) The name of the event. The event name must match the event naming configured in ZMP. |
| Timestamp | The time of the event in ISO-8601 format, for example `2026-08-07T15:56:00Z`. Epoch milliseconds are rejected with a 422 Invalid date format error. If unmapped, Zeta stamps its own server time. |

#### Subscriber data

Map Tealium attributes to `activity.subscriber` fields for the person associated with the event.

| Parameter | Description |
| --- | --- |
| UID | (Required) The unique identifier of the person, sent as `activity.subscriber.uid`. The UID must be stable across events for Zeta to resolve them to one profile. |
| Unique Client ID Name | The identifier type for a `subscriber.unique_client_id` entry. Map together with **Unique Client ID Value**. The identifier type must be registered in ZMP before use. An unregistered name is accepted with a 202 and silently discarded. |
| Unique Client ID Value | The identifier value for a `subscriber.unique_client_id` entry. Map together with **Unique Client ID Name**. |

This action does not set `identify_person`, so subscriber name fields and contacts are not available here. To map subscriber name fields and contacts, use the Track Event with Identify action.

#### Properties data

Optional. Map Tealium attributes to keys in `activity.properties`.

| Parameter | Description |
| --- | --- |
| Order ID | The order identifier, mapped to `properties.order_id`. |
| Item ID | The item identifier, mapped to `properties.items[].id`. |
| Item SKU | The item SKU, mapped to `properties.items[].sku`. |
| Item Resource Type | The item resource type, mapped to `properties.items[].resourceType`. The default is `product`. |
| Item Price | The item price, mapped to `properties.items[].price`. |
| Item Quantity | The item quantity, mapped to `properties.items[].quantity`. |
| Item Product Name | The product name, mapped to `properties.items[].productname`. |
| Item Category | The item category, mapped to `properties.items[].category`. |
| Item Subcategory | The item subcategory, mapped to `properties.items[].subcategory`. |
| Item Size | The item size, mapped to `properties.items[].size`. |
| Item URL | The item URL, mapped to `properties.items[].url`. |
| Disable E-commerce Automapping | By default, Tealium e-commerce variables (`_corder`, `_cprod`, `_csku`, `_cprice`, `_cquan`, `_cprodname`, `_ccat`, `_ccat2`, `dom.url`) are automatically mapped into `activity.properties`. Select this checkbox to disable e-commerce automapping. Explicit Properties Data mappings always take precedence over automapping. |

The Item fields (**Item ID** through **Item URL**) are combined by index position to build each item object in `properties.items[]`. Each Item attribute must resolve to an array, and all arrays must be the same length.

The connector places any custom key you add under `activity.properties`.

**Templates**

Use templates to build nested JSON structures that a flat key-to-attribute mapping cannot express.

| Parameter | Description |
| --- | --- |
| Template — nested value | Map a template to a custom key to nest its rendered JSON (object, array, or scalar) under that key in `properties`. |
| Template — Items list | Map a template that renders a JSON array of item objects to the **Items** option to set the whole `properties.items[]` list at once, using Zeta item field names (`id`, `sku`, `resourceType`, `price`, `quantity`, `productname`, `category`, `subcategory`, `size`, `url`). A mapped Items list template replaces the individual Item field mappings. Both a mapped Items list and individual Item field mappings take precedence over e-commerce automapping. Automapping only fills `items[]` when no items are mapped explicitly. |

### Track Events (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

The activity data, subscriber data, and properties data configuration for this action is identical to [Track Event](#track-event).

This batch action does not set `identify_person`, so subscriber name fields and contacts are not available here. To map subscriber name fields and contacts, use the Track Event with Identify action.

### Track Event with Identify

#### Activity data

Map Tealium attributes to the top-level fields of `activity`.

| Parameter | Description |
| --- | --- |
| Event | (Required) The name of the event. The event name must match the event naming configured in ZMP. |
| Timestamp | The time of the event in ISO-8601 format, for example `2026-08-07T15:56:00Z`. Epoch milliseconds are rejected with a 422 Invalid date format error. If unmapped, Zeta stamps its own server time. |

#### Subscriber data

Map Tealium attributes to `activity.subscriber` fields for the person associated with the event.

| Parameter | Description |
| --- | --- |
| UID | (Required) The unique identifier of the person, sent as `activity.subscriber.uid`. The UID must be stable across events for Zeta to resolve them to one profile. |
| Unique Client ID Name | The identifier type for an entry in the `unique_client_ids` list. Map together with **Unique Client ID Value**. Up to 25 identifier pairs per call. The identifier type must be registered in ZMP before use. An unregistered name is accepted with a 202 and silently discarded. |
| Unique Client ID Value | The identifier value for an entry in the `unique_client_ids` list. Map together with **Unique Client ID Name**. |
| First Name | The first name of the person. Persisted on the profile because this action sets `identify_person`. |
| Last Name | The last name of the person. Persisted on the profile because this action sets `identify_person`. |
| Name | The full name of the person. Persisted on the profile because this action sets `identify_person`. |

#### Contacts data

Optional. Map Tealium attributes to the fields of `subscriber.contacts[]` to attach an email or phone channel to the profile.


<blockquote>
Zeta associates contacts on new profiles only. An existing profile ignores the Contacts Data section.
</blockquote>


| Parameter | Description |
| --- | --- |
| Contact Value | (Required) The email address or phone number of the contact. Required whenever any other Contact field is mapped. |
| Contact Type | The type of contact: `email` or `phone`. The default is `email`. |
| Preferences | The contact preference, for example `standard` or `billing`. The default is `standard`. Additional preferences can be configured in ZMP. |
| Subscription Status | The subscription status: `new`, `active`, `inactive`, or blank. The default is `active`. A blank or null value retains the current status for an existing contact, or sets `new` for a new contact. The `new` status is retained until the contact is messaged. |
| Force Active | When creating a contact, select this to bypass the default `new` status. |
| Inactivity Reason | The reason an inactive contact is inactive, for example `unsubscribed`. |
| Double Opt In Status | The double opt-in status: `single` or `double`. |
| Phone Type | The phone type: `mobile` or `landline`. Applies to phone contacts only. |
| Last Clicked | The timestamp of the last message click, in ISO-8601 format. |
| Last Opened | The timestamp of the last message open, in ISO-8601 format. |
| Last Sent | The timestamp of the last message sent, in ISO-8601 format. |
| Signed Up At | The date the contact signed up, in ISO-8601 format, for example `2015-01-02T05:30:21Z`. The default is the created date. |

The connector writes any custom key you add into the `contact_properties` object for the contact.

**Templates**

Use templates to build nested JSON structures that a flat key-to-attribute mapping cannot express.

| Parameter | Description |
| --- | --- |
| Template — nested value | Map a template to a custom key to nest its rendered JSON under that key in `contact_properties`. |
| Template — Contacts list | Map a template that renders a JSON array of contact objects to the **Contacts** option to set the whole `subscriber.contacts[]` list at once, using Zeta's contact field names. A mapped Contacts list template replaces the individual contact-field mappings. |

#### Properties data

Optional. Map Tealium attributes to keys in `activity.properties`.

| Parameter | Description |
| --- | --- |
| Order ID | The order identifier, mapped to `properties.order_id`. |
| Item ID | The item identifier, mapped to `properties.items[].id`. |
| Item SKU | The item SKU, mapped to `properties.items[].sku`. |
| Item Resource Type | The item resource type, mapped to `properties.items[].resourceType`. The default is `product`. |
| Item Price | The item price, mapped to `properties.items[].price`. |
| Item Quantity | The item quantity, mapped to `properties.items[].quantity`. |
| Item Product Name | The product name, mapped to `properties.items[].productname`. |
| Item Category | The item category, mapped to `properties.items[].category`. |
| Item Subcategory | The item subcategory, mapped to `properties.items[].subcategory`. |
| Item Size | The item size, mapped to `properties.items[].size`. |
| Item URL | The item URL, mapped to `properties.items[].url`. |
| Disable E-commerce Automapping | By default, Tealium e-commerce variables (`_corder`, `_cprod`, `_csku`, `_cprice`, `_cquan`, `_cprodname`, `_ccat`, `_ccat2`, `dom.url`) are automatically mapped into `activity.properties`. Select this checkbox to disable e-commerce automapping. Explicit Properties Data mappings always take precedence over automapping. |

The Item fields (**Item ID** through **Item URL**) are combined by index position to build each item object in `properties.items[]`. Each Item attribute must resolve to an array, and all arrays must be the same length.

The connector places any custom key you add under `activity.properties`.

**Templates**

Use templates to build nested JSON structures that a flat key-to-attribute mapping cannot express.

| Parameter | Description |
| --- | --- |
| Template — nested value | Map a template to a custom key to nest its rendered JSON (object, array, or scalar) under that key in `properties`. |
| Template — Items list | Map a template that renders a JSON array of item objects to the **Items** option to set the whole `properties.items[]` list at once, using Zeta item field names (`id`, `sku`, `resourceType`, `price`, `quantity`, `productname`, `category`, `subcategory`, `size`, `url`). A mapped Items list template replaces the individual Item field mappings. Both a mapped Items list and individual Item field mappings take precedence over e-commerce automapping. Automapping only fills `items[]` when no items are mapped explicitly. |
