---
title: Google Analytics Connector Setup Guide
description: This article describes how to set up the Google Analytics Connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/google-analytics-connector/
---
Google Analytics lets you do more than measure sales and conversions. It also gives insights into how visitors find and use your site, and how to keep them coming back. Learn more about your customers by bringing all of your data together so everyone in your organization can explore, gain intelligence, and inform strategies to increase business performance. 

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Analytics Event Data| ✓| ✓|
|Send Analytics Event Data (Mobile Optimized)| ✓| ✓|
|Send Analytics Transaction Data| ✓| ✓|
|Send Analytics Transaction Data (Mobile Optimized)| ✓| ✓|
|Send Analytics Social Data| ✓| ✓|
|Send Analytics Social Data (Mobile Optimized)| ✓| ✓|
|Send Analytics Page View Data| ✓| ✓|
|Send Analytics Screen View Data (Mobile Optimized)| ✓| ✓|
|Send Analytics Timing Data| ✓| ✓|
|Send Analytics Timing Data (Mobile Optimized)| ✓| ✓|

## Client ID

The Google Analytics Connector requires either a client ID or user ID for all actions. You can retrieve the client ID from the `_ga` cookie, but it must be parsed before use.

For example, if your `_ga` cookie is:

`GA1.2.447986009.1565955334`

Then the client ID value is the value after `GA1.2.`:

`447986009.1565955334`

To assist in parsing client IDs, use the [Google Analytics Cookie Matching Service tag]() in your workflow and then use the `cp.utag_main__ga` cookie instead of using `cp._ga` directly.

* If you provide a correctly formatted client ID value, the connector uses this value.
* If the event includes the full `_ga` cookie value in the `client_id` mapping, the connector automatically parses and extracts only the client ID portion.
* If `cp.utag_main__ga` is available in the event data, and it contains the client ID in the correct format, the connector automatically maps this value to `client_id`.

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

After adding the connector, configure the following settings:

* **Google Tracking Id**. 
(Required) The format is `UA-XXXX-Y`

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. It&#39;s where you&#39;ll set up Actions and trigger them.

This section describes how to set up Parameters and Options for each Action.

### Action - Send Analytics Event Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;(Required) Client ID or User ID must be set&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set (if applicable): Hit Type, Client ID&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` for Premium accounts) |
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` for Premium accounts) |
|Event Tracking Data|  (Required) Map values to event parameters|
|Enhanced E-Commerce: Product Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included products&lt;/li&gt;&lt;li&gt;Required for all Enhanced E-Commerce sections&lt;/li&gt;&lt;li&gt;Must be set to value of `detail`, `click`, `add`, `remove`, `checkout`, `checkout_option`, `purchase` or `refund`&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Action Data|  &lt;ul&gt;&lt;li&gt;Map values to action transaction parameters (see: [Enhanced E-Commerce Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#enhanced-ecomm))&lt;/li&gt;&lt;li&gt;Transaction ID parameter is required if action type is `purchase` or `refund`&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Data|  &lt;ul&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;li&gt;`productIndex` corresponds to &#34;Product Impression SKU or Name&#34; array index&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to product dimension indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to product metric indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Data|  &lt;ul&gt;&lt;li&gt;Product Impressions represent information about a product that has been viewed&lt;/li&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;`listIndex` corresponds to &#34;Product Impression List Name&#34; array index and defaults to `1` if empty&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to dimension indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to metric indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotion Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included promotions&lt;/li&gt;&lt;li&gt;Must be set to value of `view` or `promo_click`&lt;/li&gt;&lt;li&gt;If not specified, default promotion action of view is assumed&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotions Data|  &lt;ul&gt;&lt;li&gt;Map values to promotion parameters (see: [Promotion Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#promo_id))&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Analytics Event Data (Mobile Optimized)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Mobile Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set from Tealium Mobile UDO: Hit Type, Client ID, Application ID, Application Name, Application Version, Device Resolution, Device Language, Data Source Origin, Viewport Size, Screen Color, User Agent&lt;/li&gt;&lt;li&gt;If a non Mobile Event or an Audience is the Source for this action, the above parameters will not be set and Client ID (cid) or User ID (uid) is required&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` for Premium accounts) |
|Custom Metrics| Map values to metric indices between `1` and `20` (`200` for Premium accounts)|
|Event Tracking Data|  (Required) Map values to event parameters|
|Enhanced E-Commerce: Product Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included products&lt;/li&gt;&lt;li&gt;Required for all Enhanced E-Commerce sections&lt;/li&gt;&lt;li&gt;Must be set to value of `detail`, `click`, `add`, `remove`, `checkout`, `checkout_option`, `purchase` or `refund`&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Action Data|  &lt;ul&gt;&lt;li&gt;Map values to action transaction parameters (see: [Enhanced E-Commerce Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#enhanced-ecomm))&lt;/li&gt;&lt;li&gt;Transaction ID parameter is required if action type is `purchase` or `refund`&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Data|  &lt;ul&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;li&gt;`productIndex` corresponds to &#34;Product Impression SKU or Name&#34; array index&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to product dimension indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to product metric indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Data|  &lt;ul&gt;&lt;li&gt;Product Impressions represent information about a product that has been viewed&lt;/li&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;`listIndex` corresponds to &#34;Product Impression List Name&#34; array index and defaults to `1` if empty&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to dimension indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to metric indices between `1` and `20` (`200` for Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotion Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included promotions&lt;/li&gt;&lt;li&gt;Must be set to value of `view` or `promo_click`&lt;/li&gt;&lt;li&gt;If not specified, default promotion action of view is assumed&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotions Data|  &lt;ul&gt;&lt;li&gt;Map values to promotion parameters (see: [Promotion Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#promo_id))&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Analytics Transaction Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;(Required) Client ID or User ID must be set&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set (if applicable): Hit Type, Client ID&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` for Premium accounts)|
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` for Premium accounts) |
|E-Commerce: Transaction Details|  (Required) Map values to transaction parameters (see: [E-Commerce Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#ecomm))|
|E-Commerce: Item Details|  Item specific information for the transaction.|

### Action - Send Analytics Transaction Data (Mobile Optimized)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Mobile Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set from Tealium Mobile UDO: Hit Type, Client ID, Application ID, Application Name, Application Version, Device Resolution, Device Language, Data Source Origin, Viewport Size, Screen Color, User Agent&lt;/li&gt;&lt;li&gt;If a non Mobile Event or an Audience is the Source for this action, the above parameters will not be set and Client ID (cid) or User ID (uid) is required&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` for Premium accounts) |
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` for Premium accounts) |
|E-Commerce: Transaction Details|  (Required) Map values to transaction parameters (see: [E-Commerce Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#ecomm))|
|E-Commerce: Item Details|  Item specific information for the transaction.|

### Action - Send Analytics Social Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;(Required) Client ID or User ID must be set&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set (if applicable): Hit Type, Client ID&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` Premium accounts)|
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` Premium accounts) |
|Social Interactions|  (Required) Map values to social parameters|

### Action - Send Analytics Social Data (Mobile Optimized)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Mobile Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set from Tealium Mobile UDO: Hit Type, Client ID, Application ID, Application Name, Application Version, Device Resolution, Device Language, Data Source Origin, Viewport Size, Screen Color, User Agent&lt;/li&gt;&lt;li&gt;If a non Mobile Event or an Audience is the Source for this action, the above parameters will not be set and Client ID (cid) or User ID (uid) is required&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions| Map values to dimension indices between `1` and `20` (`200` Premium accounts)|
|Custom Metrics| Map values to metric indices between `1` and `20` (`200` Premium accounts) |
|Social Interactions|  (Required) Map values to social parameters |

### Action - Send Analytics Page View Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;(Required) Client ID or User ID must be set&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set (if applicable): Hit Type, Client ID&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` Premium accounts)|
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` Premium accounts)|
|Content Information|  &lt;ul&gt;&lt;li&gt;(Required) Map values to page view document parameters&lt;/li&gt;&lt;li&gt;Document Location URL or Document Host Name and Document Path must be specified&lt;/li&gt;&lt;li&gt;Following parameters are automatically set: Document Location URL, Document Title, Document Referrer&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Product Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included products&lt;/li&gt;&lt;li&gt;Required for all Enhanced E-Commerce sections&lt;/li&gt;&lt;li&gt;Must be set to value of detail, click, add, remove, checkout, checkout\_option, purchase or refund&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Action Data|  &lt;ul&gt;&lt;li&gt;Map values to action transaction parameters (see: [Enhanced E-Commerce Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#enhanced-ecomm))&lt;/li&gt;&lt;li&gt;Transaction ID parameter is required if action type is purchase or refund&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Data|  &lt;ul&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;li&gt;`productIndex` corresponds to &#34;Product Impression SKU or Name&#34; array index&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to product dimension indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to product metric indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Data|  &lt;ul&gt;&lt;li&gt;Product Impressions represent information about a product that has been viewed&lt;/li&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;&#34;listIndex&#34; corresponds to &#34;Product Impression List Name&#34; array index and defaults to &#34;1&#34; if empty&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to dimension indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to metric indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotion Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included promotions&lt;/li&gt;&lt;li&gt;Must be set to value of view or promo\_click&lt;/li&gt;&lt;li&gt;If not specified, default promotion action of view is assumed&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotions Data|  &lt;ul&gt;&lt;li&gt;Map values to promotion parameters (see: [Promotion Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#promo_id))&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Analytics Screen View Data (Mobile Optimized)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Mobile Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set from Tealium Mobile UDO: Hit Type, Client ID, Application ID, Application Name, Application Version, Device Resolution, Device Language, Data Source Origin, Viewport Size, Screen Color, User Agent&lt;/li&gt;&lt;li&gt;If a non Mobile Event or an Audience is the Source for this action, the above parameters will not be set and Client ID (cid) or User ID (uid) is required&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` Premium accounts) |
|Custom Metrics|  =Map values to metric indices between `1` and `20` (`200` Premium accounts) |
|Content Information|  &lt;ul&gt;&lt;li&gt;(Required) Map values to screen view parameters&lt;/li&gt;&lt;li&gt;Screen Name must be specified&lt;/li&gt;&lt;li&gt;Following parameters are automatically set: Screen Name&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Product Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included products&lt;/li&gt;&lt;li&gt;Required for all Enhanced E-Commerce sections&lt;/li&gt;&lt;li&gt;Must be set to value of `detail`, `click`, `add`, `remove`, `checkout`, `checkout_option`, `purchase`, or `refund`&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Action Data|  &lt;ul&gt;&lt;li&gt;Map values to action transaction parameters (see: [Enhanced E-Commerce Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#enhanced-ecomm))&lt;/li&gt;&lt;li&gt;Transaction ID parameter is required if action type is `purchase` or `refund`&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Data|  &lt;ul&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;li&gt;&#34;productIndex&#34; corresponds to &#34;Product Impression SKU or Name&#34; array index&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to product dimension indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Products Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to product metric indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Data|  &lt;ul&gt;&lt;li&gt;Product Impressions represent information about a product that has been viewed&lt;/li&gt;&lt;li&gt;(Required) Either Product SKU or Name must be set if this section is configured&lt;/li&gt;&lt;li&gt;&#34;listIndex&#34; corresponds to &#34;Product Impression List Name&#34; array index and defaults to &#34;1&#34; if empty&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Dimensions|  &lt;ul&gt;&lt;li&gt;Map values to dimension indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Impressions Custom Metrics|  &lt;ul&gt;&lt;li&gt;Map values to metric indices between `1` and `20` (`200` Premium accounts)&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotion Action|  &lt;ul&gt;&lt;li&gt;Specify action type of included promotions&lt;/li&gt;&lt;li&gt;Must be set to value of `view` or `promo_click`&lt;/li&gt;&lt;li&gt;If not specified, default promotion action of view is assumed&lt;/li&gt;&lt;/ul&gt; |
|Enhanced E-Commerce: Promotions Data|  &lt;ul&gt;&lt;li&gt;Map values to promotion parameters (see: [Promotion Parameters](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#promo_id))&lt;/li&gt;&lt;li&gt;Only Array type attributes are supported and must contain same number of elements&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Analytics Timing Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;(Required) Client ID or User ID must be set&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set (if applicable): Hit Type, Client ID&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` Premium accounts) |
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` Premium accounts) |
|Timing|  Map values to timing parameters|

### Action - Send Analytics Timing Data (Mobile Optimized)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Google Tracking Id|  &lt;ul&gt;&lt;li&gt;Required if not configured in the Configuration Tab&lt;/li&gt;&lt;li&gt;This will overwrite the value defined in the Configuration Tab if the value resolves to not empty&lt;/li&gt;&lt;li&gt;The format is `UA-XXXX-Y`&lt;/li&gt;&lt;/ul&gt; |
|Mobile Measurement Parameters|  &lt;ul&gt;&lt;li&gt;Map values to measurement parameters (see: [Measurement Parameter Reference](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters))&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included&lt;/li&gt;&lt;li&gt;Following parameters are automatically set from Tealium Mobile UDO: Hit Type, Client ID, Application ID, Application Name, Application Version, Device Resolution, Device Language, Data Source Origin, Viewport Size, Screen Color, User Agent&lt;/li&gt;&lt;li&gt;If a non Mobile Event or an Audience is the Source for this action, the above parameters will not be set and Client ID (cid) or User ID (uid) is required&lt;/li&gt;&lt;/ul&gt; |
|Custom Dimensions|  Map values to dimension indices between `1` and `20` (`200` Premium accounts) |
|Custom Metrics|  Map values to metric indices between `1` and `20` (`200` for Premium accounts)|
|Timing|  Map values to timing parameters |
