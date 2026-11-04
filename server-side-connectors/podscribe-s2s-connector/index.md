---
title: Podscribe S2S Connector Setup Guide
description: Set up the Podscribe S2S connector to send server-side conversion events to Podscribe for attribution.
url: https://docs.tealium.com/server-side-connectors/podscribe-s2s-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Podscribe API
* API Endpoint: `https://verifi.podscribe.com/tag`
* Documentation: [Podscribe API](https://help.podscribe.com/sending-podscribe-conversion-events-/g4g8w3hppouCfkXZdcx6FV/sending-events-server-to-server-s2s-in-batch-or-as-an-img-tag/67UdckfSLHXAPtUAfWDyud)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **API Key**: (Required) Podscribe S2S API key used to authorize requests.
* **Advertiser ID**: (Required) Unique advertiser ID assigned by the platform.
* **User ID**: (Required) User identifier sent with every event request.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Action | Type of event (for example, user action or conversion).<br>`view`<br>`signup`<br>`lead`<br>`purchase`<br>`install`<br>`offline_purchase` |

#### Event Data

| **Parameter** | **Description** |
| --- | --- |
| `event_url` | URL where the event took place. |
| `landing_url` | Landing page URL of the session. |
| `referrer` | URL of the page that referred the user. |
| `campaign_id` | Podscribe campaign ID. |
| `timestamp` | UTC timestamp of the event. |

#### User Data

| **Parameter** | **Description** |
| --- | --- |
| `ip` | IPv6 address of the user, preferred over IPv4. If `ip` is blank and `ipv4` is populated, the connector sends the `ipv4` value in both fields. |
| `ipv4` | IPv4 address of the user. |
| `user_agent` | Browser or app user agent string. |
| `cookie` | Browser cookie or session identifier. |
| `hashed_email` | SHA256-hashed email address of the user. Trim and lowercase before hashing. |
| `device_id` | Internal user or device identifier. |
| `idfa` | Apple advertising ID (IDFA). |
| `gaid` | Google Advertising ID (GAID). |
| `is_new_customer` | Whether the user is a first-time customer. |
| `is_subscription` | Indicates if the event involves a subscription. |

#### Meta Data

| **Parameter** | **Description** |
| --- | --- |
| `value` | Purchase or conversion value. |
| `currency` | Currency code for the transaction. |
| `order_number` | Unique order or transaction ID. |
| `discount_code` | Discount or promo code used. |
| `product` | Name or ID of the product involved. |
| `category` | Product or content category for the event. |
| `channel` | Traffic channel source for the event. |
| **Disable E-Commerce Automapping** | Suppresses automatic mapping for e-commerce fields (`value`, `currency`, `order_number`, `discount_code`, `product`, `category`). Explicit direct mappings still apply. E-commerce fields are never auto-mapped for `view` events, regardless of this setting. |
| **Disable Identifier Automapping** | Suppresses automatic mapping for identifier and context fields (`ip`, `ipv4`, `user_agent`, `event_url`, `referrer`, `timestamp`, `cookie`). Explicit direct mappings still apply. |