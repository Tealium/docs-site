---
title: Amazon Advertising Tag Setup Guide
description: This article describes how to set up the Amazon Advertising tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amazon-advertising-tag/
---
Amazon Advertising System is an online advertising service that runs ads on the Amazon network. It is used to drive traffic and boost sales.

## Tag tips

* We recommend a hybrid setup using both a tag and a connector. This configuration ensures maximum data resilience, improves event matching with server-side signals, and maintains data flow continuity while retaining real-time client-side signals. For more information, see [Amazon Ads Conversions Connector](https://docs.tealium.com/amazon-ads-conversions-connector/).
* Use mappings to override or dynamically set the tag configurations.
* To make Amazon Ads Event IDs available as server-side attributes for deduplication, set **Generate Event ID** to `true` and use the latest version of the Tealium Collect tag.
* The event ID attribute names are in the format `amazon_event_id_<EventName>_<TagUID>` (for example `amazon_event_id_PageView_512`).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Region**:  
Enter your Amazon Advertising account region, for example: `NA`, `EU`, `FE`.
* **Tag IDs**:  
Enter your Amazon Advertising tag IDs as a comma-separated list.
* **Automatic Pageview Tracking**:  
When Automatic Pageview Tracking is set to `true` and the event equals `view`, the Amazon event is set to `Pageview`.
* **Automatic Purchase Tracking**:  
When Automatic Purchase Tracking is set to `true` and `order_id` is defined, the Amazon event is set to to `Purchase`.
* **Generate Event ID**:  
When Generate Event ID is set to `true`, an event ID is automatically generated for every Amazon Ads tracking event in the following format: `amazon_event_id_<EventName>_<TagUID>`. For example, `amazon_event_id_PageView_512`.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Event Mapping

Amazon Advertising events are configured through data mappings by selecting a variable that maps to an event and entering a trigger. The trigger initiates the event when the variable is equal to a specific value, as demonstrated in the following use case.

### Use Case: Add to Cart Event

To set up an add to cart event:

1. Select `tealium_event` from the variable drop-down list and click **Select a Destination**.
1. In the **Category** section, select **Events**.
1. Set the **When mapped variable equals** field to `cart_add`. A cart add is triggered when `tealium_event` equals `cart_add`.
1. In the **Trigger event** drop-down list, select `AddToCart`, which is the event triggered when `tealium_event` equals `cart_add`.
 
If additional data needs to be sent with the add to cart event, use Custom Parameters to map additional event data.

The following example passes the product ID as `productid` with the add to cart event:

1. Select `product_id` from the variable drop-down list and click **Select a Destination**.
1. In the **Category** section, select **Event-specific Parameters**.
1. Set the **Destination** field to the name `productid` for the Custom Parameter.
1. In the **For event** drop-down list, select the event `AddToCart` which the Custom Parameter collects with.

Test the mappings by using the Developer Tools offered by your browser.

1. Use the **Network** Panel and filter for `Amazon` to display all the network requests containing amazon as a keyword.
1. Confirm the `AddToCart` event was successful by looking at the name of the request.
1. Open the request and select the **Payload** to view the **Query String Parameters** and see the values of the data mappings that were configured: `AddToCart` and `productid`.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
| `region`  | String | <ul><li>Amazon Advertising account region.</li></ul> |
| `ids`  | String | <ul><li>Amazon Advertising account IDs. For multiple account IDs, enter a comma-delimited string.</li></ul> |
| `auto_page_tracking`  | Boolean | <ul><li>Toggle to enable or disable automatic PageView tracking.</li><li>Toggles whether to automatically trigger a PageView event with a page load.</li><li>Overrides tag configuration selection.</li></ul> |
|`auto_purchase_tracking`  | Boolean | <ul><li>Toggle to enable or disable automatic Purchase tracking.</li><li>Toggles whether to automatically trigger a Purchase event when `order_id` is present.</li><li>Overrides tag configuration selection.</li></ul>  |
| `generate_event_id`  | Boolean | <ul><li>Automatically generate an event ID for every Amazon Ads tracking event.</li><li>The event ID attribute names are in the format `amazon_event_id_<Event Name>_<Tag UID>`. For example: `amazon_event_id_PageView_512`.</li></ul> |
| `event_id`  | String | <ul><li>The generated event ID.</li></ul>  |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------| :------------|
| `order_id` (Overrides `_corder`)  | String | <ul><li>Unique identifier assigned to the final order.</li><li>Overrides `_corder`.</li></ul>|

### Enhanced Conversions

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `email_raw`  | String | Provide a plain text email address and the tag whitespace trims and lowercases this value. |
| `phonenumber`  | String | Provide a plain text phone number and the tag whitespace trims and removes symbols from this value. |
| `email`  | String | A SHA256-hashed version of the user's email address. |
| `gdpr.enabled`  | Boolean | Whether GDPR restrictions are active on the account.<ul><li>`1` - GDPR restrictions are enabled.</li><li>`0` - GDPR restrictions are not enabled.</li></ul> |
| `gdpr.consent`  | String | A valid [IAB version 1 or 2 consent string](https://iabtechlab.com/standards/gdpr-transparency-and-consent-framework/). |

### Events

For more information about mapping events, see [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-a-variable-mapping).

| Variable        | Description  |
|:----------------|:-------------|
|  `AddToCart`    | AddToCart    |
|  `Application`  | Application  |
|  `Checkout`     | Checkout     |
|  `Contact`      | Contact      |
|  `Lead`         | Lead         |
|  `Purchase`     | Purchase     |
|  `PageView`     | PageView     |
|  `Search`       | Search       |
|  `SignUp`       | SignUp       |
|  `Subscription` | Subscription |
|  `Custom`       | Custom       |

### Event-specific Parameters

For more information about mapping events, see [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-a-variable-mapping).

To map a parameter for a specific event only, enter the name of the parameter you want to set and then select the name of the event to set to that parameter.

To specify a custom event for the event-specific mapping to occur, select the **Custom option** from the **Events** drop-down list and enter the name of the custom event in the field that appears.