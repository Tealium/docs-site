---
title: Tealium + Google Analytics 4 Measurement Protocol Integration Guide
description: This article describes how to configure and use the Google Analytics 4 Measurement Protocol Tag and Connector together with Tealium.
url: https://docs.tealium.com/partners-and-industries/tech-partners/google-analytics-4-measurement-protocol-connector-integration-guide/
---
## How it works

The [Google Analytics 4 Measurement Protocol Connector](https://docs.tealium.com/google-analytics-4-measurement-protocol-connector/) allows developers to make HTTP requests that send events directly to Google Analytics servers. This helps developers measure how users interact with their business from any HTTP-enabled environment, which makes it easy to measure interactions that happen server-to-server.

Tealium EventStream acts as a conduit to enable Google Analytics 4 tracking. It ties together support for Mobile, Internet of Things, and Offline Event and pageview tracking by:

* Tracking both web applications and apps.
* Tying online to offline behavior.
* Measuring interactions both client-side and server-side.
* Sending events that happen outside standard user interaction, such as offline conversations.

![](https://docs.tealium.com/images/server-side-connectors/googleanalytics4measurementprotocoldiagram.png)

Tealium supports the following actions with the Google Analytics 4 Measurement Protocol Connector:

* Send PageView Event
* Send Event
* Send Firebase Event

For additional configuration details for the Google Analytics 4 Tag that appears in the diagram, see [Google Analytics 4 (GA4) Tag Setup Guide](https://docs.tealium.com/google-analytics-4-ga4-tag/).

### Considerations


<blockquote>
The Google Analytics Measurement Protocol for Google Analytics 4 connector is not a complete replacement for the client-side tag solution.
</blockquote>


### Limitations

* If any session or user data is needed, the client-side tag is required.
* The `user_id` key requires both client-side and Measurement Protocol events to include the `user_id`.
* Session data is not supported by the current iteration of the GA4 Measurement Protocol API. To obtain automatic Google Analytics session data, you must use the Google Analytics 4 (GA4) Tag.
  * When you enable the tag, the `session_start` and `first_visit` events are also sent.
* Parameter values are limited to 100 characters. Values that exceed 100 characters are either truncated or dropped from the final GA4 reports.
* Does not support `utm` parameters.
* Does not support sending campaign and traffic source data.
* Does not contain geographic data and the user agent.

## Authentication

The Measurement Protocol API uses a measurement ID and API secret that are included in the URL as query parameters.

```
https://google-analytics.com/mp/collect?measurement_id=G-1234567890&api_secret=xxxxxxxxxx
```

## Configuration

To configure the connector, enter the API Secret and either the Measurement ID or Firebase ID for the data stream.

## Response/Debugging

The Measurement Protocol always returns a `2xx` status code if the HTTP request was received. The Measurement Protocol does not return an error code if the payload data was malformed, or if the data in the payload was incorrect or was not processed by Google Analytics.

Google supplies a separate endpoint for validating events:

```
https://google-analytics.com/debug/mp/collect?
```

The Tealium Measurement Protocol connector uses this endpoint during Trace, which displays the validation process of the event data.

### Recommendations and configuration details

To mitigate issues around the noted limitations and fully cover all data requirements, implement the [Google Analytics 4 tag](https://docs.tealium.com/google-analytics-4-ga4-tag/) in Tealium iQ Tag Management. Set the tag to load on all pages, with **Send Page View** set to `false`. In addition, add the Google Analytics Cookie Matching Service tag so that the Google `clientId` is automatically added as a `utag_main__ga` cookie value.

All required events outside of Google’s automatically collected events can then be configured in the Google Analytics connector in Tealium EventStream.

The Google Analytics 4 tag automatically triggers a purchase event when `order_id `is present through the E-commerce extension mappings. If you have the E-commerce extension enabled and want to track purchases through EventStream, configure a [Set Data Values](https://docs.tealium.com/set-data-values-extension/) extension scoped to Google Analytics 4 to clear the `_corder` attribute.

![](https://docs.tealium.com/images/server-side-connectors/googleanalytics4measurementprotocolsetdatavalues.png)

Because Tealium can support a client-side implementation to better address web-client integrations, as well as supporting mobile and offline events through Tealium’s EventStream, Tealium can integrate with both solutions and create a combined approach.

For more information for configuration of a client-side tag, see [Google Analytics 4 (GA4) Tag Setup Guide](https://docs.tealium.com/google-analytics-4-ga4-tag/).

### Prerequisites

| PRODUCT |  REQUIRED | 
| --- | --- |
| Google Analytics 4 account| 	✓| 
| Tealium EventStream / AudienceStream	| ✓| 
| Tealium iQ Tag Management	|   Optional, but preferred| 

### Authentication

| VALUE	 | DESCRIPTION	| LOCATION |
| ---| ---| --- | 
| API Secret (Required)	| An API Secret generated in the Google Analytics UI.| 	To create a new secret, navigate to: **Admin** > **Data Streams** > **choose your stream** > **Measurement Protocol** > **Additional Settings** > **Measurement Protocol API secrets**.| 
| Measurement ID (Optional)	| The measurement ID associated with a stream.	| In the Google Analytics UI, navigate to: **Admin** > **Data Streams** > **choose your stream** > **Measurement ID** > **Create**.| 
| Firebase App ID (Optional)| The identifier for a Firebase app.| 	In the Firebase console, navigate to: **Project Settings** > **General** > **Your Apps** > **App ID**. |

API Version: Beta

### Event Parameters

| PARAMETER	| DESCRIPTION| 
| ---| ---|
| Page Title	| The title of the page.| 
| Page Location 	| (Required) The full URL to the page.| 
| User Properties	| User properties describe segments of the user base, such as language preference or geographic location. You can configure these into the section **Templates**.| 
| Item ID	| Either Item ID or Item Name is required.| 
| Item Name| 	Either Item ID or Item Name is required.| 
| Affiliation	 |  A product affiliation to designate a supplying company or physical store location. Event-level and item-level affiliation parameters are independent.| 
| Coupon	| The coupon name or code associated with the item. Event-level and item-level coupon parameters are independent.|
|  Currency	 |  The currency, in 3-letter ISO 4217 format. If set, event-level currency is ignored. Multiple currencies in an event are not supported, so all entries will contain the same currency value. | 
| Discount (number)	| The monetary discount value associated with the item.| 
| Index (number)	| The index or position of the item in the list.| 
| Item Brand	| The brand of the item.| 
| Item Category	| The category of the item. If used as part of a category hierarchy or taxonomy, then this is the first category.| 
| Item Category 2	| The second category hierarchy or additional taxonomy for the item.| 
| Item Category 3	| The third category hierarchy or additional taxonomy for the item.| 
| Item Category 4	| The fourth category hierarchy or additional taxonomy for the item.| 
| Item Category 5	| The fifth category hierarchy or additional taxonomy for the item.| 
| Item List ID	| The ID of the list in which the item was presented to the user. <ul><li>If set, event-level `item_list_id` is ignored.</li><li>If not set, event-level `item_list_id` is used (if present).</li></ul>| 
| Item List Name	| The name of the list in which the item was presented to the user. <ul><li>If set, event-level `item_list_name` is ignored. </li><li>If not set, event-level `item_list_name` is used (if present). </li></ul>|
| Item Variant	| The item variant or unique code or description for additional item details or options.|
| Location ID	| The location associated with the item. It's recommended that you use the Google Place ID that corresponds to the associated item. A custom location ID can also be used.  <ul><li>If set, event-level `location_id` is ignored.</li> <li>If not set, event-level `location_id` is used (if present).</li></ul>|
| Price (number)	|The monetary price of the item, in units of the specified currency parameter.|
|Quantity (number)	|Item quantity.|
|Template Variables	|Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes.|
|Templates	| Provide templates to be referenced in User Properties. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

## Send PageView Event

### Overview

This action is used to pass website page view events to Google Analytics.

### Body Parameters

| PARAMETER	| DESCRIPTION |
| ---| ---|
|Client ID	| (Required) A unique identifier for a client.<br><br> This identifier must use the Client ID set by the Google Analytics 4 tag. For more information, see [Google Analytics 4 (GA4) Tag Setup Guide](https://docs.tealium.com/google-analytics-4-ga4-tag/).|
|Measurement ID Override|	Measurement ID. For example, the identifier for a Data Stream.|
|Firebase App ID Override |	(Required) The identifier for a Firebase app. This setting overrides Firebase App ID used in the **Configuration** section.|
|User ID|	A unique identifier for a user. If you include `user_id` in your Google Analytics 4 Measurement Protocol events, you must also include it in the client-side events.|
|Timestamp Micros	|A Unix timestamp (in microseconds) for the time to associate with the event. Set this to record events that happened in the past. This value can be overridden through `user_property` or event timestamps. Events can be backdated up to three calendar days based on the property’s timezone.|
|Non Personalized Ads|	Set this to true to indicate these events are not used for personalized ads.|

### Event Parameters

|PARAMETER|	DESCRIPTION|
| ---| ---|
|Page Title|	The title of the page.
|Page Location|	(Required) The full URL to the page.|

Additional parameters can be passed, but they are not required to allow tracking of the page view event.

#### Google Payload

As shown in the following example payload, the `events.name` value is `page_view`, and required parameters are `page_location` and `client_id`:

```json
{
  "events": [
    {
      "name": "page_view",
      "params": {
        "page_location": "http://demosite.com/ecomm/category.html",
        ...other mapped parameters...
      }
    }
  ],
  "client_id": "017f6ae7e7a40014b19d17739b3d05079002707100fb8"
}
```

## Send Event

### Overview

This action is used to send a non-pageview event to Google Analytics. You can select the event type from a list of Google-defined events (for more information, see [Measurement Protocol (Google Analytics 4) Events](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference/events)). In addition, you can select a Custom Event and then map the custom event value to **Custom Event Type**.

### Body Parameters

|PARAMETER|	DESCRIPTION|
| ---| ---|
|Client ID	| (Required) A unique identifier for a client. The Client ID set by the Google Analytics 4 tag. The Cookie Matching Tag is the preferred implementation method.|
| Measurement ID Override|Measurement ID. For example, the identifier for a Data Stream.|
|Firebase App ID Override	| (Required) The identifier for a Firebase app. This setting overrides Firebase App ID used in the **Configuration** section.|
|User ID|	A unique identifier for a user. If you include `user_id` in your Google Analytics 4 Measurement Protocol events, you must also include it in the client-side events.|
|Timestamp Micros	|A Unix timestamp (in microseconds) for the time to associate with the event. Set this to record events that happened in the past. This value can be overridden through `user_property` or event timestamps. Events can be backdated up to three calendar days based on the property's timezone|
Non Personalized Ads	|Set this to true to indicate these events are not used for personalized ads.|

### Event and Event Parameters

In addition to the general event parameters listed previously, each event type accepts additional parameters. The following table lists required and optional parameters for each event type:

| EVENT TYPE	| DESCRIPTION| 	EVENT-SPECIFIC PARAMETERS| 
|-----|-----|-----|
| Add Payment Information	| When a user has submitted their payment information.	| Event Parameters: <ul><li>Currency (Required)</li><li>Value (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul> |
| Add Shipping Information	| When a user has submitted their shipping information.	| Event Parameters: <ul><li>Currency (Required)</li><li>Value (Required)</li><li>Coupon (Optional)</li><li>Shipping Tier (Optional)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul> |
| Add to Wishlist	| When an item was added to a wish list. Use this event to identify popular gift items in your app.	| Event Parameters:<ul><li>Currency (Required)</li><li>Value (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| Begin Checkout	| When a user has begun a checkout.	| Event Parameters:<ul><li>Currency (Required)</li><li>Value (Required)</li><li>Coupon (Optional)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul> | 
| Earn Virtual Currency| 	When a user has been awarded virtual currency. Log this event with `spend_virtual_currency` to better understand your virtual economy.	| Event Parameters:<ul><li>Virtual Currency Name (Optional) - The name of the virtual currency.</li><li>Value (Optional) - The value of the virtual currency.</li></ul>| 
| Generate Lead	| When a lead has been generated. Use this event to better understand the efficacy of your re-engagement campaigns.	| Event Parameters:<ul><li>Currency (Required)</li><li>Value (Required)</li></ul>| 
| Join Group	| When a user joins a group, such as a guild, team, or family. Use this event to analyze how popular certain groups or social features are.|Event Parameter:<ul><li>Group ID (Optional) - The ID of the group.</li></ul>| 
| Level Up	| When a player has leveled up. Use this event to measure the level distribution of your user base and identify levels that are difficult to complete.	| Event Parameters: <ul><li>Level (Optional) - The level of the character.</li><li>Character (Optional) - The character that leveled up.</li></ul>| 
| Login| 	When a user has logged in.	| Event Parameter:<ul><li>Method (Optional) - method used to log in.</li></ul>| 
| Post Score	| When a user posts a score. Use this event to understand how users are performing in your game and correlate high scores with audiences or behaviors.	| Event Parameters:<ul><li>score (Required) - score to post.</li><li>level (Optional) - level of the character.</li><li>character (Optional) - the character that leveled up.</li></ul>| 
| Purchase	| When one or more items have been purchased by a user.	| Event Parameters:<ul><li>Transaction ID (Required)</li><li>Value (Required)</li><li>Currency (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| Refund	| When a user was issued a refund.	| Event Parameters:<ul><li>Transaction_id (Required)</li><li>Value (Required)</li><li>Currency (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| Remove from Cart| 	When a user removed an item from a cart.	| Event Parameters:<ul><li>Currency (Required)</li><li>Value (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| Search| 	When a user performed a search. Use this event to help identify the most popular content in your app.	| Event Parameter:<ul><li>Search Term (Required)</li></ul>| 
| Select Content	| When a user selected content of a certain type. Use this event to identify popular content and categories of content in your app.|Event Parameter:<ul><li>Content Type (Optional)</li><li>Item ID (Optional)</li></ul>| 
| Select Item	| When a user selected an item from a list.	| Event Parameter:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| Select Promotion| 	When a user selected a promotion from a list.| Event Parameters:<ul><li>Creative Name (Optional)</li><li>Creative Slot (Optional)</li><li>Location ID (Optional)</li><li>Promotion ID (Optional)</li><li>Promotion Name (Optional)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| Share| 	When a user shared content.	| Event Parameters:<ul><li>Method (Optional)</li><li>Content Type (Optional)</li><li>Item ID (Optional)</li></ul>| 
| Sign up| 	When a user signs up for an account. Use this event to understand the difference between logged in and logged out users.| 	Event Parameter:<ul><li>Method (Optional)</li></ul>| 
| Spend Virtual Currency| 	When a user purchased virtual goods. Use this event to identify the most popular virtual goods.| Event Parameters:<ul><li>Value (Required)</li><li>Virtual Currency Name (Required)</li></ul>| 
| Tutorial Begin	| When a user started the on-boarding process. Use this in a funnel with `tutorial_complete` to measure how many users complete the tutorial.	| There are no required parameters for this event.| 
| Tutorial Complete	| When a user completed your on-boarding process. Use this in a funnel with `tutorial_begin` to measure how many users complete the tutorial.	| There are no required parameters for this event.| 
| Unlock Achievement| 	When a user unlocked an achievement. Use this event to better understand how users experience your game.	| Event Parameter:<ul><li>Achievement ID (Required)</li></ul>| 
| View Cart| 	When a user viewed their cart.	|Event Parameters:<ul><li>Currency (Required)</li><li>Value (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| View Item	| When a user viewed specific content. Use this event to identify the most popular viewed items.	| Event Parameters:<ul><li>Currency (Required)</li><li>Value (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| View Item List| 	When a user viewed a list of items of a certain category.	| Event Parameters:<ul><li>Item List ID (Required)</li><li>Item Name (Required)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| View Promotion	| When a user viewed a promotion from a list. | Event Parameters:<ul><li>creative name (Optional)</li><li>Creative Slot (Optional)</li><li>Location ID (Optional)</li><li>Promotion ID (Optional)</li><li>Promotion Name (Optional)</li></ul>Item Parameters:<ul><li>Item ID (Required)</li><li>Item Name (Required)</li></ul>| 
| View Search Results| 	When a user has been presented with search results.	| Event Parameter:<ul><li>Search Term (Optional)</li></ul>| 
| Custom Event	| Use this event to support custom events not defined by Google’s pre-set events.| 	There are no required parameters for this event.| 

To view a full list of supported events, see [Measurement Protocol - Google Analytics 4 events](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference/events.)

## Send Firebase Event

### Overview

This action is used to send a Firebase event to Google Analytics. The configuration is the same as Send Event, but you also need to supply an App Instance ID.

This connector action event type is primarily used to track Mobile Application data for passing to Firebase for analytics.

| PARAMETERS| 	DESCRIPTION| 
| --- |  --- | 
| App Instance ID | (Required) Uniquely identifies a specific installation of a Firebase app. This value can be retrieved through the Firebase SDK. |
| Firebase App ID Override| 	(Required) The identifier for a Firebase app. This setting overrides Firebase App ID used in the **Configuration** section.| 
| User ID (Optional)	| A unique identifier for a user.| 
| Timestamp Micros (Optional)| 	A Unix timestamp (in microseconds) for the time to associate with the event.| 
| Non Personalized Ads (Optional)| 	Set this to true to indicate these events are not used for personalized ads.| 

### Event Parameters

This action supports the same general event parameters as the Send Event action, and it also supports the same event-specific parameters.

### User Properties

User properties describe segments of your user base, such as language preference or geographic location. Analytics [automatically logs some user properties](https://support.google.com/analytics/answer/9268042). If you want to collect additional properties, you can set up to 25 additional user properties per project. Read [GA4 Custom dimensions](https://support.google.com/analytics/answer/9269570) and metrics and [Firebase Custom user properties](https://developers.google.com/analytics/devguides/collection/protocol/ga4/user-properties?client_type=firebase#example_usage) to learn how to set and register user properties.