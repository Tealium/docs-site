---
title: Awin Conversions Connector Setup Guide
description: This article describes how to set up the Awin Conversions connector.
url: https://docs.tealium.com/server-side-connectors/awin-conversions-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Awin API
* API Endpoint: `https://www.awin1.com`
* Documentation: [Awin: Awin API](https://developer.awin.com/apidocs/conversion-api)
* Authentication Type: OAuth2.0
* Tag Documentation: [Awin tag](https://docs.tealium.com/awin-tag/)

## How it works

We recommend a hybrid setup using both a tag and connector. This configuration ensures maximum data resilience, improves event matching with server-side data, and maintains data flow continuity while retaining real-time client-side data. The connector uses the Awin tag to attribute the conversions that result from a referral link containing an `awc` query string parameter to identify the source of the traffic. Using Tealium extensions or persisting the `awc` parameter and sending it from the server-side connector ensures the purchase is credited to the correct commission group.


<blockquote>
Because Awin no longer supports the use of pixel-only implementations due to various browser updates, this connector lets you use the [Awin S2S API](https://developer.awin.com/docs/direct-s2s) implementation as a fallback.
</blockquote>


## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Token**  
(Required) This token is linked to your personal user account. For more information about creating your token, see [AWIN: AWAuthentication and Authorization](https://developer.awin.com/apidocs/api-authentication).
* **Merchant (Advertiser ID)**  
Applicable Awin advertiser ID. Contact your Awin account manager for support.

Click **Done** when you are finished configuring the connector.

### Deduplication

If you are working with multiple marketing channels and/or networks, it is necessary to perform de-duplication so that commission is not paid out to several traffic sources for the same conversion. For more information, please see below regarding the Channel Parameter and [AWIN: De-duplication](https://advertiser-success.awin.com/s/article/What-is-De-Duplication).

### Channel parameter

Awin strongly advises all clients to use the **Channel Parameter** to instruct our system how to process each conversion based on the source of the traffic.

Populating that parameter with the winning channel code allows Tealium to handle the request in four ways:

* Do not process.
* Process if any Awin cookie is present.
* Only process if an Awin click cookie is present.
* Only process if an Awin post-view cookie is present.

## Actions

| **Action Name**          | **AudienceStream** | **EventStream** |
|:-------------------------|:-------------------|:----------------|
| Send Conversion          | ✓                  | ✓               |
| Product Level Conversion | ✓                  | ✓               |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion

Server to Server Tracking is a mandatory element of tracking. The requirement is that conversion data is sent (through  a HTTPS request through the Tealium Connector) directly from the Tealium Customer Data Hub to Awin’s servers.

#### Parameters

| **Parameter**| **Description**|
|:---|:--- |
| Total Amount | (Required) The subtotal amount in the order after any relevant discounts are applied, but before any additional fees such as taxes, delivery charges, or relevant service charges. The value must be a float data type, no thousand separator is allowed, and the decimal place must be a standard dot (`.`) character. |
| Order Reference | (Required) The unique booking or order ID.|
| Merchant (Advertiser ID) | The advertiser program ID. This value overwrites the value from the configuration screen.|
| Commission Group Code | Recommended. The code or codes for the commission groups you want to attribute the transaction to. This parameter can be a string for a single group or an array for multiple groups. Accepted characters are uppercase alphanumerics, underscores, and hyphens. If this parameter is not populated, Awin uses the default commission group. |
| Commission Group Amount | The commission amounts that you want to assign to each commission group. This parameter can be a string for a single group or an array for multiple groups. Array values must appear in the same order as the commission group array. If not mapped, the default value is the mapped total amount. |
| Channel | The channel name of the last click referrer. Always use **aw** for Awin, which is the default value. This value must be 20 alphanumeric characters or less. We strongly suggest that you include this parameter so the Awin system knows how to process each conversion based on the source of the traffic. Example values may include: `aw` (which should always be used for Awin), `display`, or `ppc`. For more information, see [Awin: Channel parameter](https://developer.awin.com/docs/channel-parameter). |
| AWC parameter | This value is appended to the landing page URL by Awin to identify the source of the click. You must supply a value for either the **AWC parameter** or the **Voucher Code**. The `awc` value is a parameter that is appended to the landing page URL by Awin to identify the source of the click. You must configure your site to record the `awc` value when the end user lands on the site, using a server-side scripting language. This value will be used to populate the `cks` parameter on conversion. This function needs to be called on every page. If you are capturing the awc value with a cookie, follow these guidelines: <ul><li>The cookie must be set the in HTTP response header and not in a client-side script. For example, a cookie set in PHP is fine.</li><li>The cookie should set the cookie with the HTTP Only flag.</li><li>The cookie should be set with the secure flag.</li></ul> |
| Voucher Code | A URL-encoded voucher code for the transaction. You must supply a value for either the **AWC parameter** or the **Voucher Code**.|
| Currency Code| <ul><li>Recommended. The ISO currency code of the currency that was used in the transaction, for example `GBP` or `USD`.</li><li>This parameter is highly recommended to maintain accurate tracking.</li></ul> |
| Custom Parameters | The input data for single or multiple custom tracking parameters. |
| Test Mode| Incoming tracking requests will not be processed for the purposes of testing.  |

### Product Level Conversion

Product Level Tracking lets an advertiser produce much more in-depth reporting where the performance of individual products can be measured.

#### Parameters

| Parameter | Description |
|:---|:---|
| Total Amount | (Required) The subtotal amount in the order after any relevant discounts are applied, but before any additional fees such as taxes, delivery charges, or relevant service charges. The value must be a float data type, no thousand separator is allowed, and the decimal place must be a standard dot (`.`) character. |
| Order Reference| (Required) The unique booking or order ID.|
| Merchant (Advertiser ID) | The advertiser program ID. This value overwrites the value from the configuration screen. |
| Commission Group Code | Recommended. The code or codes for the commission groups you want to attribute the transaction to. This parameter can be a string for a single group or an array for multiple groups. Accepted characters are upper-case alphanumerics, underscores, and hyphens. If this parameter is not populated, Awin uses the default commission group. The commission group code or codes is mapped to the parts parameter, and will also be mapped at the product level.</li></ul> |
| Commission Group Amount | The commission amounts that you want to assign to each commission group. This parameter can be a string for a single group or an array for multiple groups. Array values must appear in the same order as the commission group array. If not mapped, the default value is the mapped total amount. |
| Channel | The channel name of the last click referrer. Always use the default value `aw` for Awin,. This value must be 20 alphanumeric characters or less. We strongly suggest that you include this parameter so the Awin system knows how to process each conversion based on the source of the traffic. Example values may include: `aw` (which should always be used for Awin), `display`, or `ppc`. |
| AWC parameter | This value is appended to the landing page URL by Awin to identify the source of the click. You must supply a value for either the **AWC parameter** or the **Voucher Code**. If you are capturing the awc value with a cookie, follow these guidelines: <ul><li>The cookie must be set the in HTTP response header and not in a client-side script. For example, a cookie set in PHP is fine. The cookie should set the cookie with the HTTP Only flag.</li><li>The cookie should be set with the secure flag.</li></ul> |
| Voucher Code| A URL-encoded voucher code for the transaction. You must supply a value for either the **AWC parameter** or the **Voucher Code**.|
| Currency Code | Recommended. The ISO currency code of the currency that was used in the transaction, for example, `GBP` or `USD`.|
| Product Name| (Required) An array of product names in the transaction.|
| Custom Parameters | The input data for single or multiple custom tracking parameters. |
| Test Mode| Incoming tracking requests are not processed for the purposes of testing. |

#### Product

| **Parameter** | **Description** |
| --- | --- |
| Product ID| (Required) An array of unique product IDs in the transaction. |
| Product Quantity | (Required) An array of the quantity of each of the products in the transaction.|
| Product SKU | (Required) An array of the SKU of each of the products in the transaction. |
| Product Item Price| (Required) An array of the prices for a single quantity of each of the products in the transaction. This single unit price must reflect the price after any relevant discount is applied, but before any taxes or additional charges are applied. The value must be a float, no thousand separator is allowed, and the decimal place must be a standard dot character.|
| Product Category | (Required) An array of each product's category in the transaction.|