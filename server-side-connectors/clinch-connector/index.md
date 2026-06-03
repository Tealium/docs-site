---
title: Clinch Connector Setup Guide
description: This article describes how to set up the Clinch connector.
url: https://docs.tealium.com/server-side-connectors/clinch-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Clinch API
* API Version: 1.0
* API Endpoint: `https://trkweb.clinch.co/trk`

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Client ID**  
  * (Required) The Client ID. (`cid`)
* **Data Source ID**  
  * (Required) The Data Source ID. (`dsid`)

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event

#### Technical Parameters

| **Parameter** | **Description** |
| --- | --- |
| `referrer` | The page URL where the event originated from. |
| `timestamp` | The event time stamp in UTC. |
| `tcf` | The GDPR consent string using IAB (Interactive Advertising Bureau). |
| `user_ip` | The user IP address. |
| `user_agent` | The user agent. |

#### Event Type

Select the event type. The following values are available: 

| **Event type** | **Description** |
| --- | --- |
| `PageView` | Page view. | 
| `HomePage` | Home page view.|
| `Landing` | Landing page view.|
| `Search` | Search results page view.|
| `Category` | Category page view. |
| `Details` | Product details page view.|
| `DetailsExit` | Exit product details page view. |
| `AddToCart` | Add to cart. |
| `RemFromCart` | Remove from cart. |
| `CartPage` | Cart page view. |
| `AddToWishList`| Add to wishlist. |
| `Checkout` | Initiate checkout or any step of the checkout. |
| `conv` | Purchase, or any other distinct conversion event. | 
| `Registration` | Registration, also considered a conversion. |
| `OfflineConv` | Offline conversion, such as an in-store purchase. |
| `Other` | Other event. |

#### Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| `stype` | The event secondary type (usually provided in conversion events). |
| `product` | The product type, if the event contains products or categories. For example, `Ecommerce`, `Flight`, `Hotel`, `Package`, or `Car`. |

#### Identity Parameters

| **Parameter** | **Description** |
| --- | --- |
| Client-encoded ID | The client-encoded ID. If not provided, `clinchClickId` will be skipped. |
| `clinch-sid` | The Clinch cookie ID, obtained through cookie sync with Clinch or read from the website first-party cookie `clinch-sid`. |
| `clinchClickId` | The value expected for `clinchClickId_{client_enc_id}` is the first-party cookie value for the cookie `clinchId_{client_enc_id}`. |
| Email Address | (Already SHA256 hashed) Provide an email address which has been already SHA256 hashed. |
| Email Address | (Apply SHA256 hash) Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| `atsEnvelop` | The LiveRamp Authenticated Traffic Solution (ATS) envelope. |
| `uid2_0` | The `UID2.0` identifier. |
| `did` | The mobile resettable advertising ID, such as ADID and IDFA. |

#### Content (Ecommerce)

| **Parameter** | **Description** |
| --- | --- |
| `ids` | A comma-separated string of the viewed product IDs. These IDs must match product IDs in the product feed. |
| `category` | The product category. This value must match the category in the product feed. |
| `recommended` | The a comma-separated string of recommended product IDs. These are product IDs that the website or vendor recommendation engine may suggest to the user, as opposed to products that the user engaged with. These values must match product IDs in the product feed. |
| `term` | The search term from a search event. |

#### Content (Travel)

| **Parameter** | **Description** |
| --- | --- |
| `from` | The origin city or airport data code. This code must match a city or airport code in the product feed. |
| `to` | The destination city or airport data code. This code must match a city or airport code in the product feed. |
| `depart` | The departure date in `ISO 8601` format. For example, `2023-09-21`. |
| `return` | The return date in `ISO 8601` format. For example, `2023-09-21`. |
| `city` | The city code for hotel products. This code must match the city parameter in the hotel feed. |
| `ids` | A comma-separated list of the hotel IDs. |

#### Content (Car)

| **Parameter** | **Description** |
| --- | --- |
| `postal_code` | The postal code for the vehicle location. |
| `make` | The manufacturer of the vehicle. |
| `model` | The model of the vehicle. |
| `year` | The year the vehicle was manufactured. |
| `state_of_vehicle` | The current condition of the vehicle. |
| `exterior_color` |  The color of the vehicle exterior. |
| `transmission` | The type of transmission in the vehicle. |
| `body_style` | The style of the vehicle body. |
| `fuel_type` | The type of fuel the vehicle uses. |
| `drivetrain` | The vehicle drivetrain configuration. |
| `price` | The price of the vehicle. |
| `preferred_price_range` | The range of preferred prices for the vehicle. |

#### Purchase Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| `orderId` | The purchase order ID or confirmation ID. |
| `amount` | The total price amount. |
| `currency` | The three-letter currency code. |

#### Privacy &amp; Consent

| **Parameter** | **Description** |
| --- | --- |
| `tcf_string` | The GDPR TCF (Transparency and Consent Framework) string. |
| `ccpa_string` | The CCPA privacy string. This parameter is deprecated and has been replaced with Global Privacy Platform (GPP). Use `gpp_string` instead. |
| `gpp_string` | The GPP consent string. |

#### Other

Select one or more attributes. The connector sends these attributes as a comma-separated list to the user profile at Clinch.

## Examples

### Ecommerce category example

The following example table lists the parameters for an event where the user views a category page on an online store. The category is `mens-shoes`, and the user viewed three products. The event includes the `hem` hashed email identifier:

| Parameter | Example Value |
| --------- | ------------- |
| `cid`| `ter634` |
| `dsid`| `53ter45` |
| `product`| `ecommerce` |
| `type`| `Category` |
| `ids`| `111,222,333` |
| `timestamp`| `1664064000` |
| `hem`| `a64d47276a22f4eb7ee9e4203d2c627d` |
| `referrer`| `https://myonlinestore.com/category/mens-shoes` |

### Car category example

The following example table lists the parameters for an event where the user views a car page on the website and the category is `car`. The event includes the `hem` hashed email identifier:

| Parameter | Example Value |
| --------- | ------------- |
| `cid` | `ogv7Q1` |
| `dsid` | `whbb7YK` |
| `product` | `car` |
| `timestamp` | `1664064000` |
| `type` | `details` |
| `ids` | `123ABC456,789SDX023` |
| `postal_code` | `90210` |
| `make` | `Toyota` |
| `model` | `Corolla` |
| `year` | `2020` |
| `state_of_vehicle` | `New` |
| `exterior_color` | `Blue` |
| `transmission` | `Automatic` |
| `body_style` | `Sedan` |
| `fuel_type` | `Gasoline` |
| `drivetrain` | `FWD` |
| `price` | `20000` |
| `currency` | `USD` |
| `preferred_price_range` | `[15000, 25000]` |
| `hem` | `a64d47276a22f4eb7ee9e4203d2c627d` |