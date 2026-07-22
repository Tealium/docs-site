---
title: Podscribe S2S Connector Setup Guide
description: This article describes how to set up the Podscribe S2S connector.
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
* **API Key**: Podscribe S2S API key used to authorize requests.
* **Advertiser ID**: Unique advertiser ID assigned by the platform.

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
| Action | Type of event (for example, user action or conversion).<br>view<br>signup<br>lead<br>purchase<br>install<br>offline_purchase |

#### Event Data

| **Parameter** | **Description** |
| --- | --- |
| `event_url` | URL where the event took place. |
| `landing_url` | Landing page URL of the session. |
| `referrer_url` | URL of the page that referred the user. |
| `campaign_id` | Podscribe campaign ID. |
| `timestamp` | UTC timestamp of the event. |

#### User Data

| **Parameter** | **Description** |
| --- | --- |
| `ip` | IP address of the user. Prefer IPv6 if available. |
| `ipv4` | IPv4 address (used if IPv6 is unavailable). |
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
| `category` | Indicates product category. |
| `channel` | Indicates channel source. |
| Disable Automapping |  Disable automatic mapping for the connector.|