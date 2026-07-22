---
title: CDK CRM Connector Setup Guide
description: This article describes how to set up the CDK CRM connector.
url: https://docs.tealium.com/server-side-connectors/cdk-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: CDK Global API
* API Version: v1
* API Endpoint: `https://api.fortellis.io`
* Documentation: [CDK CRM Direct Post Sales Leads](https://apidocs.fortellis.io/apis/1b0047b1-feec-42e9-be1b-d3285493ac9a)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


<blockquote>
When you add this connector you are prompted to accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:
* **Organization ID**  
  * To find your Fortellis Organization ID (Entity ID), log into your Fortellis account, hover over your name, and click **Organization Management**. The Entity ID is displayed on the page.
* **Subscription ID**  
  * Select the Subscription ID.
* **Endpoint**  
  * Select the endpoint. The default endpoint is **Prod**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Lead | ✗ | ✓ |

The following section describes how to set up parameters and options for each action.

### Send Lead

#### Prospect

| **Parameter** | **Description** |
| --- | --- |
| Request Date | Date that the API call was made. |

#### ID

Use this to send the lead source.

| **Parameter** | **Description** |
| --- | --- |
| ID Source | Name of the source that created this ID. |
| ID Sequence | A number used to track the history of this piece of data. |
| ID Value | The ID value. |

#### Vehicle

| **Parameter** | **Description** |
| --- | --- |
| Interest | The customer's interest type in a vehicle. Accepted values: `buy`, `lease`, `sell`, `trade-in`, `test-drive`.|
| Status | Identify vehicle as `new` or `used`. |
| Year | Model year of the vehicle. |
| Make | Manufacturer of vehicle. |
| Model | Model of vehicle. |
| VIN | Vehicle Identification Number of the vehicle. |
| Stock | Vendor's stock number for vehicle. |
| Trim | Trim description. |
| Units | The unit of measurement of the odometer: `mi` for miles or `km` for kilometers. |
| Value | The reading on the odometer. |
| Body Style | Generic body style, such as `SUV`, `Sedan`, `Coupe`, etc. |
| Transmission | `A` (Automatic) or `M` (Manual). |
| Number of Doors | Number of doors on vehicle. |
| Price Type | The type of price. Accepted values: `quote`, `offer`, `msrp`, `invoice`, `call`, `appraisal`, `asking`. |
| Currency | ISO 4217 currency code. |
| Delta | The `Delta` value and `Relative To` properties can be used to express the price as a percentage relative to another value, such as the invoice. Accepted values: `absolute`, `relative`, `percentage`.|
| Relative To | The `Delta` value and `Relative To` properties can be used to express the price as a percentage relative to another value, such as the invoice. Accepted values: `msrp`, `invoice`. |
| Price Source | The source where this value came from, such as `Kelley Blue Book`. |
| Price Amount | The amount of the price. |
| Price Comments | Explanatory note for pricing, such as `Anniversary Edition`. |
| Comments | Comments about vehicle. |
| Financing Method | Identifies financing option. Accepted values: `cash`, `finance`, `lease`. |
| Financing Amount Type | Payment numbers for financing. Accepted values: `downpayment`, `monthly`, `total`.|
| Financing Amount Limit | Finance amount limit. Accepted values: `maximum`, `minimum`, `exact`.|
| Financing Amount Currency | ISO 4217 currency code. |
| Financing Amount Value | Amount to finance. |
| Financing Balance Type | Type of balance. Accepted values: `finance`, `residual`.|
| Financing Balance Currency | ISO 4217 currency code. |
| Financing Balance Value | Remaining balance value. |
| Interior Color | Interior color. |
| Exterior Color | Exterior color. |
| Preference | A number indicating order of preference, with `1` being the favorite. |

#### Customer

Details about a customer looking to transact a vehicle.

| **Parameter** | **Description** |
| --- | --- |
| Contact Name Part | The part of the name of the contact. Accepted values: `first`, `middle`, `suffix`, `last`, `full`. |
| Contact Name Type | The type of contact. Accepted values: `individual`, `business`. |
| Contact Name Value | The text of the name. |
| Email Preferred | Indicates if the email address is the preferred method of contact (versus a phone number). |
| Email Value | The email address. |
| Contact Phone Type | The type of phone. Accepted values: `voice`, `phone`, `fax`, `cellphone`, `pager`. |
| Contact Preferred Call Time | The preferred time to contact the phone number. Accepted values: `morning`, `afternoon`, `evening`, `nopreference`, `day`.|
| Phone Preferred | Indicates if the phone is the preferred method of contact (versus email). |
| Phone Number | The phone number. |
| Contact Address Type | The type of address. Accepted values: `work`, `home`, `delivery`. |
| Contact Street Address Value | The number and name of the street. |
| Contact Apartment Number | Apartment number of customer. |
| Contact City | The name of the city. |
| Contact Region Code | State or province. |
| Contact Zip Code | The postal code (zip code). |
| Contact Country | ISO 3166 country code. |
| Customer Comments | Comments captured from the customer. |

#### Vendor

Provides information about the vendor, usually the dealer, that the customer has requested service from.

| **Parameter** | **Description** |
| --- | --- |
| Vendor Sequence | A number used to track the history of this piece of data. |
| Vendor Source | Name of the source that created this ID. |
| Vendor ID Value | The ID of the vendor. |
| Vendor Name | Name of the vendor or dealer. |

#### Provider

Identifies the service provider that originated the lead.

| **Parameter** | **Description** |
| --- | --- |
| Provider Name Part | The part of the name of the contact. Accepted values: `first`, `middle`, `suffix`, `last`, `full`. |
| Provider Name Type | The type of provider. Accepted values: `individual`, `business`. |
| Provider Name Value | The text of the name. |
| Service | Name of service that originated the lead (subsource). |
| Lead Type | Type of lead. Accepted values: `internet`, `phone`, `showroom`, `campaign`.|