---
title: OpenAI Events Connector Setup Guide
description: This article describes how to set up the OpenAI Events connector.
url: https://docs.tealium.com/server-side-connectors/openai-events-connector/
---
## API information

This connector uses the following vendor API:

* API Name: OpenAI Events API
* API Version: v1
* API Endpoint: `https://bzr.openai.com`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **OpenAI Events API Key**: Required. The Bearer token used to authenticate requests to the OpenAI Events API. This key is sent in the Authorization header as a Bearer token. Your OpenAI account team can provision this value.
* **Pixel ID**: Required. Your OpenAI Pixel ID (`pid`). This value is appended to the API endpoint as a query parameter. Find your Pixel ID in **OpenAI Ads &gt; Settings &gt; Conversions**. Each conversion event you intend to send (for example, `page_viewed`, `items_added`, `order_created`) must be registered there for the pixel before live events count toward reporting.
* **Default Action Source**: Select the default source of the conversion event. Defaults to **Web**. Override this per action using the Action Source parameter.
* **Base URL Override**: The default is `https://bzr.openai.com`. Override only if directed by OpenAI for sandbox or staging environments.

## Connector actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Event (Real-Time) | ✓ | ✓ |
| Send Event (Batched) | ✓ | ✓ |

### Send Event (Real-Time)

#### Parameters

| Parameter | Description |
| --- | --- |
| Event Type | Required. Select the type of event to send to OpenAI.&lt;br&gt;Supported event types: **Appointment Scheduled**, **Checkout Started**, **Contents Viewed**, **Custom**, **Items Added**, **Lead Created**, **Order Created**, **Page Viewed**, **Registration Completed**, **Subscription Created**, **Trial Started**. |
| Custom Event Name | Required when Event Type is **Custom**. Provide a custom name for the event.&lt;br&gt;This value is ignored for all other event types. |

#### Event Data

Map Tealium attributes to OpenAI top-level event fields.

| Parameter | Description |
| --- | --- |
| Event ID | Required. A unique identifier for the event, used for deduplication. |
| Timestamp | Required. The event timestamp in milliseconds. Must be within 7 days in the past or 10 minutes in the future. |
| OPPRef | The OpenAI privacy-preserving identifier. |
| Source URL | Required when Action Source is `web`. The URL of the page where the event occurred. |
| Action Source | The source of the conversion event. Supported values: `web`, `mobile_app`, `offline`, `physical_store`, `phone_call`, `email`, `other`. |
| Opt Out | Set to `true` to flag the event as opted out from personalization. |

#### User Data

Map applicable user identifiers to improve attribution accuracy. You may either pre-hash PII values yourself or let the connector hash them. Hashable fields appear as two columns: **(apply SHA256 hash)** for raw values the connector normalizes and hashes, and **(already SHA256 hashed)** for pre-hashed values.

| Parameter | Description |
| --- | --- |
| Email address (apply SHA256 hash) | Provide a lowercase plain text email address and the connector hashes this value in the format OpenAI expects. Empty or null values are ignored. |
| Email address (already SHA256 hashed) | Provide an email address which has been SHA256 hashed. |
| Phone number (apply SHA256 hash) | Provide a lowercase plain text phone number and the connector hashes this value in the format OpenAI expects. Empty or null values are ignored. |
| Phone number (already SHA256 hashed) | Provide a phone number that has been SHA256 hashed. |
| External ID (apply SHA256 hash) | Provide a plain text external ID, such as a loyalty card ID or another identifier, and the connector hashes this value in the format OpenAI expects. |
| External ID (already SHA256 hashed) | Provide an external ID which has been SHA256 hashed. |
| Country (apply SHA256 hash) | Provide a country associated with the event and the connector hashes this value in the format OpenAI expects. |
| Country (already SHA256 hashed) | Provide a country value which has been SHA256 hashed. |
| City (apply SHA256 hash) | Provide a city associated with the conversion in lowercase letters and the connector hashes this value in the format OpenAI expects. |
| City (already SHA256 hashed) | Provide a city value which has been SHA256 hashed. |
| Zip code (apply SHA256 hash) | Provide a zip or postal code in lowercase and the connector hashes this value in the format OpenAI expects. |
| Zip code (already SHA256 hashed) | Provide a zip or postal code which has been SHA256 hashed. |
| External ID (raw) | A unique ID, such as a loyalty card ID or another identifier. Sent without hashing. |
| IP Address | The IP address of the device. |
| User Agent | The user agent string of the user&#39;s web browser. |

#### E-Commerce

For Customer Action events (**Appointment Scheduled**, **Lead Created**, **Registration Completed**) only the order-summary fields are accepted. OpenAI drops all other e-commerce fields from the outbound payload.

| Parameter | Description |
| --- | --- |
| Amount | An integer in minor units (for example, cents). If provided, Currency is required. |
| Currency | The currency code in ISO 4217 format (for example, `USD`). |

#### Disable Automapping

When checked, disables the default Tealium-to-OpenAI automappings for this action (timestamp, source URL, IP address, user agent, and retail extension attributes `_csubtotal`, `_ccurrency`, `_csku`, `_cprodname`, `_ccat`, `_cquan`, `_cprice`). Explicit field mappings always take precedence. Unchecking this only fills in the blanks.

#### Debug Mode

When enabled, the connector sends the event with `validate_only: true` so OpenAI validates the payload and returns any errors without persisting the event. Use this for troubleshooting and dry-runs. Leave disabled for production traffic.

#### Pixel ID Override

Optional. Override the connector-level Pixel ID for this action. If provided, the connector uses this value instead of the Pixel ID configured in the connector settings.

#### API Key Override

Optional. Override the connector-level API Key for this action. If provided, the connector uses this value instead of the API Key configured in the connector settings.

### Send Event (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

This action uses the same parameters and mapping options as the **Send Event (Real-Time)** action. For more information, see [Send Event (Real-Time)](#send-event-real-time).