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

The connector uses OAuth 2.0 client credentials authentication. It exchanges the client ID and client secret for a bearer token at `https://api.linksynergy.com/token`. Bearer tokens expire after 4 hours.

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

## Optional data by vertical

The Rakuten Advertising API supports vertical-specific optional data fields that are not available as named parameters in the connector UI. To send these fields, add them as custom mappings in any connector action that supports optional data, using the API field name as the mapping key.

### Financial

| API field | Description | Usage |
| --- | --- | --- |
| `autopay` | Indicates whether a consumer set up an account to make payments automatically. | Order level |
| `customer_segment_group` | Advertiser-defined segmentation of users into one of five groups; shown in reporting as quintiles score. | Item level |
| `designated_marketing_area` | ID of the consumer offer designated marketing area. | Order level |
| `estimated_aum` | Estimated assets under management for the consumer after the account has been opened. | Order level |
| `funded_amount` | Updated total balance of each opened account. | Item level |
| `funded_amount_range` | Advertiser-defined range representing the balance of an opened account. | Item level |
| `home_ownership` | Applicant home ownership status submitted. | Order level |
| `income_aum` | Advertiser-defined assets under management based on income entered by the consumer during onboarding. | Order level |
| `income_band` | Coded value for income submitted by the applicant. | Order level |
| `loan_amount_requested` | Loan amount requested by the applicant. | Order level |
| `loan_approval_datetime` | Approval date of the loan. | Order level |
| `loan_apr` | APR of the loan. | Order level |
| `loan_funded_datetime` | Funding date of the loan. | Order level |
| `loan_model_number` | Model number of the pre-qualification used to present the offer. | Order level |
| `loan_offer_apr` | APR for the loan as predicted by the pre-qualification model. | Order level |
| `loan_offer_badge` | Badge type for the offer as predicted by the pre-qualification model. | Order level |
| `loan_offer_term` | Loan term as predicted by the pre-qualification model. | Order level |
| `loan_origination_fee` | Origination fee of the loan. | Order level |
| `loan_purpose` | Advertiser-defined purpose for the loan. | Order level |
| `loan_purpose_applicant` | Coded value for the loan purpose as submitted by the applicant. | Order level |
| `loan_term_in_months` | Number of months in the loan term. | Order level |
| `monthly_housing_payment` | Coded value of monthly rent or housing payment submitted by the applicant. | Order level |
| `publisher_lead_id` | ID generated by the publisher to match the closed loan to their records. | Order level |

### Retail

| API field | Description | Usage |
| --- | --- | --- |
| `artist_curation_id` | ID of an artist used for customized product curation for a customer. | Order level |
| `commission_estimate` | Estimated commission for marketplace advertisers; not shown to publishers. | Order level |
| `credit_card_last_four` | Last four digits of the credit card; intended as an identifier for card-linked offers. | Order level |
| `discount_amount` | Discount amount applied at the order level. | Order level |
| `discount_amount` | Discount amount applied at the item level. | Item level |
| `discount_type` | Type of discount used at the order level. | Order level |
| `discount_type` | Type of discount used at the item level. | Item level |
| `is_clearance` | Indicates whether the product is on clearance. | Item level |
| `is_marketplace` | Indicates whether the item is from a marketplace. | Item level |
| `is_sale` | Indicates whether the product is on sale. | Item level |
| `markdown_rate` | Rate of markdown on the item, between 0 and 100. | Item level |
| `marketplace_store` | Name of the merchant store where the sale took place in a marketplace environment. | Item level |
| `marketplace_store_id` | ID of the merchant store where the sale took place in a marketplace environment. | Item level |
| `o2o_bank_partner` | Name of the banking partner used for card-linked offer tracking. | Order level |
| `o2o_store_address` | Store address. | Order level |
| `o2o_store_city` | City where the store is located. | Order level |
| `o2o_store_country` | Country where the store is located. | Order level |
| `o2o_store_id` | Store ID. | Order level |
| `o2o_store_name` | Store name. | Order level |
| `o2o_store_state` | State where the store is located. | Order level |
| `o2o_store_zip` | ZIP or postal code where the store is located. | Order level |
| `ship_country` | Country the order ships to. | Order level |
| `shipment_id` | Identifier for a group of items shipped or returned together. | Item level |
| `shipped_datetime` | When the item shipped or is expected to ship. | Order level |
| `store_category` | Category representing the store where the purchase occurred. | Order level |
| `store_id` | ID of the store where the purchase occurred. | Order level |
| `subscription_id` | Product subscription plan ID. | Item level |
| `subscription_name` | Product subscription plan name. | Item level |

### Travel

| API field | Description | Usage |
| --- | --- | --- |
| `accommodation_type` | Type of accommodation. | Item level |
| `cancel_deadline_datetime` | Deadline for a traveler to cancel their reservation. | Order level |
| `check_in_datetime` | Date the traveler checks in. | Order level |
| `check_out_datetime` | Date the traveler checks out. | Order level |
| `consumed_datetime` | Date the booking was consumed. | Order level |
| `departure_country` | Country where the traveler begins their trip. | Item level |
| `departure_location` | Location where the traveler begins their trip, such as a city, airport, cruise port, or similar location. | Item level |
| `destination_country` | Country where the traveler ends their trip. | Item level |
| `destination_location` | Location where the traveler ends their trip, such as a city, airport, cruise port, or similar location. | Item level |
| `discount_amount` | Discount amount applied at the order level. | Order level |
| `discount_amount` | Discount amount applied at the item level. | Item level |
| `discount_type` | Type of discount used at the order level. | Order level |
| `discount_type` | Type of discount used at the item level. | Item level |
| `fare_type` | Travel fare type, such as first class, business class, or economy. | Item level |
| `is_weekend` | Indicates whether the reservation took place over the weekend. | Order level |
| `number_of_rooms` | Number of rooms in the reservation. | Item level |
| `paid_in_loyalty_points` | Indicates whether the customer paid using loyalty points. | Item level |
| `property_type` | Type of property, such as hotel or motel. | Item level |
| `reservation_end_datetime` | Reservation end date. | Order level |
| `reservation_length_in_days` | Number of days in the reservation. | Order level |
| `reservation_region` | Region associated with the travel reservation; useful where the advertiser has multiple locations. | Item level |
| `reservation_start_datetime` | Reservation start date. | Order level |
| `travel_reason` | Reason for travel, such as personal or business. | Order level |
| `travel_type` | Type of travel reservation, such as airline, cruise, hotel, rental car, or activity. | Item level |
| `vehicle_type` | Vehicle type associated with a car rental, such as premium, standard, or compact. | Item level |
