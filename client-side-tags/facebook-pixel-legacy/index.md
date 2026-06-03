---
title: Facebook Pixel Setup Guide (Legacy)
description: The Facebook Pixel tag combines the functionality of the Facebook Custom Audiences Pixel and the Conversion Tracking Pixel.
url: https://docs.tealium.com/client-side-tags/facebook-pixel-legacy/
---
This is the legacy version of the tag and will soon be deprecated and replaced with the [Facebook Pixel tag]()

## Prerequisites

* Facebook Ads Account
* Upgraded Facebook Pixel (or legacy Custom Audiences pixel)
* Conversion Pixel (legacy)

## Tag Configuration

First, go to the Tealium tag marketplace and add the Facebook Pixel tag to your profile. For more information, see [Manage Tags]().

The best practice is to configure a single tag instance per pixel ID for standard PageView and event tracking.

After adding the tag, configure the settings described in the following table:

| Setting    | Description    |
|:------|:-----------------|
| Title  | &lt;ul&gt;&lt;li&gt;Enter a unique name to identify the tag&lt;/li&gt;&lt;li&gt;Important if you are adding multiple instances of this tag&lt;/li&gt;&lt;/ul&gt;       |
| Facebook Pixel ID  | &lt;ul&gt;&lt;li&gt;Your Facebook Pixel ID&lt;/li&gt;&lt;li&gt;This appears as a long series of numbers in the code snippet&lt;/li&gt;&lt;li&gt;You may add multiple pixel IDs as a comma-separated list&lt;/li&gt;&lt;li&gt;Example: `fbq(&#39;init&#39;, &#39;12345678901234&#39;)` &lt;/li&gt;&lt;/ul&gt;   |
| Conversion Pixel ID    | &lt;ul&gt;&lt;li&gt;Required only for tracking legacy Conversion Pixel (deprecated)&lt;/li&gt;&lt;li&gt;The ID appears in the code snippet as: &lt;br&gt; `fb_param.pixel_id = &#39;12345&#39;;`&lt;br&gt; OR &lt;br&gt;`fbq(&#39;track&#39;, &#39;12345&#39;) OR fbq.push([&#39;track&#39;, &#39;12345&#39;, { }]);` &lt;/li&gt;&lt;/ul&gt;     |
| Allow Default Page View    | &lt;ul&gt;&lt;li&gt;Triggers the PageView event on all pages &lt;ul&gt;&lt;li&gt;`True`  &lt;ul&gt;&lt;li&gt;Default value&lt;/li&gt;&lt;li&gt;Turns on automatic PageView tracking for non-conversion events&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;`False`  &lt;ul&gt;&lt;li&gt;Turns off PageView triggering when tracking conversion events&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; Tip: If you do not want this default behaviour, you can turn it off using the flag `disablePushState`. When you set this flag to `true`, it will stop sending `PageView` events on history state change.|
| Default Event to Send  | &lt;ul&gt;&lt;li&gt;Select the event you want to trigger by default&lt;/li&gt;&lt;li&gt;This is primarily for use with the Conversion Pixel&lt;/li&gt;&lt;/ul&gt;      |
| Advanced Matching  | &lt;ul&gt;&lt;li&gt;Enables Facebook&#39;s Advanced Matching service. ([Learn more](https://developers.facebook.com/docs/facebook-pixel/pixel-with-ads/conversion-tracking#advanced_match))&lt;/li&gt;&lt;li&gt;This is enabled by default, though customers must add data mappings to enjoy the benefits of Advanced Matching. &lt;/li&gt;&lt;/ul&gt;     |
| Auto calculate number of items | &lt;ul&gt;&lt;li&gt;Choose whether or not to automatically count the items at checkout&lt;/li&gt;&lt;li&gt;Default value is `True`&lt;/li&gt;&lt;/ul&gt;       |
| Enable trackSingle | &lt;ul&gt;&lt;li&gt;Enables the use of trackSingle and trackSingleCustom for Facebook event tracking calls.&lt;/li&gt;&lt;li&gt;These trigger tracking calls only for the pixel IDs configured in this tag in scenarios where multiple Facebook pixels are loaded.&lt;/li&gt;&lt;li&gt;Default value is `True`&lt;/li&gt;&lt;li&gt;Example: `fbq(&#39;trackSingle&#39;, &#39;FB_PIXEL_ID&#39;, &#39;Purchase&#39;, customData )` &lt;br&gt; - OR - &lt;br&gt; `fbq(&#39;trackSingleCustom&#39;, &#39;FB_PIXEL&#39;)` &lt;/li&gt;&lt;/ul&gt;    |
| Enable trackCustom | &lt;ul&gt;&lt;li&gt;Enables the use of `trackCustom` for Facebook event tracking calls.&lt;/li&gt;&lt;li&gt;You can track custom events by calling the `fbq(&#39;trackCustom&#39;)` pixel function, with your custom event name and (optionally) a JSON object as its parameters.&lt;/li&gt;&lt;li&gt;Example: To track visitors who share a promotion to get a discount, you could track them using the custom shown in the following example: `fbq(&#39;trackCustom&#39;,&#39;ShareDiscount&#39;,{promotion:&#39;share_discount_10%&#39;});` &lt;/li&gt;&lt;/ul&gt; |

## Load Rules

[Load rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule:

* For tracking standard PageView and events, use the default **All Pages** rule
* For tracking legacy Conversion Pixel, apply custom rule conditions to load the tag on specific conversion pages.

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable]() to the corresponding destination variable of the vendor tag.The destination variables for the Facebook Pixel tag are built into the Data Mapping tab. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).The following sections describe available categories:

### **Standard**

Use these mappings to override the tag configuration settings. This can be useful if you want to set values dynamically based on your data layer.

| Destination Name    | Destination Variable | Description     |
|:----|:--|:-----------|
| Facebook Pixel ID   | `cust_pixel` | Numeric identifier(s) of the Facebook Pixel     |
| Conversion Pixel ID | `conv_pixel` | Numeric identifier of the legacy conversion pixel   |
| Allow Init Page View [`true`/`false`]   | `page_view`  | &#39;init&#39; track call   |
| List of Events to fire  | `evt_list`   | Events listed either as comma-separated values or an array in your variable     |
| Enable trackSingle [`true`/false]   | `track_single`   | &lt;ul&gt;&lt;li&gt;Enables use of `trackSingle` and `trackSingleCustom` for event tracking.&lt;/li&gt;&lt;li&gt;Restricts event tracking to the pixel ID(s) added to the Facebook Pixel configuration in Tealium iQ in situations where multiple Facebook pixels are loaded.&lt;/li&gt;&lt;/ul&gt; |
| Enable trackCustom&lt;br&gt; [`true`/`false`] | `track_custom`   | &lt;ul&gt;&lt;li&gt;Enables the use of `trackCustom` for Facebook event tracking calls.&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Custom event names must be strings, and cannot exceed 50 characters in length.&lt;/li&gt;&lt;/ul&gt;  |

### **Advanced Matching**

With this additional data, you can report and optimize your ads for more conversions and build larger re-marketing audiences. You can pass the customer identifiers that you collect from your website during the check-out, account sign-in or registration process as parameters in the pixel.

In Advanced Matching, the case of the term entered is normalized unless the item to be matched is already recognized.

| Destination Name | Destination Variable | Description   |
|:------|:--|:------|
| Email    | `em` | Email |
| First Name   | `fn` | First name    |
| Last Name    | `ln` | Last name |
| Phone Number | `ph` | Numeric value of phone number |
| Gender   | `ge` | `f` or `m`    |
| Date of Birth    | `db` | [ `yyyymmdd`] |
| City | `ct` | City  |
| State    | `st` | 2-letter code |
| Zip  | `zp` | Zipcode   |

### **E-Commerce**

Since the Facebook Pixel tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension]() mappings. Manually mapping in this category is not needed unless you want to override any extension mappings or an e-commerce variable is not offered in the extension.

| Destination Name  | Destination Variable | Description    | E-Commerce Extension Variable |
|:---|:--|:---|:------|
| Order ID  | `order_id`   | Unique identifier assigned to the final order  | `_corder` |
| Sub Total | `sub_total`  | Sub total amount of the final order    | `_csubtotal`  |
| Currency  | `order_currency` | Currency used in the payment   | `_ccurrency`  |
| List of Product IDs   | `product_id` | Unique identifier of each product in the product array | `_cprod`  |
| List of Product Names | `product_name`   | Name of each product in the product array  | `_cprodname`  |
| List of Categories    | `product_category`   | Category of each product in the product array  | `_ccat`   |
| List of Prices    | `product_unit_price` | Unit price of each product in the product array    | `_cprice` |

### Limited Data Use

| Variable  | Description  |
|:---|:---------|
| `lmt_data.use_ldu` (Use LDU)  | &lt;ul&gt;&lt;li&gt;If `true`, use Facebook’s Limited Data Use option &lt;/li&gt;&lt;li&gt;If `false`, do not use Facebook’s Limited Data Use option&lt;/li&gt;&lt;/ul&gt;  |
| `lmt_data.ldu_types.geolocate` (LDU should Geolocate) | &lt;ul&gt;&lt;li&gt;If `true`, the LDU geolocates the user.&lt;/li&gt;&lt;li&gt;If `false`, the LDU does not geolocate the user. If **Use LDU** is enabled, then **LDU should Geolocate** is also enabled by default.&lt;/li&gt;&lt;/ul&gt; |
| `lmt_data.ldu_types.california` (LDU is California)   | &lt;ul&gt;&lt;li&gt;If `true`, sets the state and country California-specific values inside the template. Only enable this option if the user is located in California and needs to be processed with Limited Data Use.&lt;/li&gt;&lt;li&gt;If `false`, does not set the user’s state and country California-specific values inside the template.&lt;/li&gt;&lt;/ul&gt; |

## **Events**

Map to these destinations for triggering specific events on a page. Events are used for tracking conversions and building targetable audiences for your Facebook ads.

The Purchase event is automatically triggered when an Order ID value is available, either through the E-Commerce extension or a direct data mapping.

Use the following steps to map an event:

1. In the **Trigger** field, enter the value of the variable you are mapping to the destination that corresponds to the event selected.  
For example, if you want to trigger the **Purchase** event when `event_name=&#34;order&#34;` is in your UDO, you would enter `order` (assuming you are currently mapping the variable `event_name`).
1. In the **Event** list, select the event you want (for example, **Purchase**).
1. Click **&#43; Add.**

### **Custom Events**

For custom events, select **Custom** and enter a name for the custom event.

In this following example the custom event &#34;InboundLead&#34; will be triggered when the variable `event_name` equals `inbound_lead_event`.

![](/images/client-side-tags/custom-event.png)

To edit a custom event, single click on the destination input field to edit the event name directly. The values are entered in the form: `{VARIABLE_VALUE}:{DESTINATION_EVENT}`.

* The left-side of the colon is the variable value that will trigger the event, such as `inbound_lead_event`
* The right-side of the colon is the custom event name, such as `InboundLead`.

### **Custom Event Data**

Map to these destinations if you want to pass a custom parameter with a custom Event that you mapped in the [Events tab](#events_tab).

Use the following steps to map a Custom Event Data variable:

1. In the **Event Name** field, enter the name of the custom event exactly as specified in the **Events** tab.
1. In the **Parameter** field, enter the name of the parameter you want to send.
1. Click **&#43; Add**.

### Full List of Standard Events

| Destination Event    | Event Description    |
|:--|:------|
| AddPaymentInfo   | Visitor adds payment details during the checkout process     |
| AddToCart    | Visitor adds an item to the cart     |
| AddToWishlist    | Visitor adds an item to the wish list     |
| CompleteRegistration | &lt;ul&gt;&lt;li&gt;Visitor completes a registration form&lt;/li&gt;&lt;li&gt;Example: visitor successfully subscribes to a newsletter&lt;/li&gt;&lt;/ul&gt; |
| Contact  | When a person initiates contact with your business through telephone, SMS, email, chat, or other method. |
| Conversion   | For legacy Conversion Pixel only; requires the Conversion Pixel ID to be set |
| Custom   | &lt;ul&gt;&lt;li&gt;Visitor action is treated as a custom event&lt;/li&gt;&lt;li&gt;Can be used for reporting custom audiences and custom conversions&lt;/li&gt;&lt;/ul&gt;  |
| CustomizeProduct | When a person customizes a product.  |
| InitiateCheckout | &lt;ul&gt;&lt;li&gt;Visitor takes the first step to begin checkout process&lt;/li&gt;&lt;li&gt;Example: visitor clicks **Go to Checkout** button&lt;/li&gt;&lt;/ul&gt;   |
| Lead | &lt;ul&gt;&lt;li&gt;Visitor action indicates his or her buying intent&lt;/li&gt;&lt;li&gt;Example: visitor signup for a trial product&lt;/li&gt;&lt;/ul&gt;  |
| PageView | Visitor views any page on your site  |
| Purchase | Visitor successfully completes the last step in the checkout process&lt;br&gt; Note: This event is required for tracking conversions; make sure to map it in the **Events** Tab |
| Schedule | When a person books an appointment to visit one of your locations.   |
| Search   | Visitor performs a search action     |
| StartTrial   | When a person starts a free trial of a product or service you offer. |
| SubmitApplication    | When a person applies for a product, service, or program you offer.  |
| Subscribe    | When a person applies to start a paid subscription for a product or service you offer.   |
| ViewContent  | Visitor views a specific page, indicating their browsing intent  |

## Parameters

Map to these destinations if you want to pass additional data with the event(s) that you mapped earlier.

Parameters are only used with pre-defined events. See the [Custom Event Data](#custom-event-data) section to learn how to pass a parameter with a custom event.

Use the following steps to pass a parameter with a predefined event:

1. In the **Event** field, select a Facebook event from the drop-down list.
1. In the **Parameter** field, select a Facebook parameter from the drop-down list.
For a **Custom** parameter, enter a name to identify the parameter.
1. Click **&#43; Add**.

### Full List of Predefined Parameters

| Destination Parameter | Description   |
|:---|:---|
| Value | Value associated with the event   |
| Currency  | Currency associated with the Value parameter  |
| Content Name  | Name of the product or page   |
| Content Type  | Type of the product or page associated with the event |
| Content IDs   | Any identifier(s) associated with the event   |
| Content Category  | Category of the product or page   |
| Number of Items   | Number of items at checkout   |
| Search String | Keyword/term used in the search action    |
| Order ID  | Unique identifier of the final order  |
| Status    | Status of the CompleteRegistration event  |
| Custom    | Custom parameter to be passed with a predefined Event |

### **Hotel Parameters**

Map to the destinations listed in the following table to send hotel-related search and hotel booking details with the event(s) you mapped earlier.

#### Full List of Hotel Parameters

| Parameter  | Description|
|:------|:-----|
| Content Type   | &lt;ul&gt;&lt;li&gt;(Required) Type of the product or page associated with the hotel.&lt;/li&gt;&lt;/ul&gt; Note: Ensure that the variable value equals `hotel`. |
| Content IDs    | &lt;ul&gt;&lt;li&gt;(Required) Unique identifier(s) associated with the hotel.&lt;/li&gt;&lt;/ul&gt;|
| Destination    | &lt;ul&gt;&lt;li&gt;(Required) String value describing the city, state, or country where the hotel is located. Example: `San Fransisco`.&lt;/li&gt;&lt;/ul&gt;|
| Check-in Date  | &lt;ul&gt;&lt;li&gt;(Required) The date on which the visitor will be checking in to the hotel&lt;/li&gt;&lt;li&gt;Corresponds to timezone of the hotel&lt;/li&gt;&lt;li&gt;The following date formats are supported:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt;&lt;/li&gt;&lt;/ul&gt; |
| Check-out Date | &lt;ul&gt;&lt;li&gt;(Required) The date on which the visitor will be checking out of the hotel&lt;/li&gt;&lt;li&gt;Corresponds to timezone of the hotel&lt;/li&gt;&lt;li&gt;The following date formats are supported:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt;  &lt;/li&gt;&lt;/ul&gt;    |
| Value  | &lt;ul&gt;&lt;li&gt;(Required) Relative value of the event to the advertiser&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Required for the Purchase event&lt;/li&gt;&lt;/ul&gt;|
| Currency   | &lt;ul&gt;&lt;li&gt;(Required) Currency associated with the Value parameter&lt;/li&gt;&lt;li&gt;Required for the Purchase event&lt;/li&gt;&lt;/ul&gt;|

#### Optional Hotel Parameters

| Parameter  | Description   |
|:--|:-------|
| City   | &lt;ul&gt;&lt;li&gt;(Optional) City where the hotel is located&lt;/li&gt;&lt;/ul&gt;    |
| Region | &lt;ul&gt;&lt;li&gt;(Optional) State/District where the hotel is located&lt;/li&gt;&lt;/ul&gt;  |
| Country    | &lt;ul&gt;&lt;li&gt;(Optional) Country where the hotel is located&lt;/li&gt;&lt;/ul&gt; |
| Number of Adults   | &lt;ul&gt;&lt;li&gt;(Optional) Number of adults specified in the booking/search&lt;/li&gt;&lt;/ul&gt;   |
| Number of children | &lt;ul&gt;&lt;li&gt;(Optional) Number of children specified in the booking/search&lt;/li&gt;&lt;/ul&gt; |
| Suggested Hotels   | &lt;ul&gt;&lt;li&gt;(Optional) Identifiers of other hotels recommended for the visitor&lt;/li&gt;&lt;/ul&gt;    |
| User Score | &lt;ul&gt;&lt;li&gt;(Optional) Relative value of the visitor to the advertiser&lt;/li&gt;&lt;li&gt;Must contain a numerical value&lt;/li&gt;&lt;/ul&gt; |
| Hotel Score    | &lt;ul&gt;&lt;li&gt;(Optional) Relative value of the hotel to the advertiser&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Must contain a numerical value&lt;/li&gt;&lt;/ul&gt; |
| Purchase Currency  | &lt;ul&gt;&lt;li&gt;(Optional) Currency associated with the hotel booking transaction&lt;/li&gt;&lt;/ul&gt; |

#### Optional Hotel Parameters for Search Events Only

| Parameter   | Description    |
|:----|:-----|
| Preferred Star Ratings  | &lt;ul&gt;&lt;li&gt;(Optional) Search criteria is filtered by the hotel&#39;s star ratings&lt;/li&gt;&lt;/ul&gt; |
| Preferred Price Range   | &lt;ul&gt;&lt;li&gt;(Optional) Search criteria is filtered by room rates&lt;/li&gt;&lt;/ul&gt;   |
| Preferred Neighborhoods | &lt;ul&gt;&lt;li&gt;(Optional) Search criteria is filtered by location neighborhood&lt;/li&gt;&lt;/ul&gt;    |

### **Journey Parameters**

Map to the destinations listed in the following table to send visitor&#39;s travel details (flight or route journey) with the event(s) you mapped earlier.

#### Full List of Journey Parameters

| Parameter    | Description|
|:----|:-----------|
| Content Type | &lt;ul&gt;&lt;li&gt;(Required) Indicates whether the journey type is flight or non-flight&lt;/li&gt;&lt;/ul&gt; Note: The variable value must equal `flight` for flight journeys and `route` for non-flight journeys.|
| Origin   | &lt;ul&gt;&lt;li&gt;(Required) String value describing the city, state, or country where the journey begins.&lt;/li&gt;&lt;li&gt;Example: `San Fransisco, California, USA`.&lt;/li&gt;&lt;/ul&gt;|
| Destination  | &lt;ul&gt;&lt;li&gt;(Required) String value describing the destination city, state, or country.&lt;/li&gt;&lt;li&gt;Example: `Toronto, Ontario, Canada`.&lt;/li&gt;&lt;/ul&gt;|
| Departing Departure Date | &lt;ul&gt;&lt;li&gt;(Required) Date and time when the outbound journey begins&lt;/li&gt;&lt;li&gt;The following date formats are supported:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| Returning Departure Date | &lt;ul&gt;&lt;li&gt;(Required) Date and time when the return journey begins&lt;/li&gt;&lt;li&gt;The following date formats are supported:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;   |
| Value    | &lt;ul&gt;&lt;li&gt;(Required) Relative value of the event to the advertiser&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Required for the Purchase event&lt;/li&gt;&lt;/ul&gt;|
| Currency | &lt;ul&gt;&lt;li&gt;(Required) Currency associated with the Value parameter&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Required for the Purchase event&lt;/li&gt;&lt;/ul&gt;|

#### Required Flight Parameters

The following parameters are **required** when the `content type` value equals `flight`:

| Parameter   | Description|
|:--|:--------|
| Origin Airport  | &lt;ul&gt;&lt;li&gt;(Required) [IATA](https://en.wikipedia.org/wiki/International_Air_Transport_Association_airport_code) code (the three-letter airport identifier) of the origin airport&lt;/li&gt;&lt;/ul&gt;  |
| Destination Airport | &lt;ul&gt;&lt;li&gt;(Required) [IATA](https://en.wikipedia.org/wiki/International_Air_Transport_Association_airport_code) code (the three-letter airport identifier) of the destination airport&lt;/li&gt;&lt;/ul&gt; |

#### Optional Journey Parameters

| Parameter  | Description|
|:----|:------------|
| Origin City    | &lt;ul&gt;&lt;li&gt;(Optional) Name of the city where the journey begins&lt;/li&gt;&lt;/ul&gt;|
| Origin Region  | &lt;ul&gt;&lt;li&gt;(Optional) Name of the state/region where the journey begins&lt;/li&gt;&lt;/ul&gt;|
| Origin Country | &lt;ul&gt;&lt;li&gt;(Optional) Name of the country where the journey begins&lt;/li&gt;&lt;/ul&gt;|
| Destination City   | &lt;ul&gt;&lt;li&gt;(Optional) Name of the destination city&lt;/li&gt;&lt;/ul&gt;|
| Destination Region | &lt;ul&gt;&lt;li&gt;(Optional) Name of the destination state/region&lt;/li&gt;&lt;/ul&gt;|
| Destination Country    | &lt;ul&gt;&lt;li&gt;(Optional) Name of the destination country&lt;/li&gt;&lt;/ul&gt;|
| Departing Arrival Date | &lt;ul&gt;&lt;li&gt;(Optional) Date and time on which the visitor arrives at their destination&lt;/li&gt;&lt;li&gt;The following date formats are supported:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;|
| Returning Arrival Date | &lt;ul&gt;&lt;li&gt;(Optional) Date and time on which the visitor returns to the origin, completing the journey&lt;/li&gt;&lt;li&gt;The following date formats are supported:&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;|
| Number of Adults   | &lt;ul&gt;&lt;li&gt;(Optional) Number of adults in the travel&lt;/li&gt;&lt;/ul&gt;|
| Number of children | &lt;ul&gt;&lt;li&gt;(Optional) Number of children in the travel&lt;/li&gt;&lt;/ul&gt;|
| Number of Infants  | &lt;ul&gt;&lt;li&gt;(Optional) Number of infant babies in the travel&lt;/li&gt;&lt;/ul&gt;|
| Travel Class   | &lt;ul&gt;&lt;li&gt;(Optional) Indicates the type of class the visitor will be travelling in.&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;For `flight` journey, the variable should contain enum values such as `economy`, `premium`, `business`, `first`.&lt;/li&gt;&lt;li&gt;For `route` journey, the variable should contain a custom string value.&lt;/li&gt;&lt;li&gt;Example: `Economy`&lt;/li&gt;&lt;/ul&gt; |
| User Score | &lt;ul&gt;&lt;li&gt;(Optional) Relative value of the visitor to the advertiser&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Must contain a numerical value&lt;/li&gt;&lt;/ul&gt;|
| Purchase Value | &lt;ul&gt;&lt;li&gt;(Optional) Price of the travel booking&lt;/li&gt;&lt;li&gt;Recommended for Purchase and InitiateCheckout events.&lt;/li&gt;&lt;/ul&gt;|
| Purchase Currency  | &lt;ul&gt;&lt;li&gt;(Optional) Currency used in the booking transaction&lt;/li&gt;&lt;/ul&gt;|

#### Optional Journey Parameters for Search Events Only

| Parameter | Description|
|:----|:-------|
| Preferred Number of Stops | &lt;ul&gt;&lt;li&gt;(Optional) Search criteria is filtered by the number of stopovers&lt;/li&gt;&lt;li&gt;Set the variable value to `0` for direct flights and `1` if the visitor has specified the number of stopovers.&lt;/li&gt;&lt;/ul&gt; |

## Use Cases

This section provides use cases that represent real-life scenarios.

### Use Case: Tracking PageView and Standard/Custom Events

Set the PageView event to be fired automatically on all pages and trigger all non-conversion with mappings.

Use the following steps to set up this use case for your environment:

1. Configure the following settings:
    * **Pixel ID**: `FB_PIXEL_ID`
    * **Allow Default Page view:** `True`
    * **Default Event to Send**: `None`

1. Load the tag on all pages (default rule).
1. Map the variable `event_name` to the non-conversion event(s) of choice.

### Use Case: Tracking PageView and Conversion Event (Deprecated)

Triggering a conversion event requires the Conversion Pixel ID. You may do this in the same tag instance you are using for tracking PageView and non-conversion events.

Use the following steps to set up this use case for your environment:

1. Configure the following settings:
    * **Pixel ID**: `FB_PIXEL_ID`
    * **Conversion Pixel ID**: `CONVERSION_PIXEL_ID`
    * **Allow Default Page view**: `True`
    * **Default Event to Send**: `None`
1. Load the tag on all pages (default rule).
1. Map the variable `event_name` to the conversion event(s) of choice.

### Use Case: Tracking Legacy Conversion Pixel Only (Deprecated)

The Conversion Pixel needs to be tracked in a separate tag instance. In this tag instance, leave the Pixel ID blank and disable automatic pageview tracking. Because you are not tracking specific events, no data mappings are required.

Use the following steps to set up this use case for your environment:

1. Configure the following settings:
    * **Conversion Pixel ID**: `CONVERSION_PIXEL_ID`
    * **Allow Default Page view**: `False`
    * **Default Event to Send**: `Conversion`

1. Apply custom load rules to load this tag on specific conversion pages.

### Use Case: Multiple Pixels on A Single Page

The following use cases represent scenarios that can be used for multiple pixels on a single page:

* **Shared Event Tracking**
  * If you want multiple Facebook Pixels to share pageview and event tracking, you can add a comma-separated list of those pixel IDs to the Facebook Pixel ID field in the tag configuration settings.
  * Having several Facebook Pixels with their own pixel IDs may share event tracking with other Facebook Pixels on the page if their Enable trackSingle setting is `false`, although this may result in inconsistent tracking behavior and is not recommended.

* **Individual Event Tracking**
  * If you are loading more than one Facebook Pixel on a single page, and you want to keep the tracking events from being recorded for all of the pixels on that page, then make sure the **Enable trackSingle** setting is `true`.
  * This setting will fire event tracking only for the pixel IDs added for that tag.
  * If your Facebook Pixel in Tealium iQ was added before March of 2018, you may not be able to take advantage of the trackSingle feature.
    * In this case, [update your Facebook tag template]() to the latest version. Note that the trackSingle setting is set to `true` as default.
    * You must map to `track_single` and set the value to `false` to override and disable this feature.

* **Versions that predate March 2018**
  * If you added your tag after March of 2018, refer to the use cases above when setting up multiple Facebook pixels
  * Older versions of the Facebook Pixel were not designed to be [loaded more than once on a single page](https://www.facebook.com/business/help/community/question/?id=10100525729830570).
  * The Facebook JavaScript library initializes a single instance of the `fbq` object, which is used for all tracking that occurs on the page (thus reusing the same pixel ID).
  * If you require more than one Facebook pixel, each with a different pixel ID, to be fired on a single page, and you are unable to update the tag template, then we recommend implementing the `&lt;noscript&gt;` version of the pixel using the [Tealium Generic tag]().

#### Example Scenario

Example of Facebook Pixel `&lt;noscript&gt;` code:

```
`&lt;noscript&gt;&lt;br&gt;
&lt;img height=&#34;1&#34; width=&#34;1&#34; style=&#34;display:none&#34;&lt;br&gt;
 src=&#34;https://www.facebook.com/tr?id={{FACEBOOK_PIXEL_ID}}&amp;ev=PageView&amp;noscript=1&#34;&lt;br&gt;
/&gt;&lt;br&gt;
&lt;/noscript&gt;`
```

In this scenario, the URL of the hidden image pixel can be configured as follows:

1. Add the Tealium Generic tag.
1. Set the **Title** to `Facebook Pixel (custom)`.
1. Set the **Base URL** to `https://www.facebook.com/tr`
1. Set the **Query String** to `id={{FACEBOOK_PIXEL_ID}}&amp;ev=PageView&amp;noscript=1&#34;`.  
![](/images/client-side-tags/facebook-tag-generic-tag-pixel.png)

1. Set the load rules and data mappings you want.
1. Click **Apply**.

## Facebook Dynamic Ads for Tealium iQ

For additional information about how to set up Facebook Dynamic Ads in Tealium iQ, see the TLC article [How to Set up Facebook Dynamic Ads in Tealium iQ](/client-side-tags/facebook-dynamic-ads-tag/).

## Vendor Documentation

See the following vendor documentation for more information:

* [Migrating from Deprecated Pixels](https://developers.facebook.com/docs/facebook-pixel/pixel-migration)
* [Reference: Standard and Custom Events](https://developers.facebook.com/docs/facebook-pixel/api-reference#events)
* [The Facebook Pixel FAQ](https://www.facebook.com/business/help/651294705016616)
* [Advertiser Help Center: Using Facebook Pixel with Tealium](https://www.facebook.com/business/help/978910435507261)
* [Conversion Tracking with the Pixel](https://developers.facebook.com/docs/facebook-pixel/pixel-with-ads/conversion-tracking#advanced_match)
