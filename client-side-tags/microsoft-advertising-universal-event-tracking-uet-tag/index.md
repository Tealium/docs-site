---
title: Microsoft Advertising Universal Event Tracking (UET) Tag Setup Guide
description: This article describes how to set up the Microsoft Advertising Universal Event Tracking (UET) tag.
url: https://docs.tealium.com/client-side-tags/microsoft-advertising-universal-event-tracking-uet-tag/
---
## Tag tips

* Use mapping to:
  * Override the standard configuration values.
  * Override the E-Commerce extension values.
  * Pass custom parameters.
  * Set up event triggers.
* Mapping a parameter to **Custom Property/Parameter** in the **Standard** tab sends that parameter with all events. Use the **Event Parameters** tab to send data only to certain events.
* Supports the following e-commerce extension values:
  * Order ID.
  * Order subtotal.
  * Order shipping.
  * Order tax.
  * Order currency.
  * Order coupon/promo code.
  * List of product IDs.
  * List of names.
  * List of brands.
  * List of categories.
  * List of quantities.
  * List of prices.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag ID**: Your Microsoft Advertising tag identifier.
* **ID Sync Beacon**: Persist internal user IDs to Microsoft third-party cookie IDs. Recommended when using the [Microsoft UET Conversion API connector](https://docs.tealium.com/microsoft-uet-conversion-api-connector/).
* **Ad Storage Consent**: Set the default consent for Ad Storage. Dynamically update this value by mapping the `ad_storage` parameter in the **Data Mappings** section.
* **Automatically read from Tealium Consent Cookie**: If set to `true`, consent is set based on the [Tealium consent manager](https://docs.tealium.com/about-consent-management/). 
* **Generate Event ID**: Automatically generate an event ID for every tracking event. Recommended for deduplication when using the [Microsoft UET Conversion API connector](https://docs.tealium.com/microsoft-uet-conversion-api-connector/)

### Conversions API


<blockquote>
This feature requires an active [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).
</blockquote>


To support the Microsoft UET Conversion API, set **Generate Event ID** to `true`.  When **Generate Event ID** is enabled, this tag generates a unique event ID for each event tracked and sends it as an attribute to Tealium EventStream for use in the Microsoft UET Conversion API connector and passes it to the Microsoft Advertising UET tag in the `event_id` parameter. This event ID attribute may be mapped in the connector to synchronize the web-based tag with server-side integration. 

The tag sends event IDs using generated event attributes using the following naming convention:

```nohl
microsoft_event_id_{EVENT_TYPE}_{TAG_UID}
```

For example, a purchase event from tag #88 would send the following attribute and value:

```json
{
  "microsoft_event_id_purchase_88": "028b2ade7478..."
}
```

A page load event from the same tag would send the following attribute and value:

```json
{
  "microsoft_event_id_pageload_88": "084b1cda7461..."
}
```
#### Deduplication

To ensure proper event deduplication, the event ID from the Microsoft Advertising UET tag must be included in the payload sent by the Tealium Collect tag. To do this, use the following steps:

* From the **Tag Timing** drop-down, select **Prioritized**.
* Set the **Bundle Flag** toggle to `On`.
* Use the [Load Order Manager screen](https://docs.tealium.com/load-order-manager/) to fire the Microsoft Advertising UET tag before the Tealium Collect tag. We recommend that you fire the Tealium Collect tag last.
For information on using these event ID attributes, see [Microsoft UET Conversion API connector: Deduplication](https://docs.tealium.com/microsoft-uet-conversion-api-connector/#deduplication).

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Consent mode

There are two options to implement consent mode for this tag:

* Use [client-side consent management](https://docs.tealium.com/about-consent-management/) and automatically read the Tealium consent cookie.
* Add a [JavaScript Code extension](https://docs.tealium.com/javascript-code-extension/) to map consent choices and category mappings from your consent management platform (CMP) to this tag.

As visitors make their consent choices, the tag will choose the appropriate approach for first and third-party cookies:

* **Granted**: Both first-party and third-party cookies can be read and written.
* **Denied**: First-party cookies are neither read nor written, and third-party cookies are read-only for fraud and spam purposes, not for advertising.

### Client-side consent management

To implement consent mode for this tag using client-side consent management, set **Automatically read from Tealium Consent Cookie** to `true` in the tag configuration.

### JavaScript Code extension

To map end-user consent choices to Microsoft consent mode settings, use the JavaScript Code extension. Configure the extension as follows:

* Set **Scope** to **After Load Rules (default)** 
* Set **Occurrence** to **Run Always**
* Enter the JavaScript code for your CMP. You can customize the following code template for your CMP by replacing `CUSTOM_LOGIC` with the logic for your vendor.
```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

For example, the following code is for OneTrust.
```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

If you use these exact variable names, no additional mapping is required. The latest version of the tag uses these variables by default. Overwrite these variables by mapping the `ad_storage` parameter to attributes for your specific case.  

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tagid`|  <ul><li>Tag ID.</li><li>Your tag identifier provided by Microsoft Advertising.</li></ul> |
|`event_category`|  <ul><li>Event category.</li><li>Sends information about the element or object being tracked.</li><li>Example: `Button`.</li></ul> |
|`event_action`|  <ul><li>Event action.</li><li>Sends user actions.</li><li>Example: `click`, `mousedown`.</li></ul> |
|`event_label`|  <ul><li>Event label.</li><li>Sends informative labels or details about the event goal.</li><li>Example: `Product demo`.</li></ul> |
|`event_value`|  <ul><li>Event value.</li><li>Sends the numerical value of the event goal.</li></ul> |
|`description`|  <ul><li>Error description.</li><li>The description with the error experienced by the user.</li></ul> |
|`fatal`|  <ul><li>Error fatal.</li><li>Whether the error experienced by the user is fatal.</li></ul> |
|`method`|  <ul><li>Method.</li><li>The method associated with the user's action.</li></ul> |
|`screen_name`|  <ul><li>Screen name.</li><li>The name associated with the screen the user is currently viewing.</li></ul> |
|`search_term`|  <ul><li>Search term.</li><li>The term used in the user's search.</li></ul> |
|`content_type`|  <ul><li>Content type.</li><li>The type of content selected by the user.</li></ul> |
|`content_id`|  <ul><li>Content ID.</li><li>The ID of the content selected by the user.</li></ul> |
|`promotion_creative_name`|  <ul><li>List of promotion creative names.</li><li>An array of creative names used in the promotion.</li></ul> |
|`promotion_creative_slot`|  <ul><li>List of promotion creative slots.</li><li>An array of creative slot names used in the promotion.</li></ul> |
|`promotion_id`|  <ul><li>List of promotion IDs.</li><li>An array of promotion IDs used in the promotion.</li></ul> |
|`promotion_name`|  <ul><li>List of promotion names.</li><li>An array of promotion names used in the promotion.</li></ul> |
| `enableAutoSpaTracking` | Enable automatic SPA tracking. |
| `id_sync_beacon` | ID sync beacon. |
| `customer_id` | Microsoft customer ID. |
| `visitor_id` | Visitor ID. |
| `user_id` | User ID. |
|`custom.myvar`|  <ul><li>Custom property/parameter.</li><li>A custom property for your events.</li><li>Sent with all events, use Event Parameters to set properties for specific events.</li><li>Replace `myvar` with the name of your property.</li></ul> |
| `generate_event_id` | `Boolean` | Generate event IDs. |
| `event_id` | `String` | Event ID. |

### E-Commerce

|Variable| Description|
|---| ---|
|`checkout_step`|  <ul><li>Checkout step.</li><li>The current step of the checkout process the user is on.</li></ul> |
|`checkout_option`|  <ul><li>Checkout option.</li><li>The current checkout option chosen by the user.</li></ul> |
|`order_id`|  <ul><li>Order ID.</li><li>Use to override the default e-commerce value `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Sub total.</li><li>Use to override the default e-commerce value `_csubtotal`.</li></ul> |
|`order_shipping`|  <ul><li>Shipping amount.</li><li>Use to override the default e-commerce value `_cship`.</li></ul> |
|`order_tax`|  <ul><li>Tax amount.</li><li>Use to override the default e-commerce value `_ctax`.</li></ul> |
|`order_currency`|  <ul><li>Currency.</li><li>Use to override the default e-commerce value `_ccurrency`.</li></ul> |
|`order_coupon_code`|  <ul><li>Promo code.</li><li>Use to override the default e-commerce value `_cpromo`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of product IDs.</li><li>Use to override the default e-commerce value `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of names.</li><li>Use to override the default e-commerce value `_cprodname`.</li></ul> |
|`product_brand`|  <ul><li>Array</li><li>List of brands.</li><li>Use to override the default e-commerce value `_cbrand`.</li></ul> |
|`product_category`|  <ul><li>Array</li><li>List of categories.</li><li>Use to override the default e-commerce value `_ccat`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of quantities.</li><li>Use to override the default e-commerce value `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of prices.</li><li>Use to override the default e-commerce value `_cprice`.</li></ul> |
| List of Product Creative Names |  <ul><li>Array</li><li>An array of creative names used for the product.</li></ul> |
| List of Product Creative Slots |  <ul><li>Array</li><li>An array of creative slots used for the product.</li></ul> |
| List of Product Location IDs |  <ul><li>Array</li><li>An array of location IDs used for the product.</li></ul> |

### Events and engagements

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select an event from the list.  
Choose from the predefined list, or create a custom event.
  * For a custom event, enter a name with which to identify it.

1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the plus sign (**+**) and repeat Steps 1 and 2.
1. Click **Apply**.  
The event triggers when the value supplied is found in the data layer.

|Variable| Description|
|---| ---|
|`add_payment_info`|  <ul><li>Add payment info.</li><li>User has added new payment information to the transaction.</li></ul> |
|`add_to_cart`|  <ul><li>Add to cart.</li><li>User has added one or more items to a shopping cart.</li></ul> |
|`add_to_wishlist`|  <ul><li>Add to wishlist.</li><li>User has added one or more items to a wish list.</li></ul> |
|`begin_checkout`|  <ul><li>Begin checkout.</li><li>User has begun the checkout process.</li></ul> |
|`checkout_progress`|  <ul><li>Checkout progress.</li><li>User has exchanged steps in the checkout progress.</li></ul> |
|`exception`|  <ul><li>Exception.</li><li>The user has encountered an exception.</li></ul> |
|`generate_lead`|  <ul><li>Generate lead.</li><li>The user's action has generated a lead.</li></ul> |
|`login`|  <ul><li>Login.</li><li>The user has logged in.</li></ul> |
|`page_view`|  <ul><li>Page view.</li><li>The user has viewed a page.</li></ul> |
|`purchase`|  <ul><li>Purchase.</li><li>The user has completed a purchase of one or more products.</li></ul> |
|`refund`|  <ul><li>Refund.</li><li>The user has requested a refund on one or more products.</li></ul> |
|`remove_from_cart`|  <ul><li>Remove from cart.</li><li>The user has removed one or more items from a shopping cart.</li></ul> |
|`screen_view`|  <ul><li>Screen view.</li><li>The user has viewed a screen.</li></ul> |
|`search`|  <ul><li>Search.</li><li>The user has searched.</li></ul> |
|`select_content`|  <ul><li>Select content.</li><li>The user has selected on one or more content items.</li></ul> |
|`set_checkout_option`|  <ul><li>Set checkout option.</li><li>The user has selected a checkout option for the current checkout step.</li></ul> |
|`share`|  <ul><li>Share</li><li>The user has shared content.</li></ul> |
|`sign_up`|  <ul><li>Sign up.</li><li>The user has signed up.</li></ul> |
|`timing_complete`|  <ul><li>Timing complete.</li><li>The timing information for the user's page load.</li></ul> |
|`view_item`|  <ul><li>View item.</li><li>The user has viewed a singular item, often a detail page.</li></ul> |
|`view_item_list`|  <ul><li>View item list.</li><li>The user has viewed a list page with one or more items.</li></ul> |
|`view_promotion`|  <ul><li>View promotion.</li><li>The user has clicked on a promotion.</li></ul> |
|`view_search_results`|  <ul><li>View search results.</li><li>The user has viewed the results of a search.</li></ul> |
| `update_consent` | <ul><li>Update consent.</li></ul>  |
|`custom`|  <ul><li>Custom event.</li><li>The user has initiated action related to a custom event.</li></ul> |

### Product audience events

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select an event from the list.  
Choose from the predefined list, or create a custom event.
  * For a custom event, enter a name with which to identify it.

1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the plus sign (**+**) and repeat Steps 1 and 2.
1. Click **Apply**.  
The event triggers when the value supplied is found in the data layer.

|Variable| Description|
|---| ---|
|`retail`|  <ul><li>Retail.</li><li>Send data for retail-based marketing.</li></ul> |
|`travel`|  <ul><li>Travel.</li><li>Send data for travel-based marketing.</li></ul> |
|`hotel`|  <ul><li>Hotel.</li><li>Send data for hotel-based marketing.</li></ul> |

### Enhanced conversion data

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `em` | `String` | Email. |
| `ph` | `String` | Phone. |

### Consent management

| Variable | Description |
|:---------|:------------|
| `ad_storage` | Ad storage. |

### Event parameters

Map to these destinations if you want to pass additional data with events mapped earlier.


<blockquote>
Parameters are only used with predefined events. For more information on how to pass a parameter with a custom event, see .
</blockquote>


Use the following steps to pass a parameter with a predefined event:

1. Select an event from the list.
1. Select a parameter from the list.  
If using a custom parameter, enter a name with which to identify it.
1. Click **Add**.

|Variable| Description|
|---| ---|
|`event_category`|  <ul><li>Event category.</li><li>The category of the current event.</li><li>Sends information about the element or object, such as a button being clicked on.</li></ul> |
|`event_action`|  <ul><li>Event action.</li><li>The action name of the current event.</li><li>Sends user actions, such as click or mousedown.</li></ul> |
|`event_label`|  <ul><li>Event label.</li><li>The label of the current event.</li><li>Sends informative labels or details, such as product demo, about the product goal.</li></ul> |
|`event_value`|  <ul><li>Event value.</li><li>Send the numerical value of the event goal for the current event.</li></ul> |
|`custom`|  <ul><li>Custom property/parameter.</li><li>A custom property associated with the current event.</li></ul> |
|`description`|  <ul><li>Error description.</li><li>The description of the error experienced by the user.</li></ul> |
|`fatal`|  <ul><li>Error fatal.</li><li>Whether or not the error experienced by the user is fatal.</li></ul> |
|`method`|  <ul><li>Method.</li><li>The method associated with the user's action.</li></ul> |
|`screen_name`|  <ul><li>Screen name.</li><li>The name associated with the current screen the user is viewing.</li></ul> |
|`search_term`|  <ul><li>Search term.</li><li>The term used in the user's search.</li></ul> |
|`content_type`|  <ul><li>Content type.</li><li>The type of content selected by the user.</li></ul> |
|`content_id`|  <ul><li>Content ID.</li><li>The ID of the content selected by the user.</li></ul> |
|`checkout_step`|  <ul><li>Checkout step.</li><li>The current step of the checkout process the user is on</li></ul> |
|`checkout_option`|  <ul><li>Checkout option.</li><li>The current checkout option chosen by the user.</li></ul> |
|`order_id`|  <ul><li>Order ID.</li><li>Use this to override the default e-commerce value `_corder`.</li></ul> |
|`order_total`|  <ul><li>Order total.</li><li>Use this to override the default e-commerce value `_ctotal`.</li></ul> |
|`order_subtotal`|  <ul><li>Sub total.</li><li>Use this to override the default e-commerce value `_csubtotal`.</li></ul> |
|`order_shipping`|  <ul><li>Shipping amount.</li><li>Use this to override the default e-commerce value `_cship`.</li></ul> |
|`order_tax`|  <ul><li>Tax amount.</li><li>Use this to override the default e-commerce value `_ctax`.</li></ul> |
|`order_currency`|  <ul><li>Currency.</li><li>Use this to override the default e-commerce value `_ccurrency`.</li></ul> |
|`order_coupon_code`|  <ul><li>Promo code.</li><li>Use this to override the default e-commerce value `_cpromo`.</li></ul> |
|`product_id`|  <ul><li>List of product IDs.</li><li>Use this to override the default e-commerce value `_cprod`.</li></ul> |
|`product_name`|  <ul><li>List of names.</li><li>Use this to override the default e-commerce value `_cprodname`.</li></ul> |
|`product_brand`|  <ul><li>List of brands.</li><li>Use this to override the default e-commerce value `_cbrand`.</li></ul> |
|`product_category`|  <ul><li>List of categories.</li><li>Use this to override the default e-commerce value `_ccat`.</li></ul> |
|`product_quantity`|  <ul><li>List of quantities.</li><li>Use this to override the default e-commerce value `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>List of prices.</li><li>Use this to override the default e-commerce value `_cprice`.</li></ul> |
|`product_creative_name`|  <ul><li>Array</li><li>List of product creative names.</li><li>An array of creative names used for the product.</li></ul> |
|`product_creative_slot`|  <ul><li>Array</li><li>List of product creative slots.</li><li>An array of creative slots used for the product.</li></ul> |
|`promotion_creative_name`|  <ul><li>Array</li><li>List of promotion creative names.</li><li>An array of creative names used in the promotion.</li></ul> |
|`promotion_creative_slot`|  <ul><li>Array</li><li>List of promotion creative slots.</li><li>An array of creative slot names used in the promotion.</li></ul> |
|`promotion_id`|  <ul><li>Array</li><li>List of promotion IDs.</li><li>An array of promotion IDs used in the promotion.</li></ul> |
|`promotion_name`|  <ul><li>Array</li><li>Promotion names.</li><li>An array of promotion names used in the promotion.</li></ul> |

### Product audience parameters

Map to these destinations if you want to pass additional data with events mapped earlier.


<blockquote>
Parameters are only used with predefined events. For more information on how to pass a parameter with a custom event, see .
</blockquote>


Use the following steps to pass a parameter with a predefined event:

1. Select an event from the list.
1. Select a parameter from the list.  
If using a custom parameter, enter a name with which to identify it.
1. Click **Add**.

|Variable| Description|
|---| ---|
|`ecomm_prodid`|  <ul><li>Product ID.</li><li>One or more IDs currently visible to or selected by the user.</li></ul> |
|`ecomm_pagetype`|  <ul><li>Page type.</li><li>The current page type visible to the user.</li></ul> |
|`ecomm_totalvalue`|  <ul><li>Total value.</li><li>The total value currently associated with the user.</li></ul> |
|`ecomm_category`|  <ul><li>Category.</li><li>The current category visible to the user.</li></ul> |
|`travel_destid`|  <ul><li>Destination ID.</li><li>The ID for the destination the user has selected.</li></ul> |
|`travel_originid`|  <ul><li>Origin ID.</li><li>The ID for the user's origin location.</li></ul> |
|`travel_startdate`|  <ul><li>Start date.</li><li>The date the user wants to start travel.</li></ul> |
|`travel_enddate`|  <ul><li>End date.</li><li>The date the user wants to end travel.</li></ul> |
|`travel_totalvalue`|  <ul><li>Total value.</li><li>The total value of the travel the user wants to embark on.</li></ul> |
|`hct_bpr`|  <ul><li>Hotel base price.</li><li>The base price of the hotel the user wants to book.</li></ul> |
|`hct_tpr`|  <ul><li>Hotel total price.</li><li>The total price, including tax and discounts, of the hotel the user wants to book.</li></ul> |
|`hct_bid`|  <ul><li>Hotel booking ID.</li><li>The ID for the user's booking.</li></ul> |
|`hct_cid`|  <ul><li>Hotel check-in date.</li><li>The check-in date for the user's stay.</li></ul> |
|`hct_cod`|  <ul><li>Hotel checkout date.</li><li>The checkout date for the user's stay.</li></ul> |
|`hct_los`|  <ul><li>Hotel length of stay.</li><li>The total length of the user's stay.</li></ul> |
|`hct_pid`|  <ul><li>Hotel partner ID.</li><li>The partner ID for the hotel the user wants to book.</li></ul> |
|`hct_pagetype`|  <ul><li>Hotel page type.</li><li>The current page type visible to the user.</li></ul> |

### Product audience - Retail

| Variable           | Description             |
| ------------------ | --------------- |
| `ecomm_prodid`     | <ul><li>Product ID.</li><li>One or more IDs currently visible to or selected by the user.</li></ul>      |
| `ecomm_pagetype`   | <ul><li>Page type.</li><li>The current page type visible to the user.</li><li>One of `home`, `searchresults`, `category`, `product`, `cart`, `purchase`, or `other`.</li></ul> |
| `ecomm_totalvalue` | <ul><li>Total value.</li><li>The total value currently associated with the user.</li></ul>            |
| `ecomm_category`   | <ul><li>Category.</li><li>The current category visible to the user.</li></ul>   |

### Product audience - Travel

|Variable| Description|
|---| ---|
|`travel_destid`|  <ul><li>Destination ID.</li><li>The ID for the destination the user has selected.</li></ul> |
|`travel_originid`|  <ul><li>Origin ID.</li><li>The ID for the user's origin location.</li></ul> |
|`travel_pagetype`|  <ul><li>Page type.</li><li>The current page type visible to the user.</li><li>One of `home`, `searchresults`, `offerdetail`, `conversionintent`, `conversion`, `cancel`, or `other`.</li></ul> |
|`travel_startdate`|  <ul><li>Start date.</li><li>The date the user wants to start travel.</li><li>Date format is `YYYY-MM-DD`.</li></ul> |
|`travel_enddate`|  <ul><li>End date.</li><li>The date the user wants to end travel.</li><li>Date format is `YYYY-MM-DD`.</li></ul> |
|`travel_totalvalue`|  <ul><li>Total value.</li><li>The total value of the travel the user wants to embark on.</li></ul> |

### Product audience - Hotel

|Variable| Description|
|---| ---|
|`hct_base_price`|  <ul><li>Hotel base price.</li><li>The base price of the hotel the user wants to book.</li></ul> |
|`hct_total_price`|  <ul><li>Hotel total price.</li><li>The total price, including tax and discounts, of the hotel the user wants to book.</li></ul> |
| `hct_checkin_date` |  <ul><li>Hotel check in date.</li><li>The check in date for the user's stay.</li><li>Date format is `YYYY-MM-DD`.</li></ul> |
| `hct_checkout_date` |  <ul><li>Hotel checkout date.</li><li>The checkout date for the user's stay.</li><li>Date format is `YYYY-MM-DD`.</li></ul> |
|`hct_length_of_stay`|  <ul><li>Hotel length of stay.</li><li>The total length of the user's stay.</li></ul> |
|`hct_partner_hotel_id`|  <ul><li>Hotel partner ID.</li><li>The partner ID for the hotel the user wants to book.</li></ul> |
| `hct_booking_ref` |  <ul><li>Obfuscated booking reference number.</li></ul> |
| `hct_pagetype` |  <ul><li>Hotel page type.</li><li>The current page type visible to the user.</li><li>One of `home`, `searchresults`, `property`, `cart`, `purchase`, `cancel`, or `other`.</li></ul> |

## Vendor documentation

* [Microsoft Bing: Tracking sales and other conversions](http://help.bingads.microsoft.com/#apex/3/en/n5012/2)
* [Microsoft Bing: What is UET and how can it help me?](https://help.bingads.microsoft.com/#apex/3/en/56681/0)
* [Microsoft Bing: FAQs](http://help.bingads.microsoft.com/apex/index/3/en-us/53056)