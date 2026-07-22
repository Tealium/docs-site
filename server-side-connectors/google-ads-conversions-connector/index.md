---
title: Google Ads Conversions Connector Setup Guide
description: This article describes how to set up the Google Ads Conversions connector.
url: https://docs.tealium.com/server-side-connectors/google-ads-conversions-connector/
---
## How it works

A Google Ads conversion occurs when a user performs a specified action after clicking an ad or viewing a Display Network ad. The Google Ads Conversions connector uses the Google Ads API, which supports uploading offline conversions and adjusting previously captured conversion values. You can use the connector to upload offline click conversions into Google Ads to track ads that led to sales in the offline world, such as over the phone or through a sales representative. You can upload offline call conversions to track when ads lead to phone calls and when those phone calls lead to valuable customer actions.

## Requirements

* To send offline conversions, configure a Google Ads Import conversion action, and specify either calls or clicks as the source. For more information, see [Google Help documentation regarding offline conversions](https://support.google.com/google-ads/answer/2998031?sjid=13815989904284925133-NC). 
* To adjust a conversion, you must have the original conversion's transaction ID or have the `gclid` and conversion date and time to locate the conversion you want to adjust.

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upload Call Conversion - Legacy | ✓ | ✓ |
| Upload Click Conversion - Legacy | ✓ | ✓ |
| Conversion Restatement | ✓ | ✓ |
| Conversion Retraction | ✓ | ✓ |
| Upload Call Conversion | ✓ | ✓ |
| Upload Click Conversion | ✓ | ✓ |

## API information

This connector uses the following vendor API:

* API Name: Google Ads API
* API Version: v18
* API Endpoint: `https://googleads.googleapis.com/`
* Documentation: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2000
* Max time since oldest request: 10 minutes
* Max size of requests: 2 MB

## Delayed actions

Actions are delayed for 30 minutes to accommodate uploading offline conversions, as per Google’s best practices. For more information about delayed actions using the Google Campaign Manager 360 Floodlight connector, see Google's [Best practices for uploading offline conversions](https://support.google.com/searchads/answer/6074338?hl=en) documentation.


<blockquote>
Actions are not delayed when using [trace](https://docs.tealium.com/manage-traces/) in EventStream or AudienceStream.
</blockquote>


### Consent

The connector sends the value of `GRANTED` for `adUserData` and `adPersonalization` consent by default. To override the default, map a relevant EventStream attribute to `Ad User Data Consent` and/or `Ad Personalization Consent` with a value of `DENIED`.

## Configure settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Customer ID**: Enter an Ads account customer ID to manage, or use the dynamic override field in the action configuration.
* **Manager Customer ID**: If accessing a managed account, enter the **Manager Customer ID**, and the **Customer ID**.

After you configure the connector, click **Done**.

## Action settings - parameters and options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the list.

The following section describes how to set up parameters and options for each action.

### Action - Upload Call Conversion - Legacy

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Customer ID| (Required) Select the customer account ID. Available options reflect accessible customer accounts for authenticated user. |
|Conversion Action|  (Required) Select existing conversion action. Only Google Ads conversion actions of type `UPLOAD_CALLS` are displayed. For more information, see [Google: Google Ads Conversion Tracking](https://support.google.com/google-ads/answer/1722022). |

#### Conversion Data parameters

|**Parameter**| **Description**|
|---| ---|
|Caller ID| (Required) The caller ID from which this call was placed. Caller ID is expected in E.164 format and preceded by the plus (`+`) character. For example, `+16502531234`. |
|Call Start Datetime| (Required) The date and time at which the call occurred. The timezone must be specified. The format is **yyyy-mm-dd hh:mm:ss±hh:mm**. For example, `2020-01-01 12:32:45-8:00`. |
|Conversion Datetime|  (Required) The date and time at which the conversion occurred. This date and time must be after the call time. The timezone must be specified. The format is **yyyy-mm-dd hh:mm:ss±hh:mm**.  For example, `2020-01-01 12:32:45-8:00`. |
|Conversion Value|  The value of the conversion for the advertiser. |
|Currency Code| The currency associated with the conversion value. This is the ISO 4217 3-character currency code. For example,`USD` or `EUR`. |

#### Optional parameters

|**Parameter**| **Description**|
|---| ---|
| Conversion Action Override | Provide a conversion action ID to override the **Conversion Action** parameter. This field lets you use EventStream variables to populate the **Conversion Action ID** parameter. |
| Custom Variables | The custom variables associated with this conversion. For more information, see [Google: Custom Variable](https://developers.google.com/google-ads/api/reference/rpc/v8/CustomVariable). |
|Ad User Data Consent | Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |

### Action - Upload Click Conversion - Legacy

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Customer ID|  Select the customer account ID. Available options reflect accessible customer accounts for authenticated user. |
|Conversion Action| Select the existing conversion action. For more information, see [Google: Google Ads Conversion Tracking](https://support.google.com/google-ads/answer/1722022). |

#### Conversion Data parameters

|**Parameter**| **Description**|
|---| ---|
|Google Click ID|  (Required) The Google click ID (`gclid)` associated with this conversion. Google Click ID, `gbraid`, or `wbraid` are required. |
|Conversion Datetime|  (Required) The date and time at which the conversion occurred. This date and time must be after the call time. The timezone must be specified. The format is **yyyy-mm-dd hh:mm:ss±hh:mm**. For example, `2020-01-01 12:32:45-8:00`. |
|Conversion Value|   The value of the conversion for the advertiser. |
|Currency Code|  Currency associated with the conversion value. This is the ISO 4217 3-character currency code. For example, `USD` or `EUR`. |
|Order ID|  (Required) The order ID associated with the conversion. An order ID can only be used for one conversion per conversion action. |
|External Attribution Credit|  This parameter represents the fraction of the conversion that is attributed to the Google Ads click.  |
|External Attribution Model|  The specified attribution model name. For more information, see [Google: Google Ads API Click Conversion](https://developers.google.com/google-ads/api/reference/rpc/v3/ClickConversion). |
| gbraid | (Required) Click identifier for clicks associated with app conversions and originating from iOS devices, starting with iOS14. Value can be the Google Click ID, `gbraid`, or `wbraid`.  |
| wbraid |  (Required) Click identifier for clicks associated with web conversions and originating from iOS devices, starting with iOS14. Value can be the Google Click ID, `gbraid`, or `wbraid`.  |

#### Cart Data parameters

|**Parameter**| **Description**|
|---| ---|
|Merchant ID| The Merchant Center ID where the items are uploaded. |
|Feed Country Code|  The country code associated with the feed where the items are uploaded.  |
|Feed Language Code|  The language code associated with the feed where the items are uploaded.  |
|Local Transaction|  The sum of all transaction level discounts, such as free shipping and coupon discounts for the whole cart. The currency code is the same as that in the `ClickConversion` message. |
|Product ID| The shopping ID of the item. This value must be equal to the Merchant Center product identifier. Use an array to add multiple items. Array type attributes must be of equal length.  |
|Quantity| The number of items sold. Use an array to add multiple items. Array type attributes must be of equal length.  |
|Unit Price| The unit price excluding tax, shipping, and any transaction level discounts. The currency code is the same as that in the `ClickConversion` message. Use an array to add multiple items. Array type attributes must be of equal length.  |

#### Optional parameters

|**Parameter**| **Description**|
|---| ---|
| Conversion Action Override | Provide a conversion action ID to override the **Conversion Action** parameter. You can use EventStream variables to populate the **Conversion Action ID** parameter. |
| Custom Variables | The custom variables associated with this conversion. For more information, see [Google: Custom Variable](https://developers.google.com/google-ads/api/reference/rpc/v8/CustomVariable). |
|Ad User Data Consent | Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |

### Action — Conversion Restatement

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Conversion Action| Select existing conversion action. For more information, see [Google: Google Ads Conversion Adjustments](https://support.google.com/google-ads/answer/7686447). |
|Restatement Value| (Required) The value of the conversion after restatement.|
|Restatement Date Time| (Required) The date and time at which the adjustment occurred. The format is **yyyy-mm-dd hh:mm:ss+&#124;-hh:mm**. Date attributes are converted to the format Google expects.|
|Order ID|  Either **Order ID** or **Google Click ID** with **Conversion Date Time** must be provided. If the conversion was reported with an order ID specified, that order ID must be used. |
|Google Click ID|  Either **Order ID** or **Google Click ID** with **Conversion Date Time** must be provided. If the conversion was reported with an order ID specified, that order ID must be used. |
|Conversion Date Time| The date and time of the conversion. The format is **yyyy-mm-dd hh:mm:ss+&#124;-hh:mm**. Date attributes will be converted to the format Google expects.|
|Currency Code| The currency of the restated value. If not provided, then the default currency from the conversion action is used.|

#### Optional parameter

|**Parameter**| **Description**|
|---| ---|
| Conversion Action Override | Provide a conversion action ID to override the **Conversion Action** parameter. This field lets you use EventStream variables to populate the **Conversion Action ID** parameter. |
| Customer ID Override | (Optional) Provide a customer ID to override the **Customer ID** in the connector configuration. If you use this option, you must also use the Conversion Action Override. |
| Manager Customer ID Override | (Optional) Provide a Manager Customer ID if you are using the Customer ID Override and accessing a client customer. |

### Action — Conversion Retraction

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Conversion Action| Select existing conversion action. For more information, see [Google: Google Ads Conversion Adjustments](https://support.google.com/google-ads/answer/7686447).|
|Retraction Date Time| (Required) The date and time at which the retraction occurred. The format is **yyyy-mm-dd hh:mm:ss+&#124;-hh:mm**. Date attributes are converted to the format Google expects.|
|Order ID|  Either **Order ID** or **Google Click ID** with **Conversion Date Time** must be provided. If the conversion was reported with an order ID specified, that order ID must be used. |
|Google Click ID|  Either **Order ID** or **Google Click ID** with **Conversion Date Time** must be provided. If the conversion was reported with an order ID specified, that order ID must be used. |
|Conversion Date Time| This parameter must be in the format **yyyy-mm-dd hh:mm:ss+&#124;-hh:mm**. Date attributes will be converted to the format Google expects. |
| Conversion Action Override | Provide a conversion action ID to override the **Conversion Action** parameter. You can use EventStream variables to populate the **Conversion Action ID** parameter. |
| Customer ID Override | (Optional) Provide a customer ID to override the **Customer ID** in the connector configuration. If you use this option, you must also use the Conversion Action Override. |
| Manager Customer ID Override | (Optional) If you are using the Customer ID Override and accessing a client customer, provide a Manager Customer ID. |

### Action - Upload Call Conversion

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Conversion Action|  (Required) Select existing conversion action. Only Google Ads conversion actions of type `UPLOAD_CALLS` are displayed. For more information, see [Google: Google Ads Conversion Tracking](https://support.google.com/google-ads/answer/1722022). |

#### Conversion Data parameters

|**Parameter**| **Description**|
|---| ---|
|Caller ID| (Required) The caller ID from which this call was placed. Caller ID is expected in E.164 format and preceded by plus (`+`). For example, `+16502531234`. |
|Call Start Datetime| (Required) The date and time at which the call occurred. The timezone must be specified. The format is **yyyy-mm-dd hh:mm:ss±hh:mm**. For example, `2020-01-01 12:32:45-8:00±hh:mm`. |
|Conversion Datetime|  (Required) The date and time at which the conversion occurred. This date and time must be after the call time. The timezone must be specified. The format is **yyyy-mm-dd hh:mm:ss±hh:mm**.  For example, `2020-01-01 12:32:45-8:00±hh:mm`. |
|Conversion Value|  The value of the conversion for the advertiser. |
|Currency Code| The ISO 4217 3-character currency code associated with the conversion value. For example,`USD` or `EUR`. |

#### Optional parameters

|**Parameter**| **Description**|
|---| ---|
| Custom Variables | The custom variables associated with this conversion. For more information, see [Google: Custom Variable](https://developers.google.com/google-ads/api/reference/rpc/v8/CustomVariable). |
| Conversion Action Override | Provide a conversion action ID to override the **Conversion Action** parameter. This field lets you use EventStream variables to populate the **Conversion Action ID** parameter. |
|Ad User Data Consent | Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |
|Customer ID Override | (Required) Select the customer account ID. Available options reflect accessible customer accounts for authenticated user. |
| Manager Customer ID Override | (Optional) If you are using the Customer ID Override and accessing a client customer, provide a Manager Customer ID. |

### Action - Upload Click Conversion

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Conversion Action| Select the existing conversion action. For more information, see [Google: Google Ads Conversion Tracking](https://support.google.com/google-ads/answer/1722022). |

#### Conversion Data parameters

|**Parameter**| **Description**|
|---| ---|
|Google Click ID|  (Required) The Google click ID (`gclid)` associated with this conversion. Google Click ID, `gbraid`, or `wbraid` are required. |
|Conversion Datetime|  (Required) The date and time at which the conversion occurred. This date and time must be after the call time. The timezone must be specified. The format is **yyyy-mm-dd hh:mm:ss±hh:mm**. For example, `2020-01-01 12:32:45-8:00`. |
|Customer Type|   The type of customer associated with the conversion. Accessible only to customers on the allow-list. Acceptable values are `new` or `returning`. |
|Conversion Value|   The value of the conversion for the advertiser. |
|Currency Code|  The ISO 4217 3-character currency code associated with the conversion value. For example, `USD` or `EUR`. |
|Order ID|  (Required) The order ID associated with the conversion. An order ID can only be used for one conversion per conversion action. |
|External Attribution Credit| The fraction of the conversion that is attributed to the Google Ads click.  |
|External Attribution Model|  The specified attribution model name. For more information, see [Google: Google Ads API Click Conversion](https://developers.google.com/google-ads/api/reference/rpc/v3/ClickConversion). |
| gbraid | (Required) Click identifier for clicks associated with app conversions and originating from iOS devices, starting with iOS14. Value can be the Google Click ID, `gbraid`, or `wbraid`.  |
| wbraid |  (Required) Click identifier for clicks associated with web conversions and originating from iOS devices, starting with iOS14. Value can be the Google Click ID, `gbraid`, or `wbraid`.  |


#### Cart Data parameters

|**Parameter**| **Description**|
|---| ---|
|Merchant ID| The Merchant Center ID where the items are uploaded. |
|Feed Country Code|  The country code associated with the feed where the items are uploaded.  |
|Feed Language Code|  The language code associated with the feed where the items are uploaded.  |
|Local Transaction|  The sum of all transaction level discounts, such as free shipping and coupon discounts for the whole cart. The currency code is the same as that in the `ClickConversion` message. |
|Product ID| The shopping ID of the item. This value must be equal to the Merchant Center product identifier. Use an array to add multiple items. Array type attributes must be of equal length.  |
|Quantity| The number of items sold. Use an array to add multiple items. Array type attributes must be of equal length.  |
|Unit Price| The unit price excluding tax, shipping, and any transaction level discounts. The currency code is the same as that in the `ClickConversion` message. Use an array to add multiple items. Array type attributes must be of equal length.  |

#### Optional parameters

|**Parameter**| **Description**|
|---| ---|
| Custom Variables | The custom variables associated with this conversion. For more information, see [Google: Custom Variable](https://developers.google.com/google-ads/api/reference/rpc/v8/CustomVariable). |
|Ad User Data Consent | Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |
| Conversion Action Override | Provide a conversion action ID to override the **Conversion Action** parameter. This field lets you use EventStream variables to populate the **Conversion Action ID** parameter. |
|Customer ID Override | (Required) Select the customer account ID. Available options reflect accessible customer accounts for authenticated user. |
| Manager Customer ID Override | (Optional) If you are using the Customer ID Override and accessing a client customer, provide a Manager Customer ID. |
