---
title: Mapp Intelligence (Legacy Pixel) Tag Setup Guide
description: This article describes how to set up the Mapp Intelligence (Legacy Pixel) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/mapp-intelligence-tag/
---
Mapp Intelligence offers analysts and marketers in depth analyses and valuable insights of website usage and a deeper understanding of their customers. It provides the necessary information to target audiences with the right message at the right time and in the right channel.

## Tag Tips

* Values added to data mapping will be inserted into the Webtrekk (`wt`) object. For example, use data mappings to set `wt_config.contentId` or `internalSearch` ).
* The Mapp Intelligence tag triggers `formTrackInstall()` automatically by setting a value to **Form HTML ID** (`formTrackInstall`).
* Event tracking can be done with a function call using `utag.link()`.
* The E-Commerce extension is required to automatically set order values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Library Version**: The library version you are using.
* **Track ID**: ID used to assign requests to an account. Locate your track ID by navigating to **Data Collection** in the Mapp **System Configuration**. If the same information needs to be recorded to multiple accounts, enter the corresponding track IDs of the accounts as a comma-separated list.
* **Track Domain**: Your Mapp Intelligence track domain provided by your account manager.
* **Param First**: Semi-colon separated list of parameters that will be sent first.
* **Domain**: Domain of website being tracked. You can enter multiple domains, separated by a semicolon.
* **Link Tracking**: The Mapp Intelligence tag provides two ways to track HTML links:
  * **Link**: All HTML links are automatically tracked when clicked
  * **Standard**: All labeled HTML links of a page are tracked when clicked.
* **Link Track Attribute**: Name of the HTML attribute used for link names.
* **Link Track Params**: Name of query string parameters in the link URL that will be used as link name.
* **Link Track Downloads**: Extensions of download files to track. For example, `.zip`, `.rar`, `.doc`
* **Pixel Sampling**: Define whether only every n-th user should be tracked on your page.
* **Force HTTPS**: Select **on** or **off**.
* **Cookie Handling**: Select the cookies you want to use: first-party cookies or third-party cookies.
* **Cookie Domain**
* **mediaCode**: Set **mediaCode** to identify which parameter you will use for standard campaign tracking.
* **mediaCodeCookie**: If the **mediaCode** query parameter is in the address bar (for example, with AJAX-driven websites), set **mediaCodeCookie** to `sid`.
* **WT Object Name**: Name of the WT object. Leave the default of `wt` if using a single Webtrekk instance.
* **Form Tracking**: Enables global form tracking. To enable form tracking for single pages, use **Form HTML ID** in Data Mappings.
* **Request Queue**: Select **on** or **off**.
* **Server to Server Tracking**: Select **on** or **off**.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable                                                              | Description     |
|:----------------------------------------------------------------------|:----------------|
| WT Object Name (`wt_object_name`)                                     | [String]        |
| Request of Obfusacation (`requestObfuscation`)                        | [Boolean]       |
| Secure Configuration (`secureConfig`)                                 | [String]        |
| Send via SDK ( `sendViaSDK` )                                         | [Boolean]       |
| Parameters to Include First (`wt_config.paramFirst`)                  |                 |
| Ignore Pre-rendering (`wt_config.ignorePrerendering`)                 | [Boolean]       |
| Form Path Analysis (`wt_config.formPathAnalysis`)                     | [Boolean]       |
| tabBrowsing (`wt_config.tabBrowsing`)                                 | [Boolean]       |
| globalVisitorIds (`wt_config.globalVisitorIds`)                       | [Boolean]       |
| execCDB (`wt_config.execCDB`)                                         | [Boolean]       |
| useCDBCache (`wt_config.useCDBCache`)                                 | [Boolean]       |
| useCDBScript (`wt_config.useCDBScript`)                               | [Boolean]       |
| requestLimitAmount (`wt_config.requestLimitAmount`)                   |                 |
| requestLimitTime (`wt_config.requestLimitTime`)                       |                 |
| Track ID (`wt_config.trackId`)                                        |                 |
| Track Domain (`wt_config.trackDomain`)                                |                 |
| Domain (`wt_config.domain`)                                           |                 |
| Link Track ( `wt_config.linkTrack` )                                  |                 |
| Link Track Attribute (`wt_config.linkTrackAttribute`)                 |                 |
| Link Track Params (`wt_config.linkTrackParams`)                       |                 |
| Link Track Downloads (`wt_config.linkTrackDownloads`)                 | [RegExp Object] |
| Link Track Pattern (`wt_config.linkTrackPattern`)                     |                 |
| Llink Track Replace (`wt_config.linkTrackReplace`)                    |                 |
| Link Track Ignore Pattern (`wt_config.linkTrackIgnorePattern`)        |                 |
| No Delay Link Track Attribute (`wt_config.noDelayLinkTrackAttribute`) |                 |
| Pixel Sampling (`wt_config.pixelSampling`)                            |                 |
| Force HTTPS (`wt_config.forceHTTPS`)                                  |                 |
| Cookie Handling (`wt_config.cookie`)                                  |                 |
| Cookie Domain (`wt_config.cookieDomain`)                              |                 |
| contentId (`wt_config.contentId`)                                     |                 |
| Form (`wt_config.form`)                                               |                 |
| executePluginFunction (`wt_config.executePluginFunction`)             |                 |
| Media Code Cookie (`wt_config.mediaCodeCookie`)                       |                 |
| Media Code (`wt_config.mediaCode`)                                    |                 |
| Custom wt config item (`wt_config.###`)                               |                 |

### General

| Variable                           | Description  |
|:-----------------------------------|:-------------|
| Custom Visitor ID                  |              |
| Login Status (`loginStatus`)       |              |
| URM Categories (`urmCategory.###`) |              |
| Email RID (`emailRID`)             |              |
| Email Opt-In (`emailOptin`)        |              |
| Gender (`gender`)                  |              |
| Birthday (`birthday`)              | [`YYYYMMDD`] |
| Birthday Year (`birthdayJ`)        | [`YYYY`]     |
| Birthday Month (`birthdayM`)       | [`MM`]       |
| Birthday Day (`birthdayD`)         |              |
| CRM Category 1                     |              |
| CRM Category 2                     |              |
| CRM Category 3                     |              |
| CRM Category 4                     |              |
| CRM Category 5                     |              |
| CRM Category 6                     |              |
| CRM Category 7                     |              |
| CRM Category 8                     |              |
| CRM Category 9                     |              |
| CRM Category 10                    |              |
| Custom Session Parameter 1         |              |
| Custom Session Parameter 2         |              |
| Custom Session Parameter 3         |              |
| Custom Session Parameter 4         |              |
| Custom Session Parameter 5         |              |
| Custom Session Parameter 6         |              |
| Custom Session Parameter 7         |              |
| Custom Session Parameter 8         |              |
| Custom Session Parameter 9         |              |
| Custom Session Parameter 10        |              |

### Page Data

| Variable                                        | Description |
|:------------------------------------------------|:------------|
| Page Title (`pageTitle`)                        | [String]    |
| Content ID (`contentId`)                        |             |
| URL Pattern (`pageURLPattern`)                  |             |
| URL Replace (`pageURLReplace`)                  |             |
| Tab Browsing (`tabBrowsing`)                    | [Boolean]   |
| Internal Search (`internalSearch`)              | [String]    |
| Number of Search Result (`numberSearchResults`) | [Number]    |
| Error Messages (`errorMessages`)                | [String]    |
| Page Type (`pageType`)                          | [String]    |
| Page Length (`pageLength`)                      | [String]    |
| Article Title (`articleTitle`)                  | [String]    |
| Days Since Publication (`daysSincePublication`) | [Number]    |
| Paywell Calls (`paywell`)                       | [String]    |
| Content Tags (`contentTags`)                    | [String]    |
| Content Group 1                                 |             |
| Content Group 2                                 |             |
| Content Group 3                                 |             |
| Content Group 4                                 |             |
| Content Group 5                                 |             |
| Content Group 6                                 |             |
| Content Group 7                                 |             |
| Content Group 8                                 |             |
| Content Group 9                                 |             |
| Content Group 10                                |             |
| Content Group 11                                |             |
| Content Group 12                                |             |
| Content Group 13                                |             |
| Content Group 14                                |             |
| Content Group 15                                |             |
| Content Group 16                                |             |
| Content Group 17                                |             |
| Content Group 18                                |             |
| Content Group 19                                |             |
| Content Group 20                                |             |
| Content Group 21                                |             |
| Content Group 22                                |             |
| Content Group 23                                |             |
| Content Group 24                                |             |
| Content Group 25                                |             |
| Custom Parameter 1                              |             |
| Custom Parameter 2                              |             |
| Custom Parameter 3                              |             |
| Custom Parameter 4                              |             |
| Custom Parameter 5                              |             |
| Custom Parameter 6                              |             |
| Custom Parameter 7                              |             |
| Custom Parameter 8                              |             |
| Custom Parameter 9                              |             |
| Custom Parameter 10                             |             |
| Custom Parameter 11                             |             |
| Custom Parameter 12                             |             |
| Custom Parameter 13                             |             |
| Custom Parameter 14                             |             |
| Custom Parameter 15                             |             |
| Custom Parameter 16                             |             |
| Custom Parameter 17                             |             |
| Custom Parameter 18                             |             |
| Custom Parameter 19                             |             |
| Custom Parameter 20                             |             |
| Custom Parameter 21                             |             |
| Custom Parameter 22                             |             |
| Custom Parameter 23                             |             |
| Custom Parameter 24                             |             |
| Custom Parameter 25                             |             |
| Custom Parameter 26                             |             |
| Custom Parameter 27                             |             |
| Custom Parameter 28                             |             |
| Custom Parameter 29                             |             |
| Custom Parameter 30                             |             |
| Custom Parameter 31                             |             |
| Custom Parameter 32                             |             |
| Custom Parameter 33                             |             |
| Custom Parameter 34                             |             |
| Custom Parameter 35                             |             |
| Custom Parameter 36                             |             |
| Custom Parameter 37                             |             |
| Custom Parameter 38                             |             |
| Custom Parameter 39                             |             |
| Custom Parameter 40                             |             |
| Custom Parameter 41                             |             |
| Custom Parameter 42                             |             |
| Custom Parameter 43                             |             |
| Custom Parameter 44                             |             |
| Custom Parameter 45                             |             |
| Custom Parameter 46                             |             |
| Custom Parameter 47                             |             |
| Custom Parameter 48                             |             |
| Custom Parameter 49                             |             |
| Custom Parameter 50                             |             |

### Search & Form Tracking

| Variable                                           | Description      |
|:---------------------------------------------------|:-----------------|
| Form (`form`)                                      | [`0`/`1`]        |
| Form Attribute (`formAttribute`)                   | [String]         |
| Form Value Attribute (`formValueAttribute`)        | [String]         |
| Form Field Attribute (`formFieldAttribute`)        | [String]         |
| Full Content Form Tracking (`formFullContent`)     | [Array]          |
| Form Path Analysis (`formPathAnalysis`)            | [`true`/`false`] |
| Anonymous Form Tracking (`formAnonymous`)          | [`0`/`1`]        |
| Form Field Default Value (`formFieldDefaultValue`) | [String]         |
| Form HTML ID (`formTrackInstall`)                  |                  |

### Click Tracking

| Variable                                                    | Description     |
|:------------------------------------------------------------|:----------------|
| Link Track (`linkTrack`)                                    | [link/standard] |
| Link Track Attribute (`linkTrackAttribute`)                 | [String]        |
| Link Track Pattern (`linkTrackPattern`)                     | [RegExp Object] |
| Link Track Ignore Pattern (`linkTrackIgnorePattern`)        | [String]        |
| Link Track Replace (`linkTrackReplace`)                     | [String]        |
| Link Track Downloads (`linkTrackDownloads`)                 | [Array]         |
| Delay Link Track (`delayLinkTrack`)                         | [true/false]    |
| Delay Link Track Time (`delayLinkTrackTime`)                | [Number]        |
| No Delay Link Track Attribute (`noDelayLinkTrackAttribute`) | [String]        |
| Link Track Params                                           |                 |
| Link ID for custom utag.link tracking (`linkId`)            |                 |

### Campaign Tracking

| Variable                              | Description |
|:--------------------------------------|:------------|
| Media Code (`mediaCode`)              |             |
| Media Code Cookie (`mediaCodeCookie`) |             |
| Campaign ID (`campaignId`)            |             |
| Campaign Action (`campaignAction`)    |             |
| Custom Campaign Parameter 1           |             |
| Custom Campaign Parameter 2           |             |
| Custom Campaign Parameter 3           |             |
| Custom Campaign Parameter 4           |             |
| Custom Campaign Parameter 5           |             |
| Custom Campaign Parameter 6           |             |
| Custom Campaign Parameter 7           |             |
| Custom Campaign Parameter 8           |             |
| Custom Campaign Parameter 9           |             |
| Custom Campaign Parameter 10          |             |

### Server Tracking

| Variable                                                          | Description      |
|:------------------------------------------------------------------|:-----------------|
| Send Via Server Activated (`sendViaServerActivated`)              | [`true`/`false`] |
| Send Via Server Domain (`sendViaServerDomain`)                    | [String]         |
| Send Via Server Path (`sendViaServerPath`)                        | [String]         |
| Send Via Server Dropped Requests (`sendViaServerDroppedRequests`) |                  |
| Send Via Server Blacklist (`sendViaServerBlacklist`)              |                  |

### Cookies

| Variable                                     | Description |
|:---------------------------------------------|:------------|
| Update Cookie (`updateCookie`)               | [Boolean]   |
| Cookie Secure (`cookieSecure`)               | [Boolean]   |
| Cookie Ever ID Timeout (`cookieEidTimeout`)  | [Number]    |
| Validate Ever ID (`validateEverId`)          | [Boolean]   |
| Cookie OptOut Name (`optoutName`)            | [String]    |
| Cookie OptOut Time Frame (`optoutTimeFrame`) |             |

### Request Queue

| Variable                                                  | Description |
|:----------------------------------------------------------|:------------|
| Request Queue Activated (`requestQueueActivated`)         | [Boolean]   |
| requestQueueResendInterval (`requestQueueResendInterval`) | [Number]    |
| Reqquest Queue TTL (`requestQueueTTL`)                    | [Number]    |
| Request Queue Size (`requestQueueSize`)                   | [Boolean]   |

### Anonymous Tracking

| Variable                                                              | Description |
|:----------------------------------------------------------------------|:------------|
| Enable Anonymous Function (`enableAnonymousFunction`)                 | [Boolean]   |
| Anonymous Opt In (`anonymousOptIn`)                                   | [Boolean]   |
| Anonymous Cookie Name (`anonymousCookieName`)                         | [String]    |
| Suppress Identification Parameter (`suppressIdentificationParameter`) | [Array]     |

### E-Commerce

| Variable                                | Description                                                   |
|:----------------------------------------|:--------------------------------------------------------------|
| Order ID (`order_id`)                   | (Overrides `_corder` )                                        |
| Order Total (`order_total`)             | (Overrides `_ctotal` )                                        |
| Currency (`order_currency`)             | (Overrides `_ccurrency` )                                     |
| Coupon Value (`order_couponValue`)      |                                                               |
| List of Names (`product_name`)          | [Array]<br> (Overrides `_cprodname` )                         |
| List of Quantities (`product_quantity`) | [Array]<br> (Overrides `_cquan` )                             |
| List of Prices (`product_unit_price`)   | [Array] <br> (Overrides `_cprice` )                           |
| productCategory (`product_category`)    | [Array] <br> List of Categories <br> (Overrides `_ccat` )     |
| productCategory (`product_brand`)       | [Array]<br> List of Brands <br> (Overrides `_cbrand` )        |
| productCategory (`product_subcategory`) | [Array]<br> List of Sub Categories <br> (Overrides `_ccat2` ) |
| Product Status (`productStatus`)        |                                                               |
| Payment Method (`paymentMethod`)        | [String]                                                      |
| Shipping Service (`shippingService`)    | [String]                                                      |
| Shipping Speed (`shippingSpeed`)        | [String]                                                      |
| Shipping Costs (`shippingCosts`)        | [Number]                                                      |
| Gross Margin (`grossMargin`)            | [Number]                                                      |
| Order Status (`orderStatus`)            | [String]                                                      |
| Product Variant (`productVariant`)      | [String]                                                      |
| Product Sold Out (`productSoldOut`)     | [`0`/`1`]                                                     |
| Product Category 1                      |                                                               |
| Product Category 2                      |                                                               |
| Product Category 3                      |                                                               |
| Product Category 4                      |                                                               |
| Product Category 5                      |                                                               |
| Product Category 6                      |                                                               |
| Product Category 7                      |                                                               |
| Product Category 8                      |                                                               |
| Product Category 9                      |                                                               |
| Product Category 10                     |                                                               |
| Product Category 11                     |                                                               |
| Product Category 12                     |                                                               |
| Product Category 13                     |                                                               |
| Product Category 14                     |                                                               |
| Product Category 15                     |                                                               |
| Product Category 16                     |                                                               |
| Product Category 17                     |                                                               |
| Product Category 18                     |                                                               |
| Product Category 19                     |                                                               |
| Product Category 20                     |                                                               |
| Product Category 21                     |                                                               |
| Product Category 22                     |                                                               |
| Product Category 23                     |                                                               |
| Product Category 24                     |                                                               |
| Product Category 25                     |                                                               |
| Custom E-Commerce Parameter 1           |                                                               |
| Custom E-Commerce Parameter 2           |                                                               |
| Custom E-Commerce Parameter 3           |                                                               |
| Custom E-Commerce Parameter 4           |                                                               |
| Custom E-Commerce Parameter 5           |                                                               |
| Custom E-Commerce Parameter 6           |                                                               |
| Custom E-Commerce Parameter 7           |                                                               |
| Custom E-Commerce Parameter 8           |                                                               |
| Custom E-Commerce Parameter 9           |                                                               |
| Custom E-Commerce Parameter 10          |                                                               |
| Custom E-Commerce Parameter 11          |                                                               |
| Custom E-Commerce Parameter 12          |                                                               |
| Custom E-Commerce Parameter 13          |                                                               |
| Custom E-Commerce Parameter 14          |                                                               |
| Custom E-Commerce Parameter 15          |                                                               |
| Custom E-Commerce Parameter 16          |                                                               |
| Custom E-Commerce Parameter 17          |                                                               |
| Custom E-Commerce Parameter 18          |                                                               |
| Custom E-Commerce Parameter 19          |                                                               |
| Custom E-Commerce Parameter 20          |                                                               |
| Custom E-Commerce Parameter 21          |                                                               |
| Custom E-Commerce Parameter 22          |                                                               |
| Custom E-Commerce Parameter 23          |                                                               |
| Custom E-Commerce Parameter 24          |                                                               |
| Custom E-Commerce Parameter 25          |                                                               |
| Custom E-Commerce Parameter 26          |                                                               |
| Custom E-Commerce Parameter 27          |                                                               |
| Custom E-Commerce Parameter 28          |                                                               |
| Custom E-Commerce Parameter 29          |                                                               |
| Custom E-Commerce Parameter 30          |                                                               |
| Custom E-Commerce Parameter 31          |                                                               |
| Custom E-Commerce Parameter 32          |                                                               |
| Custom E-Commerce Parameter 33          |                                                               |
| Custom E-Commerce Parameter 34          |                                                               |
| Custom E-Commerce Parameter 35          |                                                               |
| Custom E-Commerce Parameter 36          |                                                               |
| Custom E-Commerce Parameter 37          |                                                               |
| Custom E-Commerce Parameter 38          |                                                               |
| Custom E-Commerce Parameter 39          |                                                               |
| Custom E-Commerce Parameter 40          |                                                               |
| Custom E-Commerce Parameter 41          |                                                               |
| Custom E-Commerce Parameter 42          |                                                               |
| Custom E-Commerce Parameter 43          |                                                               |
| Custom E-Commerce Parameter 44          |                                                               |
| Custom E-Commerce Parameter 45          |                                                               |
| Custom E-Commerce Parameter 46          |                                                               |
| Custom E-Commerce Parameter 47          |                                                               |
| Custom E-Commerce Parameter 48          |                                                               |
| Custom E-Commerce Parameter 49          |                                                               |
| Custom E-Commerce Parameter 50          |                                                               |
