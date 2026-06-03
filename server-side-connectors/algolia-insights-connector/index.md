---
title: Algolia Insights Connector Setup Guide
description: This article describes how to set up the Algolia Insights connector.
url: https://docs.tealium.com/server-side-connectors/algolia-insights-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Algolia Insights API
* API Version: v1
* API Endpoint: `https://insights.algolia.io/1/events`
* Documentation: [Algolia Insights API](https://www.algolia.com/doc/rest-api/insights/)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 5 minutes
* Max size of requests: 2 MB

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Events (Real-Time) | ✗ | ✓ |
| Send Events (Batched) | ✗ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **API Key**  
(Required) Your API key with search [access control list](https://www.algolia.com/doc/guides/security/api-keys/#access-control-list-acl) permission.
* **Application ID**  
(Required) Your Algolia application ID.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Events (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The event type: `click`, `conversion`, or `view`.|

#### Event Parameters

 Event should include one or more **Object IDs** on one or more **Filters**, and a single event must not include both **Object IDs** and **Filters**. 

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) Name of the specific event. The format must be 1-64 ASCII characters, except control characters. To maximize the impact of your events, you should use consistent event names and consistent formatting. |
| Value | The monetary value of the event, measured in currency. For example, the total value of a purchase. |
| Currency | If you include pricing information in the `objectData` parameter or provide value, you must also specify the currency as ISO 4217 currency code, such as `USD` or `EUR`. |
| Index | (Required) Index name. Events are related to items from an Algolia index. The format must be the same as the index name used by the search engine.|
| User Token | (Required) Pseudonymous or anonymous user identifier. Never include personal identifiable information in user tokens. |
| Timestamp | The time of the event in milliseconds in Unix epoch time. By default, the Algolia Insights API uses the time it receives an event as its timestamp. If this field is not mapped, it will be initialized with the current timestamp. The Algolia Insights API accepts events from up to 4 days in the past. &lt;ul&gt;&lt;li&gt;For sending events not in real time (for example, a backend search), ensure you set the correct timestamp.&lt;/li&gt;&lt;li&gt; For batched events, if you do not include a timestamp, all events will have the same timestamp. &lt;/li&gt; &lt;li&gt;Timestamps for click and conversion events must be within 1 hour of the corresponding search or browse request.&lt;/li&gt;&lt;/ul&gt; |
| Query ID | A unique identifier for a search query. A `queryID` is required for events related to search or browse requests. |
| Object IDs | An array of object identifiers for items of an Algolia index. You can include up to 20 object IDs. |
| Filters | An array of facet filters in the following format: `${attribute}:${value}`. For example, `brand:apple`. You can include up to 10 filters. |
| Positions | The position of the clicked objects in the search results. This property is required for click events with **Query ID**. You must provide one position for each **Object ID**. Algolia uses this parameter to calculate the average click position. The position is absolute, and not relative, to any results page. |
| Event Subtype | The subtype of the event. For conversion events, the value is either `addToCart` or `purchase`. For all other events, omit this value. |

#### Object Data

| **Parameter** | **Description** |
| --- | --- |
| Query ID | The ID of the query associated with this particular record. Used to track purchase events with multiple items originating from different searches. |
| Price | The price of the item. This should be the final price, inclusive of any discounts in effect. |
| Discount | Absolute value of the discount in effect for this object, measured in currency. |
| Quantity | The quantity of the purchased or added-to-cart item. The total value of a purchase is the sum of quantity multiplied with the price for each purchased item. |

### Send Events (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The event type: `click`, `conversion`, or `view`.|

#### Event Parameters

 Event should include one or more **Object IDs** on one or more **Filters**, and a single event must not include both **Object IDs** and **Filters**. 

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) Name of the specific event. The format must be 1-64 ASCII characters, except control characters. To maximize the impact of your events, you should use consistent event names and consistent formatting. |
| Value | The monetary value of the event, measured in currency. For example, the total value of a purchase. |
| Currency | If you include pricing information in the `objectData` parameter or provide value, you must also specify the currency as ISO 4217 currency code, such as `USD` or `EUR`. |
| Index | (Required) Index name. Events are related to items from an Algolia index. The format must be the same as the index name used by the search engine.|
| User Token | (Required) Pseudonymous or anonymous user identifier. Never include personal identifiable information in user tokens. |
| Timestamp | The time of the event in milliseconds in Unix epoch time. By default, the Algolia Insights API uses the time it receives an event as its timestamp. If this field is not mapped, it will be initialized with the current timestamp. The Algolia Insights API accepts events from up to 4 days in the past. &lt;ul&gt;&lt;li&gt;For sending events not in real time (for example, a backend search), ensure you set the correct timestamp.&lt;/li&gt;&lt;li&gt; For batched events, if you do not include a timestamp, all events will have the same timestamp. &lt;/li&gt; &lt;li&gt;Timestamps for click and conversion events must be within 1 hour of the corresponding search or browse request.&lt;/li&gt;&lt;/ul&gt; |
| Query ID | A unique identifier for a search query. A `queryID` is required for events related to search or browse requests. |
| Object IDs | An array of object identifiers for items of an Algolia index. You can include up to 20 object IDs. |
| Filters | An array of facet filters in the following format: `${attribute}:${value}`. For example, `brand:apple`. You can include up to 10 filters. |
| Positions | The position of the clicked objects in the search results. This property is required for click events with **Query ID**. You must provide one position for each **Object ID**. Algolia uses this parameter to calculate the average click position. The position is absolute, and not relative, to any results page. |
| Event Subtype | The subtype of the event. For conversion events, the value is either `addToCart` or `purchase`. For all other events, omit this value. |

#### Object Data

| **Parameter** | **Description** |
| --- | --- |
| Query ID | The ID of the query that this specific record is attributable to. Used to track purchase events with multiple items originating from different searches. |
| Price | The price of the item. This should be the final price, inclusive of any discounts in effect. |
| Discount | Absolute value of the discount in effect for this object, measured in currency. |
| Quantity | The quantity of the purchased or added-to-cart item. The total value of a purchase is the sum of quantity multiplied with the price for each purchased item. |