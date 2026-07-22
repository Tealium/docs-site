---
title: Rakuten Advertiser Transaction API Connector Setup Guide
description: This article describes how to set up the Rakuten Advertiser Transaction API connector.
url: https://docs.tealium.com/server-side-connectors/rakuten-advertiser-transaction-api-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Rakuten Advertiser Transactions API
* API Version: v1
* API Endpoint: `https://api.linksynergy.com`
* Documentation: [Rakuten Advertising Developer Portal](https://developers.rakutenadvertising.com/)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Rakuten Advertiser ID**: Your Rakuten Advertiser ID.
* **Client ID**: The OAuth client ID provided by Rakuten.
* **Client Secret**: The OAuth client secret key provided by Rakuten.

The connector uses OAuth 2.0 client credentials authentication. It exchanges the Client ID and Client Secret for a bearer token at `https://api.linksynergy.com/token`. Bearer tokens expire after 4 hours.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Transaction | ✗ | ✓ |
| Send Refund | ✗ | ✓ |

### Send Transaction

#### Order data

| Parameter | Description |
| --- | --- |
| Transaction Timestamp | (Required) UTC time the user completed the online commissionable action. |
| Order ID | (Required) Unique order ID, preferably consumer-facing for replies to transaction inquiries. |
| Currency | (Required) Order currency code. |
| Click ID | Required if not reporting linkless. The 34-character ID sent from Rakuten in redirects or on the final landing page. |
| Landing Timestamp | Required if not reporting linkless. UTC time the user landed on your site. This timestamp must be earlier than the Transaction Timestamp. |

#### Optional order data

| Parameter | Description |
| --- | --- |
| Alternative Order ID | An alternative version of the reported order ID. |
| Commission Reason | The reason commission is not being paid on the transaction. Use with Is Commissionable. |
| Consumed Datetime | The date the booking was consumed. |
| Consumer Country | The country the consumer lives in. |
| Consumer Operating System | The operating system of the consumer's device at the time of the commissionable action. |
| Consumer Region | The region the consumer lives in. |
| Conversion Type | The conversion attribution method used by the advertiser. Example: `post click`. |
| Coupon | The coupon or discount code used with the transaction. |
| Credit Card Type | The type of credit card used for the purchase. |
| Customer ID | An ID that represents the customer. |
| Customer Rank | The advertiser rank or score assigned to the customer. |
| Customer Segment | The advertiser's segment for the customer. |
| Customer State | The state the customer lives in. |
| Customer Status | The advertiser status of the customer. Example: `new`, `existing`. |
| Event Datetime | The date and time of the event. Example: concert, sporting event. |
| Mobile Device ID | The advertising ID of a mobile device. |
| Order Status | The status of the order. |
| Purchase Site | The domain of the purchase. |
| Tracking Source | How the tracking data was sent to Rakuten. |
| Traffic Source | The source of traffic that triggered the conversion event. |

#### Items data

| Parameter | Description |
| --- | --- |
| Product Prices | (Required) List of product prices. By default, the connector multiplies each price by its corresponding quantity before sending. To send price values without modification, enable the **Disable product prices calculation** checkbox. |
| Product SKUs | (Required) List of product SKUs. |
| Product Quantities | (Required) List of product quantities. |
| Product Names | (Required) List of product names. |

#### Optional items data

| Parameter | Description |
| --- | --- |
| Product Brands | List of product brands. |
| Product Categories | List of product categories. Use templating to create more complex per-item category arrays for Rakuten. |
| Product Category IDs | List of product category IDs. Use templating to create more complex per-item category arrays for Rakuten. |
| Product Coupons | List of product-level coupons. |
| Product IDs | List of product IDs. |
| Higher Commission Rates | List of booleans indicating products associated with a higher commission rate. |
| Product Sequences | List identifying the sequence of items included in a shipment. |
| Product Statuses | List of item statuses. |
| Is Commissionable | List of booleans indicating whether each product is commissionable. |
| Product Margins | List of product-level margins. |
| Marketplace Stores | List of stores where the sale took place in a marketplace environment. |
| Marketplace Store IDs | List of store IDs where the sale took place in a marketplace environment. |
| Is Tax Exempt | List of booleans indicating whether each product is tax-exempt. |

#### Disable product prices calculation

Rakuten requires product prices to be sent as price × quantity. The connector performs this calculation automatically. Enable this checkbox to send the mapped price values without modification.

### Send Refund

#### Refund data

| Parameter | Description |
| --- | --- |
| Transaction Timestamp | (Required) UTC time the user completed the original commissionable action. |
| Order ID | (Required) Unique order ID for the transaction being refunded. |
| Currency | (Required) Order currency code. |
| Click ID | (Required) The 34-character ID sent from Rakuten in redirects or on the final landing page. |
| Landing Timestamp | (Required) UTC time the user landed on your site. This timestamp must be earlier than the Transaction Timestamp. |

#### Items data

| Parameter | Description |
| --- | --- |
| Product Prices | (Required) List of product prices. The connector sends item amounts as negative numbers per Rakuten's refund API requirements. By default, the connector also multiplies each price by its corresponding quantity before applying the sign change. To disable the multiplication, enable the **Disable product prices calculation** checkbox. |
| Product SKUs | (Required) List of product SKUs. |
| Product Quantities | (Required) List of product quantities. |
| Product Names | (Required) List of product names. |

#### Disable product prices calculation

Rakuten requires product prices to be sent as price × quantity. The connector performs this calculation automatically. Enable this checkbox to send the mapped price values without modification.
