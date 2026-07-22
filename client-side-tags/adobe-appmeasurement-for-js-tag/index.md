---
title: Adobe Analytics AppMeasurement for JS Tag Setup Guide
description: This article describes how to set up the Adobe Analytics AppMeasurement for JS tag in your iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adobe-appmeasurement-for-js-tag/
---
## Tag Tips

* To use the Adobe Experience Cloud ID Service, add the Adobe Experience Cloud ID Service tag before adding this tag.
* Not all legacy H26 features are supported with the AppMeasurement tag.
* Ensure that you enter the server value correctly. For example, third party servers may have `112.2o7.net` or `122.2o7.net`.
* To use AppMeasurement for mobile, the Tealium Mobile SDK must be implemented in your application.
* For a list of supported plug-ins, see: [Adobe: AppMeasurement Plug-ins Overview](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/plugins/impl-plugins).
* For additional information, see: [Adobe: Implement Adobe Analytics with AppMeasurement for JavaScript](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview)

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the following settings:

* **Code Version**
  * The version of the `AppMeasurement.js` library.
* **Device Type**
  * Select one of the following based on the platform of your implementation:
    * **Standard** for desktop website installations.
    * **Mobile App** for native mobile installations with [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/) or [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/).
* **Report Suite**
  * (Required) Set a default value even when using mapping to dynamically set report suite.
  * The default report suite to use. which may change based on the value set in the Dynamic Acct List.
  * Reference AppMeasurement.js: `s.account`
* **Server**
  * (Required) Data collection server.
  * Reference AppMeasurement.js: `s.trackingServer`
  * For example, `metrics.tealium.com` or `tealiumclient.122.2o7.net`
* **Server Secure**
  * (Required) The `https` data collection server.
  * Reference AppMeasurement.js: `s.trackingServerSecure`
  * For example, `smetrics.tealium.com` or `tealiumclient.122.2o7.net`
* **Auto Event Serialization Detection**
  * Automatically detect event serialization within trigger strings.
  * Must be set to **No** if your event trigger value contains the colon character (`:`).
* **Auto Link Tracking**
  * Default value is **Yes** and is the recommended selection.
  * If set to **No**, must replicate the automatic link tracking using other methods, such as the [Link Tracking Extension](https://docs.tealium.com/link-tracking-extension/).
* **Internal Link Filters**
  * A comma-separated list of your domains ,classified as internal, that is used to ensure that link clicks are not reported as exit clicks to Adobe report.
  * Reference AppMeasurement.js: `s.linkInternalFilters`
  * For example, `tealium.com,tealiumiq.com`
* **Run clearVars**
  * Default value is **No**.
  * Clears the props, eVars, and events set in the global S-Object after each tracking request. 
  * In the **Data Mapping** screen, use the `clearVars_in_RPTCallback` parameter to assign the `clearVars` action to occur inside the `registerPostTrack` callback.
* **S-Object Name**
  * (Required) Default name is `s`.
  * Set a different name if you are running multiple instances of Adobe Analytics or AppMeasurement on the page.
* **Namespace**
  * (Optional) The visitor namespace.
  * Only applies to third party cookies when Server and Server Secure end in `2o7.net`.
  * Reference AppMeasurement.js: `s.visitorNamespace`
* **Experience Cloud ID**
  * (Optional) Your Adobe Experience Cloud ID.
  * If using the Visitor API supported in versions 1.3.x and higher, enter your Enterprise Cloud ID here.
  * For more information, see [Adobe: Enterprise Cloud ID Service](https://experienceleague.adobe.com/en/docs/id-service/using/home).
* **Run Advertising Cloud Viewthrough**
  * Only available for version 2.17 and up.
  * Load the Advertising Cloud Viewthrough file and send the viewthrough data.
* **Viewthrough Interval**
  * Set the interval, in milliseconds, between each attempt to load the viewthrough script.
* **Viewthrough Max Tries**
  * Set the maximum number of attempts to load viewthrough before running only analytics.
* **Send Timestamp**
  * Allow a timestamp to be sent with each tracking call. Applies to mobile device tracking only.
* **Decode Link Parameters**
  * Set to `false` to encode link tracking variables once.
  * Set to `true` to encode link tracking variables twice.
  * Default value is `false`.
  * For more information, see [Adobe: `decodeLinkParameters`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/decodelinkparameters).

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended load rule: **All Pages**.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/about-the-data-layer/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standards

| Variable | Description|
|:---------|:------------|
| `adobe_org_id` | <ul><li>Experience Cloud ID</li></ul>|
| `pageName` | <ul><li>Page name</li><li>This is not the page's URL or path name.</li><li>Should instead be something business users recognize, such as `Home Page` or `Checkout`.</li></ul>|
| `channel` | <ul><li>Sections of your site</li></ul>|
| `server` | <ul><li>Domain of a web page or the server that hosts the page to this destination.</li></ul>|
| `visitorID` | <ul><li>Unique visitor ID.</li><li>Up to 100 alphanumeric characters long.</li><li>Cannot contain a hyphen.</li></ul>|
| `s_account` | <ul><li>Report Suite Override.</li><li>Mapping to this destination overrides the report suite set in the Tag configuration.</li></ul>|
| `linkTrackVars` | <ul><li>Link Variable Override</li></ul>|
| `linkTrackEvents` | <ul><li>Link Event Override</li></ul>|
| Combine Link Variables | <ul><li>Values are `true` or `false`.</li></ul>|
| `charSet` | <ul><li>Character set</li></ul> |
| `collectHighEntropyUserAgentHits`  | <ul><li>Boolean</li><li>Collect High Entropy User Agent Hints</li></ul> |
| `contextData.myvar` | <ul><li>Custom Context Data.</li><li>Context variables in general:  <ul><li>Are unlimited in the number of context variables you may define.</li><li>Have no character limits on what you can place in a context variable.</li><li>Can contain any name you prefer.</li></ul> </li><li>Context data lets you define the name of the variable that you assign a particular value to.</li><li>Provides additional detail to what SiteCatalyst traditionally passes.</li><li>Simplifies the ability to standardize your implementation if you need to, for example, combine data from different sites.</li><li>Your data organization is at your discretion, mapping through Tealium lets you define the context data variables.</li></ul> |
| `contextData.namespace.myvar` | <ul><li>Custom Context Data With Custom Namespace.</li><li>Use the namespace prefix to avoid conflicts in variable names.</li><li>The namespace `a` is reserved for mobile implementation.</li></ul> |
| `clearVars_in_RPTCallback` | <ul><li>Boolean</li><li> Requires **Run clearVars** to be set to **Yes**.</li><li>If `clearVars_in_RPTCallback`  is set to `true`, the `clearVars` action occurs in the `registerPostTrack` (RPT) callback. If set to `false`, the `clearVars` action will occur outside the RPT callback.</li><li>The default is `false`.</li></ul> |

### Events

Mapping for events differs from mapping for the other destinations.

Use the following steps to map an event:

1. Under **Data Mappings**, select your event variable from the **Variables** drop-down list.
1. Click **Select Destination** and go to the **Event Triggers** category.
1. In the **Value** field, enter the value of the variable being mapped.  
This variable becomes the trigger string.
1. From the **Trigger** drop-down list, select the event you want to trigger.  
You can click the plus icon (**+**) to add additional value/trigger combinations.

| Destination Name | Description |
|:-----------------|:-------------|
| Value | <ul><li>The value of the mapped Variable that triggers the assigned event.</li></ul> |
| Trigger | <ul><li>The event to trigger.</li><li>Select:  <ul><li>**prodView** for product views.</li><li>**scOpen** for opening/initializing a new shopping cart.</li><li>**scAdd** for adding an item to the shopping cart.</li><li>**scRemove** for removing an item from the shopping cart.</li><li>**scView** for viewing a shopping cart.</li><li>**scCheckout** for beginning a checkout.</li><li>**purchase** for completing an order.</li><li>**event1** through **event1000** to set a custom event. <br>**Note: Events 101-1000 are available only to library versions 1.4 and up.** <ul><li>SiteCatalyst lets you use 100 custom events, also referred to as success events.</li><li>These events typically count specific things that happen on a site and do not normally contain a value, such as logins and form views.</li></ul> </li></ul> </li></ul> |

#### Product-Level Events

SiteCatalyst provides 100 destinations for sending product-specific actions.

| Destination Name | Description |
|:----------------------------------------------|:-----------------------------|
| `PRODUCTS_event1` through `PRODUCTS_event100` | The product event to assign. |

#### Value Events

SiteCatalyst provides 100 destinations for sending value events.

| Destination Name | Description |
|:----------------------------------------|:---------------------------|
| `VALUE_event1` through `VALUE_event100` | The value event to assign. |

#### Props

SiteCatalyst lets you use custom props, also called traffic variables.

| Destination Name | Description |
|:----------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `PRODUCTS_event1` through `PRODUCTS_event100` | <ul><li>The product event to assign.</li><li>Props above 75 are not built-into the mapping toolbox.</li></ul> |

SiteCatalyst lets you use 75 custom props, also called traffic variables. Props contain data that is not meant to persist beyond a page view. If you want to correlate a prop with another variable, ensure both variables get set on the same page. Use events to hold certain numeric values when passed in the product string or being serialized.

Use the following steps to map custom destinations:

1. Map a variable to any prop destination.
1. In the text box at the top, enter your custom destination in place of the built-in destination you selected.
1. Continue mapping other variables or click **Done** to finish.

#### eVars

| Destination Name | Description |
|:-------------------------------|:-------------|
| `eVar0` | <ul><li>Campaign.</li><li>For campaign/promotion tracking</li></ul> |
| `eVar1` through <br> `eVar250` | <ul><li>SiteCatalyst lets you use 250 eVars, also called conversion variables.</li><li>`evar76` through `evar250` are available only to library versions 1.4 and up.</li><li>eVars contain data that is meant to persist beyond a single page view and can be used to correlate data from an eVar to another variable, depending on how you set up your reports within Omniture.</li><li>eVars typically include internal search terms, A/B testing, campaign/promotion tracking, merchandising categories, and user types.</li></ul> |

#### Merchandising eVars

Merchandising eVars allow you to associate a product with some value in addition to the category you specify in the products string.

| Destination Name | Description |
|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `eVar0` | <ul><li>Campaign.</li><li>For campaign/promotion tracking</li></ul> |
| `PRODUCTS_eVar1` through `PRODUCTS_eVar75` | <ul><li>SiteCatalyst lets you use 250 eVar parameters, also called conversion variables.</li><li>eVars contain data that is meant to persist beyond a single page view and can be used to correlate data from an eVar to another variable depending on how you set up your reports within Omniture.</li></ul> eVars usually include internal search terms, A/B testing, campaign/promotion tracking, merchandising categories, and user types. |

#### Commerce

Since the AppMeasurement tag is e-commerce enabled, it automatically uses the default [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) mappings. Manually mapping in this category is generally not needed unless you want to override any extension mappings or a specific e-commerce variable is not offered in the extension.

Several SiteCatalyst variables, including the Product String, are automatically populated by the E-Commerce extension. SiteCatalyst uses the Product String to capture product information, revenue, units sold, and other pieces of information around purchases. A standard Product string looks like this:

![](https://docs.tealium.com/images/client-side-tags/product-string.png)

##### Best practices for the product string:

* The semicolon `;` is a standard separator for most items in the Products string.
* Delimit multiple Merchandising eVars with a pipe (`|`) character.
* Delimit multiple product instances with a comma (`,`).
* The total price is the price per unit multiplied by the quantity. The E-Commerce extension's total price (`_ctotal`) output does not automatically map to the Products string.
* A SiteCatalyst best practice is to leave the Category empty because you cannot change the category for a product once it is set in SiteCatalyst. Tealium does; however, allow you to set the category at the time of the conversion if changing the category later is not a concern.

#### E-Commerce Destinations

The following e-commerce destinations are built into the toolbox:

| Destination Name | Description | Ecommerce Extension Variable |
|:---------------------------|:--------------------------------------------------------------------|:-----------------------------|
| purchaseID | <ul><li>Unique order identifier to this destination.</li></ul> | `_corder` |
| transactionID | <ul><li>Correlates offline data to an online transaction.</li></ul> | N/A |
| state | <ul><li>Name of the state specified in the conversion</li></ul> | N/A |
| zip | <ul><li>Zip code specified in the conversion</li></ul> | N/A |
| Product IDs (array) | <ul><li>Unique ID of each product in the product array</li></ul> | `_cprod` |
| Product Categories (array) | <ul><li>Name of each category in the product array</li></ul> | `_ccat` |
| Product Quantities (array) | <ul><li>Quantity of each product in the product array</li></ul> | `_cquan` |
| Product Prices (array) | <ul><li>Unit price of each product in the product array</li></ul> | `_cprice` |

#### Other

| Variable | Description |
|:---------------------------------|:------------|
| Link Tracking - doneAction param | (H25 only) |
| List 1 | |
| List 2 | |
| List 3 | |

#### Mobile

| Variable | Description |
|:---------|:---------------|
| App ID | (`contextData.a.AppID`) |
| Device Name | (`contextData.a.DeviceName`) |
| Operating System | (`contextData.a.OSEnvironment`) |
| Operating System Version | (`contextData.a.OSVersion`) |
| Carrier Name | (`contextData.a.CarrierName`) |
| Resolution | (`contextData.a.Resolution`) |
| Install Date | (`contextData.a.InstallDate`) |
| Launch Number | (`contextData.a.Launches`) |
| Days Since First Use | (`contextData.a.DaysSinceFirstUse`) |
| Days Since Last Use | (`contextData.a.DaysSinceLastUse`) |
| Installs | (`contextData.a.InstallEvent`) |
| Upgrades | (`contextData.a.UpgradeEvent`) |
| Launches | (`contextData.a.LaunchEvent`) |
| Crashes | (`contextData.a.CrashEvent`) |
| Previous Session Length | (`contextData.a.PrevSessionLength`) |
| Hour Of Day | (`contextData.a.HourOfDay`) |
| DayOfWeek | (`contextData.a.DayOfWeek`) |
| Days Since Last Upgrade | (`contextData.a.DaysSinceLastUpgrade`) |
| Launches Since Ugrade | (`contextData.a.LaunchesSinceUpgrade`) |
| Daily Engaged Users | (`contextData.a.DailyEngUserEvent`) |
| Monthly Engaged Users | (`contextData.a.MonthlyEngUserEvent`) |
| `disable_wake_track` | <ul><li>Disable Wake Tracking</li><li>Values are `true` or `false`.</li></ul> |
| `disable_sleep_track` | <ul><li>Disable Sleep Tracking</li><li>Values are `true` or `false`.</li></ul> |
| `send_timestamp` | <ul><li>Send Timestamp Toggle</li><li>Values are `true` or `false`.</li></ul> |
| `timestamp` | <ul><li>Timestamp</li><li>ISO 8601 format</li><li>Unix Time</li></ul> |

#### Link Tracking

| Variable | Description |
|:-----------|:------------|
| `linkType` | Link Type |
| `linkName` | Link Name |

### Event Serialization Detection

The AppMeasurement tag automatically detects [event serialization](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/events/event-serialization) within the trigger values of your data layer. When the tag fires, the tag attempts to match the trigger string mapped in the **Events** tab with the trigger value in the data layer, checking to see if either trigger contains a colon.

* **Event serialization detection: On**  
When event serialization detection is turned on (default setting), the tag detects the trigger value next to the colon and attempts to match the remaining string with your mapped trigger. If there is an exact match, the event is serialized.
* **Event serialization detection: Off**  
When event serialization detection is turned off, the tag does not detect colons. The tag attempts to match both trigger values in their entirety. This setting is highly recommended if your mapped trigger string contains a colon. Turning off event serialization detection is the only way to have an event correctly trigger on a value with a colon.


<blockquote>
Whether event serialization detection is on or off, serials mapped directly with the **Event Serialization** tab always take precedence (see [scenario 3 example](#scenario3)).
</blockquote>


This following scenarios help you understand how event serialization detection interprets a trigger value with and without a colon.


<blockquote>
Throughout this section, the term "mapped trigger" refers to the value in the tag's data mapping configuration and the term "data layer trigger" refers to the value found in the data layer of your website.
</blockquote>


#### Example: Mapped trigger without a colon

As an example, if you want to trigger a `prodView` event and serialize it when the page contains `fireEvt`, you would do the following:

1. Map the UDO variable `serial` to `SERIAL_prodView` in the Event Serialization tab.
1. Map the UDO variable `trigger` to `prodView` under Events.
1. Map `fireEvt` as the trigger string for `prodView`.  
![](https://docs.tealium.com/images/client-side-tags/trigger-without-colon.jpeg)

There are many scenarios that could occur in your data layer.

#### Scenario 1: Data layer trigger is `fireEvt` and the `serial` value is empty

```js
var utag_data = {
  trigger: "fireEvt",
  serial: ""
}

```

* **Event serialization detection: On**  
The tag matches `fireEvt` with the mapped trigger and successfully fires `prodView` on the page, however there is no serialization.
* **Event serialization detection: Off**  
Same result as above.

A successful network call looks like this:

![](https://docs.tealium.com/images/client-side-tags/scene-1-network-call-.png)

#### Scenario 2: Data layer trigger is `fireEvt:123` and the `serial` value is empty

```
var utag_data = {
  trigger: "fireEvt:123",
  serial: ""
}
```

* **Event serialization detection: On**  
The tag serializes `123` then matches `fireEvt` with the mapped trigger and successfully fires `prodView` on the page.  
![](https://docs.tealium.com/images/client-side-tags/scene-2-network-call.png)

* **Event serialization detection: Off**  
The tag fails to match `fireEvt:123` with your mapped trigger, as a result `prodView` does not fire on the page.

#### Scenario 3: Data layer trigger is `fireEvt:123` and the serial value is `456` {#scenario3}

```
var utag_data = {
  trigger: "fireEvt:123",
  serial: "456"
}
```

* **Event serialization detection: On**  
Initially, the tag serializes `123` and matches `fireEvt` with your mapped trigger. Then `prodView` fires successfully and is serialized with `456` instead of `123`.  
This happens because serial values detected by event serialization mapping (`456`) take precedence over those detected by event serialization detection (`123`).  
![](https://docs.tealium.com/images/client-side-tags/scene-3-network-call.png)
* **Event serialization detection: Off**  
The tag fails to match `fireEvt:123` with your mapped trigger. As a result, `prodView` does not fire on the page.

#### Example: Mapped trigger with a colon

This example follows the same path as scenario 2, but the mapped trigger is `fireEvt:123` instead of `fireEvt`.

![](https://docs.tealium.com/images/client-side-tags/trigger-with-colon.png)

#### Scenario: Data layer trigger is `fireEvt:123`

```js
var utag_data = {
  trigger: "fireEvt:123",
  serial: ""
}
```

* **Event serialization detection: On**  
The tag serializes `123` but fails to match `fireEvt` with your mapped trigger. As a result, `prodView` does not fire on the page.
* **Event serialization detection: Of**  
The tag successfully matches `fireEvt:123` with your mapped trigger and `prodView` fires successfully. For this reason we recommend turning off event serialization detection if your string contains a colon.

## Advanced Configuration

### Setting s.events

Tealium offers a function called `u.addEvent()` to assist in setting the `s.event` string. This method appends new values to the end of `s.events`, which allows you keep all previously set events and add another event when needed. To use this method, add variable named `sc_events` to your configuration.

Use the following steps to customize `s.events` using `u.addEvent`:

1. Add a [Set Data Values](https://docs.tealium.com/set-data-values-extension/) extension.
1. Set the **Scope** to the Adobe Analytics tag.
1. From the **Set** menu, select **sc_events**.
1. From the **To** menu select **JS Code**.
1. In the text field, enter: `u.addEvent("CUSTOM_EVENT")`  
Where `CUSTOM_EVENT` is the event you want to append to the `s.events `string, such as `event10`.
1. To add multiple events in one step, pass an array to `u.addEvent`, as follows:  
`u.addEvent(["event1","event2","scView"]);`

To add values directly in the string(s) passed to the function: `u.addEvent(['event500=500', 'event501=' + b.demo_event_value]);`

To add serializations directly in the string(s) passed to the function: `u.addEvent("event78:" + b.booking_reference);`

## Supported Versions

The following code versions of AppMeasurement for JavaScript are supported:

* 2.26.0 bundled optimized
* 2.26.0
* 2\.25.0
* 2\.24.0
* 2\.23.0
* 2\.22.4
* 2\.22.3
* 2\.22.0
* 2\.21.0
* 2\.20.0
* 2\.18.0
* 2\.17.0
* 2\.15.0
* 2\.14.0
* 2\.12.0
* 2\.9.0
* 2\.8.2
* 2\.7.0
* 2\.6.0
* 2\.4.0
* 2\.3.0
* 2\.1.0
* 1\.8.0
* 1\.6.3
* 1.6.1
* 1.6.0
* 1\.5.3
* 1.5.2
* 1.5.1
* 1\.4.1
* 1\.3.2
* 1\.2.2
* 1.2.1
* 1\.0.1

### Release Notes

##### v2.23.0 Release Date September 23,

* Added support for high entropy user agent information.

##### v2.22.3 Released December 21, 2021

##### v2.20.0 Released March 5, 2020

* Updated IE detection to suppress JSLint warning to corrected a security-related issue.

##### v2.18.0 Released February 13, 2020

* AppMeasurement can now force cookies to include the Secure attribute by setting the `writeSecureCookies` variable. The entire client website must be severed securely using HTTPS to support this variable.

##### v2.17.0 Released August 23, 2019

* Added support for Baidu query string reordering.
* Corrected an issue that caused stale visitor values in hits that were queued while waiting for opt-in.

##### v2.15.0 Released July 15, 2019

* Added ActivityMap scroll reach tracking to the Activity Map extension (AN-172949)

* Added DIL 9.2 to AppMeasurement (AN-182472)

##### v2.9.0 Released May 24, 2018


<blockquote>
Visitor API 3.0 or higher is required for customers using the Experience Cloud ID Service. Adobe recommends upgrading to the latest Visitor API version when associated code libraries are updated, such as at.js, AppMeasurement.js, etc.
</blockquote>


* Updated AppMeasurement to use the updated Visitor interface for requesting IDs. (AN-151483)
* Corrected issue where link tracking cookie is being written after link tracking is turned off. (AN-156332)
* Corrected issue where `registerPreTrackCallback` and `registerPostTrackCallback` breaks callback function signature when called multiple times. (AN-158566)

##### v2.8.2 Released April 12, 2018

* Updated AppMeasurement to use the updated visitor interface for requesting IDs.
* Corrected issue with link tracking cookie.
* Reduce AppMeasurement default cookie lifetime from five (5) years to two (2) years.
* Supports Visitor API (aka Enterprise Cloud ID Service), version 3.1.2

##### v2.7.0 Released January 18, 2018

* Deprecates support for Internet Explorer (IE), versions 6 through 9.
* Includes DIL v7.00
* Supports Visitor API (aka Marketing Cloud ID Service), version 3.0

##### v2.6.0 Released November 9, 2017

* Fixed an issue where AppMeasurement library does not always set the correct account combination when `s_gl` is called. (AN-152153)
* Inclusion of `dil.js` 6.12 (Audience Manager module).
* Supports Visitor API 2.5.0.

##### v2.3.0 Released August 22, 2017

* Fixed bug where `s.Util.getQueryParam` was capturing `#`.
* Included latest version of `dil.js` (v6.10).
* Supports multiple AppMeasurement instantiation orders.
* Supports Visitor API (aka Marketing Cloud ID Service) version 2.2.0.

##### v2.1.0 Released May 11, 2017

* Supports AppMeasurement JavaScript 2.1.0
* Supports Marketing Cloud ID Service version 2.1.0
* Included latest version of `dil.js`.
* Added support for `adobe_mc_ref` parameter which overrides the page referrer.
* Added `mcorgid` parameter.
* Added `cp` (customerPerspective) parameter.

##### v1.8.0 Released March 10, 2017

* Supports AppMeasurement JavaScript 1.8.0.
* Supports Marketing Cloud ID Service version 2.0.0.
* Added two call hooks: [`s.registerPreTrackCallback`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/registerpretrackcallback) and [`s.registerPostTrackCallback`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/registerposttrackcallback).

##### v1.6.3 Released August 23, 2016

* Fixed an issue where AppMeasurement prematurely terminated request connections.
* Fixed an issue causing AppMeasurement to call the wrong obfuscated method in the Visitor API.
* Fixed an issue causing the JavaScript error: "Attribute only valid on v:image".
* Separated the Marketing Cloud ID support (aka Visitor API) into a new Tag called the Marketing Cloud ID Service Tag.


<blockquote>
The Marketing Cloud ID Service Tag has to load before all other Adobe Tags (including AppMeasurement) in your profile. Without that, you'll lose visitor tracking integrity. To load the tag first, enable the [bundle setting](https://docs.tealium.com/tag-advanced-settings/) on All Pages and load it before other Adobe tags.
</blockquote>


View [full Adobe AppMeasurement release notes](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates).

##### v1.6.1 Released July 28, 2016

The following updates affect AppMeasurement's Events, Value Events, and Event Serialization:

* Added a new Event Serialization mapping tab in the Data Mapping toolbox.
* Added a new drop-down list in the AppMeasurement Tag configuration for turning ON/OFF Event Serialization

##### v1.6.1 Released July 14, 2016

* Added new version 1.6.1
* Supports Visitor API versions 1.5.7 and 1.5.6
* Improved mechanism for handling link click tracking in Firefox.

View [full Adobe AppMeasurement release notes](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates).

## Vendor Documentation

* [Adobe Experience League: About AppMeasurement for JavaScript](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview)
* [Adobe Experience League: AppMeasurement Release History](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates)
* [Adobe Experience League: Enabling activity map](https://experienceleague.adobe.com/en/docs/analytics/analyze/activity-map/getting-started)
* [Adobe Experience League: Understanding Mobile Metrics](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/overview)
* [Adobe Experience League: Mobile Metrics Reference](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/lifecycle-metrics)
