---
title: CJ Tracking API Connector Setup Guide
description: This article describes how to set up the CJ Tracking API connector.
url: https://docs.tealium.com/server-side-connectors/cj-tracking-api-connector/
---
CJ recommends that you use the Universal Tag and Tracking API concurrently for web tracking events because each supports or enhances CJ's offerings. Using the Tracking API requires back-end changes on the CJ side and requires collaboration with your Client Integration team. Contact your CJ account team or `support@cj.com` for more details.

## API Information

This connector uses the following vendor API:

* API Name: CJ API
* API Endpoint:
    * Without trace (live endpoint): `https://tracking.api.cj.com/graphql/`
    * With trace (test endpoint): `https://tracking.api.cj.com/graphqltest/`
* Documentation: [CJ API](https://developers.cj.com/graphql/reference/private/Tracking)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 10 minutes
* Max size of requests: 100 MB

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Order Data | ✗  | ✓ |
| Send Order Restatement | ✗ | ✓ |
| Send Order Cancellation | ✗ | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/server-side/connectors/manage/) article.

After adding the connector, configure the following settings:

* **Personal Access Token**  
(Required) Your CJ Tracking API personal access token. Generate your personal access token by navigating to the [CJ personal access tokens](https://developers.cj.com/account/personal-access-tokens) page and logging into your account.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Order Data

#### Parameters

| **Parameter**  | **Destination**  | **Description** |
|:----------|:-----------|:---------------|
| Enterprise ID | `enterpriseId`  | (Required) The unique client ID assigned by CJ's Client Integration team.     |
| Action Tracker ID | `actionTrackerId` | (Required) The static value given by CJ's Client Integration team for the action taken.   |
| CJ Event  | `ciEvent` | (Required) CJ-defined correlating event ID (also known as the CJ Click ID).     |
| Order ID  | `orderId` | (Required) Client-defined Order identifier.     |
| Event Time  | `eventTime` | (Required) The timestamp of the event.      |
| Order Amount  | `amount`  | (Required) The total order amount.      |
| Order Discount  | `discount`  | The discount applied to the order.      |
| Coupon Code | `coupon`  | The coupon code applied to the order.     |
| Currency  | `currency`  | The currency used on the order.     |
| Product Prices  | `unitPrice` | An array of the unit price of each product in the order.    |
| Product SKUs  | `sku` | An array of each product's SKU in the order.      |
| Product Quantities  | `quantity`  | An array of the amount ordered of each product.     |
| Product Discounts | `discount`  | An array of the amount of a product discount applied to the product's unit price.   |
| Advertiser Vertical |   | Supported values are: `Retail`, `Finance`, `Travel`, `NetworkServices`.   |
| Ancillary Spend | `ancillarySpend`  | The ancillary spend amount for the transaction (Advertiser-only attribute),     |
| Annual Fee  | `annualFee` | Annual fee associated with this product.      |
| Application Status  | `applicationStatus` | Identifies the status of the application at the time the transaction is sent to CJ.   |
| Apr | `apr` | APR at time of application approval.      |
| Apr Transfer  | `aprTransfer` | APR for transfers.      |
| Apr Transfer Time | `aprTransferTime` | APR transfer period in months.      |
| Booking Date  | `bookingDate` | The date booking was made in format `YYYY-MM-DD`.     |
| Booking Status  | `bookingStatus` | The status of the booking. For example: `confirmed`, `pending`, etc.     |
| Booking Value Post Tax  | `bookingValuePostTax` | The value of the booking after taxes.     |
| Booking Value Pre Tax | `bookingValuePreTax`  | The value of the booking before taxes.      |
| Brand | `brand` | The brand of item or items purchased.     |
| Brand ID  | `brandId` | The brand identifier of the item booked.      |
| Business Unit | `businessUnit`  | The business unit the customer purchased through.     |
| Campaign ID | `campaignId`  | The advertiser-specific marketing campaign ID.      |
| Campaign Name | `campaignName`  | The advertiser-specific marketing campaign name.      |
| Card Category | `cardCategory`  | The card category's name.     |
| Car Options | `carOptions`  | Other car options chosen during the transaction. For example, `insurance`.     |
| Cash Advance Fee  | `cashAdvanceFee`  | The cash advance fee associated with this product.      |
| Category  | `category`  | The category of the item. For example, if a customer applies for a Personal Cash-back Credit card: `service_type=cc&item_type=personal&category=cashback`).  |
| City  | `city`  | The city name of the hotel or event's location.     |
| Class | `class` | The class rating of the item booked or purchased.     |
| Confirmation Number | `confirmationNumber`  | The confirmation number for the provider. For example, a flight confirmation number from an airline.   |
| Contract Length | `contractLength`  | The length of the contract, in months.      |
| Contract Type | `contractType`  | An advertiser-specific description of the contract.     |
| Country Code  | `countryCode` | The country where the transaction occurred.     |
| Coupon Discount | `couponDiscount`  | Amount discounted from any coupon used.     |
| Coupon Type | `couponType`  | The type of coupon used.      |
| Credit Line | `creditLine`  | The amount of credit extended to the customer.      |
| Credit Quality  | `creditQuality` | Quality of customer's credit. Supported values are: 300-579=Very Poor, 580-669=Fair, 670-739=Good, 740-799=Very Good, 800-850=Exceptional.  |
| Credit Report | `creditReport`  | If the customer received a credit report, purchased it, got a free report, or started a trial for a reporting service.  |
| Cruise Type | `cruiseType`  | The type of cruise. For example: `Alaskan`, `Caribbean`, etc.    |
| Customer Country  | `customerCountry` | The country the customer purchasing is in, per ISO 3166-1 alpha 2 country codes. For example, `US`, `UK`, `AU`, `FR`.   |
| Customer Segment  | `customerSegment` | The advertiser-specific customer segment.     |
| Customer Status | `customerStatus`  | If the customer is new or existing.     |
| Customer Type | `customerType`  | The type of customer. For example: `company`, `individual consumer`, `business`, `leisure`.    |
| Delivery  | `delivery`  | The method of delivery.       |
| Description | `description` | Product or card description.      |
| Destination City  | `destinationCity` | The destination city's name.      |
| Destination Country | `destinationCountry`  | The service destination's country, formatted using ISO 3166-1 alpha 2 country codes. For example, `US`, `UK`, `AU`, `FR`.   |
| Destination ID  | `destinationId` | The service destination ID, typically an advertiser-defined code representing a destination city or destination state/province. For example: `728660`. |
| Destination State | `destinationState`  | The service destination state/province, formatted using ISO 3166-2 state codes.   |
| Domestic  | `domestic`  | If the customer resides in the United States.     |
| Dropoff Iata  | `dropoffIata` | IATA code for dropoff location, if the dropoff is at an airport.    |
| Dropoff ID  | `dropoffId` | Unique car rental agency ID for the dropoff location.     |
| Duration  | `duration`  | Duration of event or item in days, such as nights for a hotel stay or length of a trial subscription.   |
| End Date Time | `endDateTime` | The check-out date/time, departure date/time, etc.    |
| Flight Fare Type  | `flightFareType`  | The type of flight fare. For example `Gotta Get Away`.     |
| Flight Options  | `flightOptions` | Other options selected for a flight package. For example, `wiki`.    |
| Flight Type | `flightType`  | The type of flight. For example, `direct`, `layover`, `overnight`.     |
| Flyer Miles | `flyerMiles`  | If flyer miles were earned from this flight.      |
| Funded Amount | `fundedAmount`  | Account of the account funding.     |
| Funded Currency | `fundedCurrency`  | The currency of the account's initial funding.      |
| Genre | `genre` | The entertainment category or genre. For example, `books`, `movies`, `streaming`, `music`, etc. This parameter is transaction-level only.  |
| Guests  | `guests`  | The number of guests.       |
| Iata  | `iata`  | The code for each city in a flight schedule in a comma-separated list; commas must be URL-encoded.    |
| Introductory Apr  | `introductoryApr` | The intro APR for purchases. If the introductory APR is not different than overall APR, use the **APR** parameter.   |
| Introductory Apr Time | `introductoryAprTime` | The introductory APR period in months.      |
| Item ID | `itemId`  | The ID for item or items purchased. If multiple items, the parameter uses a comma-separated list.   |
| Item Name | `itemName`  | The name of the purchased item.     |
| Item Type | `itemType`  | The type of item. For example, if a customer applies for a Personal Cash-back Credit card: `service_type=cc&item_type=personal&category=cashback`). |
| Itinerary ID  | `itineraryId` | The booking itinerary ID.     |
| Lifestage | `lifestage` | The general demographic (such as new mover or student or small business) that indicates how and why a card will be used.  |
| Location  | `location`  | An advertiser-specific ID or name that can be used to identify the store or location the customer will visit or has visited.  |
| Loyalty Earned  | `loyaltyEarned` | The level of the customer's loyalty status.     |
| Loyalty First Time Signup | `loyaltyFirstTimeSignup`  | If this order resulted in the consumer joining the loyalty program.     |
| Loyalty Level | `loyaltyLevel`  | If loyalty points were used.      |
| Loyalty Redeemed  | `loyaltyRedeemed` | if loyalty points were earned.      |
| Loyalty Status  | `loyaltyStatus` | The customer's status of membership.      |
| Margin  | `margin`  | The advertiser-only attribute that indicates the profit margin for the transaction.   |
| Marketing Channel | `marketingChannel`  |  The marketing channel.     |
| Minimum Balance | `minimumBalance`  | The value of the minimum cash balance requirement for the account.    |
| Minimum Deposit | `minimumDeposit`  | The minimum deposit amount.     |
| Minimum Stay Duration | `minimumStayDuration` | The minimum required stay duration, in days.      |
| No Cancellation | `noCancellation`  | If a no cancellation allowed policy exists on the transaction, `yes` or `no`.     |
| Order Subtotal  | `orderSubtotal` | The subtotal of the order.      |
| Origin City | `originCity`  | The service origin city name, such as New York.     |
| Origin Country  | `originCountry` | The service origin country code, formatted using ISO 3166-1 alpha 2 country codes. For example, `US`, `UK`, `AU`, `FR`.   |
| Origin State  | `originState` | The service origin state/province formatted using ISO 3166-2 state codes.     |
| Paid at Booking Post Tax  | `paidAtBookingPostTax`  | Amount paid at booking after taxes.     |
| Paid at Booking Pre Tax | `paidAtBookingPreTax` | Amount paid at booking before taxes.      |
| Payment Model | `paymentMethod` | The model of payment used. For example, `advertiser-specific`.     |
| Pickup Iata | `pickupIata`  | The IATA code for an airport pickup location.     |
| Pickup ID | `pickupId`  | The unique car rental agency location ID used for pickup.     |
| Platform ID | `platformId`  | The device that the customer is using. For example, `mobile`, `tablet`, etc.   |
| Point of Sale | `pointOfSale` | The customer's point of sale.     |
| Port  | `port`  | Departure port for cruises.     |
| Preorder  | `preorder`  | If the customer purchased the item before it was available for sale.    |
| Prepaid | `prepaid` | If the customer prepaid the transaction, `yes` or `no`.     |
| Prequalify  | `prequalify`  | If the applicant was pre-qualified for the card.      |
| Promotion | `promotion` | The promotion applied. For example: `summer sale`.     |
| Promotion Amount  | `promotionAmount` | The numeric amount associated with the promotion. For example, if the promotion is $500 cash back, this value is `promotion=dollars&promotion_amt=500`) |
| Promotion Condition Threshold | `promotionConditionThreshold` | The threshold needed to get the discount.     |
| Promotion Condition Type  | `promotionConditionType`  | Types of promotional conditions.      |
| Promotion Ends  | `promotionEnds` | The date the promotion ends formatted using ISO 8601 standards. For example, `2022-12-25T15:30:50.111Z`.    |
| Promotion Starts  | `promotionStarts` | The date the promotion begins formatted using ISO 8601 standards. For example, `2022-12-25T15:30:50.111Z`.  |
| Promotion Type  | `promotionType` | The promotion type.       |
| Quantity  | `quantity`  | The quantity for a given SKU, simple actions only. If you are using an item-based action, use `QTYx`.   |
| Rating  | `rating`  | The star rating of the item booked or purchased.      |
| Room Type | `roomType`  | The type of room booked for a hotel or cruise.      |
| Rooms | `rooms` | The number of rooms booked.     |
| Service Type  | `serviceType` | The type of financial service the customer signed up for or purchased.    |
| Ship Name | `shipName`  | The name of the cruise ship.      |
| Start Date Time | `startDateTime` | The check-in date/time, arrival date/time, or similar start time for the booked or purchased item.    |
| State | `state` | Defines the state or province where the store is located, formatted using ISO 3166-2 state codes. For example, Alaska’s code is `US-AK` and Bangkok is `TH-10`. |
| Subscription Fee  | `subscriptionFee` | The cost of subscription fee featured when signing up for free trial.     |
| Subscription Length | `subscriptionLength`  | Product duration. For example: `indefinite`, `1 month`, `3 months`, or `6 months`).    |
| Tax Amount  | `taxAmount` | The amount of tax.      |
| Tax Type  | `taxType` | The type of tax.      |
| Transfer Fee  | `transferFee` | The transfer fee amount for a credit card.      |
| Travel Type | `travelType`  | The type of travel being booked. For example: `air`, `car`, `activities`, `cruise`, `events`, `hotel`, `package`, `restaurants`, `travel guides`, `vacation rental`, `other`.  |
| Trip Type | `tripType`  | The type of trip booked or purchased. For example: one-way, round-trip, multi-city, round trip and hotel.    |
| Upsell  | `upsell`  | If the customer converted from a trial to a subscription.     |
| CJ User |   | The CJ user ID.       |

### Action - Send Order Restatement

This action lets you send order restatements to CJ Tracking. Order restatements allow attributes to be changed for, or added to, a commissionable order that is not already locked or closed. This action completely overwrites the current state of the order and updates the order to contain only the information provided in the restatement.

#### Parameters

| Parameter                  | Destination        | Required? | Description |
|----------------------------|-------------------|-----------|-------------|
| Enterprise ID | `enterpriseId`      | Required  | Unique client ID assigned by CJ's Client Integration team. |
| Action Tracker ID          | `actionTrackerId`   | Required  | Static value given by CJ's Client Integration team for the action taken. |
| Order ID                   | `orderId`           | Required  | Client defined order identifier. |
| Update Time  | `updateTime`        | Required  | A datetime in UTC ISO 8601 format with `Z` as the zone designator for UTC offset, rendered in JSON as a string. For example: `1970-03-27T12:13:14-05:00` or `1970-03-27T12:18:14Z`. |
| CJ Event    | `cjEvent`           | Optional  | CJ defined correlating event ID (also referred to as CJ Click ID). |
| Order Amount               | `amount`            | Optional  | Total order amount. |
| Order Discount             | `discount`          | Optional  | Discount applied to the order. |
| Vertical Parameters        | `verticalParameters` | Optional  | Additional information to capture specific verticals the restatement is associated with. |
| Custom Parameters          | `customParameters`  | Optional  | If any items are present in the array, values cannot be null. |
| Items                      | `items`             | Optional  | If any items are present in the array, values cannot be null. |
| Coupon Code                | `coupon`            | Optional  | Coupon code applied to the order. |
| Currency                   | `currency`          | Optional  | Currency used for the order. For example, `USD`. |
| Bypass Channel             | `bypassChannel`     | Optional  | Customizes the attribution process for transactions. For example, `Channel=CJ`. The value can be one of the following: <ul><li>`CJ`</li><li>`Direct`</li><li>`Affiliate_other`</li><li>`Display`</li><li>`Social`</li><li>`Search`</li><li>`Email`</li><li>`Other` |
| Status                     | `status`            | Optional  | The status of the order. Value can be `Pending` or `Accepted`. |
| Reason for Correction      | `correctionReason`  | Optional  | The value can be one of the following: <ul><li>`InvalidCreditCard`</li><li>`UnqualifiedLead`</li><li>`CannotShipSoldOut`</li><li>`DuplicateOrder`</li><li>`ReturnedMerchandise`</li><li>`Other`</li></ul> |

### Action - Send Order Cancellation

This Action tells CJ that you want to cancel an existing order and do not want to pay a commission or fee for that order. This concept is similar to what CJ traditionally calls a full correction. 

#### Parameters

| Parameter             | Destination      | Required? | Description |
|-----------------------|-----------------|-----------|-------------|
| Enterprise ID        | `enterpriseId`    | Required  | Unique client ID assigned by CJ's Client Integration team. |
| Action Tracker ID    | `actionTrackerId` | Required  | Static value given by CJ's Client Integration team for the action taken. |
| Order ID            | `orderId`        | Required  | Client defined order identifier. |
| Update Time        | `updateTime`      | Required  | A datetime in UTC ISO 8601 format with `Z` as the zone designator for UTC offset, rendered in JSON as a string. For example, `1970-03-27T12:13:14-05:00` or `1970-03-27T12:18:14Z`. |
| Reason for Cancellation | `correctionReason` | Optional  | The value can be one of the following: <ul><li>`InvalidCreditCard`</li><li>`UnqualifiedLead`</li><li>`CannotShipSoldOut`</li><li>``DuplicateOrder</li><li>`ReturnedMerchandise`</li><li>`Other`</li></ul> |
| Status              | `status`         | Optional  | If the order you intend to cancel uses open-ended locking, you must set Status to `Declined` for the cancellation request. |

## Vendor documentation

For additional information, see the following vendor documentation:

* [CJ Tracking API Overview](https://developers.cj.com/docs/advertiser-api-tracking/api-overview)
* [Order Restatements](https://developers.cj.com/docs/advertiser-api-tracking/restatements)
* [Order Cancellations](https://developers.cj.com/docs/advertiser-api-tracking/cancellations)