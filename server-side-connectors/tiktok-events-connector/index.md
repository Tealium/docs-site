---
title: TikTok Events Connector Setup Guide
description: This article describes how to set up the TikTok Events connector.
url: https://docs.tealium.com/server-side-connectors/tiktok-events-connector/
---
## API information

This connector uses the following vendor API:

* API Name: TikTok HTTP API
* API Version: v1.3 (Events 2.0)
* API Endpoint: `https://business-api.tiktok.com/open_api/v1.3/event/track/`
* Documentation: [TikTok Events 2.0](https://business-api.tiktok.com/portal/docs?id=1771101303285761)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 50
* Maximum time since oldest request: 5 minutes
* Maximum size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Access Token**: The Access Token that is configured in TikTok.
* **Pixel ID**: If a TikTok pixel is already integrated for the website, use the existing pixel code. Log in to your TikTok Ads Manager account to find the `pixel_code`. Create one pixel per website.

## Deduplication
 
To configure this connector to receive event IDs from the TikTok Pixel tag in your Tealium iQ Tag Management account, look for event attributes using the following naming convention:

```nohl
tiktok_event_id_&lt;TIKTOK_EVENT&gt;_&lt;TAG_UID&gt;
```

For example, an event from a tag with a UID of `174` sends the following attribute:

```nohl
tiktok_event_id_Checkout_174
```

Find your tag UID in the Tealium iQ **Tags** table or the tag details screen:

![](/images/server-side-connectors/tiktok-pixel-uid.png)

For each event ID that matches this event ID format, configure a separate action. Map the event-specific event ID attribute to `Event ID` and map the corresponding event name to `Event Name`.

For example:

| Tealium Attribute/Value | TikTok Parameter |
|-------|------|
| `tiktok_event_id_Checkout_174` | Event ID |
| `Checkout` (Custom Text) | Event Name |

For more information, see [TikTok Pixel Tag Setup Guide]().

### Automatic deduplication

If multiple events with the same event source ID (`event_source_id`), event type (for example, `AddToCart`), and event ID (`event_id`) are received, TikTok uses the first event and discards any later events received within forty-eight hours of the first event.

If a later event is received within five minutes of the first event, TikTok merges its data into the first event. For example, if the first event does not include user email (`user.email`) but a later duplicate event (received within five minutes) contains this information, TikTok merges the email data into the first event.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Track Event | ✓ | ✓ |

Use the Track endpoint to report App, Web, Offline, or CRM events.

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Send Track Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Event Source | Select the event source. Possible values are: &lt;ul&gt;&lt;li&gt;`WEB`&lt;/li&gt;&lt;li&gt;`APP`&lt;/li&gt;&lt;li&gt;`OFFLINE`&lt;/li&gt;&lt;li&gt;`CRM`&lt;/li&gt;&lt;/ul&gt; |
| Event Type | The conversion event name. Possible values are: &lt;ul&gt;&lt;li&gt;`Achieve a Level`&lt;/li&gt;&lt;li&gt;`Add Payment Information`&lt;/li&gt;&lt;li&gt;`Add to Cart`&lt;/li&gt;&lt;li&gt;`Add to Wishlist`&lt;/li&gt;&lt;li&gt;`Check Out`&lt;/li&gt;&lt;li&gt;`Click Button`&lt;/li&gt;&lt;li&gt;`Complete Payment`&lt;/li&gt;&lt;li&gt;`Complete Registration`&lt;/li&gt;&lt;li&gt;`Complete the Tutorial`&lt;/li&gt;&lt;li&gt;`Contact`&lt;/li&gt;&lt;li&gt;`Create a Group`&lt;/li&gt;&lt;li&gt;`Create a Role`&lt;/li&gt;&lt;li&gt;`Custom`&lt;/li&gt;&lt;li&gt;`Download`&lt;/li&gt;&lt;li&gt;`Generate a Lead`&lt;/li&gt;&lt;li&gt;`Initiate Checkout`&lt;/li&gt;&lt;li&gt;`Install the App`&lt;/li&gt;&lt;li&gt;`In-app AD Click`&lt;/li&gt;&lt;li&gt;`In-app AD Impression`&lt;/li&gt;&lt;li&gt;`Join a Group`&lt;/li&gt;&lt;li&gt;`Launch the App`&lt;/li&gt;&lt;li&gt;`Load an Application`&lt;/li&gt;&lt;li&gt;`Loan is Approved`&lt;/li&gt;&lt;li&gt;`Loan is Disbursed`&lt;/li&gt;&lt;li&gt;`Log in Successfully`&lt;/li&gt;&lt;li&gt;`Place an Order`&lt;/li&gt;&lt;li&gt;`Purchase`&lt;/li&gt;&lt;li&gt;`Rate`&lt;/li&gt;&lt;li&gt;`Search`&lt;/li&gt;&lt;li&gt;`Spend Credits`&lt;/li&gt;&lt;li&gt;`Start the Trial`&lt;/li&gt;&lt;li&gt;`Submit Form`&lt;/li&gt;&lt;li&gt;`Subscribe`&lt;/li&gt;&lt;li&gt;`Unlock an Achievement`&lt;/li&gt;&lt;li&gt;`View Content`&lt;/li&gt;&lt;/ul&gt; |
| Event Source ID | (Required) An ID to track events. &lt;ul&gt;&lt;li&gt;If `event_source` is `web`, specify a pixel code in this field.&lt;/li&gt;&lt;li&gt;If `event_source` is `offline`, specify an offline event ID in this field.&lt;/li&gt;&lt;li&gt;If `event_source` is `app`, specify a TikTok App ID in this field.&lt;/li&gt;&lt;li&gt;If `event_source` is `crm`, specify a CRM event  ID in this field. To obtain a CRM event ID, use `/crm/list/`.&lt;/li&gt;&lt;/ul&gt;|
| Event Time  | (Required) The timestamp when the event took place in Unix epoch format, measured in seconds. If you do not provide a timestamp, the connector uses the current timestamp. |
| Custom Event Name | The custom event name. Required when choosing **Custom** from the **Event Type** drop-down. |
| Pixel ID Override  | Pixel ID that can be found in the **TikTok Events Manager**. This setting overrides **Pixel ID** used in the **Configuration** section. |
| Access Token Override | A custom access token to override the value in the configuration. |
| Event ID  | Any hashed ID that can identify a unique user or session. For example, `SessionID_RandomNumber`. If you set [Generate Event ID in the TikTok Pixel tag]() to `true`, this ID is automatically generated for every TikTok tracking event. |
| Limited Data Use | This field is only supported when the Event Source is `WEB` or `APP`. Limited data processing setting. To learn more about the Limited Data Use Feature, see [TikTok: Limited Data Use](https://business-api.tiktok.com/portal/docs?id=1771101204435970). |
| Test Event Code | Send test events to exclude them from production data in TikTok Events Manager (`TTEM`). Retrieve the `test_event_code` in the `Test Events` tab of `TTEM`. |

#### Ad Data

| Parameter | Description |
| --- | --- |
| Callback | The value of `ttclid` used to match website visitor events with TikTok ads. |
| Campaign ID  | The campaign ID.  |
| Ad ID  | The ad group ID.  |
| Creative ID | The Ad ID. |
| Is Retargeting   | Whether the user is retargeting a user.  |
| Attributed | Whether the event is attributed to a provider.  |
| Attribution Type   | The type of attribution.  |
| Attribution Provider   | The attribution provider name.  |

#### Page Data

| Parameter | Description |
| --- | --- |
| Referrer | Page referrer. |
| URL | Page URL when the event happened. |

#### User Data

| Parameter | Description |
| --- | --- |
| User Email | Recommended. The user&#39;s email address, hashed with SHA256. |
| User Phone Number | Recommended. The user&#39;s phone number, hashed with SHA256. Include country code with `&#43;` and remove any other characters (spaces, `-`) between numbers (for example, for the USA: `&#43;12125551212`). If the country code is `86`, do not include country code (for example: `13800000000`). |
| User External ID | Recommended. The external user ID, hashed with SHA256. |
| Cookie ID  | The ID of the cookie.  |
| IP | The non-hashed public IP address of the browser. To increase the probability of matching website visitor events with TikTok ads, we recommend sending both **IP** and **User Agent**. |
| User Agent | The non-hashed user agent from the user&#39;s device. To increase the probability of matching website visitor events with TikTok ads, we recommend sending both **IP** and **User Agent**. Unless you disable automapping, this parameter is automapped to the **User Agent** of the visitor. |
| IDFA |  The iOS identifier for advertisers. |
| IDFV |  The iOS identifier for vendors. |
| GAID |  The Google Advertising ID.|
| Locale | The locale language and locale in `la-CO` format where `la` is a two-letter code representing the language and `CO` is a two-letter uppercase code representing the country. |
| Att Status |  Whether the user has authorized your mobile app to access app-related data for tracking the user or the device. This is an iOS-only field. Supported values are `AUTHORIZED`, `DENIED`, `NOT_DETERMINED`, `NOT_APPLICABLE`. |
| Vertical Choice | Select the vertical to display vertical-specific parameters under **Property Data**. Available options are `Hotel`, `Flight`, `Destination`, and `No Vertical Selected`. |

#### Property Data

| Parameter | Description |
| --- | --- |
| Content Type | The type of the product. This value must be `product` or `product_group`, depending on how your data feed is configured for your product catalog. |
| Currency  | Three-character ISO 4217 code. For example, `EUR`, `USD`, `JPY`.  |
| Value | Total value of the order or items sold.  |
| Query | The text used in a search query. |
| Description  | A description of the app event.  |
| Order ID | The order ID. |
| Shop ID | The shop ID. |

#### Hotel vertical specific parameters

| Parameter | Description |
| --- | --- |
| Content IDs | Product IDs associated with the event, such as SKUs. |
| City | Hotel city location. |
| Region | Hotel region. |
| Country | Hotel country. |
| Check-in Date | Hotel check-in date. |
| Check-out Date | Hotel check-out date. |
| Number of Adults | Number of adults in the booking. |
| Number of Children | Number of children in the booking. |
| Suggested Hotels | Suggested hotels for this user. Can be a string or an array of strings. |

#### Flight vertical specific parameters

| Parameter | Description |
| --- | --- |
| Destination City | Destination city name. |
| Departing Departure Date | Date of flight departure. Accepted formats are `YYYYMMDD`, `YYYY-MM-DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`. For example, `20180623`, `2018-06-23`, `2017-06-23T15:30GMT`, `2017-06-23T15:30:00GMT`. |
| Returning Departure Date | Date of return flight. Accepted formats are `YYYYMMDD`, `YYYY-MM-DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`. For example, `20180623`, `2018-06-23`, `2017-06-23T15:30GMT`, `2017-06-23T15:30:00GMT`. |
| Origin Airport | Origin airport code. For example, `JFK`. |
| Destination Airport | Destination airport code. For example, `CDG`. |
| Number of Adults | Number of adults. |
| Number of Children | Number of children. |
| Number of Infants | Number of infants. |
| Travel Class | Class of the flight ticket. This value must be `economy`, `premium`, `business`, or `first`. |
| User Score | Represents the relative value of this potential customer to the advertiser. For example, `50`. |
| Preferred Number of Stops | Number of preferred stops. |

#### Destination vertical specific parameters

| Parameter | Description |
| --- | --- |
| Content IDs | Product IDs associated with the event, such as SKUs. |
| City | Destination city location. |
| Region | Destination region. |
| Country | Destination country. |
| Travel Start | The start date of the user&#39;s trip. Accepted formats are `YYYYMMDD`, `YYYY-MM-DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`. For example, `20180623`, `2018-06-23`, `2017-06-23T15:30GMT`, `2017-06-23T15:30:00GMT`. |
| Travel End | The end date of the user&#39;s trip. Accepted formats are `YYYYMMDD`, `YYYY-MM-DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`. For example, `20180623`, `2018-06-23`, `2017-06-23T15:30GMT`, `2017-06-23T15:30:00GMT`. |
| Number of Adults | Number of adults. |
| Number of Children | Number of children. |
| Number of Infants | Number of infants. |
| Suggested Destinations | A list of IDs representing destination suggestions for this user. |

#### Content Data

| Parameter | Description |
| --- | --- |
| Price | The price of the item. Supports number and array of numbers data types. |
| Quantity  | The number of items. Supports integer and array of number data types. |
| Content ID  | The product ID or IDs in your system. Supports string and array of strings data types. |
| Content Category | The category or categories of the page or product. Supports string and array of strings data types.|
| Content Name | The name of the page or product. Supports string and array of strings data types.|
| Brand | The brand of the product item. Supports string and array of strings data types. |

#### App Data

| Parameter | Description |
| --- | --- |
| App ID | The mobile app ID. |
| App Version | The app version number. |
| Application Name | The application name. |

#### Lead Data

| Parameter | Description |
| --- | --- |
| Lead ID | ID of TikTok leads. |
| Lead Event Source | The lead event source. |

#### Automatic Deduplication

| Parameter | Description |
| --- | --- |
| Disable Automapping | If automapping is disabled, any automatically mapped parameters are not sent to the vendor by default. |

The connector automatically maps the following parameters by default:

* TikTok Click ID (`ttclid`)
* User Agent

To disable automapping, set **Disable Automapping** to `true`. Any automatically mapped parameters are not sent to the vendor.

#### Custom events

To select a custom event for this connector:

1. Under the **Event Type** category, select `Custom` for the **Conversion event name**.
1. In the **Custom Event Name** field, enter the custom event name and click **&#43; Add Mapping**.