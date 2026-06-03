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

Go to the tag marketplace to add a new tag. For more information, see [About tags]().

When adding the tag, configure the following settings:

* **Tag ID**: Your Microsoft Advertising tag identifier.
* **ID Sync Beacon**: Persist internal user IDs to Microsoft third-party cookie IDs. Recommended when using the [Microsoft UET Conversion API connector]().
* **Ad Storage Consent**: Set the default consent for Ad Storage. Dynamically update this value by mapping the `ad_storage` parameter in the **Data Mappings** section.
* **Automatically read from Tealium Consent Cookie**: If set to `true`, consent is set based on the [Tealium consent manager](). 
* **Generate Event ID**: Automatically generate an event ID for every tracking event. Recommended for deduplication when using the [Microsoft UET Conversion API connector]()

### Conversions API

 This feature requires an active [Tealium Collect tag](). 

To support the Microsoft UET Conversion API, set **Generate Event ID** to `true`.  When **Generate Event ID** is enabled, this tag generates a unique event ID for each event tracked and sends it as an attribute to Tealium EventStream for use in the Microsoft UET Conversion API connector and passes it to the Microsoft Advertising UET tag in the `event_id` parameter. This event ID attribute may be mapped in the connector to synchronize the web-based tag with server-side integration. 

The tag sends event IDs using generated event attributes using the following naming convention:

```nohl
microsoft_event_id_{EVENT_TYPE}_{TAG_UID}
```

For example, a purchase event from tag #88 would send the following attribute and value:

```json
{
  &#34;microsoft_event_id_purchase_88&#34;: &#34;028b2ade7478...&#34;
}
```

A page load event from the same tag would send the following attribute and value:

```json
{
  &#34;microsoft_event_id_pageload_88&#34;: &#34;084b1cda7461...&#34;
}
```
#### Deduplication

To ensure proper event deduplication, the event ID from the Microsoft Advertising UET tag must be included in the payload sent by the Tealium Collect tag. To do this, use the following steps:

* From the **Tag Timing** drop-down, select **Prioritized**.
* Set the **Bundle Flag** toggle to `On`.
* Use the [Load Order Manager screen]() to fire the Microsoft Advertising UET tag before the Tealium Collect tag. We recommend that you fire the Tealium Collect tag last.
For information on using these event ID attributes, see [Microsoft UET Conversion API connector: Deduplication]().

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Consent mode

There are two options to implement consent mode for this tag:

* Use [client-side consent management]() and automatically read the Tealium consent cookie.
* Add a [JavaScript Code extension]() to map consent choices and category mappings from your consent management platform (CMP) to this tag.

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
b.consent_decision = (tealiumConsentRegister &amp;&amp; tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? &#39;granted&#39; : &#39;denied&#39;;
```

For example, the following code is for OneTrust.
```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister &amp;&amp; tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf(&#39;C0004&#39;) !== -1  ? &#39;granted&#39; : &#39;denied&#39;;
```

If you use these exact variable names, no additional mapping is required. The latest version of the tag uses these variables by default. Overwrite these variables by mapping the `ad_storage` parameter to attributes for your specific case.  

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tagid`|  &lt;ul&gt;&lt;li&gt;Tag ID.&lt;/li&gt;&lt;li&gt;Your tag identifier provided by Microsoft Advertising.&lt;/li&gt;&lt;/ul&gt; |
|`event_category`|  &lt;ul&gt;&lt;li&gt;Event category.&lt;/li&gt;&lt;li&gt;Sends information about the element or object being tracked.&lt;/li&gt;&lt;li&gt;Example: `Button`.&lt;/li&gt;&lt;/ul&gt; |
|`event_action`|  &lt;ul&gt;&lt;li&gt;Event action.&lt;/li&gt;&lt;li&gt;Sends user actions.&lt;/li&gt;&lt;li&gt;Example: `click`, `mousedown`.&lt;/li&gt;&lt;/ul&gt; |
|`event_label`|  &lt;ul&gt;&lt;li&gt;Event label.&lt;/li&gt;&lt;li&gt;Sends informative labels or details about the event goal.&lt;/li&gt;&lt;li&gt;Example: `Product demo`.&lt;/li&gt;&lt;/ul&gt; |
|`event_value`|  &lt;ul&gt;&lt;li&gt;Event value.&lt;/li&gt;&lt;li&gt;Sends the numerical value of the event goal.&lt;/li&gt;&lt;/ul&gt; |
|`description`|  &lt;ul&gt;&lt;li&gt;Error description.&lt;/li&gt;&lt;li&gt;The description with the error experienced by the user.&lt;/li&gt;&lt;/ul&gt; |
|`fatal`|  &lt;ul&gt;&lt;li&gt;Error fatal.&lt;/li&gt;&lt;li&gt;Whether the error experienced by the user is fatal.&lt;/li&gt;&lt;/ul&gt; |
|`method`|  &lt;ul&gt;&lt;li&gt;Method.&lt;/li&gt;&lt;li&gt;The method associated with the user&#39;s action.&lt;/li&gt;&lt;/ul&gt; |
|`screen_name`|  &lt;ul&gt;&lt;li&gt;Screen name.&lt;/li&gt;&lt;li&gt;The name associated with the screen the user is currently viewing.&lt;/li&gt;&lt;/ul&gt; |
|`search_term`|  &lt;ul&gt;&lt;li&gt;Search term.&lt;/li&gt;&lt;li&gt;The term used in the user&#39;s search.&lt;/li&gt;&lt;/ul&gt; |
|`content_type`|  &lt;ul&gt;&lt;li&gt;Content type.&lt;/li&gt;&lt;li&gt;The type of content selected by the user.&lt;/li&gt;&lt;/ul&gt; |
|`content_id`|  &lt;ul&gt;&lt;li&gt;Content ID.&lt;/li&gt;&lt;li&gt;The ID of the content selected by the user.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_name`|  &lt;ul&gt;&lt;li&gt;List of promotion creative names.&lt;/li&gt;&lt;li&gt;An array of creative names used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_slot`|  &lt;ul&gt;&lt;li&gt;List of promotion creative slots.&lt;/li&gt;&lt;li&gt;An array of creative slot names used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_id`|  &lt;ul&gt;&lt;li&gt;List of promotion IDs.&lt;/li&gt;&lt;li&gt;An array of promotion IDs used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_name`|  &lt;ul&gt;&lt;li&gt;List of promotion names.&lt;/li&gt;&lt;li&gt;An array of promotion names used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
| `enableAutoSpaTracking` | Enable automatic SPA tracking. |
| `id_sync_beacon` | ID sync beacon. |
| `customer_id` | Microsoft customer ID. |
| `visitor_id` | Visitor ID. |
| `user_id` | User ID. |
|`custom.myvar`|  &lt;ul&gt;&lt;li&gt;Custom property/parameter.&lt;/li&gt;&lt;li&gt;A custom property for your events.&lt;/li&gt;&lt;li&gt;Sent with all events, use Event Parameters to set properties for specific events.&lt;/li&gt;&lt;li&gt;Replace `myvar` with the name of your property.&lt;/li&gt;&lt;/ul&gt; |
| `generate_event_id` | `Boolean` | Generate event IDs. |
| `event_id` | `String` | Event ID. |

### E-Commerce

|Variable| Description|
|---| ---|
|`checkout_step`|  &lt;ul&gt;&lt;li&gt;Checkout step.&lt;/li&gt;&lt;li&gt;The current step of the checkout process the user is on.&lt;/li&gt;&lt;/ul&gt; |
|`checkout_option`|  &lt;ul&gt;&lt;li&gt;Checkout option.&lt;/li&gt;&lt;li&gt;The current checkout option chosen by the user.&lt;/li&gt;&lt;/ul&gt; |
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub total.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Shipping amount.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax amount.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;Currency.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;Promo code.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of product IDs.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of names.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of brands.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cbrand`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of categories.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of quantities.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of prices.&lt;/li&gt;&lt;li&gt;Use to override the default e-commerce value `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
| List of Product Creative Names |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;An array of creative names used for the product.&lt;/li&gt;&lt;/ul&gt; |
| List of Product Creative Slots |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;An array of creative slots used for the product.&lt;/li&gt;&lt;/ul&gt; |
| List of Product Location IDs |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;An array of location IDs used for the product.&lt;/li&gt;&lt;/ul&gt; |

### Events and engagements

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select an event from the list.  
Choose from the predefined list, or create a custom event.
  * For a custom event, enter a name with which to identify it.

1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the plus sign (**&#43;**) and repeat Steps 1 and 2.
1. Click **Apply**.  
The event triggers when the value supplied is found in the data layer.

|Variable| Description|
|---| ---|
|`add_payment_info`|  &lt;ul&gt;&lt;li&gt;Add payment info.&lt;/li&gt;&lt;li&gt;User has added new payment information to the transaction.&lt;/li&gt;&lt;/ul&gt; |
|`add_to_cart`|  &lt;ul&gt;&lt;li&gt;Add to cart.&lt;/li&gt;&lt;li&gt;User has added one or more items to a shopping cart.&lt;/li&gt;&lt;/ul&gt; |
|`add_to_wishlist`|  &lt;ul&gt;&lt;li&gt;Add to wishlist.&lt;/li&gt;&lt;li&gt;User has added one or more items to a wish list.&lt;/li&gt;&lt;/ul&gt; |
|`begin_checkout`|  &lt;ul&gt;&lt;li&gt;Begin checkout.&lt;/li&gt;&lt;li&gt;User has begun the checkout process.&lt;/li&gt;&lt;/ul&gt; |
|`checkout_progress`|  &lt;ul&gt;&lt;li&gt;Checkout progress.&lt;/li&gt;&lt;li&gt;User has exchanged steps in the checkout progress.&lt;/li&gt;&lt;/ul&gt; |
|`exception`|  &lt;ul&gt;&lt;li&gt;Exception.&lt;/li&gt;&lt;li&gt;The user has encountered an exception.&lt;/li&gt;&lt;/ul&gt; |
|`generate_lead`|  &lt;ul&gt;&lt;li&gt;Generate lead.&lt;/li&gt;&lt;li&gt;The user&#39;s action has generated a lead.&lt;/li&gt;&lt;/ul&gt; |
|`login`|  &lt;ul&gt;&lt;li&gt;Login.&lt;/li&gt;&lt;li&gt;The user has logged in.&lt;/li&gt;&lt;/ul&gt; |
|`page_view`|  &lt;ul&gt;&lt;li&gt;Page view.&lt;/li&gt;&lt;li&gt;The user has viewed a page.&lt;/li&gt;&lt;/ul&gt; |
|`purchase`|  &lt;ul&gt;&lt;li&gt;Purchase.&lt;/li&gt;&lt;li&gt;The user has completed a purchase of one or more products.&lt;/li&gt;&lt;/ul&gt; |
|`refund`|  &lt;ul&gt;&lt;li&gt;Refund.&lt;/li&gt;&lt;li&gt;The user has requested a refund on one or more products.&lt;/li&gt;&lt;/ul&gt; |
|`remove_from_cart`|  &lt;ul&gt;&lt;li&gt;Remove from cart.&lt;/li&gt;&lt;li&gt;The user has removed one or more items from a shopping cart.&lt;/li&gt;&lt;/ul&gt; |
|`screen_view`|  &lt;ul&gt;&lt;li&gt;Screen view.&lt;/li&gt;&lt;li&gt;The user has viewed a screen.&lt;/li&gt;&lt;/ul&gt; |
|`search`|  &lt;ul&gt;&lt;li&gt;Search.&lt;/li&gt;&lt;li&gt;The user has searched.&lt;/li&gt;&lt;/ul&gt; |
|`select_content`|  &lt;ul&gt;&lt;li&gt;Select content.&lt;/li&gt;&lt;li&gt;The user has selected on one or more content items.&lt;/li&gt;&lt;/ul&gt; |
|`set_checkout_option`|  &lt;ul&gt;&lt;li&gt;Set checkout option.&lt;/li&gt;&lt;li&gt;The user has selected a checkout option for the current checkout step.&lt;/li&gt;&lt;/ul&gt; |
|`share`|  &lt;ul&gt;&lt;li&gt;Share&lt;/li&gt;&lt;li&gt;The user has shared content.&lt;/li&gt;&lt;/ul&gt; |
|`sign_up`|  &lt;ul&gt;&lt;li&gt;Sign up.&lt;/li&gt;&lt;li&gt;The user has signed up.&lt;/li&gt;&lt;/ul&gt; |
|`timing_complete`|  &lt;ul&gt;&lt;li&gt;Timing complete.&lt;/li&gt;&lt;li&gt;The timing information for the user&#39;s page load.&lt;/li&gt;&lt;/ul&gt; |
|`view_item`|  &lt;ul&gt;&lt;li&gt;View item.&lt;/li&gt;&lt;li&gt;The user has viewed a singular item, often a detail page.&lt;/li&gt;&lt;/ul&gt; |
|`view_item_list`|  &lt;ul&gt;&lt;li&gt;View item list.&lt;/li&gt;&lt;li&gt;The user has viewed a list page with one or more items.&lt;/li&gt;&lt;/ul&gt; |
|`view_promotion`|  &lt;ul&gt;&lt;li&gt;View promotion.&lt;/li&gt;&lt;li&gt;The user has clicked on a promotion.&lt;/li&gt;&lt;/ul&gt; |
|`view_search_results`|  &lt;ul&gt;&lt;li&gt;View search results.&lt;/li&gt;&lt;li&gt;The user has viewed the results of a search.&lt;/li&gt;&lt;/ul&gt; |
| `update_consent` | &lt;ul&gt;&lt;li&gt;Update consent.&lt;/li&gt;&lt;/ul&gt;  |
|`custom`|  &lt;ul&gt;&lt;li&gt;Custom event.&lt;/li&gt;&lt;li&gt;The user has initiated action related to a custom event.&lt;/li&gt;&lt;/ul&gt; |

### Product audience events

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select an event from the list.  
Choose from the predefined list, or create a custom event.
  * For a custom event, enter a name with which to identify it.

1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the plus sign (**&#43;**) and repeat Steps 1 and 2.
1. Click **Apply**.  
The event triggers when the value supplied is found in the data layer.

|Variable| Description|
|---| ---|
|`retail`|  &lt;ul&gt;&lt;li&gt;Retail.&lt;/li&gt;&lt;li&gt;Send data for retail-based marketing.&lt;/li&gt;&lt;/ul&gt; |
|`travel`|  &lt;ul&gt;&lt;li&gt;Travel.&lt;/li&gt;&lt;li&gt;Send data for travel-based marketing.&lt;/li&gt;&lt;/ul&gt; |
|`hotel`|  &lt;ul&gt;&lt;li&gt;Hotel.&lt;/li&gt;&lt;li&gt;Send data for hotel-based marketing.&lt;/li&gt;&lt;/ul&gt; |

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

Parameters are only used with predefined events. For more information on how to pass a parameter with a custom event, see .

Use the following steps to pass a parameter with a predefined event:

1. Select an event from the list.
1. Select a parameter from the list.  
If using a custom parameter, enter a name with which to identify it.
1. Click **Add**.

|Variable| Description|
|---| ---|
|`event_category`|  &lt;ul&gt;&lt;li&gt;Event category.&lt;/li&gt;&lt;li&gt;The category of the current event.&lt;/li&gt;&lt;li&gt;Sends information about the element or object, such as a button being clicked on.&lt;/li&gt;&lt;/ul&gt; |
|`event_action`|  &lt;ul&gt;&lt;li&gt;Event action.&lt;/li&gt;&lt;li&gt;The action name of the current event.&lt;/li&gt;&lt;li&gt;Sends user actions, such as click or mousedown.&lt;/li&gt;&lt;/ul&gt; |
|`event_label`|  &lt;ul&gt;&lt;li&gt;Event label.&lt;/li&gt;&lt;li&gt;The label of the current event.&lt;/li&gt;&lt;li&gt;Sends informative labels or details, such as product demo, about the product goal.&lt;/li&gt;&lt;/ul&gt; |
|`event_value`|  &lt;ul&gt;&lt;li&gt;Event value.&lt;/li&gt;&lt;li&gt;Send the numerical value of the event goal for the current event.&lt;/li&gt;&lt;/ul&gt; |
|`custom`|  &lt;ul&gt;&lt;li&gt;Custom property/parameter.&lt;/li&gt;&lt;li&gt;A custom property associated with the current event.&lt;/li&gt;&lt;/ul&gt; |
|`description`|  &lt;ul&gt;&lt;li&gt;Error description.&lt;/li&gt;&lt;li&gt;The description of the error experienced by the user.&lt;/li&gt;&lt;/ul&gt; |
|`fatal`|  &lt;ul&gt;&lt;li&gt;Error fatal.&lt;/li&gt;&lt;li&gt;Whether or not the error experienced by the user is fatal.&lt;/li&gt;&lt;/ul&gt; |
|`method`|  &lt;ul&gt;&lt;li&gt;Method.&lt;/li&gt;&lt;li&gt;The method associated with the user&#39;s action.&lt;/li&gt;&lt;/ul&gt; |
|`screen_name`|  &lt;ul&gt;&lt;li&gt;Screen name.&lt;/li&gt;&lt;li&gt;The name associated with the current screen the user is viewing.&lt;/li&gt;&lt;/ul&gt; |
|`search_term`|  &lt;ul&gt;&lt;li&gt;Search term.&lt;/li&gt;&lt;li&gt;The term used in the user&#39;s search.&lt;/li&gt;&lt;/ul&gt; |
|`content_type`|  &lt;ul&gt;&lt;li&gt;Content type.&lt;/li&gt;&lt;li&gt;The type of content selected by the user.&lt;/li&gt;&lt;/ul&gt; |
|`content_id`|  &lt;ul&gt;&lt;li&gt;Content ID.&lt;/li&gt;&lt;li&gt;The ID of the content selected by the user.&lt;/li&gt;&lt;/ul&gt; |
|`checkout_step`|  &lt;ul&gt;&lt;li&gt;Checkout step.&lt;/li&gt;&lt;li&gt;The current step of the checkout process the user is on&lt;/li&gt;&lt;/ul&gt; |
|`checkout_option`|  &lt;ul&gt;&lt;li&gt;Checkout option.&lt;/li&gt;&lt;li&gt;The current checkout option chosen by the user.&lt;/li&gt;&lt;/ul&gt; |
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;Order total.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub total.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Shipping amount.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax amount.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;Currency.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;Promo code.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;List of product IDs.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;List of names.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;List of brands.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cbrand`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;List of categories.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;List of quantities.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;List of prices.&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
|`product_creative_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of product creative names.&lt;/li&gt;&lt;li&gt;An array of creative names used for the product.&lt;/li&gt;&lt;/ul&gt; |
|`product_creative_slot`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of product creative slots.&lt;/li&gt;&lt;li&gt;An array of creative slots used for the product.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of promotion creative names.&lt;/li&gt;&lt;li&gt;An array of creative names used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_slot`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of promotion creative slots.&lt;/li&gt;&lt;li&gt;An array of creative slot names used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of promotion IDs.&lt;/li&gt;&lt;li&gt;An array of promotion IDs used in the promotion.&lt;/li&gt;&lt;/ul&gt; |
|`promotion_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion names.&lt;/li&gt;&lt;li&gt;An array of promotion names used in the promotion.&lt;/li&gt;&lt;/ul&gt; |

### Product audience parameters

Map to these destinations if you want to pass additional data with events mapped earlier.

Parameters are only used with predefined events. For more information on how to pass a parameter with a custom event, see .

Use the following steps to pass a parameter with a predefined event:

1. Select an event from the list.
1. Select a parameter from the list.  
If using a custom parameter, enter a name with which to identify it.
1. Click **Add**.

|Variable| Description|
|---| ---|
|`ecomm_prodid`|  &lt;ul&gt;&lt;li&gt;Product ID.&lt;/li&gt;&lt;li&gt;One or more IDs currently visible to or selected by the user.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm_pagetype`|  &lt;ul&gt;&lt;li&gt;Page type.&lt;/li&gt;&lt;li&gt;The current page type visible to the user.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm_totalvalue`|  &lt;ul&gt;&lt;li&gt;Total value.&lt;/li&gt;&lt;li&gt;The total value currently associated with the user.&lt;/li&gt;&lt;/ul&gt; |
|`ecomm_category`|  &lt;ul&gt;&lt;li&gt;Category.&lt;/li&gt;&lt;li&gt;The current category visible to the user.&lt;/li&gt;&lt;/ul&gt; |
|`travel_destid`|  &lt;ul&gt;&lt;li&gt;Destination ID.&lt;/li&gt;&lt;li&gt;The ID for the destination the user has selected.&lt;/li&gt;&lt;/ul&gt; |
|`travel_originid`|  &lt;ul&gt;&lt;li&gt;Origin ID.&lt;/li&gt;&lt;li&gt;The ID for the user&#39;s origin location.&lt;/li&gt;&lt;/ul&gt; |
|`travel_startdate`|  &lt;ul&gt;&lt;li&gt;Start date.&lt;/li&gt;&lt;li&gt;The date the user wants to start travel.&lt;/li&gt;&lt;/ul&gt; |
|`travel_enddate`|  &lt;ul&gt;&lt;li&gt;End date.&lt;/li&gt;&lt;li&gt;The date the user wants to end travel.&lt;/li&gt;&lt;/ul&gt; |
|`travel_totalvalue`|  &lt;ul&gt;&lt;li&gt;Total value.&lt;/li&gt;&lt;li&gt;The total value of the travel the user wants to embark on.&lt;/li&gt;&lt;/ul&gt; |
|`hct_bpr`|  &lt;ul&gt;&lt;li&gt;Hotel base price.&lt;/li&gt;&lt;li&gt;The base price of the hotel the user wants to book.&lt;/li&gt;&lt;/ul&gt; |
|`hct_tpr`|  &lt;ul&gt;&lt;li&gt;Hotel total price.&lt;/li&gt;&lt;li&gt;The total price, including tax and discounts, of the hotel the user wants to book.&lt;/li&gt;&lt;/ul&gt; |
|`hct_bid`|  &lt;ul&gt;&lt;li&gt;Hotel booking ID.&lt;/li&gt;&lt;li&gt;The ID for the user&#39;s booking.&lt;/li&gt;&lt;/ul&gt; |
|`hct_cid`|  &lt;ul&gt;&lt;li&gt;Hotel check-in date.&lt;/li&gt;&lt;li&gt;The check-in date for the user&#39;s stay.&lt;/li&gt;&lt;/ul&gt; |
|`hct_cod`|  &lt;ul&gt;&lt;li&gt;Hotel checkout date.&lt;/li&gt;&lt;li&gt;The checkout date for the user&#39;s stay.&lt;/li&gt;&lt;/ul&gt; |
|`hct_los`|  &lt;ul&gt;&lt;li&gt;Hotel length of stay.&lt;/li&gt;&lt;li&gt;The total length of the user&#39;s stay.&lt;/li&gt;&lt;/ul&gt; |
|`hct_pid`|  &lt;ul&gt;&lt;li&gt;Hotel partner ID.&lt;/li&gt;&lt;li&gt;The partner ID for the hotel the user wants to book.&lt;/li&gt;&lt;/ul&gt; |
|`hct_pagetype`|  &lt;ul&gt;&lt;li&gt;Hotel page type.&lt;/li&gt;&lt;li&gt;The current page type visible to the user.&lt;/li&gt;&lt;/ul&gt; |

### Product audience - Retail

| Variable           | Description             |
| ------------------ | --------------- |
| `ecomm_prodid`     | &lt;ul&gt;&lt;li&gt;Product ID.&lt;/li&gt;&lt;li&gt;One or more IDs currently visible to or selected by the user.&lt;/li&gt;&lt;/ul&gt;      |
| `ecomm_pagetype`   | &lt;ul&gt;&lt;li&gt;Page type.&lt;/li&gt;&lt;li&gt;The current page type visible to the user.&lt;/li&gt;&lt;li&gt;One of `home`, `searchresults`, `category`, `product`, `cart`, `purchase`, or `other`.&lt;/li&gt;&lt;/ul&gt; |
| `ecomm_totalvalue` | &lt;ul&gt;&lt;li&gt;Total value.&lt;/li&gt;&lt;li&gt;The total value currently associated with the user.&lt;/li&gt;&lt;/ul&gt;            |
| `ecomm_category`   | &lt;ul&gt;&lt;li&gt;Category.&lt;/li&gt;&lt;li&gt;The current category visible to the user.&lt;/li&gt;&lt;/ul&gt;   |

### Product audience - Travel

|Variable| Description|
|---| ---|
|`travel_destid`|  &lt;ul&gt;&lt;li&gt;Destination ID.&lt;/li&gt;&lt;li&gt;The ID for the destination the user has selected.&lt;/li&gt;&lt;/ul&gt; |
|`travel_originid`|  &lt;ul&gt;&lt;li&gt;Origin ID.&lt;/li&gt;&lt;li&gt;The ID for the user&#39;s origin location.&lt;/li&gt;&lt;/ul&gt; |
|`travel_pagetype`|  &lt;ul&gt;&lt;li&gt;Page type.&lt;/li&gt;&lt;li&gt;The current page type visible to the user.&lt;/li&gt;&lt;li&gt;One of `home`, `searchresults`, `offerdetail`, `conversionintent`, `conversion`, `cancel`, or `other`.&lt;/li&gt;&lt;/ul&gt; |
|`travel_startdate`|  &lt;ul&gt;&lt;li&gt;Start date.&lt;/li&gt;&lt;li&gt;The date the user wants to start travel.&lt;/li&gt;&lt;li&gt;Date format is `YYYY-MM-DD`.&lt;/li&gt;&lt;/ul&gt; |
|`travel_enddate`|  &lt;ul&gt;&lt;li&gt;End date.&lt;/li&gt;&lt;li&gt;The date the user wants to end travel.&lt;/li&gt;&lt;li&gt;Date format is `YYYY-MM-DD`.&lt;/li&gt;&lt;/ul&gt; |
|`travel_totalvalue`|  &lt;ul&gt;&lt;li&gt;Total value.&lt;/li&gt;&lt;li&gt;The total value of the travel the user wants to embark on.&lt;/li&gt;&lt;/ul&gt; |

### Product audience - Hotel

|Variable| Description|
|---| ---|
|`hct_base_price`|  &lt;ul&gt;&lt;li&gt;Hotel base price.&lt;/li&gt;&lt;li&gt;The base price of the hotel the user wants to book.&lt;/li&gt;&lt;/ul&gt; |
|`hct_total_price`|  &lt;ul&gt;&lt;li&gt;Hotel total price.&lt;/li&gt;&lt;li&gt;The total price, including tax and discounts, of the hotel the user wants to book.&lt;/li&gt;&lt;/ul&gt; |
| `hct_checkin_date` |  &lt;ul&gt;&lt;li&gt;Hotel check in date.&lt;/li&gt;&lt;li&gt;The check in date for the user&#39;s stay.&lt;/li&gt;&lt;li&gt;Date format is `YYYY-MM-DD`.&lt;/li&gt;&lt;/ul&gt; |
| `hct_checkout_date` |  &lt;ul&gt;&lt;li&gt;Hotel checkout date.&lt;/li&gt;&lt;li&gt;The checkout date for the user&#39;s stay.&lt;/li&gt;&lt;li&gt;Date format is `YYYY-MM-DD`.&lt;/li&gt;&lt;/ul&gt; |
|`hct_length_of_stay`|  &lt;ul&gt;&lt;li&gt;Hotel length of stay.&lt;/li&gt;&lt;li&gt;The total length of the user&#39;s stay.&lt;/li&gt;&lt;/ul&gt; |
|`hct_partner_hotel_id`|  &lt;ul&gt;&lt;li&gt;Hotel partner ID.&lt;/li&gt;&lt;li&gt;The partner ID for the hotel the user wants to book.&lt;/li&gt;&lt;/ul&gt; |
| `hct_booking_ref` |  &lt;ul&gt;&lt;li&gt;Obfuscated booking reference number.&lt;/li&gt;&lt;/ul&gt; |
| `hct_pagetype` |  &lt;ul&gt;&lt;li&gt;Hotel page type.&lt;/li&gt;&lt;li&gt;The current page type visible to the user.&lt;/li&gt;&lt;li&gt;One of `home`, `searchresults`, `property`, `cart`, `purchase`, `cancel`, or `other`.&lt;/li&gt;&lt;/ul&gt; |

## Vendor documentation

* [Microsoft Bing: Tracking sales and other conversions](http://help.bingads.microsoft.com/#apex/3/en/n5012/2)
* [Microsoft Bing: What is UET and how can it help me?](https://help.bingads.microsoft.com/#apex/3/en/56681/0)
* [Microsoft Bing: FAQs](http://help.bingads.microsoft.com/apex/index/3/en-us/53056)