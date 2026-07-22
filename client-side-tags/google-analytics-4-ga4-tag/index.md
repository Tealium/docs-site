---
title: Google Analytics 4 (GA4) Tag Setup Guide
description: This article describes how to set up the Google Analytics 4 tag (GA4) in your Tealium iQ Tag Management account and considerations to be aware of during implementation.
url: https://docs.tealium.com/client-side-tags/google-analytics-4-ga4-tag/
---
## How it works

Google Analytics 4 (GA4) is the new version of Google Analytics. One of the differences between GA4 and Google Universal Analytics is that GA4 uses a different reporting method. If your site is currently running Google Universal Analytics, we recommend that you run both Google Universal Analytics and GA4 concurrently for a few months before switching completely to GA4. This approach allows historical data to continue to be collected in Google Universal Analytics while you gain familiarity with the reporting in GA4.

Note that Google Universal Analytics stopped processing data on July 1, 2023 (October 1, 2023 for 360 accounts).

Google Universal Analytics has several hit types, including event tracking, pageviews, timing events, and social shares. GA4 is completely event-based, meaning that there are only event hits. GA4 does not have the event categories, actions, labels, and values used in Google Universal Analytics. Instead, the data sent with GA4 events includes an event name and customizable event parameters that contain contextual data for the event.

For more information about migrating to GA4 from Google Universal Analytics, see [Migrating from Universal Analytics to Google Analytics 4](https://support.tealiumiq.com/en/support/solutions/articles/36000363506-migrating-from-universal-analytics-gtag-jsanalytics-js-to-google-analytics-4-ga4-).

## Tag tips

* Use mappings to:
  * Dynamically override the E-Commerce extension values
  * Setup event triggers
* Supports the following E-Commerce extension values:
  * Order ID
  * Order Total
  * Shipping Amount
  * Tax Amount
  * Store
  * Promo Code
  * Customer ID
  * List of Product IDs
  * List of Names
  * List of Brands
  * List of Categories
  * List of Prices
  * List of Quantities
  * List of Discounts
  * Custom Item-Scoped Dimensions

## Configuring the Google Analytics 4 tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Measurement ID**
  * Measurement ID of the Google Analytics property for which you want to send data. The measurement ID begins with "G-". For example, `G-12345678M`.
  * Use a comma-separated list of measurement IDs to send data for multiple GA4 properties.
* **Global Object**
  * The name of the Global Object used for the event queue.
  * If not specified, `gtag` is used.
  * For most implementation, the default is used.
* **Data Layer Name**
  * By default, the data layer initiated and referenced by the global site tag is named `dataLayer`.
  * For most implementation, the default is used.
* **Send Page View**
  * By default, Page View events are automatically recorded for each page on your site.
  * If you do not want to send Page View events to Google Analytics, set this option to false.
* **Clear Vars**
  * Clears items usually set for the lifetime of the tracker after each tracking request.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## GA4 event types

GA4 is event-based and provides the following types of events:

* Automatically Collected Events
* Enhanced Measurement Events
* Recommended Events
* Custom Events

The following diagram shows how to determine which type of event you need for your use case:

![](https://docs.tealium.com/images/client-side-tags/ga4-flowchart-event-type-v3.png)

### Automatic events

GA4 automatically generates some events, with no configuration required. For more information on automatically generated events and their parameters, see [Google Analytics 4 Automatically Collected Events](https://support.google.com/analytics/answer/9234069/ga4-automatically-collected-events).

### Enhanced measurement events

You can enable enhanced measurement options (events) in the Google Analytics interface to measure interactions with your content. No configuration in Tealium iQ is required. When you enable enhanced measurement options, additional events are sent that provide information on user activity such as file downloads and searches. For more information, see the GA4 documentation for [Enhanced Measurement Events](https://support.google.com/analytics/answer/9216061?hl=en&ref_topic=9756175).

### Recommended events

GA4 provides recommended events, including events recommended for all sites, as well as events specific to online sales and to games. Each recommended event has one or more parameters that provide additional context for the event. For more information on these events and their parameters, see the Google [Recommended Events](https://support.google.com/analytics/answer/9267735?hl=en&ref_topic=9756175) documentation.

### Dynamic Events Trigger

Map a data layer attribute to **Dynamic Events Trigger** to trigger a GA4 event based on the value of the mapped attribute.

For example:

1. Map `event_name` to the Dynamic Events Trigger.
1. Map `variable1` to `variable2`.
1. If the data layer is `{event_name:'value',variable1:'abc'}`, then the tag triggers `gtag('event','value',{variable2:'abc'})`.

| Variable | Description |
|:---------|:------------|
| `dynamic_event` | Dynamic Events Trigger  |

#### Check the tag template version

To use Dynamic Events Trigger, you must update your template to the May 26, 2023 (`20230526`) template or newer. To check the template version and update it, perform the following steps;

1. Navigate to the **Tag Configuration** tab, click **Advanced Settings**
1. Click **Edit Template**. The template window appears.
1. At the top of the template is a date (timestamp) that begins with the template ID and the date in format `YYYYMMDD`.
1. If you customized your tag template, edit the template to include those customizations.
1. Click **Update** to update the template.

For more information, see [Manage Templates](https://docs.tealium.com/manage-templates/).

### Custom events

If your event does not fit one of the event types described above, send a custom event. For more information, see [GA4 Custom Events](https://support.google.com/analytics/answer/12229021?hl=en&ref_topic=9756175).

## Event mapping examples

This section provides mapping examples of event mapping for two events that will be sent to GA4:

* Visitor logs in
* Visitor clicks a contact us link

To map an event in Tealium iQ, map a data layer variable value that specifies when an event should be fired. These examples use the `tealium_event` variable to identify the event to be sent.

### Login event example

For the login event, the following data is sent to Tealium iQ in a `utag.link` call:

```
utag.link({
   "tealium_event" : "sign in",
   "signin_method" : "email"
 });
```

Login is one of the GA4 recommended events, and has one parameter, `method`, that indicates how the user logged in. When you configure the GA4 tag, use the mapping toolbox to map the `tealium_event` and `signin_method` variables, as follows:

* `tealium_event` – Select **Event Triggers** for the **Category**, and then enter `sign in` in the **Trigger** field and select `login` for **Event**.   
![](https://docs.tealium.com/images/client-side-tags/map-tealium-event.png)
* `signin_method` – Select **Event-specific Parameters** for the **Category**, and then enter `method` in the **Event parameter** field and select `login` for **For event**.  
![](https://docs.tealium.com/images/client-side-tags/map-signin-method.png)

For more information on mapping variables, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

### Contact Us link event example

For the contact us link event, the following data is sent to Tealium iQ in a `utag.link` call:

```
utag.link({
   "tealium_event" : "contact us"
 });
```

This event is not one of the GA4 recommended events, so it's mapped as a custom event, as follows:

* `tealium_event` – Select **Event Triggers** for the **Category**, and then enter `contact us` in the **Trigger** field. Select `Custom Event` for **Event** and enter `contact_us_click` in the **Custom Name** field.  
![](https://docs.tealium.com/images/client-side-tags/map-contactus-example.png)

For more information on mapping variables, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

## Tracking e-commerce events

GA4 has ecommerce events that are equivalent to the enhanced ecommerce events for Google Universal Analytics. The differences in the GA4 ecommerce events are as follows:

* The `checkout_step` and `checkout_options` events have been replaced with the `view_cart`, `begin_checkout`, `add_shipping_info`, and `add_payment_info` events in GA4.
* The `product_click` and `select_content` (with an `items` array parameter) events have been replaced with the `select_item` event in GA4.
* The `promotion_click` and `select_content` (with a `promotions` array parameter) events have been replaced with the `select_promotion` event in GA4.

### Items parameter for recommended events

Some ecommerce events have an `items` parameter. For these events, the `items` array is automatically populated from E-commerce extension values, such as product name, category, and price.

For more information, see [E-commerce Extension](https://docs.tealium.com/e-commerce-extension/).

### Custom items

If you want to map product-related data to item-scoped custom dimensions, map the `utag` data to a member of the `item.myDimension` array.

For example, to capture and map the product color, map `utag_data.product_color` to `item.product_color`.

## Custom dimensions

Currently, GA4 has two scopes for custom dimensions:

* User-Scoped
* Event-Scoped

Google Universal Analytics has four scopes:

* Hit (similar to Event in GA4)
* Session
* User (similar to User in GA4)
* Product

When translating requirements from Google Universal Analytics to GA4, consider passing session-scoped variables as user-scoped variables where reasonable. Product-scoped variables can be passed as e-commerce parameters. For more information, see [Universal Analytics versus Google Analytics 4 data > Custom dimensions/metrics](https://support.google.com/analytics/answer/9964640?hl=en#custom-dim)

### User properties

GA4 collects user-scoped properties, which describe segments of your visitors, such as their language preference or geographic location.

To set user properties, choose the data layer variable to map, then select the **User Properties** category and enter the GA4 property name. The mapping is added in the format `set.user_properties.USER_PROPERTY` where `USER_PROPERTY` represents the GA4 property name.

![](https://docs.tealium.com/images/client-side-tags/ga4-user-property.png)

### User provided data

GA4 also collects user-provided data. User-provided data enables customers to supply additional user-provided data along with `User-ID` to send consented, hashed first-party data to GA4. This data is then matched with Google data in a privacy-safe way to power Enhanced Conversions and demographic and interests reporting.

The following user-provided destinations are available:

* Email Address (`email`)
* Hashed Email Address (`user_data.sha256_email_address`)
* Phone Number (`user_data.phone_number`)
* Hashed Phone Number (`user_data.sha256_phone_number`)
* First Name (`user_data.address.first_name`)
* Hashed First Name (`user_data.address.sha256_first_name`)
* Last Name (`user_data.address.last_name`)
* Hashed Last Name (`user_data.address.sha256_last_name`)
* Street Address (`user_data.address.street`)
* City (`user_data.address.city`)
* Region (`user_data.address.region`)
* Postal Code (`user_data.address.postal_code`)
* Country (`user_data.address.country`)

## Validating a GA4 implementation

### Event batching

In Google Universal Analytics, one network call is made for each hit that was triggered. GA4 is different in that it batches events that occur within a few seconds into a single call. When investigating network calls to validate the implementation, be aware that multiple events may be sent with a single network request.

### Reporting latency

Per the Google documentation, it can take 24-48 hours after the call is made for GA4 reports to be generated. You can use Realtime reports and Debug View in GA4 to verify that data is being sent to your GA4 property.