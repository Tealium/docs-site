---
title: TikTok Pixel Tag Setup Guide
description: This article describes how to set up the TikTok Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/tiktok-pixel-tag/
---
## Tag tips

*   Use mappings to override and dynamically set the tag configuration.
*   By default, the tag template detects if mapped product parameters contain a single or multiple products per event. If a single product is detected, the individual TikTok product variables (`content_id`, `content_category`, `content_name`) are used. If multiple products are detected, the `contents` array is automatically populated and used.
*   By default, the `Identify` method is automatically sent for each event where user data (hashed or un-hashed email or phone number) is populated. Disable this in the tag configuration. As a best practice, TikTok automatically hashes raw customer information with SHA256 before the value enters their servers for matching.
*   For TikTok to collect an unhashed email, it must detect the `@` character in the value and it must end with a domain designation.
*   For TikTok to collect an unhashed phone number, the values must follow the E.164 format: `+{country code}{phone number}`. For example, `+14135552671` (US), `+442071838750` (GB), and `+551155256325` (BR).
*   Use the Crypto Extension to encrypt and populate the hashed email and phone number values.
*   The `value` parameter is automatically calculated and set based on product prices and quantities.
*   By default, the TikTok pixel base code tracks a `Pageview` event on every page. Disable this in the tag configuration or with a data mapping for `auto_page_tracking`.
*   By default, the `CompletePayment` event occurs when an order ID is populated. Disable this in the tag configuration or with a data mapping for `auto_purchase_tracking`.

  
<blockquote>
Custom or non-standard parameters are not processed by TikTok. Advertisers can request a custom report from their TikTok account representative to calculate metrics for the custom parameters.
</blockquote>


## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Pixel ID**: Your TikTok Pixel ID.
* **Content Type**: Sets `content_type` to determine how to track products based on the format of your product catalog. Select `Product` to track events associated with individual products (commonly formatted as a SKU) or select `Product Group` to track events associated with product groups (often a prefix in the product ID). For more information, see [TikTok: About parameters](https://ads.tiktok.com/help/article/about-parameters?lang=en).
* **Generate Event ID**: If enabled, use with the [TikTok Events connector](https://docs.tealium.com/tiktok-events-connector/) and map the event ID parameter in the connector to synchronize web and server based integrations. This feature requires an active Tealium Collect tag.
* **Automatic Pageview Tracking**: Automatically track the `Pageview` event on every page. Override this setting by mapping `auto_page_tracking`.
* **Automatic Purchase Tracking**: Automatically track the `CompletePayment` event when an order ID is detected. Override this setting by mapping `auto_purchase_tracking`.
* **Automatic Identity Tracking**: Enable the TikTok Advanced Matching feature that helps you match customer information such as email, phone number, and other identifiers with actions people take on your website. When enabled, the tag calls `ttq.identify()` for every event where user data (email or phone number) is detected. For more information, see [TiKTok: About advanced matching for web](https://ads.tiktok.com/help/article/advanced-matching-web).
* **Limited Data Use**: A feature to help facilitate advertiser's compliance with the right to opt-out of sale and sharing of personal data under certain U.S. state privacy laws. For more information, see [TikTok: Limited Data Use](https://business-api.tiktok.com/portal/docs?id=1770092377990145).

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `pixel_code`  | String | Pixel ID. |
|  `content_type`  | String | Content type. |
|  `auto_page_tracking`  | Boolean | Automatic pageview tracking. |
|  `auto_purchase_tracking`  | Boolean | Automatic purchase tracking. |
|  `auto_identity_tracking`  | Boolean | Automatic identity tracking. |
|  `ldu`  | Boolean | Limited data use. |

### User Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `email`  | String | User email.| 
|  `phone_number`  | String | User phone number.| 
|  `sha256_email`  | String | User hashed email.| 
| `sha256_phone_number`  | String | User hashed phone number. | 
| `external_id`| String | An identifier that represents a user on an advertiser’s platform, such as a customer ID, loyalty card number, or order ID. If provided in plain text, the TikTok library hashes the ID before ingestion. | 
| `sha256_external_id`| String | A SHA256-hashed identifier that represents a user on an advertiser’s platform, such as a customer ID, loyalty card number, or order ID. Trim any leading or trailing spaces before hashing. | 

### Standard Tracking Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `currency`   | String | Currency (Overrides `_ccurrency`). |
|  `value`   | Number | Value (Overrides `_ctotal`). |
|  `query`  | String | Query. |
|  `description`  | String | Description. |
|  `status`  | String | Status. |
|  `contents`  | Array of objects | Contents. |
|  `content_id`   | Array of Strings | Content ID (Overrides `_cprod`). |
|  `content_name`  | Array of Strings | Content name (Overrides `_cprodname`). |
|  `content_category`   | Array of Strings | Content Category (Overrides `_ccat`). |
|  `quantity`   | Array of Numbers | Quantity (Overrides `_cquan`). | 
|  `price`   | Array of Numbers | Price (Overrides `_cprice`). |

### Events

For more information about mapping events, see [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Description |
|:---------|:------------|
| `AddPaymentInfo` | AddPaymentInfo |
| `AddToCart` | AddToCart |
| `AddToWishlist` | AddToWishlist |
| `ClickButton` | ClickButton |
| `CompletePayment` | CompletePayment |
| `CompleteRegistration` | CompleteRegistration |
| `Contact` | Contact |
| `Download` | Download |
| `InitiateCheckout` | InitiateCheckout |
| `PlaceAnOrder` | PlaceAnOrder |
| `Search` | Search |
| `SubmitForm` | SubmitForm |
| `Subscribe` | Subscribe |
| `ViewContent` | ViewContent |
| `Custom` | Custom |

### Travel - Hotel Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `hotel.content_id` | `String or Array of Strings` | Product IDs associated with the event, such as SKUs |
| `hotel.city` | `String` | Hotel city location |
| `hotel.region` | `String` | Hotel region |
| `hotel.country` | `String` | Hotel country |
| `hotel.checkin_date` | `String` | Hotel check-in date. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`. |
| `hotel.checkout_date` | `String` | Hotel check-out date, Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`. |
| `hotel.num_adults` | `Number` | Number of adults |
| `hotel.num_children` | `Number` | Number of children |
| `hotel.suggested_hotels` | `String or Array of Strings` | Suggested hotels for this user |


### Travel - Flight Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `flight.content_id` | `String or Array of Strings` | Product IDs associated with the event, such as SKUs. |
| `flight.destination_city` | `String` | Destination city name |
| `flight.departing_departure_date` | `String` | Takeoff date of departure flight. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`. |
| `flight.departing_arrival_date` | `String` | Landing date of departure flight. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`.|
| `flight.returning_departure_date` | `String` | Takeoff date of return flight. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`.|
| `flight.returning_arrival_date` | `String` | Landing date of return flight. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`.|
| `flight.origin_airport` | `String` | Origin airport code, for example `JFK` |
| `flight.destination_airport` | `String` | Destination airport code, for example `CDG` |
| `flight.num_adults` | `Number` | Number of people |
| `flight.num_children` | `Number` | Number of children |
| `flight.num_infants` | `Number` | Number of infants |
| `flight.travel_class` | `String` | Class of the flight ticket. Accepted values: `eco`, `prem`, `bus`, or `first`. |
| `flight.user_score` | `Number` | Represents the relative value of this potential customer to advertiser |
| `flight.preferred_num_stops` | `Number` | Number of preferred stops |


### Travel - Destination Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `destination.content_id` | `String or Array of Strings` | Product IDs associated with the event, such as SKUs |
| `destination.city` | `String` | Destination city location |
| `destination.region` | `String` | Destination region |
| `destination.country` | `String` | Destination country |
| `destination.travel_start` | `String` | The start date of user's trip. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`. |
| `destination.travel_end` | `String` | The end date of user's trip. Accepted date formats: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, and `YYYY-MM-DDThh:mm:ssTZD`. Examples: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, and `2025-06-23T15:30:00GMT`. |
| `destination.num_adults` | `Number` | Number of people |
| `destination.num_children` | `Number` | Number of children |
| `destination.num_infants` | `Number` | Number of infants |
| `destination.suggested_destinations` | `String or Array of Strings` | A list of IDs representing destination suggestions for this user |
