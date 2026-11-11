---
title: CJ Affiliate Mobile Application Tag Setup Guide
description: This article describes how to set up the CJ Affiliate Mobile Application Tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/cj-affiliate-mobile-application-tag/
---
CJ Affiliate is the leading global affiliate marketing network, specializing in pay-for-performance programs that drive results for businesses around the world. The purpose of the CJ Affiliate Mobile Application Tag is to inform CJ of user activity across clients' Mobile Applications, allowing for tracking of installations and In App Events.

## Tag tips

Use mappings to:

* Dynamically override config data.
* Dynamically override the E-Commerce extension values.
* Send additional data values.
* Trigger events.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client ID (CID)**: This value is set as each client's CJ Enterprise ID, a static value provided by CJ.
* **Type**: This is a static value provided by CJ. Each Action will have a unique TYPE value.
* **Sale Tag Type**:  
Standard: `CID`, `OID`, `TYPE` and `CURRENCY` are sent.  
Advanced: Sends additional values `ITEM`, `AMT`, `QTY`, `DCNT`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Type | Description|
|---| ---| ---|
|User Agent (UA)| String | (Required) The User Agent.|
|CJ Client ID (CID) | Number | (Required) Each client's CJ Enterprise ID, a static value provided by CJ.|
|CJ Action ID (TYPE) | Number | (Required) Each Action will have a unique TYPE value, a static value provided by CJ.|
|Order Number/Unique ID (OID)|  Alphanumeric | (Required) A unique order or invoice identifier, used to reconcile orders in the client's system with CJ to validate each sale or lead. <ul><li>This value is truncated after the 96th character.</li><li>May only contain alphanumeric characters, or underscores.</li><li>Does not include PII, such as a full or partial email address.</li></ul> |
|Method (METHOD)|  String | (Required) |
|Time Of Action (EVENTTIME)| Alphanumeric | (Required) The URL-encoded time of the event in any of the following formats:  <ul><li>ISO 8601 standard </li><li>`yyyy-mm-ddThh24:mm:ss+/-hh:mm` </li><li>year, month, date, time, offset from UTC </li><li>`YYYY-MM-DDTHH:MM:SSS.SSSZ` </li></ul> |
|CJEVENT Value From URL (CJEVENT)| Alphanumeric | (Required) A unique CJ-generated token passed to your site that stores referring publisher data for cookieless attribution.|
|Subtotal Associated With Action (AMOUNT)| Number | (Required) The subtotal of the purchase, not including shipping or tax.|
|Currency Code (CURRENCY) | ISO Currency Code |  (Required) A three-letter code that identifies the currency used for the order's amount value. If not specified, will default to the Advertiser functional currency in the CJ interface.|
|Vendor Name (VENDOR) | Alphanumeric | (Required) The name of the vendor sending the postback to CJ.|
|Discount (DISCOUNT) | Number | (Required) A discount value applied to the entire order.|
|Coupon (COUPON)| String|  A coupon, voucher, or discount code used at the time of purchase.|
|SKU (SKU) (Overrides `_cprod`)|  Array|  The identifier of each item in the order. <ul><li>This value must be less or equal to 100 characters.</li><li>There is a maximum of 100 sets of item-based values in each order.</li><li>Only alphanumeric strings, dashes, and underscores are allowed.</li></ul> |
|Items Amount (AMT) (Overrides `_cprice`)| Array | The price of each item in the order.|
|Quantity (QTY) (Overrides `_cquan`)| Array | The quantity of each item in the order. Any decimals in the value are ignored, so `1.0` will be interpreted as `10`.|
|Items Discount (DCNT) (Overrides `_cpdisc`)| Array | The discount value that is applied to each individual item in the order.|

### Additional parameters

|Variable| Type | Description|
|---| ---| ---|
|Brand (`brand`)| Alphanumeric | Brand of items purchased. If multiple brands were purchased, one will be selected.|
|Brand Id (`brandId`)| Alphanumeric | Identifier of the brand of items purchased. If multiple brands were purchased, one will be selected.|
|Category (`category`)| Alphanumeric | Category of items purchased. If multiple categories were purchased, one will be selected.|
|Customer Status (`customerStatus`)| Alphanumeric | Customer's status based on past purchases (for example: `new`, `lapsed`, `return`, etc.).|
|Delivery (`delivery`)| Alphanumeric Method of delivery (for example: `in_store_pick_up`, `digital`, `express`, etc.).|
|Loyalty Earned (`loyaltyEarned`)| Alphanumeric|  Loyalty points earned on the transaction.|
|Loyalty First Time Signup (`loyaltyFirstTimeSignup`)| Alphanumeric | Whether this order coincided with the customer joining the loyalty program.|
|Loyalty Level (`loyaltyLevel`)| Alphanumeric | The customer's level in the loyalty program.|
|Loyalty Redeemed (`loyaltyRedeemed`)| Alphanumeric | Loyalty points used during the transaction.|
|Loyalty Status (`loyaltyStatus`)| Alphanumeric | Whether the customer is a loyalty member.|
|Marketing Channel (`marketingChannel`)| Alphanumeric | Any additional advertiser-defined marketing channels assigned to this transaction.|

## Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|Purchase (`purchase`)| purchase|
|Conversion (`conversion`)| conversion|
|Custom| custom|
