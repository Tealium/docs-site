---
title: Viant VDP Conversion API Connector Setup Guide
description: This article describes how to set up the Viant VDP Conversion API connector.
url: https://docs.tealium.com/server-side-connectors/viant-vdp-conversion-api/
---
## API Information

This connector uses the following vendor API:

* API Name: Viant API
* API Version: v1
* API Endpoint: `https://vdp-connect-api.viantinc.com`
* Documentation: [Viant API](https://docs.api.viantinc.com/reference/how-to-get-started)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Client ID**: Required. Client ID for Viant VDP API authentication.
* **Client Secret**: Required. Client secret for Viant VDP API authentication.
* **Account ID**: Required. Viant account ID.
* **Advertiser ID**: Required. Viant advertiser ID.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion Event | ✓ | ✓ |
| Send Healthcare Conversion Event | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Conversion Event Type | **PageView** - Page view event&lt;br&gt;**LandingPage** - Landing page event&lt;br&gt;**ItemView** - Item view event&lt;br&gt;**AddToCart** - Add to cart event&lt;br&gt;**InitiateCheckout** - Initiate checkout event&lt;br&gt;**AddPaymentInfo** - Add payment info event&lt;br&gt;**Purchase** - Purchase event&lt;br&gt;**Lead** - Lead event |

#### Sales Data

| **Parameter** | **Description** |
| --- | --- |
| Transaction ID | Unique identifier for the transaction. Automapping applied, map attribute to override. |
| Conversion Timestamp | ISO 8601 timestamp of the conversion. For example, `2025-07-28T15:32:00Z`. Automapping applied, map attribute to override. |
| Store ID | Unique identifier for the store or location. |
| Amount | Total conversion or transaction amount. Automapping applied, map attribute to override. |
| Currency | Currency code. For example, `USD`, `EUR`. Automapping applied, map attribute to override. |
| Sales Channel | Sales channel. For example, `Online`, `In-store`. |

#### Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Apply SHA256 | Plain text email address of the customer. Connector will normalize and apply SHA256 Hashing. |
| Email Already SHA256 | SHA256 hashed customer email address. |
| Address Apply SHA256 | Plain text address of the customer. Connector will normalize and apply SHA256 Hashing. |
| Address Already SHA256 | SHA256 hashed customer address. |
| IP Address | Customer `IP` address. |
| Mobile ID | Customer mobile `ID`. |
| Cookie | Event cookie. |

#### Purchased Items

| **Parameter** | **Description** |
| --- | --- |
| Item ID | (Required if items present) Unique identifier for the product SKU. |
| Product Name | Human-readable name of the product. |
| Product Category | Category of the product. |
| Price | (Required if items present) Price per unit. |
| Quantity | (Required if items present) Quantity purchased. |
| Custom Data | Up to 10 custom key-value metadata pairs for any additional context. For example, `campaign IDs`, `user segments`. |

#### Conversion Location

| **Parameter** | **Description** |
| --- | --- |
| Conversion Country | The country of the conversion location. |
| Conversion State | The state of the conversion location. |
| Conversion City | The city of the conversion location. |
| Disable Automapping | Disable automatic mapping for the connector. |

### Send Healthcare Conversion Event

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Healthcare Event Name | (Required) The anonymized event code to send to Viant. For example, `Page View`, `Event 1`, `Event 2`. Use short opaque codes rather than descriptive event names to comply with HIPAA requirements. |

#### Sales Data

| Parameter | Description |
| --- | --- |
| Transaction ID | (Required) Unique identifier for the transaction. Used to group Impression ID and Click ID. |
| Conversion Timestamp | ISO 8601 timestamp of the conversion. For example, `2025-07-28T15:32:00Z`. Current time used if not provided. |
| Store ID | Unique identifier for the store or location. |
| Sales Channel | Sales channel. For example, `Online`, `In-store`. |

#### Healthcare Identifiers

| Parameter | Description |
| --- | --- |
| Viant Impression ID | Viant pseudonymous impression tracking ID from the creative macro `${ADELPHIC_IMPRESSIONID}`. Used for post-view conversion attribution. |
| Viant Click ID | Viant pseudonymous click tracking ID from the creative macro `${ADELPHIC_CLICKID}`. Used for post-click conversion attribution. |
| Custom Identifier | (Optional) A customer-defined pseudonymous key. For example, internal encounter or funnel ID. |
| Custom Data | (Optional) Key-value metadata pairs for additional context. The `healthcare_capi` flag is automatically included. |

#### Conversion Location

| Parameter | Description |
| --- | --- |
| Conversion Country | The country of the conversion location. |
| Conversion State | The state of the conversion location. |
| Conversion City | The city of the conversion location. |