---
title: Adobe Analytics 1.4 Connector Setup Guide
description: This article describes how to set up the Adobe Analytics 1.4 connector.
url: https://docs.tealium.com/server-side-connectors/adobe-analytics-connector/
---
## How it works

The Adobe Analytics 1.4 Connector in the Tealium Customer Data Hub uses Adobe&#39;s [Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) to send analytics data server-side, in place of using the JavaScript beacon on a web page or mobile app. This reduces the amount of data transmitted from the client-side, and also offers the advantage of being able to pass audience and visitor data from EventStream or AudienceStream to Adobe Analytics.

 The end of life date for Adobe Analytics 1.4 is August 12, 2026, including WSSE authentication. Although the Data Insertion API will remain accessible beyond that date, it will not receive updates or active support. Adobe strongly recommends migrating to Adobe Analytics 2.0, and we recommend that you migrate to use the [Adobe Analytics 2 connector]().

## Connector Actions

| **Action Name**      | **AudienceStream** | **EventStream** |
|:---------------------|:-------------------|:----------------|
| Send Analytics Event | ✓                  | ✓               |

## Connector Configuration

Use the following steps in the interface to configure the Adobe Analytics connector:

1. Go to the **Connector Marketplace** and add the Adobe Analytics connector.  
Read the [Connector Overview]() article for general instructions on how to add a connector.

1. In the **Title** field, enter a title for the connector.
1. In the **Data Insertion Domain** field, enter the domain for your Adobe Analytics data collection servers. For example, `namespace.122.2o7.net`.
1. In the **Report Suite ID** field, enter your Report Suite ID.  
This is the Report Suite used to submit the data. To send data to multiple destinations use a comma-separated list of report suites.  
    This value can also be set with a data mapping.
1. In the **Notes** field, enter any relevant notes about this connector.
1. Click **Next**.  
You are now on the **Actions** tab.
1. From the **Actions** drop-down list, select **Send Analytics Event** from the drop-down list and configure the following parameters:

| **Group**                                                          | **Description**                                                                                                                                                                                                                                                                                                                                                                                        |
|:-------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Event Parameters                                                   | &lt;ul&gt;&lt;li&gt;See &#34;General Attributes&#34; below&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                       |
| Auto-mapping of Lifecycle Event Attributes for Mobile Data-sources | &lt;ul&gt;&lt;li&gt;Check this checkbox to automatically map values from the Event Parameters section to Adobe data elements.&lt;/li&gt;&lt;li&gt;Auto mapping only applies to Mobile EventStream App Lifecycle only.&lt;/li&gt;&lt;li&gt;For more information see [Adobe Analytics Connector Lifecycle Mappings]()&lt;/li&gt;&lt;/ul&gt; |
| Context Data                                                       | &lt;ul&gt;&lt;li&gt;Specify keys using the dot format.&lt;/li&gt;&lt;li&gt;For example `my.a`.&lt;/li&gt;&lt;li&gt;Multiple key-value pairs can be specified.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                    |
| eVars                                                              | &lt;ul&gt;&lt;li&gt;Specify the event eVars by mapping an attribute to a number.&lt;/li&gt;&lt;li&gt;For example: Map `event_count` to `1` for **eVar1**.&lt;/li&gt;&lt;li&gt;Valid range is `1` through `100`, `250` for Premium Accounts&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                       |
| Hierarchy                                                          | &lt;ul&gt;&lt;li&gt;A hierarchy string.&lt;/li&gt;&lt;li&gt;Select from `1` through `5`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                             |
| List                                                               | &lt;ul&gt;&lt;li&gt;A list of values that are passed into a variable, then reported as individual line items for reporting&lt;/li&gt;&lt;li&gt;Select from `1` through `3`.&lt;/li&gt;&lt;li&gt;Requires Array type in data layer.&lt;/li&gt;&lt;li&gt;Tealium will format the data correctly to be passed along&lt;/li&gt;&lt;/ul&gt;                                                                                                                             |
| Properties                                                         | &lt;ul&gt;&lt;li&gt;Analytics property name.&lt;/li&gt;&lt;li&gt;Specify the name by mapping an attribute to a number.&lt;/li&gt;&lt;li&gt;For example: Map `lifetime_value` to `1` for **prop1**.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                               |
| Events                                                             | &lt;ul&gt;&lt;li&gt;Specify a list of events, or a comma-separated custom value.&lt;/li&gt;&lt;li&gt;see [Adobe Analytics Configure Events Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)&lt;/li&gt;&lt;/ul&gt;                                                                                                                                      |
| Event Mapping                                                      | &lt;ul&gt;&lt;li&gt;Map a potential value contained in the Events Array (configured above) to the Adobe Analytics Custom Event name.&lt;/li&gt;&lt;li&gt;For example, registration to `event3` would replace `registration` with `event3` in the event payload.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                      |
| Event Values                                                       | &lt;ul&gt;&lt;li&gt;Specify values for `Counter`, `Numeric`, and `Currency` events.&lt;/li&gt;&lt;li&gt;To specify an event, use a number.&lt;/li&gt;&lt;li&gt;As an example, 1 will be sent over as `event1`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                   |
| Products                                                           | &lt;ul&gt;&lt;li&gt;Specify product attributes (`Id`, `Category`, `Quantity`, `Price`)&lt;/li&gt;&lt;li&gt;All arrays must be equal-sized and order-aligned&lt;/li&gt;&lt;li&gt;For additional information, see [Adobe Analytics Product Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)&lt;/li&gt;&lt;/ul&gt;                                                                  |
| Product eVars                                                      | &lt;ul&gt;&lt;li&gt;Specify product eVars values.&lt;/li&gt;&lt;li&gt;All arrays must be equal-sized to those in the **Product** section.&lt;/li&gt;&lt;li&gt;Empty values will be ignored.&lt;/li&gt;&lt;li&gt;Specify eVar mappings with a number.&lt;/li&gt;&lt;li&gt;As an example, `1` will be mapped to `eVar1`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                   |
| Product Events                                                     | &lt;ul&gt;&lt;li&gt;Specify product event values.&lt;/li&gt;&lt;li&gt;All arrays must be equal-sized to those in the **Product** section.&lt;/li&gt;&lt;li&gt;Empty values will be ignored.&lt;/li&gt;&lt;li&gt;Specify event mappings with a number.&lt;/li&gt;&lt;li&gt;As an example, `1` will be mapped to `event1`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                  |
| Brands                                                    | &lt;ul&gt;&lt;li&gt;Specify brand attributes.&lt;/li&gt;&lt;li&gt;Available attributes are **brand** and **version**.&lt;/li&gt;&lt;li&gt;All arrays must be equal-sized.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                  |

When you are done configuring parameters, click **Save**, and then Save and Publish your changes.

## General Attributes

For a full reference of all attributes, including details on exactly what each field should contain, see Adobe&#39;s [API documentation](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md) and the [Visitor &amp; Experience Cloud IDs](#visitor-and-experience-cloud-ids) section of this article.

#### Report Suite IDs

* Specify a report suite ID, which will override any value previously entered in the Connector Configuration UI. If you do not need to override that value, you can leave this field blank. You can use either a data layer variable, or a **Custom Value**. If you want to send data to multiple report suites, you may use a comma-separated list.
* This will overwrite the value defined in the Configuration Tab
* Specifies the report suites where you want to submit data. Contained in the URL
* If specifying Data Layer attributes, use simple attribute types per row. We will format the data correctly to be passed along

| Map From                                                                                               | Map To                    | Notes                                                                                                                                                                                                                                                                                                                                                                                         | Sample Connector Output                                                                                                                            |
|:-------------------------------------------------------------------------------------------------------|:--------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|
| Customer Data Hub attribute containing a persistent visitor ID, for example, tealium\_visitor\_id      | visitorID\*               | &lt;ul&gt;&lt;li&gt;Ensure that this is a visitor-level persistent value.&lt;/li&gt;&lt;li&gt;Example: Tealium Visitor ID&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                   | `&lt;visitorID&gt;01619ea9a91a001af7e29b75797104079005c07101008M&lt;/visitorID&gt;`                                                                            |
| Customer Data Hub attribute containing a page name/title                                               | pageName                  | &lt;ul&gt;&lt;li&gt;String value&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                | `&lt;pageName&gt;Homepage&lt;/pageName&gt;`                                                                                                                    |
| Customer Data Hub attribute containing the current URL (for example, built-in &#34;Current URL&#34; attribute) | pageURL                   | &lt;ul&gt;&lt;li&gt;String value&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                | `&lt;pageURL&gt;[http://www.tealium.com](http://www.tealium.com%5C)&lt;/pageURL&gt;`                                                                           |
| Customer Data Hub attribute containing the Adobe Experience Cloud ID                                   | marketingCloudVisitorID\* | &lt;ul&gt;&lt;li&gt;Usually retrieved through the Visitor API JavaScript tag.&lt;/li&gt;&lt;li&gt;Implemented in iQ Tag Management.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                             | `&lt;marketingCloudVisitorID&gt;&lt;/marketingCloudVisitorID&gt;`                                                                                              |
| Customer Data Hub attribute containing the link name                                                   | linkName                  | &lt;ul&gt;&lt;li&gt;String value.&lt;/li&gt;&lt;li&gt;Example: tealium\_event&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                               | `&lt;linkName&gt;Buy Now&lt;/linkName&gt;`                                                                                                                     |
| Customer Data Hub attribute containing the URL of the link clicked                                     | linkURL                   | &lt;ul&gt;&lt;li&gt;String value&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                | `&lt;linkURL&gt;[https://www.tealium.com/products/widgets/buynow\](https://www.tealium.com/products/widgets/buynow%5C)&lt;/linkURL&gt;`                        |
| Customer Data Hub attribute containing the order ID                                                    | purchaseID                | &lt;ul&gt;&lt;li&gt;String value.&lt;/li&gt;&lt;li&gt;E-commerce Order ID&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                   | `&lt;purchaseID&gt;ORD12345&lt;/purchaseID&gt;`                                                                                                                |
| Customer Data Hub attribute containing the document referrer                                           | referrer                  | &lt;ul&gt;&lt;li&gt;Recommend using built-in &#34;Referring URL&#34; attribute.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                         | `&lt;referrer&gt;[https://www.tealium.com/shop\](https://www.tealium.com/shop%5C)&lt;/referrer&gt;`                                                            |
| Customer Data Hub attribute containing the timestamp from the time the event occurred                  | timestamp                 | &lt;ul&gt;&lt;li&gt;(Optional) Unix epoch seconds or ISO 8601 format.&lt;/li&gt;&lt;li&gt;Do not map if your report suite is not explicitly configures to accepts timestamped hits.&lt;/li&gt;&lt;li&gt;For more information, see the [Timestamp Implementation Guide](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/timestamp.html?lang=en &#34;Timestamp Implementation Guide&#34;).&lt;/li&gt;&lt;/ul&gt; | `&lt;timestamp&gt;1519207951063&lt;/timestamp&gt;`                                                                                                             |
| Customer Data Hub attribute containing the IP address of the visitor                                   | ipaddress                 | &lt;ul&gt;&lt;li&gt;To use this optional attribute, you must have enabled the Visitor IP attribute in your account.&lt;/li&gt;&lt;li&gt;Contact your account manager if you need this feature.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                              | `&lt;ipaddress&gt;127.0.0.1&lt;/ipaddress&gt;`                                                                                                                 |
| Customer Data Hub attribute containing the user agent of the browser/device                            | userAgent                 | &lt;ul&gt;&lt;li&gt;Recommend using the built-in User Agent attribute in Customer Data Hub&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                      | `&lt;userAgent&gt;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.167 Safari/537.36&lt;/userAgent&gt;` |
| Customer Data Hub attribute containing the transaction ID for a custom event (not order ID)            | transactionID             | &lt;ul&gt;&lt;li&gt;This is not the same as purchaseID.&lt;/li&gt;&lt;li&gt;See the [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/transactionid.html?lang=en) documentation for details.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                | `&lt;transactionID&gt;CMPSUMMER18&lt;/transactionID&gt;`                                                                                                       |

#### User Agent Client Hints

Client Hints, from Chromium browsers such as Google Chrome and Microsoft Edge, offer device-specific information. This set of data replaces the user agent string as the primary source for device information.

These mapping selections appear in the **Event Parameters** section.

|Map From|Map To|Notes|Sample Connector Output|
|----|----|----|----|
| Customer Data Hub attribute containing the system architecture hint. | `architecture` | &lt;ul&gt;&lt;li&gt;String value.&lt;/li&gt;&lt;li&gt;For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.&lt;/li&gt;&lt;/ul&gt; | `&lt;architecture&gt;x64&lt;/architecture&gt;` |
| Customer Data Hub attribute containing the number of bits that the application running uses. | `bitness` | &lt;ul&gt;&lt;li&gt;String value.&lt;/li&gt;&lt;li&gt;For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.&lt;/li&gt;&lt;/ul&gt; | `&lt;bitness&gt;64&lt;/bitness&gt;` |
| Customer Data Hub attribute containing the brands hint. | `brands` | &lt;ul&gt;&lt;li&gt;Send as an array of objects.&lt;/li&gt;&lt;li&gt;For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.&lt;/li&gt;&lt;/ul&gt;  | `&lt;brands&gt;&lt;brand&gt;&lt;name&gt;Chromium&lt;/name&gt;&lt;version&gt;100&lt;/version&gt;&lt;/brand&gt;&lt;/brands&gt;` |
| Customer Data Hub attribute indicating whether the custom event occurred through a mobile connection. | `mobile` | &lt;ul&gt;&lt;li&gt;Boolean value.&lt;/li&gt;&lt;li&gt;For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.&lt;/li&gt;&lt;/ul&gt;  | `&lt;mobile&gt;true&lt;/mobile&gt;` |
| Customer Data Hub attribute containing the platform hint. | platform | &lt;ul&gt;&lt;li&gt;String value.&lt;/li&gt;&lt;/ul&gt; | `&lt;platform&gt;win&lt;/platform&gt;` |
| Customer Data Hub attribute containing the platform version hint. | `platformVersion` | &lt;ul&gt;&lt;li&gt;String value.&lt;/li&gt;&lt;li&gt;For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.&lt;/li&gt;&lt;/ul&gt;  | `&lt;platformVersion&gt;10&lt;/platformVersion&gt;` |
| Customer Data Hub attribute containing an indicator that Windows is running the 32-bit subsystem. For more information, see [WoW64 at Wikipedia](https://en.wikipedia.org/wiki/WoW64) | `wow64` | &lt;ul&gt;&lt;li&gt;Boolean value.&lt;/li&gt;&lt;li&gt;For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.&lt;/li&gt;&lt;/ul&gt; | `&lt;wow64&gt;true&lt;/wow64&gt;` |

### Link Type

This field is used for link tracking, and allows setting of a [Link Type](https://experienceleague.adobe.com/docs/analytics/components/dimensions/custom-link.html?lang=en).

| Map From                                                           | Map To                                                                   | Description                                                                       | Example                            | Sample Connector Output  |
|:-------------------------------------------------------------------|:-------------------------------------------------------------------------|:----------------------------------------------------------------------------------|:-----------------------------------|:-------------------------|
| Select any attribute from the drop-down list or enter custom value | Link type: &#34;d&#34; - Download Link &#34;e&#34; - Exit Link &#34;o&#34; - Custom (other) Link | Sends a Link Type to Adobe Analytics only if the attribute selected has a value\* | Map: (Custom Value): &#34;true&#34; to &#34;o&#34; | `&lt;linkType&gt;o&lt;/linkType&gt;` |

If the attribute selected has a value of `null`, `undefined` or `&#34;&#34;` (empty string), the Link Type will not be set on the outgoing request.

### Context Data

[Context Data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en) may be used as a more user-friendly alternative to props and eVars. You can map any event attribute or visitor attribute to Context Data variables in Adobe Analytics. Context Data variables may have any name, but is is an Adobe best practice is to prefix all variables with a unique key, such as your company name. Some variables are reserved and may only be used for predetermined functionality, such as Lifecycle Metrics; these variables are prefixed with `a.`.

| Map From                                                  | Map To                   | Description                                                            | Example                                                                    | Sample Connector Output                                                                             |
|:----------------------------------------------------------|:-------------------------|:-----------------------------------------------------------------------|:---------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|
| Select any attribute from dropdown, or enter custom value | companyname.someproperty | Maps a defined Customer Data Hub attribute to a Context Data attribute | Map: (Customer Data Hub Attribute) Campaign Name to &#34;tealium.productColor&#34; | `&lt;contextData&gt;&amp;lt;tealium.productColor&amp;gt;Red&amp;lt;/tealium.productColor&amp;gt;`&lt;/contextData&gt; |

### Analytics eVars

This field is used to map Customer Data Hub attributes to [eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en). eVars must be specified using the word &#34;eVar&#34; (not case-sensitive), plus the number of the eVar, for example, &#34;eVar11&#34;. Valid range is 1 through 250.

| Map From                                                  | Map To                                            | Description                                                                     | Example                                                      | Sample Connector Output                 |
|:----------------------------------------------------------|:--------------------------------------------------|:--------------------------------------------------------------------------------|:-------------------------------------------------------------|:----------------------------------------|
| Select any attribute from dropdown, or enter custom value | eVarX, where X is an integer in the range 1 - 250 | Maps a defined Customer Data Hub attribute to an eVar in your analytics reports | Map: (Customer Data Hub Attribute) Campaign Name to &#34;eVar75&#34; | `&lt;eVar75&gt;Summer2018`&lt;/eVar75&gt; |

### Analytics Property Name (s.props)

This field is used to map Customer Data Hub attributes to [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en). Props must be specified using the word `prop`, plus the number of the prop, for example, &#34;prop4&#34;. Valid range is 1 through 75. [List props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props) are supported, but these require prior configuration in your Adobe Analytics Report Suite admin interface.

| Map From                                                  | Map To                                           | Description                                                                     | Example                                                 | Sample Connector Output            |
|:----------------------------------------------------------|:-------------------------------------------------|:--------------------------------------------------------------------------------|:--------------------------------------------------------|:-----------------------------------|
| Select any attribute from dropdown, or enter custom value | propX, where X is an integer in the range 1 - 75 | Maps a defined Customer Data Hub attribute to an prop in your analytics reports | Map: (Customer Data Hub Attribute) Link Name to &#34;prop4&#34; | `&lt;prop4&gt;Buy Now`&lt;/prop4&gt; |

### Events (s.events)

[Events](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en) allow you to measure how frequently a particular event is occurring on your website or in your app. The events variable is a comma-separated string listing all the events that should be counted for a particular analytics event. Both [predefined events](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en) and [custom events](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en) are sent in the same string.

In the Adobe Analytics connector, the following two methods are used to specify events:

* Map an array value containing a list of event names that has been populated elsewhere (for example, an extension in iQ Tag Management, an Enrichment, or directly in your data layer).  

| Map From                                                  | Data Type | Example Input                  | Sample Connector Output                           |
|:----------------------------------------------------------|:----------|:-------------------------------|:--------------------------------------------------|
| Customer Data Hub attribute representing a list of events | Array     | [&#34;event1&#34;, &#34;event5&#34;, &#34;event9&#34;] | `&lt;events&gt;event1,event5,event9&lt;/events&gt;` |

* Specify an array of string values which map to specific event numbers, and specify the event number mappings in the &#34;Custom Event Mapping&#34; section as follows:  

| Map From                                                             | Map To                                        | Example Event Array                              | Example Input              | Sample Connector Output                                                                                      |
|:---------------------------------------------------------------------|:----------------------------------------------|:-------------------------------------------------|:---------------------------|:-------------------------------------------------------------------------------------------------------------|
| Custom text value containing a string to look up in the Events array | Name of event to trigger, for example, event8 | [&#34;newsletter\_registration&#34;, &#34;homepage\_viewed&#34;] | &#34;newsletter\_registration&#34; | `&lt;events&gt;event8&lt;/events&gt;` (because string &#34;newsletter\_registration&#34; appeared in the events array) |

### Event Value Mapping

This field allows numerical values to be assigned to events. This field is not correlated to the &#34;Custom Event Mapping&#34; field; that is, if &#34;event2&#34; is specified in the &#34;Custom Event Mapping&#34; and is also specified as a &#34;Value&#34; event, it would be included in the event variable twice - once with no value, and once with.

| Map From                                 | Data Type | Map To                                     | Example Input       | Sample Connector Output               |
|:-----------------------------------------|:----------|:-------------------------------------------|:--------------------|:--------------------------------------|
| Attribute representing a numerical value | Number    | eventX, where X is the number of the event | Map &#34;9&#34; to &#34;event5&#34; | `&lt;events&gt;event5=9&lt;/events&gt;` |

### Event Serialization

Configure event serialization by mapping an attribute that contains the event ID to a number that specifies the event. For example, mapping &#34;ABC123&#34; to &#34;2&#34; sends &#34;event2=ABC123&#34;.

| Map From                           | Data Type | Map To           | Example Input                                | Sample Connector Output                                  |
|:-----------------------------------|:----------|:-----------------|:---------------------------------------------|:---------------------------------------------------------|
| Attribute representing an event ID | String    | The event number | Map &#34;ABC123&#34; to &#34;1&#34;,&lt;br&gt; Map &#34;ABC123&#34; to &#34;2&#34; | `&lt;events&gt;event1=ABC123,event2:ABC123&lt;/events&gt;` |

### Lifecycle Events

Adobe Analytics has the ability to track Application Lifecycle events. The Tealium mobile libraries each have an optional module available to support this feature, which automatically generates the required data for Adobe Analytics.


| Tealium Attribute  | Adobe Variable | Description | Data Type | Example |
| --- | --- | --- | --- | --- |
| lifecycle\_diddetect\_crash | a.CrashEvent | Was a crash detected during this launch/wake event. Populated only if true. | Boolean | true |
| lifecycle\_dayofweek\_local | a.DayOfWeek | Local day of week that call was made - 1=Sunday, 2=Monday, etc.) | Number | 13 |
| lifecycle\_dayssincelaunch | a.DaysSinceFirstUse | Days since first launch in integer increments | Number | 23 |
| lifecycle\_dayssinceupdate | a.DaysSinceLastUpgrade | Days since the last detected app version update in integer increments | Number | 46 |
| lifecycle\_dayssincelastwake | a.DaysSinceLastUse | Days since last detected wake in integer increments | Number | 1 |
| lifecycle\_firstlaunchdate\_MMDDYYYY | a.InstallDate | GMT Timestamp formatted as MM/DD/YYYY | String | 01/18/2012 |
| lifecycle\_hourofday\_local | a.HourOfDay | Local hour of day that call was made (24 hour format) | String | true |
| lifecycle\_isfirstlaunch | a.InstallEvent | Only present if call is very first launch/wake call | String | true |
| lifecycle\_isfirstlaunchupdate | a.UpgradeEvent | Only present if call is first launch/wake after a detected updated | Boolean | true |
| lifecycle\_isfirstwakemonth | a.MonthlyEngUserEvent | Only present if call is first launch/wake of the month | Boolean | true |
| lifecycle\_priorsecondsawake | a.PrevSessionLength | Whole seconds app was awake since last launch only. Aggregates total from all wakes prior. Sent only with lifecycle\_type: launch calls. | Number | 126 |
| lifecycle\_totalwakecount | a.Launches | Total number of launches &#43; wakes since install (only reset if app deleted) | Number | &#34;563&#34; |
| lifecycle\_type | a.LaunchEvent if lifecycle\_type == &#34;launch&#34; | Type of lifecycle call | String | &#34;launch&#34;, &#34;wake&#34;, &#34;sleep&#34; |
| device (obj-c/android) or model\_name (swift) | a.DeviceName | Device model | String | iPhone 7 Plus |
| carrier (obj-c/android) or network\_name (swift) | a.CarrierName | Network carrier name | String | Verizon |
| device\_resolution | a.Resolution | Screen Resolution | String | 1080x1920 |
| resolution | Screen Resolution | String | 1080x1920 |
| app\_id | a.AppID | App ID | String | Digital Velocity 1.0 |
| device\_os\_version (obj-c/android) or os\_version (swift) | a.OSVersion | Operating system version | String | 11.1 |

For more information, see [Adobe: Lifecycle Metrics](https://marketing.adobe.com/resources/help/en_US/mobile/android/metrics.html).

### Products

The [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) variable is used wherever it is necessary to capture e-commerce information about one or more products on a particular page (Category, Product ID, Price, Quantity).

Only Customer Data Hub attributes with Array data types may be used to populate the Products variable. All arrays must be equal in length. For example:, if there are five products on the page, Product ID, Quantity, Price, and Category must all be five elements in length).

| Map From                                                  | Data Type | Map To            | Example Input Data   | Sample Connector Output                              |
|:----------------------------------------------------------|:----------|:------------------|:---------------------|:-----------------------------------------------------|
| Customer Data Hub attribute representing Product Category | Array     | Products Category | [&#34;Shoes&#34;, &#34;Shirts&#34;]  | `&lt;products&gt;Shoes;;;,Shirts;;;`&lt;/products&gt;  |
| Customer Data Hub attribute representing Product ID       | Array     | Products ID       | [&#34;ABC123&#34;, &#34;EFG234&#34;] | `&lt;products&gt;;ABC123;;,;EFG234;;`&lt;/products&gt; |
| Customer Data Hub attribute representing Quantity         | Array     | Products Quantity | [&#34;1&#34;, &#34;2&#34;]           | `&lt;products&gt;;;1;,;;2;;`&lt;/products&gt;          |
| Customer Data Hub attribute representing Price            | Array     | Products Price    | [&#34;149.99&#34;, &#34;79.80&#34;]  | `&lt;products&gt;;;;149.99,;;;79.80`&lt;/products&gt;  |

### Product Event Value Mapping

This field allows a custom conversion event to be assigned to each product in the [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) variable, and a numerical value to be assigned to each event.

If a &#34;simple&#34; variable is mapped (singular value, or custom text value), then the same value is applied to all products in the list. If a list (array) value is mapped, then the array must have the same length as the rest of the product arrays, and each item in the array will have a different value (according to its position in the array).

For these examples, assume the following product arrays are present as event attributes:

```
Product Category: [&#34;Footwear&#34;, &#34;Apparel&#34;] Product ID: [&#34;Running Shoes&#34;, &#34;T-Shirt&#34;] Quantity: [&#34;1&#34;, &#34;1&#34;] Price: [&#34;99.99&#34;, &#34;49.99&#34;]
```

| Map From                                                         | Data Type | Map To                                         | Example Input Value   | Sample Connector Output                                                                                                                                      |
|:-----------------------------------------------------------------|:----------|:-----------------------------------------------|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Custom text value containing a numerical value                   | String    | Name of event to trigger, for example, event8  | &#34;9.99&#34; (custom value) | `&lt;events&gt;event8&lt;/events&gt;``&lt;products&gt;Footwear;Running Shoes;1;99.99;**event8=9.99**,Apparel;T-Shirt;1;49.99;**event8=9.99**`&lt;/products&gt;   |
| Customer Data Hub attribute representing array of numerical data | Array     | Name of event to trigger, for example, event12 | [&#34;1.99&#34;, &#34;4.99&#34;]      | `&lt;events&gt;event8&lt;/events&gt;``&lt;products&gt;Footwear;Running Shoes;1;99.99;**event12=1.99**,Apparel;T-Shirt;1;49.99;**event12=4.99**`&lt;/products&gt; |

### Product Merchandising eVars

This field allows eVars to be assigned to each product in the [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) variable.

These work in the same way as the &#34;Product Event Value Mapping&#34; field, detailed above.

| Map From                                                                                   | Data Type | Map To                                      | Example Input Value | Sample Connector Output                                                                                                                                                 |
|:-------------------------------------------------------------------------------------------|:----------|:--------------------------------------------|:--------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Custom text value containing an eVar value                                                 | String    | Name of eVar to trigger, for example, eVar4 | &#34;my\_custom\_value&#34; | `&lt;products&gt;Footwear;Running Shoes;1;99.99;event8=9.99;**eVar4=my\_custom\_value**,Apparel;T-Shirt;1;49.99;event8=9.99;**eVar4=my\_custom\_value**`&lt;/products&gt; |
| Customer Data Hub attribute representing array of eVar values (for example, Product Color) | Array     | Name of eVar to trigger, for example, eVar6 | [&#34;red&#34;, &#34;green&#34;]    | `&lt;products&gt;Footwear;Running Shoes;1;99.99;event8=9.99;**eVar6=red**,Apparel;T-Shirt;1;49.99;event8=9.99;**eVar6=green**`&lt;/products&gt;                           |

### Hierarchy Data

Page [Hierarchy](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en) helps to classify a page within your site/app&#39;s navigation structure. There are five (5) available slots: hier1 - hier5. The only supported Customer Data Hub attribute type that can be used as a hierarchy var is an Array.

| Map From                                                  | Data Type | Map To                              | Description                                                                                                | Example                                                           | Sample Connector Output            |
|:----------------------------------------------------------|:----------|:------------------------------------|:-----------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------|:-----------------------------------|
| Select any attribute from dropdown, or enter custom value | Array     | hier1 - hier5 (drop-down selection) | Maps a defined Customer Data Hub attribute in Array format to a specified hierarchy var in Adobe Analytics | Map: (Customer Data Hub Attribute) Page Classification to &#34;hier1&#34; | `&lt;hier1&gt;Article`&lt;/hier1&gt; |

### List Data

[List Variables](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en) are delimited strings containing multiple values, and are often used for attribution purposes. A maximum of 3 list variables is available for each Report Suite. The only supported Customer Data Hub attribute type that can be used as a list var is an Array.

| Map From                                 | Data Type | Map To                                   | Description                                                                                           | Example                                                     | Sample Connector Output               |
|:-----------------------------------------|:----------|:-----------------------------------------|:------------------------------------------------------------------------------------------------------|:------------------------------------------------------------|:--------------------------------------|
| Select any array attribute from dropdown | Array     | list1, list2, list3 (dropdown selection) | Maps a defined Customer Data Hub attribute in Array format to a specified list var in Adobe Analytics | Map: (Customer Data Hub Attribute) Referrer List to &#34;list1&#34; | `&lt;list1&gt;google.com`&lt;/list1&gt; |

## Visitor and Experience Cloud IDs

See the Adobe Analytics documentation on [Visitor IDs](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en), and the order of preference in the event that multiple IDs are provided.

### Use Case 1: No prior Adobe Analytics implementation

If this will be a brand new Adobe Analytics implementation, 100% server-side, you may use your own unique visitor ID, and pass it to the visitorID attribute in the connector. You will need to decide what constitutes a suitable visitor ID, within the [constraints](https://marketing.adobe.com/resources/help/en_US/sc/implement/visitorID.html) set out by Adobe.

### Use Case 2: Migrating from existing Adobe Analytics client-side JavaScript

If you are migrating from a JavaScript-based Adobe Analytics tag to the server-side connector, you will need to keep a consistent visitor ID to avoid &#34;losing&#34; visitors when/if you migrate fully. You will also need to migrate the visitor IDs if you are implementing the Adobe Analytics Customer Data Hub connector as a secondary collection mechanism (where you are still using the JavaScript tag on your web pages or in your apps as the primary collection mechanism).

Use the following steps to migrate from existing Adobe Analytics client-side JavaScript, as described in this use case:

1. Follow [these instructions]() to configure the Adobe Experience Cloud ID tag and set up the tag in iQ Tag Management.
1. In this step, you will store the Adobe visitor IDs in a first-party cookie. This cookie ensures that the value is transmitted to the Customer Data Hub on each hit without needing to re-request the value for the duration of the session.  
    * In iQ Tag Management, go to the Data Layer tab and create two new First-Party Cookie variables called `utag_main_adobe_mcid` and `utag_main_aa_vid`.  
        You may rename these variables if you want to, but be sure to retain the `utag_main_` prefix, which will save cookie space by stacking into the `utag_main` cookie. If you rename the variables, you will need to also update the JavaScript snippet below.  
    * Create a new JavaScript Code extension, scoped to the Adobe Experience Cloud ID Service tag, and paste in the following code:  
        ```
        `if (typeof vAPI !== &#34;undefined&#34;) {
        vAPI.getInstance(u.data.adobe_org_id,
	      function (visitor) {
	      var mcID = visitor.getMarketingCloudVisitorID(),
	      analyticsID = visitor.getAnalyticsVisitorID(),
	      sessionExpiry = &#34;;exp-session&#34;;
	      // store Adobe IDs for the session duration
	      if (!mcID) {
	        // something went wrong - the visitor IDs could not be retrieved
	        utag.DB(&#34;MCID could not be returned&#34;);
	      } else {
	        utag.loader.SC(&#34;utag_main&#34;,{&#34;adobe_mcid&#34; : mcID &#43; sessionExpiry, &#34;aa_vid&#34; : analyticsID &#43; sessionExpiry});
	        // optionally, trigger an empty utag.link call to trigger sending the cookie values to UDH
	        // if utag.track call is omitted (default), values will be sent on the next utag.link or utag.view call anyway
	        // utag.track is used to avoid calling other third-party tags; only the collect tag should respond
	        // utag.track(&#34;adobe_vid_updated&#34;, {});
	      }
        },
        u.clearEmptyKeys(u.data.config), u.data.customer_ids);
        }   
        ```
        This extension creates a callback to the Adobe Visitor ID service which is called when the visitor ID(s) have been successfully retrieved from Adobe&#39;s servers, and stores the Visitor ID and Experience Cloud ID in Tealium&#39;s own first-party cookie (`utag_main`). The cookie expires at the end of the session in case the Visitor ID gets updated in the future. If you want to make the cookie persistent (non-expiring), set `sessionExpiry` to `&#34;&#34;` in the above code.
    * Add a condition to the JavaScript extension &#34;utag\_main\_adobe\_mcid `is not defined` AND utag\_main\_aa\_vid `is not defined`&#34;. This prevents the code from running again during this session.
1. Configure the Customer Data Hub for AudienceStream and EventStream.   
    * AudienceStream Configuration - If you have AudienceStream, you can store the Adobe Visitor ID and Experience Cloud ID as visitor-level string attributes. Do not store them as Visitor ID attributes. For any actions triggered by an audience event, you may then map the new attribute to `visitorID` and `marketingCloudVisitorID` in the connector configuration.
    * EventStream Configuration  - If you only have EventStream, you do not have the ability to store visitor ID variables, which is why we stored the value in a cookie. If you have already published your iQ Tag Management configuration from the previous step to Prod, you will find the new `utag_main_adobe_mcid` and `utag_main_aa_vid` values already present in your [Event Attributes]().
    * If you have not published to Prod, you may manually add the event attributes, using the **First Party Cookie** string attribute type. Once you have defined these attributes, you may now choose them in the Adobe Analytics connector and map them to `marketingCloudVisitorID` and `visitorID` , respectively.

## Debugging Common Issues

* To test the connector, we recommend using [trace](). While running a trace, look for the &#34;HTTP Request Body&#34; field, which will show the formatted XML that was sent to Adobe. You can compare the XML output to the &#34;Sample Connector Output&#34; fields in the above tables to verify the output.
* Look for any errors in the response code being returned from Adobe. Anything other than HTTP Response Status: 200/Successful indicates that there was an error with the request.
* The full URL structure for the Data Insertion API follows the format `http://namespace.112.2o7.net/b/ss//6`. Note that the double forward slash is intentional and valid (in the JavaScript Adobe Analytics implementation, the Report Suite ID would reside here). `/6` indicates that an XML payload is being transmitted, and the reportSuite value is sent as part of the XML payload. This is the value you will see when running a [trace]() session.  
    You do not need to enter the full URL value into the connector configuration; Tealium auto-generates the URL based on the Data Insertion Domain value. You will only see the full URL when running a Trace session.
* For your specific implementation, you may have a different value for the Data Insertion Domain (for example, `sc.omtrdc.net`), but the namespace should always precede the domain (for example, `namespace.sc.omtrdc.net`), except where you have your own first-party tracking domain (for example, `smetrics.acme.com`).
* If data is not being received by Adobe Analytics, check the [**Timestamps Optional**](https://experienceleague.adobe.com/docs/analytics/technotes/timestamps-optional.html?lang=en) section of your report suite. If timestamp is not optional, be sure to map a valid timestamp.
* We highly recommend that you map to User Agent or Client Hints. Not mapping this value will result in Adobe picking up the server&#39;s User Agent (for example, `Apache-HttpClient/4.5.5(Java/11.0.17`), which may be identified as bot traffic.
