---
title: Google Analytics 4 Measurement Protocol Connector Setup Guide
description: This article describes how to set up the Google Analytics 4 Measurement Protocol connector.
url: https://docs.tealium.com/server-side-connectors/google-analytics-4-measurement-protocol-connector/
---
The Google Analytics 4 Measurement Protocol is intended to augment existing events collected using gtag, GTM, or Firebase. Some event and parameter names are reserved for automatic collection and cannot be sent by the Measurement Protocol. The Google Analytics 4 Measurement Protocol connector can be used to send events to Google Analytics without using gtag, GTM, or Firebase, but only partial reporting may be available. 

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **API Secret (Required)**  
An API Secret generated in the Google Analytics UI. To create a secret, navigate to: **Admin &gt; Data Streams &gt; choose your stream &gt; Measurement Protocol &gt; Create**.
* **Measurement ID (Optional)**  
The measurement ID associated with a stream. Found in the Google Analytics UI under: **Admin &gt; Data Streams &gt; choose your stream &gt; Measurement ID**.
* **Firebase App ID (Optional)**  
The Firebase App ID. The identifier for a Firebase app. Found in the Firebase console under: **Project Settings &gt; General &gt; Your Apps &gt; App ID**.

### Mapping client ID

Client ID is a required parameter for web-based events that uniquely identifies a user instance of a web client.

Google Analytics stores the client ID in a cookie named `_ga`. The format of this cookie is `GA1.2.12349876.1500644855` where the client ID is `12349876.150064485`. You can get the `clientId` value directly from the Google Analytics tracker.

* If you provide a correctly formatted client ID value, the connector uses this value.
* If the event includes the full `_ga` cookie value in the `client_id` mapping, the connector automatically parses and extracts only the client ID portion.
* If `cp.utag_main__ga` is available in the event data, and it contains the client ID in the correct format, the connector automatically maps this value to `client_id`.

### Consent

The connector will not send any consent signals by default. If you don&#39;t specify consent, then Google Analytics will use the consent settings from corresponding online interactions for the client instance. Consent states are either granted or denied when setting consent for `ad_user_data` and `ad_personalization`.

### Event names

Select an event name. Other mappings are dependent on the selected event name, so choose an event first, then apply the related mappings.

For more information and a list of available events, see [Events](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference/events).

* `add_payment_info`
* `add_shipping_info`
* `add_to_cart`
* `add_to_wishlist`
* `begin_checkout`
* `custom_event`
* `campaign_details`
* `earn_virtual_currency`
* `generate_lead`
* `join_group`
* `level_up`
* `login`
* `page_view`
* `post_score`
* `purchase`
* `refund`
* `remove_from_cart`
* `screen_view`
* `search`
* `select_content`
* `select_item`
* `select_promotion`
* `share`
* `sign_up`
* `spend_virtual_currency`
* `tutorial_begin`
* `tutorial_complete`
* `unlock_achievement`
* `view_cart`
* `view_item`
* `view_item_list`
* `view_promotion`
* `view_search_results`

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event (gtag.js) | ✓ | ✓ |
| Send Firebase Event | ✓ | ✓ |
| Send PageView Event (gtag.js) Deprecated | ✓ | ✓ |

The Send PageView Event action is deprecated. Use the Send Event action to send a `page_view` event.

The following section describes how to set up parameters and options for each action.

For more information, see [Google: Send Measurement Protocol events to Google Analytics](https://developers.google.com/analytics/devguides/collection/protocol/ga4/sending-events?client_type=gtag).

### Send Event (gtag.js)

#### Body parameters

| **Parameter** | **Description** |
| --- | --- |
| Client ID | (Required) A unique identifier for a client. For more information, see [Mapping client ID](#mapping-client-id). |
| Measurement ID Override | The identifier for a Google Analytics data stream. Found in the Google Analytics UI under **Admin &gt; Data Streams &gt; choose your stream &gt; Measurement ID**. This setting overrides **Measurement ID**  in the **Configuration** section. |
| API Secret Override | The Measurement Protocol API Secret for the data stream. This setting overrides the **API Secret** in the **Configuration** section. |
| User ID | A unique identifier for a user. |
| Timestamp Micros | A Unix timestamp (in microseconds) for the time to associate with the event.  |
| Non Personalized Ads | Set to `true` to indicate these events should not be used for personalized ads. |
| User Agent | The device user agent for Google Analytics to use to derive device information for the request. |
| IP Override | IP address of the visitor. Use this mapping if you don&#39;t use the geographic mappings. For more information, see [Google Analytics Measurement Protocol: Geographic information](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference?client_type=gtag#payload_geo_info). |

#### Event parameters

| **Parameter** | **Description** |
| --- | --- |
| Achievement ID | The ID of the achievement that was unlocked. |
| Affiliation | A product affiliation to designate a supplying company or brick and mortar store location. |
| Campaign ID | The campaign ID. |
| Campaign | The name used to identify a specific promotion or strategic campaign. |
| Character | The character that achieved the score. |
| Content | The campaign content used for A/B testing and content-targeted ads to differentiate ads or links that point to the same URL. |
| Content Type | The type of selected content. |
| Coupon | The coupon name/code associated with the event. |
| Creative Name | The name of the promotional creative. |
| Creative Slot | The name of the promotional creative slot associated with the event. |
| Currency | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| Custom Event Name | The custom event name. |
| Engagement Time | The amount of time a visitor spends with your web page in focus or app screen in the foreground. |
| Group ID | The ID of the group. |
| Item ID | The identifier for the item that was selected or shared. |
| Item List ID | The ID of the list in which the item was presented to the user. |
| Item List Name | The name of the list in which the item was presented to the user. |
| Item Name | The name of the item the virtual currency is being used for. |
| Level (number) | The level of the character. |
| Location ID | The ID of the location. |
| Medium | The campaign medium. |
| Method | The method used to login/sign up/share. |
| Payment Type | The chosen method of payment. |
| Promotion ID | The ID of the promotion associated with the event. |
| Promotion Name | The name of the promotion associated with the event. |
| Score (number) | The score to post. |
| Screen Class | The class of the screen. |
| Screen Name | The name of the screen being viewed. |
| Search Term | The term that was searched for. |
| Session ID | The timestamp of when a session began. |
| Shipping (number) | Shipping cost associated with a transaction. |
| Shipping Tier | The shipping tier (for example, Ground, Air, Next-day) selected for delivery of the purchased item. |
| Source | The campaign traffic source. |
| Tax (number) | Tax cost associated with a transaction. |
| Term | The campaign term used with paid search to supply the keywords for ads. |
| Transaction ID | The unique identifier of a transaction. |
| Value (number) | The monetary value of the event. |
| Virtual Currency Name | The name of the virtual currency. |
| Session ID | The timestamp of when a session began. |
| Engagement Time | Amount of time someone spends with your web page in focus or app screen in the foreground. |

#### User-provided data

The `User ID` parameter must be set whenever user-provided data is set.

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address that has already been whitespace trimmed, lowercased, and SHA256 hashed. Remove all periods (.) that precede the domain name in `gmail.com` and `googlemail.com` email addresses before hashing. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector will remove all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses, and whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number in E164 format that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will remove all non-digit symbols, prefix the number with a plus sign (`&#43;`), whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: First Name (already SHA256 hashed) | Provide first name that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) | Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: Last Name (already SHA256 hashed) | Provide last name that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Last Name (apply SHA256 hash) | Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: Street Address (already SHA256 hashed) | Provide street address that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Street Address (apply SHA256 hash) | Provide a plain text street address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: City | City of the user&#39;s address. |
| Address Info: State | State code of the user&#39;s address. |
| Address Info: Postal Code | Postal code of the user&#39;s address. |
| Address Info: Country | Two-letter country code in ISO 3166-1 alpha-2 format of the user&#39;s address. |

#### User properties

| **Parameter** | **Description** |
| --- | --- |
| User Properties | User properties describe segments of user base, such as language preference or geographic location. |

#### Items data

| **Parameter** | **Description** |
| --- | --- |
| Item ID | The ID of the item. |
| Item Name | The name of the item. |
| Affiliation | A product affiliation to designate a supplying company or brick and mortar store location. |
| Coupon | The coupon name/code associated with the item. |
| Currency | The currency, in 3-letter ISO 4217 format. |
| Discount | The monetary discount value associated with the item. |
| Index | The index/position of the item in a list. |
| Item Brand | The brand of the item. |
| Item Category | The category of the item. If used as part of a category hierarchy or taxonomy then this will be the first category. |
| Item Category 2 | The second category hierarchy or additional taxonomy for the item. |
| Item Category 3 | The third category hierarchy or additional taxonomy for the item. |
| Item Category 4 | The fourth category hierarchy or additional taxonomy for the item. |
| Item Category 5 | The fifth category hierarchy or additional taxonomy for the item. |
| Item List ID | The ID of the list in which the item was presented to the user. |
| Item List Name | The name of the list in which the item was presented to the user. |
| Item Variant | The item variant or unique code or description for additional item details/options. |
| Location ID | The location associated with the item. We recommend using the Google Place ID that corresponds to the associated item. A custom location ID can also be used. |
| Price | The monetary price of the item, in units of the specified currency parameter. |
| Quantity | Item quantity. |

#### Additional parameters

| **Parameter** | **Description** |
| --- | --- |
| Debug | This connector uses the GA4 debug endpoint by default when using Trace. Map a boolean value to override this behavior. |

#### Consent

| **Parameter** | **Description** |
| --- | --- |
| Ad User Data | Sets consent for sending user data to Google for advertising purposes. |
| Ad Personalization | Sets consent for personalized advertising. |

#### Device information

To provide device information for events in a request, use the user agent, or device-level attributes.
If you map device attributes then the user agent is ignored.

If a request specifies neither device nor user agent, Google Analytics derives device information from tagging events using client ID.

Google recommends providing as many device attributes as possible, with category as the minimum requirement.

| **Parameter** | **Description** |
| --- | --- |
| Category | The category of the device. For example, `desktop`, `tablet`, `mobile`, `smart TV`. |
| Language | The language in ISO 639-1 format. For example, `en` or `en-US`. |
| Screen Resolution | The resolution of the device, formatted as `WIDTHxHEIGHT`. For example, `1280x2856`. |
| Operating System | The operating system or platform. For example, `MacOS`. |
| Operating System Version | The version of the operating system or platform. For example, `13.5`. |
| Model | The model of the device. For example, `Pixel 9 Pro` or `Samsung Galaxy S24`. |
| Brand | The brand of the device. For example, `Google` or `Samsung`. |
| Browser | The brand or type of browser. For example, `Chrome` or `Firefox`. |
| Browser Version | The version of the browser. For example, `136.0.7103.60` or `5.0`. |

#### Geographic information

If you map location attributes, the IP override mapping is ignored.

Google recommends providing as many attributes as possible, with country ID and region ID as a minimum requirement.

For more information, see [Google Analytics Measurement Protocol: Geographic information](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference?client_type=gtag#payload_geo_info).

| **Parameter** | **Description** |
| --- | --- |
| City | The city name of the visitor. |
| Region ID | The ISO 3166 country and subdivision of the visitor. For example, `US-CA`, `US-AR`, `CA-BC`, `GB-LND`, or `CN-HK`. |
| Country ID | The country of the visitor in ISO 3166-1 alpha-2 format. For example, `US`, `AU`, `ES`, or `FR`. |
| Subcontinent ID | The subcontinent of the visitor in UN M49 format. For example, `011`, `021`, `030`, `039`. |
| Continent ID | The continent of the visitor in UN M49 format. For example, `002`, `019`, `142`, `150`. |

### Send Firebase Event

#### Body parameters

| **Parameter** | **Description** |
| --- | --- |
| App Instance ID | (Required) Uniquely identifies a specific installation of a Firebase app. This value needs to be retrieved through the Firebase SDK.  |
| Firebase App ID Override | The identifier for a Firebase app. This setting overrides **Firebase App ID** in the **Configuration** section. |
| API Secret Override | The Measurement Protocol API Secret for the data stream. This setting overrides the **API Secret** in the **Configuration** section. |
| User ID | A unique identifier for a user. |
| Timestamp Micros | A Unix timestamp (in microseconds) for the time to associate with the event. |
| Non Personalized Ads | Set to `true` to indicate these events should not be used for personalized ads. |
| User Agent | The device user agent for Google Analytics to use to derive device information for the request. |
| IP Override | IP address of the visitor. Use this mapping if you don&#39;t use the geographic mappings. For more information, see [Google Analytics Measurement Protocol: Geographic information](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference?client_type=gtag#payload_geo_info). |

For other parameters, see [Send Event (gtag.js)](#send-event-gtagjs).

### Send PageView Event (gtag.js)

The **Send PageView Event** action is deprecated. Use the [Send Event (gtag.js) action](#send-event-gtagjs) to send a `page_view` event.

#### Body parameters

| **Parameter** | **Description** |
| --- | --- |
| Client ID | (Required) A unique identifier for a client. For more information, see [Mapping client ID](#mapping-client-id). |
| Measurement ID Override | The identifier for a Google Analytics data stream. Found in the Google Analytics UI under **Admin &gt; Data Streams &gt; choose your stream &gt; Measurement ID**. This setting overrides **Measurement ID** in the **Configuration** section. |
| API Secret Override | The Measurement Protocol API Secret for the data stream. This setting overrides the **API Secret** in the **Configuration** section. |
| User ID | A unique identifier for a user. See [GA4 Help: User-ID for cross-platform analysis](https://support.google.com/analytics/answer/9213390) for more information on this identifier. Can include only utf-8 characters.|
| Timestamp Micros | A Unix timestamp (in microseconds) for the time to associate with the event. |
| Non Personalized Ads | Set to `true` to indicate these events should not be used for personalized ads. |

#### Event parameters

| **Parameter** | **Description** |
| --- | --- |
| Page Title | The title of the page. |
| Page Location | (Required) The full URL to the page. |

#### User-provided data

The `User ID` parameter must be set whenever user-provided data is set.

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address that has already been whitespace trimmed, lowercased, and SHA256 hashed. Remove all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses before hashing. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector will remove all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses, and whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number in E164 format that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will remove all non-digit symbols, prefix the number with a plus sign (&#43;), whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: First Name (already SHA256 hashed) | Provide first name that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) | Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: Last Name (already SHA256 hashed) | Provide last name that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Last Name (apply SHA256 hash) | Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: Street Address (already SHA256 hashed) | Provide street address that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Street Address (apply SHA256 hash) | Provide a plain text street address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: City | City of the user&#39;s address. |
| Address Info: State | State code of the user&#39;s address. |
| Address Info: Postal Code | Postal code of the user&#39;s address. |
| Address Info: Country | Two-letter country code in ISO 3166-1 alpha-2 format of the user&#39;s address. |

#### User properties

| **Parameter** | **Description** |
| --- | --- |
| User Properties | User properties describe segments of user base, such as language preference or geographic location. |

#### Items data

| **Parameter** | **Description** |
| --- | --- |
| Item ID | The ID of the item. |
| Item Name | The name of the item. |
| Affiliation | A product affiliation to designate a supplying company or brick and mortar store location. |
| Coupon | The coupon name/code associated with the item. |
| Currency | The currency, in 3-letter ISO 4217 format. |
| Discount | The monetary discount value associated with the item. |
| Index | The index/position of the item in a list. |
| Item Brand | The brand of the item. |
| Item Category | The category of the item. If used as part of a category hierarchy or taxonomy then this will be the first category. |
| Item Category 2 | The second category hierarchy or additional taxonomy for the item. |
| Item Category 3 | The third category hierarchy or additional taxonomy for the item. |
| Item Category 4 | The fourth category hierarchy or additional taxonomy for the item. |
| Item Category 5 | The fifth category hierarchy or additional taxonomy for the item. |
| Item List ID | The ID of the list in which the item was presented to the user. |
| Item List Name | The name of the list in which the item was presented to the user. |
| Item Variant | The item variant or unique code or description for additional item details/options. |
| Location ID | The location associated with the item. We recommend that you use the Google Place ID that corresponds to the associated item. A custom location ID can also be used. |
| Price | The monetary price of the item, in units of the specified currency parameter. |
| Quantity |  Item quantity. |

#### Additional parameters

| **Parameter** | **Description** |
| --- | --- |
| Debug | This connector uses the GA4 debug endpoint by default when using Trace. Map a boolean value to override this behavior. |

#### Consent

Consent states are either `granted` or `denied`. If you don&#39;t specify consent, then Google Analytics will use the consent settings from corresponding online interactions for the client instance.

| **Parameter** | **Description** |
| --- | --- |
| Ad User Data | Sets consent for sending user data to Google for advertising purposes. |
| Ad Personalization | Sets consent for personalized advertising. |

## Debug

The Google Analytics 4 Measurement Protocol supplies the following endpoint for validating events:

```none
https://google-analytics.com/debug/mp/collect?
```

The Tealium Google Analytics 4 Measurement Protocol connector uses this endpoint during [Trace](), giving you insights into the validation of the event data. You can view Google Analytics 4 Measurement Protocol validation messages in the HTTP response content of the API call within Trace.