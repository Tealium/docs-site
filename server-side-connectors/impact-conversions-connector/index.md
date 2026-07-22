---
title: Impact Conversions Connector Setup Guide
description: This article describes how to set up the Impact Conversions connector.
url: https://docs.tealium.com/server-side-connectors/impact-conversions-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion | ✓ | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. For more information, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Account SID**  
(Required) Defined by Impact. For example: `MhyXaouO5Ijnw658m6kXoqwlo1IasLKJBX`.
* **Auth Token**  
(Required) Defined by Impact. For example: `t0k5Lr3GciUAqR0JNj1CzxKE2XTEmK5i`.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Send Conversion

#### Conversion Parameters

You must include the following two parameters:

| **Parameter** | **Description** |
| --- | --- |
| Campaign ID | (Required) Unique integer campaign identifier provided by Impact. |
| Order ID | (Required) The unique alphanumeric trackable ID for the in-app conversion. |

You must include one of the following two parameters:

| **Parameter** | **Description** |
| --- | --- |
| Action Tracker ID | Unique integer tracker identifier provided by Impact. |
| Event Type Code | The conversion event type. Go to **Events Types > Actions > View/Edit > Codes** in the Impact platform to view all codes. |

You must include at least one of the following attribution key parameters:

| **Parameter** | **Description** |
| --- | --- |
| Custom Profile ID | Advertiser’s own user identifier value of string type. If custom profile ID was passed when the user logged an initial visit event, the same custom profile ID value must be passed here. |
| Click ID | Click ID string value that was captured on the landing page URL or in the Page Load API response. |
| Customer ID | Unique alphanumeric customer identifier your platform assigns to customer accounts. |
| Unique Conversion URL | The unique URL for a partner or source that referred the conversion. Use this parameter only if you configure and assign Unique Domains to your partners. |
| Google Advertising ID | Google advertising ID associated with the mobile device the customer converted on. |
| IDFA | Apple ID for advertising (IDFA) associated with the mobile device the customer converted on. |
| IDFV | Apple ID for vendors (IDFV) associated with the mobile device the customer converted on. |
| Media ID | Unique identifier of the partner or source to which you want to force attribution. |

The following additional parameters are available:

| **Parameter** | **Description** |
| --- | --- |
| Device Manufacturer | The manufacturer of the mobile device the customer used to convert.<ul><li>Android: `manufacturer = android.os.Build.MANUFACTURER;`</li><li>Apple: `NSString *manufacturer = @"Apple";`</li></ul> |
| App Package | The package name for the mobile app that the user installed. Only for mobile conversions.  |
| App Install Referrer |  The install referrer that the Google Play Store passes when the app is installed. Only for Android conversions. |
| App Version | Version of the mobile app. Only for mobile conversions. |
| Caller ID | The unique identifier of the customer in call tracking conversions. Value is used to match the conversion to the originating call record. |
| Location ID | Used for accommodation events, this is the unique identifier for the location specified in this conversion. |
| Location Name | Used for accommodation events, this is the name for the location specified in this conversion. |
| Location Type | Used for accommodation events, this is the category for the location specified in this conversion.|
| Property ID | For mobile app conversions, this value is the **System App ID** of your app on `impact.com`. To find this value, go to **Settings > Mobile Apps** on the Impact platform. |
| Tracking Consent | Indicates whether the user has provided consent to be tracked at the moment of the request. Derived from your consent management platform or through frameworks like Apple’s ATT (App Tracking Transparency) available on iOS. |
| Customer City | The customer's city. |
| Disposition Code | If you have a custom disposition code configured in Impact's event type settings, you can submit that value as a default disposition for the action that results from this conversion. |
| Customer Email | SHA1 hash string of customer’s email. |
| Customer Status | Use string values of `New` or `Returning`. |
| Customer Post Code | Customer’s postal code. |
| Payment Type | String representing payment type of the order. |
| Order Rebate | Decimal representing amount of the order rebate. Used for reporting only. |
| Event Date | Use a string value of `NOW` or dates in <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> or "dd-MMM-yyyy HH:mm:ss z" formats. The default value is `NOW` |
| Order Promo Code | Coupon or promo code string. If there is no promo code for the order, use an empty string. The default value is an empty string. This parameter only supports single codes; it does not support  multiple codes. |
| Currency Code | Required for Sale Actions. The default value is `USD`. Accepts <a href="https://en.wikipedia.org/wiki/ISO_4217">ISO 4217</a> currency codes. |
| User Agent | String identifying the browser and operating system. |
| IP Address | String representing IP Address of the customer. |

#### Conversion Sale Items

If you are passing item-level details, the following item parameters are required:


<blockquote>
All arrays and lists must be of equal length. Single value attributes are expanded to an array that is the same length as all other arrays, repeating the value.
</blockquote>


| **Parameter** | **Description** |
| --- | --- |
| Item Category | Item category identifier of string type. Map array and list values to keys to pass to Impact. |
| Item SKU | Alphanumeric item-specific identifier. Map array and list values to keys to pass to Impact. |
| Item Subtotal | Map array and list values to keys to pass to Impact.  |
| Item Quantity | Integer value representing quantity of the line item. Map array and list values to keys to pass to Impact. |
| Item Price |  Individual unit price for each product in this item. If you use **Item Subtotal**, do not set a value for this parameter.  |

The following item parameters are optional:

| **Parameter** | **Description** |
| --- | --- |
| Item Promo Code |  Promotional code applied to the item for the order. This parameter does not work with unique tracking codes setup for particular partners. |
| Item Total Discount | Discount applied to this line item (not just for each product of this type). This amount is automatically subtracted from the ItemSubTotal to determine the final sale amount for payout and reporting purposes.  |
| Item Sub Category |If applicable, the subcategory for the product referenced at the item level. |
| Item Name | The name for the product referenced.  |
| Item MPN | Manufacturer part number (MPN) for the product referenced. |
| Item Brand |Brand name for the product referenced.   |
| Item Discount | Discount applied to each item purchased of this type.  |
| Item Delivery Type | Type of delivery method specified for this item, for example, `STORE`.  |
| Payment Type |  String representing the payment type for the order. |
| Order Sub Total Post Discount | Used when reporting conversions at the order-level (no item reporting). The subtotal of the order after discounts, taxes, shipping, and any other costs. If you submit item-level data, do not set this value.  |
| Order Discount |For sales, this is the discount applied to the order overall. The discount is automatically subtracted from the order total on processing. If item amounts are used, the discount is subtracted proportionally from each item amount sent in. Do not include shipping costs.   |
| Order Shipping | This parameter is primarily used for retail sales. This is the cost of shipping for this conversion. Do not include shipping costs in the total sale amount used for payout purposes.  |
| Order Tax |  This parameter is primarily used for retail sales. This is the cost of tax for this conversion. Do not include shipping costs in the total sale amount used for payout purposes. |
| Order Margin | This parameter is primarily used for retail sales. This is the total margin made on the conversion (revenue less costs). Typically this is provided either at an item level through the `ItemMargin` parameter or through the product catalog.  |
| Gift Purchase |  If you are tracking gift purchases, set to `true` to mark the order in the conversion as a gift purchase. Set to `false` if the order isn't a gift purchase. |

## Vendor documentation

* [Impact: The conversion object](https://integrations.impact.com/impact-brand/reference/the-conversion-object)