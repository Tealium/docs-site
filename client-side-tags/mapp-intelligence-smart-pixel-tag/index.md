---
title: Mapp Intelligence Smart Pixel Tag Setup Guide
description: This article describes how to set up the Mapp Intelligence Smart Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/mapp-intelligence-smart-pixel-tag/
---
Mapp Intelligence offers analysts and marketers in depth analyses and valuable insights of website usage and a deeper understanding of their customers. It provides the necessary information to target audiences with the right message at the right time and in the right channel.

## Tag Tips

* Values added to the mapping are inserted into the `wt` object (for example, use mapping to set `contentId` or `internalSearch`).
* The `formTrackInstall()` function is triggered automatically when you set a value for the form HTML ID.
* Track events by calling the `utag.link()` function.
* The E-Commerce Extension is required to automatically set order values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Library Version**: Select the library version to use.
* **Track ID**: Use Track IDs to assign requests to an account. Find the Track ID under **Mapp Q3 > Configuration > System Configuration > Data Collection** in the Mapp **System Configuration**. To record the same information for multiple accounts, separate Track IDs with commas.
* **Track Domain**: Enter the Mapp Intelligence track domain provided by your account manager.
* **Domain**: Override the default behavior of excluding the Smart Pixel’s domain as a referrer.
* **Cookie Handling**: Indicate whether to set cookies with the browser or server. Server-side cookies are recommended only if you use a custom Track Domain that matches your web domain. This allows first-party tracking and the highest data quality.
* **Secure Cookie**: Enable this option to add the secure flag to all Mapp Intelligence cookies. This allows a secure cookie to be transmitted only over HTTPS.
* **Opt-Out Name**: Provide an alternative name for the opt-out cookie.
* **Request Obfuscation**: Obfuscate all tracking requests to make it harder for ad blockers to identify and block Mapp Intelligence track requests. This option is deactivated by default but can be activated using the `requestObfuscation` key.
* **Force Old EverId**: Force the use of the old Mapp Intelligence `EverID`.
* **Product Merge**: Deactivate the merging of multiple products with the same product ID if needed.
* **Support server-to-server tracking functionality**: Enable server-to-server tracking functionality.
* **Use Hash for Default Page Name**: Include the URL hash in the default page name.
* **Use Params For Default Page Name**: Include specific URL parameters in the default page name.
* **Request Queue**: Enable offline queuing for all tracking requests.
* **Request Limit**: Enable to set a maximum number of requests to reduce the risk of errors caused by large request volumes.
* **User Identification**: Enable anonymous tracking.
* **Enable auto-tracking**: Enable auto-tracking with the `wtSmart.track()` function when the tag is triggered.
* **Enable auto-tracking page data only**: Enable auto-tracking with the `wtSmart.trackPage()` function for page data.
* **Enable auto-tracking event data only**: Enable auto-tracking with the `wtSmart.trackAction()` function for event data.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `trackId` | `String` | The track ID. |
| `trackDomain` | `String` | The track domain. |
| `domain` | `Array of Strings` | The domain. |
| `cookie` | `String` | Cookie settings. |
| `secureCookie` | `Boolean` | Secure cookie. |
| `optOutName` | `String` | Alternative name for the opt-out cookie. |
| `requestObfuscation` | `Boolean` | Request obfuscation. |
| `forceOldEverId` | `Boolean` | Force old `EverID`. |
| `productMerge` | `String` | Product merge. |
| `sendViaServer.activated` | `Boolean` | Server-to-server tracking. |
| `useHashForDefaultPageName` | `Boolean` | Use hash for the default page name. |
| `useParamsForDefaultPageName` | `Array of Strings` | Use params for the default page name. |
| `requestQueue.activated` | `Boolean` | Offline queue for tracking requests. |
| `requestLimit` | `Boolean` | Request limit. |
| `userIdentification.enableAnonymousFunction` | `Boolean` | Anonymous tracking. |
| `autoTracking` | `Boolean` | Automatic tracking. |
| `autoTrackingPage` | `Boolean` | Automatic page tracking. |
| `autoTrackingEvent` | `Boolean` | Automatic event tracking. |
| `keepData` | `Boolean` | After sending, the pixel automatically deletes all data from the cache and cannot access it anymore. To keep the data accessible, set this to `true`. Default: `false`. |

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `execCDB` | `Boolean` | Activates or deactivates the Cross Device Bridge. |
| `useCDBCache` | `Boolean` | Activates or deactivates the image cache for the Cross Device Bridge. |
| `sendViaServer.serverDomain` | `String` | Specifies the domain where the server-to-server library is hosted. |
| `sendViaServer.serverPath` | `String` | Specifies the path where the server-to-server library is saved on your server. |
| `sendViaServer.droppedRequests` | `Number` | The number of dropped requests. |
| `sendViaServer.blacklist` | `String` | Specifies the specific page requests that need to be discarded by the pixel. |
| `requestQueue.ttl` | `Number` | Specifies the maximum time a request can remain in the queue until it is deleted. |
| `requestQueue.resendInterval` | `Number` | The resend interval. |
| `requestQueue.size` | `Number` | Defines the maximum number of requests saved in the queue. |
| `requestQueue.retries` | `Number` | The number of retries. |
| `requestQueue.retriesOption` | `Number` | Retries option. |
| `requestLimit.amount` | `Number` | The maximum number of requests allowed in the specified time period. |
| `requestLimit.duration` | `Number` | The time interval in seconds for sending the maximum number of requests. |
| `userIdentification.anonymousCookieName` | `String` | An alternative name for the anonymous tracking cookie. |
| `userIdentification.anonymousOptIn` | `String` | Enable if you want to use anonymous tracking by default. |
| `userIdentification.suppressParameter` | `Array of Strings` | Suppress parameter. |
| `userIdentification.temporarySessionId` | `String` | Temporary session ID. |
| `userIdentification.saveTemporarySessionId` | `Boolean` | Save temporary session ID. |

### Page

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `name` | `String` | Overwrites the default page naming. |
| `search` | `String` | Search terms used in internal search. |
| `numberSearchResults` | `Number` | Number of internal search results. |
| `errorMessages` | `String` | Track error messages. |
| `paywall` | `Boolean` | Mark an article, if it is behind the paywall. |
| `articleTitle` | `String` | The article title. |
| `contentTags` | `String` | Tags of an article. |
| `title` | `String` | Title of the page. |
| `e.g. "overview"` | `String` | Type of the page. |
| `e.g. "large"` | `String` | Length of the page. |
| `daysSincePublication` | `Number` | Days since publication. |
| `testVariant` | `String` | Name of the test variant. |
| `testExperiment` | `String` | Name of the test. |
| `parameter` | `Object` | You can use parameters to enrich analytics data with your own website-specific information and/or metrics. |
| `called "Content Groups" in Mapp` | `Object` | Page categories. |
| `goal` | `Object` | When using website goals, all central goals are quickly available for analyzing and filtering. |

### Event parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `eventName` | `String` | A unique identification for the event. |
| `eventParameter` | `Array` | Parameters used to enrich analytical data with specific information and/or metrics. Follow syntax guidelines when defining parameters.  |
| `eventGoal` | `Object` | Required for tracking website goals based on events. Website goals measure the success of your website. |

### Campaign

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `campaignId` | `String` | The campaign ID, consisting of a media code name and its value, separated by `=`. |
| `mediaCode` | `Array of Strings` | (Overrides `_cpromo`) If you use media codes as a data source for your campaign tracking, entering their name can raise the accuracy of the measurement. |
| `oncePerSession` | `Boolean` | Track each campaign just once within a session. |
| `campaignParameter` | `Object` | Campaign parameters always refer to an advertising medium. |

### Customer

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `customerId` | `String` | (Overrides `_ccustid`) A unique identifier of the user. |
| `emailRID` | `String` | The email receiver `ID` of the user, which serves as a link between Mapp Intelligence and your email tool. |
| `emailOptin` | `String` | The email opt-in status of the user. |
| `registrationEmail` | `String` | The email address used to identify the user in Mapp Engage. |
| `registrationGroupId` | `String` | Provide the group `ID` in the case of a new registration for the user in Mapp Engage. |
| `registrationMode` | `String` | Provide the registration method used to register for marketing activities. Options include: `c` (CONFIRMED OPT IN), `d` (DOUBLE OPT IN), `o` (OPT IN). |
| `registrationFirstName` | `String` | First name of the user to be used in Mapp Engage. |
| `registrationLastName` | `String` | Last name of the user to be used in Mapp Engage. |
| `undisclosed` | `String` | Gender of the user. Options include: `u` (undisclosed), `f` (female), `m` (male). |
| `registrationTitle` | `String` | The title of the user to be used in Mapp Engage. |
| `default` | `Boolean` | Provide information that the user consented to use their data. Options include: `true` (User consent), `false` (No consent).  |
| `customerCategory` | `Object` | Use categories to enrich customer information with additional data. Categories must be specified within the `MIUserCategories` object. |

### Order

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `orderValue` | `String` | (Overrides `_ctotal`) Total order value including/excluding shipping, taxes, etc. This property must be entered if total order values are to be tracked. |
| `order ID` | `String` | (Overrides `_corder`) A unique order number. |
| `orderCurrency` | `String` | (Overrides `_ccurrency`) The currency of an order can be set with the property `currency`. The value must be passed to the Mapp Intelligence pixel in line with the `ISO` standard. |
| `couponValue` | `Number` | (Overrides `_cpromo`) Contains the value of a coupon. Use this parameter if the customer makes an order with a coupon. |
| `paymentMethod` | `String` | Transmit the payment method for the order. |
| `shippingService` | `String` | Transmit the shipping service for the order. |
| `shippingSpeed` | `String` | Transmit the shipping speed for the order. |
| `shippingCosts` | `Number` | (Overrides `_cship`) Transmit the shipping costs for the order. |
| `grossMargin` | `Number` | Transmit the margin or mark-up of the order. |
| `orderStatus` | `String` | Transmit the status of the order. For example, Shipped, Returned. |
| `orderParameter` | `Object` | Use parameters to enrich analytical data with your own website-specific information and/or metrics. |

### Session

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `visit` | `String` | Session parameters always refer to a complete session. |
| `visit` | `Object` | Session parameters always refer to a complete session. |

### Product

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `productId` | `Array of Strings` | (Overrides `_cprod`) A unique identifier for the product. |
| `cost` | `Array of Numbers` | (Overrides `_cprice`) The cost of the product. Default: `0`. |
| `quantity` | `Array of Numbers` | (Overrides `_cquan`) The quantity of the product available. Default: `0`. |
| `soldOut` | `Array of Booleans` | Indicates whether the product is sold out. Default: `false`. |
| `productParameter` | `Array of Objects` | Use parameters to enrich analytical data with your own specific information and/or metrics. |
| `productCategory` | `Array of Objects` | (Overrides `_ccat`) Use categories to classify products. Categories must be specified within the `MIProductCategories` object. |
