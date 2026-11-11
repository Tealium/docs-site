---
title: ChatGPT Conversions API Connector Setup Guide
description: This article describes how to set up the ChatGPT Conversions API connector.
url: https://docs.tealium.com/server-side-connectors/chatgpt-conversions-api-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Conversions API
* API Version: v1
* API Endpoint: `https://bzr.openai.com`

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Conversions API Key**: Required. Your Conversions API key. The connector sends it in the `Authorization` header as a Bearer token. Create the key on the Conversions tab in OpenAI Ads Manager.
* **Pixel ID**: Required. Your Pixel ID (`pid`). The connector appends it to the API endpoint as a query parameter. Find your Pixel ID on the Conversions tab in OpenAI Ads Manager. Register each conversion event you send (for example, `page_viewed`, `items_added`, `order_created`) for the pixel there, or live events don't count toward reporting.
* **Default Action Source**: Select the default source of the conversion event. Defaults to **Web**. Override this per action using the Action Source parameter.
* **Base URL Override**: The default is `https://bzr.openai.com`. Override only if directed by OpenAI for sandbox or staging environments.

After you configure the connector, click **Done**.

## Connector actions

| Action name | Visitor profile | Event data |
| ----------- | :------------: | :---------: |
| Send Event (Real-Time) | ✓ | ✓ |
| Send Event (Batched) | ✓ | ✓ |

### Send Event (Real-Time)

#### Parameters

**Event Type**

Required. Select the type of event to send. Each value maps to the `type` field in the Conversions API request. Supported values:

* `appointment_scheduled`
* `attribution_appended`
* `checkout_started`
* `contents_viewed`
* `custom`
* `items_added`
* `lead_created`
* `order_created`
* `page_viewed`
* `registration_completed`
* `subscription_created`
* `trial_started`

Each event type maps to one of five data type objects: `contents`, `customer_action`, `plan_enrollment`, `custom`, or `attribution`. See [Original Event Data](#original-event-data) and [Attribution Data](#attribution-data) for the `attribution_appended` fields.

`attribution_appended` sends a separate attribution report that references an earlier conversion. In **Event Data**, **Event ID** is the attribution report ID. It must be unique and reused on exact retries. **Timestamp** is the report-generation time and defaults to the send time.


<blockquote>
`attribution_appended` is only available after OpenAI enables it for your advertiser pixel. Contact your OpenAI account team to confirm availability before using it in production.
</blockquote>


**Custom Event Name**

Required when Event Type is **Custom**. Provide a custom name for the event. This value is ignored for all other event types.

**OPPRef**

Optional. An OpenAI attribution identifier. Map the original value without modification. The value is sent as `events[].oppref` and is not part of Event Data.

#### Event data

Map Tealium attributes to OpenAI top-level event fields.


<blockquote>
For **Attribution Appended** events, only **Event ID**, **Timestamp**, **Action Source**, **Source URL**, and **OPPRef** are sent. **Event ID** is the attribution report ID. It must be unique and reused on exact retries. **Timestamp** is the report-generation time and defaults to the send time if not mapped.
</blockquote>


| Parameter | Description |
| --- | --- |
| Event ID | Required. A unique identifier for the event, used for deduplication. |
| Timestamp | Required. The event timestamp in milliseconds. Must be within 7 days in the past or 10 minutes in the future. |
| Source URL | Required when Action Source is `web`. The URL of the page where the event occurred. |
| Action Source | The source of the conversion event. Supported values: `web`, `mobile_app`, `offline`, `physical_store`, `phone_call`, `email`, `other`. |
| Opt Out | Set to `true` to flag the event as opted out of personalization. |

#### User data


<blockquote>
User Data is not sent for **Attribution Appended** events.
</blockquote>


* Map applicable user identifiers to improve attribution accuracy. For each PII field you can either pre-hash the value yourself or let the connector hash it for you.
* Send only data the user has consented to share with OpenAI. OpenAI applies field-specific normalization and hashing rules.
* Hashable fields offer two columns: **(apply SHA256 hash)** for raw values that the connector normalizes and hashes, and **(already SHA256 hashed)** for values you have already hashed. If both are mapped, the connector sends the already-hashed values.
* Supported hashed PII keys: `email_address`, `phone_number`, `external_id`, `first_name`, `last_name`.
* List fields accept a single value or a list attribute, and several attributes can map to the same field. The connector removes duplicates and sends at most the first 3 values per field.
* Fields sent un-hashed: `country` (two-letter code, for example `US`), `city`, `region`, `postal_code`, `android_advertising_id`, `ip_address`, `user_agent`.
* Android GAID applies to Android devices only and uses UUID format. All-zero or malformed IDs are not sent.


<blockquote>
The **External ID (raw)**, hashed **Country**, hashed **City**, and hashed **Zip code** options are no longer offered in the field dropdown. Existing connector profiles that use these options continue to send data. The connector normalizes and hashes stored External ID raw values into `external_ids_sha256`, and reads the hashed geographic values as raw before sending them to the new `countries`, `cities`, and `postal_codes` fields.
</blockquote>


| Parameter | Description |
| --- | --- |
| Email address list (apply SHA256 hash) | Provide a lowercase plain text email address, or a list attribute of up to 3 email addresses, and the connector normalizes and hashes each value before sending it to `emails_sha256`. Empty or null values are ignored. |
| Email address list (already SHA256 hashed) | Provide an email address, or a list of up to 3 email addresses, that have already been SHA256 hashed. |
| Phone number list (apply SHA256 hash) | Provide a plain text phone number, or a list attribute of up to 3 phone numbers, and the connector normalizes and hashes each value before sending it to `phone_numbers_sha256`. Empty or null values are ignored. |
| Phone number list (already SHA256 hashed) | Provide a phone number, or a list of up to 3 phone numbers, that have already been SHA256 hashed. |
| External ID list (apply SHA256 hash) | Provide a plain text external ID, such as a loyalty card ID or another identifier, or a list attribute of up to 3 external IDs, and the connector hashes each value before sending it to `external_ids_sha256`. |
| External ID list (already SHA256 hashed) | Provide an external ID, or a list of up to 3 external IDs, that have already been SHA256 hashed. |
| First name list (apply SHA256 hash) | Provide a plain text first name, or a list attribute of up to 3 first names, and the connector normalizes and hashes each value before sending it to `first_names_sha256`. |
| First name list (already SHA256 hashed) | Provide a first name, or a list of up to 3 first names, that have already been SHA256 hashed. |
| Last name list (apply SHA256 hash) | Provide a plain text last name, or a list attribute of up to 3 last names, and the connector normalizes and hashes each value before sending it to `last_names_sha256`. |
| Last name list (already SHA256 hashed) | Provide a last name, or a list of up to 3 last names, that have already been SHA256 hashed. |
| Country list | Provide a two-letter ISO country code (for example, `US`), or a list attribute of up to 3 country codes. Sent raw to `countries`. |
| City list | Provide a city name, or a list attribute of up to 3 city names. Sent raw to `cities`. |
| Region list | Provide a region value in the format OpenAI expects, or a list attribute of up to 3 region values. State or province abbreviations may not match. Sent raw to `regions`. |
| Postal code list | Provide a postal code, or a list attribute of up to 3 postal codes. Sent raw to `postal_codes`. |
| Android GAID | Provide an Android advertising identifier. For mobile app events only. Sent raw to `android_advertising_id`. |
| IP Address | The IP address of the device. |
| User Agent | The user agent string of the user's web browser. |

#### Original event data

These fields apply only when **Event Type** is set to `attribution_appended`. Map them to the original conversion event that this attribution report references.

| Parameter | Description |
| --- | --- |
| Event ID | Required. The `event_id` of the original conversion event. Copy this value exactly. Do not regenerate it. |
| Event Type | Required. The `type` value from the original conversion event. Supported values: `app_installed`, `app_opened`, `appointment_scheduled`, `checkout_started`, `contents_viewed`, `custom`, `items_added`, `lead_created`, `order_created`, `page_viewed`, `registration_completed`, `subscription_created`, `trial_started`. |
| Timestamp (ms) | Required. The timestamp of the original conversion event in Unix milliseconds. May be older than 7 days. |
| Custom Event Name | Required when original Event Type is `custom`. Omit for all other event types. |
| Order ID | Optional. A metadata reference to the original order. Not a replacement for **Event ID**. |

#### Attribution data

These fields apply only when **Event Type** is set to `attribution_appended`. They describe the OpenAI ad touchpoint credited for the original conversion and are never automapped or generated by Tealium.

If any required attribution field is missing, the connector does not send the event. A validation error appears in Trace and the connector logs.

| Parameter | Description |
| --- | --- |
| Ad ID | Required. The OpenAI ad (`ad_id`) receiving credit. |
| Touchpoint Timestamp (ms) | Required. The timestamp of the ad touchpoint in Unix milliseconds. May be older than 7 days. |
| Touchpoint Type | Required. The type of touchpoint (for example, `ad_click`). |
| Attribution Share | Required. A number from 0 through 1 inclusive. |
| Attributed Amount | Required. An integer in currency minor units (for example, `6500` = $65.00). |
| Attribution Model | Required. Supported values: `customized_multi_touch`, `data_driven`, `first_click`, `first_touch`, `last_click`, `last_touch`, `linear`, `position_based`, `time_decay`. |
| Total Credit | Optional. A number representing the total credit value. |
| Attribution Window (days) | Optional. A nonnegative whole number of days for the attribution window. |

#### E-commerce

For Customer Action events (**Appointment Scheduled**, **Lead Created**, **Registration Completed**), only the order-summary fields are accepted. OpenAI drops all other e-commerce fields from the outbound payload.

For **Attribution Appended** events, only **Currency**, **Amount**, **Amount - convert to minor units**, **Minor Unit Factor**, **Data Content Type**, and **Customer Segmentation** are accepted. No e-commerce automapping applies.

Two approaches are available for monetary values:

* **Pre-converted values**: Map a value already expressed in minor units (for example, `2990` for $29.90 USD) to **Amount** or **Content Amount (per unit)**.
* **Convert on send**: Map a major-unit decimal value (for example, `29.90`) to **Amount - convert to minor units** or **Content Amount (per unit) - convert to minor units**, and set **Minor Unit Factor** to the appropriate multiplier for the currency (for example, `100` for USD/EUR/GBP, `1` for JPY/KRW, or `1000` for KWD/BHD/OMR).

If both variants are mapped for the same field, the pre-converted value takes precedence.

| Parameter | Description |
| --- | --- |
| Amount | An integer already expressed in minor units (for example, `2990` for $29.90 USD). If provided, Currency is required. For Attribution Appended events, this is the original conversion value. If both **Amount** and **Amount - convert to minor units** are mapped, this value takes precedence. |
| Amount - convert to minor units | A major-unit decimal value (for example, `29.90`). The connector multiplies this value by **Minor Unit Factor** and rounds the result half-up to an integer before sending. If provided, Currency is required. If no factor is set, the connector rounds the value to the nearest integer without multiplying. |
| Minor Unit Factor | The multiplier to apply when using the convert-to-minor-units variants. Use `100` for USD, EUR, or GBP. Use `1` for JPY or KRW. Use `1000` for KWD, BHD, or OMR. Must be a positive number. This value is not sent to OpenAI. |
| Currency | Required when **Amount** or **Amount - convert to minor units** is provided. Also required for Attribution Appended events. The currency code in ISO 4217 format (for example, `USD`). |
| Content Amount (per unit) | An integer already expressed in minor units. The per-item price for line-item contents. If both **Content Amount (per unit)** and **Content Amount (per unit) - convert to minor units** are mapped, this value takes precedence. |
| Content Amount (per unit) - convert to minor units | A major-unit decimal per-item price. The connector multiplies this value by **Minor Unit Factor** and rounds the result half-up to an integer before sending. If no factor is set, the connector rounds the value to the nearest integer without multiplying. |
| Data Content Type | Attribution Appended events only. Optional. |
| Customer Segmentation | Attribution Appended events only. Optional. |

#### Disable e-commerce automapping

* When checked, disables the default Tealium-to-OpenAI e-commerce automappings for this action: `timestamp_ms` (from Tealium event time), `source_url` (from standard URL attribute), and retail extension attributes `_csubtotal`, `_ccurrency`, `_csku`, `_cprodname`, `_ccat`, `_cquan`, `_cprice`.
* Explicit field mappings always take precedence. Unchecking this only fills in the blanks.
* When **Minor Unit Factor** is mapped, the connector also multiplies automapped `_csubtotal` and `_cprice` values by the factor before sending.
* Identity automapping (IP Address and User Agent) is controlled separately by the **Disable Identity Automapping** checkbox.


<blockquote>
If you had the legacy **Disable Automapping** checkbox enabled to suppress IP address and user agent from being auto-mapped, you must also enable **Disable Identity Automapping**. The legacy checkbox now controls only e-commerce field automapping.
</blockquote>


#### Disable identity automapping

* When checked, the connector does not automatically map IP Address and User Agent. Use this if you prefer full manual control over identity metadata or must suppress these fields for privacy reasons.
* When unchecked (default), the connector automatically maps `ip_address` (from Tealium standard IP attribute) and `user_agent` (from Tealium standard User Agent attribute).

#### Debug mode

When enabled, the connector sends the event with `validate_only: true` so OpenAI validates the payload and returns any errors without persisting the event. Use this for troubleshooting and dry-runs. Leave disabled for production traffic.

#### Pixel ID override

Optional. Override the connector-level Pixel ID for this action. If provided, the connector uses this value instead of the Pixel ID configured in the connector settings.

#### API key override

Optional. A Conversions API key to use for this action instead of the connector's **Conversions API Key**. Map an attribute that holds the key, or enter the key as a custom value.

A custom value is stored in the action and shown in plain text. To keep the key out of the action, map it from an attribute.

### Send Event (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

This action uses the same parameters and mapping options as the **Send Event (Real-Time)** action. For more information, see [Send Event (Real-Time)](#send-event-real-time).


<blockquote>
Batched delivery for the `attribution_appended` event type is not yet supported. Use the **Send Event (Real-Time)** action for attribution events.
</blockquote>
