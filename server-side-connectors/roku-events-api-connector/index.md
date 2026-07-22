---
title: Roku Events API Connector Setup Guide
description: This article describes how to set up the Roku Events API connector.
url: https://docs.tealium.com/server-side-connectors/roku-events-api-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Roku API
* API Version: v1
* API Endpoint: `https://events.ads.rokuapi.net`
* Documentation: [Roku API](https://help.ads.roku.com/en/articles/8880744-events-api)

## Batch Limits
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see Batched Actions. Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **API Key**  
  * To generate an API key, go to the settings page within the events tab of Roku Ads Manager.
* **Event Group ID**  
  * An event group is used to represent one online property such as a website or an app or channel. For more information about creating an event group ID, see [Roku: Event Groups](https://help.ads.roku.com/en/articles/9451133-event-groups).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | The type of event. Below are the events supported by Roku:<ul><li>`AD_VIEW` - The Ad views.</li><li>`ADD_PAYMENT_INFO` - Payment information is added in the checkout flow.</li><li>`ADD_TO_CART` - A product is added to the shopping cart.</li><li>`ADD_TO_WISHLIST` - A product is added to a wish list.</li><li>`APP_INSTALL` - A mobile app is installed.</li><li>`COMPLETE_REGISTRATION` - A registration form is completed.</li><li>`CONTACT` - A customer initiates contact with your business through telephone, `SMS`, email, chat, or other contact method.</li><li>`CUSTOMIZE_PRODUCT` - A customer customized a product.</li><li>`DONATE` - A donation is made to your organization or cause.</li><li>`DOWNLOAD` - A download of a doc, info, or service.</li><li>`FIND_LOCATION` - A customer searches for your physical store location through a website or app, with an intention to visit.</li><li>`INITIATE_CHECKOUT` - A customer enters the checkout flow before completion.</li><li>`LEAD` - A customer completes a sign-up form.</li><li>`PAGE_VIEW` - The default number of pixel tracking page visits.</li><li>`PURCHASE` - A purchase or checkout flow is completed.</li><li>`SCHEDULE` - A customer books an appointment to visit one of your locations.</li><li>`SEARCH` - A search query is made.</li><li>`SIGN_UP` - A sign-up event.</li><li>`START_TRIAL` - A free trial is initiated.</li><li>`SUBMIT_APPLICATION` - A customer applies for an offered product, service, or program.</li><li>`SUBSCRIBE` - A customer starts a paid subscription for an offered product or service.</li><li>`SUBSCRIPTION_CANCELLATION` - A customer cancels a paid subscription for a product or service.</li><li>`SUBSCRIPTION_RENEWAL` - A customer renews a paid subscription for a product or service.</li><li>`UNLOCK_ACHIEVEMENT` - A customer unlocks an achievement or a reward.</li><li>`VIEW_CONTENT` - A customer visits a page of interest. For example, a product page or landing page. This event is not specific about the actions on the page. This event can also be used to capture an in-app `VIEW`, whether it's for a particular page or content such as a movie or television show.</li></ul> |

#### Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Time | A UNIX timestamp in epoch seconds when the event occurred. |
| Event Source | The source of the event. Sources include `website`, `phone_call`, and `physical_store`. For a full list of sources, see [Roku: Events API](https://help.ads.roku.com/en/articles/8880744-events-api). |
| Event ID | An ID used by Roku to de-duplicate the same event sent from both server and browser. Verify the ID is unique to one pair of events sent from browser and server. |
| Event Source URL | The page URL where the event originated. |
| Referrer URL | The page URL where the user was directly before landing on the subject URL. |
| Event Type | If unmapped, the connector will send `conversion` as the default. |
| Opt Out | A value of `true` triggers the Limited Data Use flag. For more information, see [Roku: Limited Data Use](https://help.ads.roku.com/en/articles/8766138-limited-data-use). |

#### User Data

| **Parameter** | **Description** |
| --- | --- |
| Email (already SHA256 hashed) | Provide an email address already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email (apply SHA256 hash) | Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number that contains only numeric characters, has been whitespace trimmed, and SHA256 hashed. Remove any leading zeros before hashing. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will remove all non-numeric characters and leading zeroes, whitespace trim, and hash this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Birthdate (already SHA256 hashed) | Provide a birth date (yyyy-mm-dd) already whitespace trimmed, lowercased, and SHA256 hashed. |
| Birthdate (apply SHA256 hash) | Provide a plain text birth date (yyyy-mm-dd) and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |

#### Custom Data

| **Parameter** | **Description** |
| --- | --- |
| Content Category | The category of the page or product in the request. |
| Content IDs | The product IDs associated with the event. |
| Content Name | The name of the page or product. |
| Content Type | Either `product` or `product_group`, depending on the type of content IDs in the request. |
| Product IDs | An array of product IDs. |
| Product Quantity | An array of product quantities. |
| Product Price | An array of product prices. |
| Currency Code | Three letter currency code. For a list of supported currencies, see see [Roku: Events API](https://help.ads.roku.com/en/articles/8880744-events-api). |
| Number of Items | The number of items when checkout was initiatied. |
| Predicted LTV | The predicted lifetime value of a subscriber, as defined by the advertiser and expressed as an exact value. |
| Search String | The string entered by the user for a search event. |
| Status | The status of the order or service. |
| Value | The total value of all products being purchased. |
| Order ID | The order ID of a transaction. |
| Purchase Type | Accepted purchase type values are `first_time_purchase` and `repeat_purchase`. |
| Delivery Category | The type of delivery for a purchase event. Accepted values are `in_store`, `curbside`, and `home_delivery`. |

#### Automatic deduplication

| **Parameter** | **Description** |
| --- | --- |
| Tealium iQ Tag ID | When the Tealium iQ Tag ID is provided, the connector automatically looks for your Event ID value sent from Tealium iQ and sends this value to Roku.  |