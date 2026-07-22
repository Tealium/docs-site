---
title: Adobe Analytics 2.0 Connector Setup Guide
description: This article describes how to set up the Adobe Analytics 2.0 connector.
url: https://docs.tealium.com/server-side-connectors/adobe-analytics-2-connector/
---
## How it works

The Adobe Analytics 2.0 connector uses the [Adobe Bulk Data Insertion API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/endpoints/bulk-data-insertion/) to send analytics data, in place of using the JavaScript beacon on a web page or mobile app. This reduces the amount of data transmitted from the client-side, and also offers the advantage of being able to pass audience and visitor data from EventStream or AudienceStream to Adobe Analytics.


<blockquote>
The end of life date for Adobe Analytics 1.4 is August 12, 2026, including WSSE authentication. Although the Data Insertion API will remain accessible beyond that date, it will not receive updates or active support. We recommend that you use the Adobe Analytics 2 connector instead.
</blockquote>


## Adobe Analytics 2.0 connector differences

The following Adobe Analytics 1.4 connector features are not available in the Adobe Analytics 2.0 connector:

* Custom Field Mapping (Advanced)
* Enable auto-mapping of Lifecycle Event Attributes for Mobile Data-sources

Some Adobe Analytics 1.4 parameters are not available in the Adobe Analytics 2.0 connector, as shown in the following table. An ✗ in the **Adobe Analytics 2.0 parameter** column indicates that parameter is not available in the 2.0 connector.

| Adobe Analytics 1.4 parameter | Adobe Analytics 2.0 parameter |
| ----- | ----- |
| a4t | tnta |
| architecture | hints.architecture |
| bitness | hints.bitness |
| browserHeight | browserHeight |
| browserWidth | browserWidth |
| campaign | campaign |
| channel | channel |
| connectionType | connectionType |
| cookiesEnabled | cookiesEnabled |
| currencyCode | currencyCode |
| customerPerspective | ✗ |
| fallbackVisitorID | ✗ |
| homePage | ✗ |
| imsregion | ✗ |
| ipaddress | ipaddress |
| javaEnabled | javaEnabled |
| javaScriptVersion | ✗ |
| language | language |
| linkName | linkName |
| linkType | linkType |
| linkURL | linkURL |
| marketingCloudOrgID | ✗ |
| marketingCloudVisitorID | marketingCloudVisitorID |
| mobile | hints.mobile |
| pageName | pageName |
| pageType | pageType |
| pageURL | pageURL |
| platform | hints.platform |
| platformVersion | hints.platformversion |
| plugins | ✗ |
| purchaseID | purchaseID |
| referrer | referrer |
| reportSuiteID | reportSuiteID |
| resolution | resolution |
| server | server |
| state | ✗ |
| timestamp | timestamp |
| timezone | ✗ |
| transactionID | transactionID |
| userAgent | userAgent |
| visitorID | visitorID |
| wow64 | hints.wow64 |
| zip | zip |

For information on migrating Adobe Analytics 1.4 connectors to Adobe Analytics 2.0 connectors, see [Migrator Tool]().

## Configuration

Configuring the Adobe Analytics 2.0 Connector requires the Client ID (API Key) and Client Secret for the Adobe Analytics 2.0 API. To create credentials in the Adobe Developer Console and obtain the Client ID and Client Secret for Adobe Analytics 2.0 API, use the following steps:

1. Go to the Adobe Developer Console and log in with your Adobe ID.
1. Click **Create a new project**.
1. Enter a name for your project, then click **Save**.
1. In your project dashboard, click **Add API**.
1. In the list of available APIs, select **Adobe Analytics**.
1. For **Authentication Type**, select **Server-to-Server Authentication**.
1. For the type of integration, select **OAuth Server-to-Server**.
1. Select the **Product Profiles** you want to provide access to.
1. To retrieve the Client ID and Client Secret, go to the **Credentials** section in your project.
1. To view and copy the Client ID and Client Secret, click **Retrieve Client Secret**. 

After you have obtained the Client ID and Client Secret, use the following steps in the interface to configure an Adobe Analytics connector:

1. Go to the **Connector Marketplace** and add the Adobe Analytics connector.  
For general instructions on how to add a connector, see [Connector Overview](https://docs.tealium.com/about-connectors/).
1. Select an **Audience** and a **Trigger**, then click **Continue**.
1. Click **Add Connector**.
1. Enter a **Name** for the connector.
1. Enter the **Client ID** and **Client Secret**.
1. (Optional) Click **Test Connection**.
1. Click **Done**, then click **Continue**.

The next step is [configuring an action]().

### Batch limits

Adobe Analytics 2.0 only allows a compressed file to be sent in each call, which means the connector cannot perform a real-time action. The connector performs a 30-second micro-batched action instead. 

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 250,000
* Maximum time since oldest request: 30 minutes
* Maximum size of requests: Compressed file 100 MB; Uncompressed file 300 MB


<blockquote>
If your requests exceed the size limits, create more connector actions with smaller batch sizes per action.
</blockquote>


## Actions

| Action Name      | AudienceStream | EventStream |
|:---------------------|:-------------------|:----------------|
| Send Analytics Event | ✓                  | ✓               |
| Send Analytics Event (Batch) | ✓          | ✓               |

### Configure an action

Select an action, then configure the following parameters:

| **Group**  | **Description** |
|-------------|-----------------|
| Event Parameters | <ul><li>For more information, see [General Attributes](#general-attributes).</li></ul> |
| Context Data | <ul><li>Specify keys using the dot format.</li><li>For example `my.a`.</li><li>Multiple key-value pairs can be specified.</li></ul> |
| eVars | <ul><li>Specify the event eVars by mapping an attribute to a number.</li><li>For example: Map `event_count` to `1` for **eVar1**.</li><li>Valid range is `1` through `100`, `250` for Premium Accounts</li></ul> |
| Hierarchy | <ul><li>A hierarchy string.</li><li>Select from `1` through `5`.</li></ul> |
| List | <ul><li>A list of values that are passed into a variable, then reported as individual line items for reporting</li><li>Select from `1` through `3`.</li><li>Requires Array type in data layer.</li><li>Tealium will format the data correctly to be passed along</li></ul> |
| Properties | <ul><li>Analytics property name.</li><li>Specify the name by mapping an attribute to a number.</li><li>For example: Map `lifetime_value` to `1` for **prop1**.</li></ul> |
| Events | <ul><li>Specify a list of events, or comma-separated custom values.</li><li>For more information, see [Adobe Analytics Configure Events Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)</li></ul> |
| Event Mapping | <ul><li>Map a potential value contained in the Events Array to the Adobe Analytics Custom Event name.</li><li>For example: Mapping purchase to 3, will replace purchase with event3, so the final output based on the original Events example would change from event1,event2,event3,purchase to event1,event2,event3,event4.</li></ul> |
| Event Values | <ul><li>Specify values for `Counter`, `Numeric`, and `Currency` events.</li><li>To specify an event, use a number.</li><li>For example, mapping 9.99 to 2 results in the following output: `event1,event2=9.99,event3,event4`.</li></ul> |
| Event Serialization | <ul><li>Specifies event IDs to use to serialize events.</li><li>For more information see, [Event Serialization](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/events/event-serialization#vars).</li><li>For example, mapping page_view to 3, results in the following output: `event1,event2,event3:page_view,event4`.</li></ul> |
| Products | <ul><li>Specify product attributes (`Id`, `Category`, `Quantity`, `Price`)</li><li>All arrays must be equal-sized and order-aligned</li><li>For additional information, see [Adobe Analytics Product Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)</li></ul> |
| Product eVars | <ul><li>Specify product eVars values.</li><li>All arrays must be equal-sized to those in the **Product** section.</li><li>Empty values will be ignored.</li><li>Specify eVar mappings with a number.</li><li>As an example, `1` will be mapped to `eVar1`.</li></ul> |
| Product Events | <ul><li>Specify product event values.</li><li>All arrays must be equal-sized to those in the **Product** section.</li><li>Empty values will be ignored.</li><li>Specify event mappings with a number.</li><li>As an example, `1` will be mapped to `event1`.</li></ul> |
| Brands | <ul><li>Specify brand attributes.</li><li>Available attributes are **brand** and **version**.</li><li>All arrays must be equal-sized.</li></ul> |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `30` minutes. |

When you are done configuring parameters, click **Save**, and then Save and Publish your changes.

## General attributes

For a full reference of all attributes, including details on exactly what each field should contain, see [Adobe: API documentation](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md) and the [Visitor & Experience Cloud IDs](#visitor-and-experience-cloud-ids) section of this article.

### User agent client hints

Client Hints, from Chromium browsers such as Google Chrome and Microsoft Edge, offer device-specific information. This set of data replaces the user agent string as the primary source for device information.

These mapping selections appear in the **Event Parameters** section.

|Map From|Map To|Notes|Sample Connector Output|
|----|----|----|----|
| Server-side attribute containing the system architecture hint. | `hints.architecture` | <ul><li>String value.</li><li>For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.</li></ul> | `x64` |
| Server-side attribute containing the number of bits that the application running uses. | `hints.bitness` | <ul><li>String value.</li><li>For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.</li></ul> | `64` |
| Server-side attribute indicating whether the custom event occurred through a mobile connection. | `hints.mobile` | <ul><li>Boolean value.</li><li>For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.</li></ul>  | `true` |
| Server-side attribute containing the platform hint. | `hints.platform` | <ul><li>String value.</li></ul> | `win` |
| Server-side attribute containing the platform version hint. | `hints.platformVersion` | <ul><li>String value.</li><li>For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.</li></ul>  | `10` |
| Server-side attribute containing an indicator that Windows is running the 32-bit subsystem. For more information, see [WoW64 at Wikipedia](https://en.wikipedia.org/wiki/WoW64) | `hints.wow64` | <ul><li>Boolean value.</li><li>For more information, see [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) at Adobe.</li></ul> | `true` |

### Context data

[Context Data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en) may be used as a more user-friendly alternative to props and eVars. You can map any event attribute or visitor attribute to Context Data variables in Adobe Analytics. Context Data variables may have any name, but it is an Adobe best practice to prefix all variables with a unique key, such as your company name. Some variables are reserved and may only be used for predetermined functionality, such as Lifecycle Metrics; these variables are prefixed with `a.`.

| Map From | Map To | Description | Example | 
|---------------|------------|------------------|---------------|
| Select any attribute from the list, or enter a custom value. | companyname.someproperty | Maps a defined server-side attribute to a Context Data attribute | Map: (Server-side Attribute) Campaign Name to `tealium.productColor` |

### Analytics eVars

This field is used to map server-side attributes to [eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en). eVars must be specified by mapping an attribute to a number. Valid range is `1` through `250`.

| Map From | Map To | Description | Example |
|---------------|------------|------------------|---------------|
| Select any attribute from the list, or enter a custom value. | X, where X is an integer in the range 1-250 | Maps a defined server-side attribute to an eVar in your analytics reports | For example, map `event_count` to `1` for `eVar1`. |

### Analytics property name (s.props)

This field is used to map server-side attributes to [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en). Props must be specified using the word `prop`, plus the number of the prop, for example, `prop4`. Props must be specified by mapping an attribute to a number. Valid range is `1` through `75`. [List props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props) are supported, but these require prior configuration in your Adobe Analytics Report Suite admin interface.

| Map From | Map To | Description | Example | 
|---------------|------------|------------------|---------------|
| Select any attribute from the list, or enter a custom value. | X, where X is an integer in the range `1` through `75`. | Maps a defined server-side attribute to a prop in your analytics reports. | Map `lifetime_value` to `1` for `prop1`. |

### Events (s.events)

[Events](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en) allow you to measure how frequently a particular event is occurring on your website or in your app. The events variable is a comma-separated string listing all the events that should be counted for a particular analytics event. Both [predefined events](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en) and [custom events](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en) are sent in the same string.

Map an array value containing a list of event names that has been populated elsewhere (for example, an extension in iQ Tag Management, an Enrichment, or directly in your data layer).  

| Input | Sample Connector Output |
|------------|----------------------------|
| Server-side attribute representing a list of events. | `event1,event5,event9` |

### Events mapping

If you need to rename any event name above by an event X, it can be renamed by mapping.

For example, mapping `purchase` to `4`, replaces `purchase` with `event4`, so the final output based on the Events Mapping example in the [Configure an action]() section would change from `event1,event2,event3,purchase` to `event1,event2,event3,event4`.

| Map From | Data Type | Map To | Example Input | Sample Connector Output  |
|:---------|:----------|:-------|:--------------|:-------------------------|
| Custom text value containing a string to look up in the Events array. | Name of event to trigger, for example, `event8`. | `["newsletter_registration", "homepage_viewed"]` | `newsletter_registration` |

### Event values

This field allows numerical values to be assigned to events.

| Map From | Data Type | Map To | Example Input  | Sample Connector Output  |
|:---------|:----------|:-------|:---------------|:-------------------------|
| Attribute representing a numerical value. | Number    | X, where X is the number of the event. | Map `9` to `event5` | `event5=9` |

### Event serialization

Configure event serialization by mapping an attribute that contains the event ID to a number that specifies the event.

| Map From | Data Type | Map To | Example Input | Sample Connector Output  |
|:---------|:----------|:-------|:--------------|:-------------------------|
| Attribute representing an event ID. | String    | The event number. | Map `ABC123` to `1`,<br> Map `ABC123` to `2` | `event1:ABC123,event2:ABC123` |

### Products

The [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) variable is used wherever it is necessary to capture e-commerce information about one or more products on a particular page (Category, Product ID, Price, Quantity).

Only server-side attributes with array data types may be used to populate the Products variable. All arrays must be equal in length. For example, if there are five products on the page, Product ID, Quantity, Price, and Category must all be five elements in length.

| Map From | Data Type | Map To | Example Input Data | Sample Connector Output |
|--------------|--------------|-------------|------------------------|-----------------------|
| Server-side attribute representing Product Category | Array       | Products Category | `["Shoes", "Shirts"]`  | `Shoes;;;,Shirts;;;`  |
| Server-side attribute representing Product ID       | Array       | Products ID       | `["ABC123", "EFG234"]` | `;ABC123;;,;EFG234;;` |
| Server-side attribute representing Quantity         | Array       | Products Quantity | `["1", "2"]`           | `;;1;,;;2;;`          |
| Server-side attribute representing Price            | Array       | Products Price    | `["149.99", "79.80"]`  | `;;;149.99,;;;79.80`  |

### Product events

This field allows a custom conversion event to be assigned to each product in the [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) variable, and a numerical value to be assigned to each event.

If a simple variable is mapped (a singular value, or a custom text value), then the same value is applied to all products in the list. If a list (array) value is mapped, then the array must have the same length as the rest of the product arrays, and each item in the array will have a different value (according to its position in the array).

For these examples, assume the following product arrays are present as event attributes:

```
Product Category: ["Footwear", "Apparel"] Product ID: ["Running Shoes", "T-Shirt"] Quantity: ["1", "1"] Price: ["99.99", "49.99"]
```

| Map From  | Data Type | Map To  | Example Input Value | Sample Connector Output |
|-----------|----------|----------|---------------------|-------------------------|
| Custom text value containing a numerical value. | String   | Name of event to trigger. For example, `event8`. | `9.99` (custom value) | `Footwear;RunningShoes;1;99.99;event8=9.99,Apparel;T-Shirt;1;49.99;event8=9.99` |
| Server-side attribute representing numerical array. | Array    | Name of event to trigger. For example, `event12`. | `["1.99", "4.99"]`  | `Footwear;RunningShoes;1;99.99;event12=1.99,Apparel;T-Shirt;1;49.99;event12=4.99` |

### Product eVars

This field allows eVars to be assigned to each product in the [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) variable.

These work in the same way as the **Product Events** field, described above.

| Map From | Data Type | Map To | Example Input Value | Sample Connector Output |
|--------------|---------------|------------|-----------------------|-------------------|
| Custom text value containing a numerical value. | String | Name of event to trigger. For example, `event8`. | `9.99` (custom value) | `Footwear;RunningShoes;1;99.99;event8=9.99,Apparel;T-Shirt;1;49.99;event8=9.99` |
| Server-side attribute representing an array of numerical data. | Array | Name of event to trigger. For example, `event12`. | `["1.99", "4.99"]` | `Shoes;1;99.99;event12=1.99,Apparel;T-Shirt;1;49.99;event12=4.99` |

### Hierarchy

Page [Hierarchy](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en) helps to classify a page within your site/app's navigation structure. There are five available slots: `hier1` through `hier5`.

### List data

[List Variables](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en) are delimited strings containing multiple values, and are often used for attribution purposes. A maximum of three list variables is available for each Report Suite. Array vars will be converted to a comma separated string.

| Map From | Data Type | Map To | Description | Example | Sample Connector Output |
|-------------|------------|-------------|---------------|---------------|--------------------|
| Select any array attribute from the list. | Array | `list1`, `list2`, `list3` (list selection) | Maps a defined Server-side attribute in array format to a specified list variable in Adobe Analytics. | Map: (Server-side Attribute) Referrer List to `list1` | `google.com,yahoo.com` |

### Custom ID values

Adobe offers a way to simplify the process of generating an identifier used by the Adobe Experience Cloud Identity Service. Adobe can use one of the customer IDs in the [setCustomerIDs](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/setcustomerids) method as a seed to generate an Adobe Experience Cloud visitor ID for you.

For more information, refer to [Adobe Analytics 2.0 APIS](https://github.com/AdobeDocs/analytics-2.0-apis/blob/main/src/pages/guides/endpoints/bulk-data-insertion/mcseed.md). 

#### Fields

* **customerIDType**: Specifies the type of Customer ID for which you want to provide values. For example, `email`.
* **id**: The ID used in the Experience Cloud Identity Service `setCustomerIDs` method. Mapped to customerID.[customerIDType].id. For example, customerID.email.id ↔︎ Customer Email.
* **isMCSeed**: An integer boolean that lets you use `customerID.[customerIDType].id` as the hit's identifier. Use `1` for true and `0` for false. 
* **authState**: The authState used in the Experience Cloud Identity Service `setCustomerIDs` method. String values are not case-sensitive. The supported values are as follows:
    * `0` or an empty string: Not logged in
    * `1` or `AUTHENTICATED`: Logged in
    * `2` or `LOGGED_OUT`: Logged out.
    
#### Method parameters

| Parameter    | Description |
| ---------------  | --------------- |
| `customerIDType` | Identifies the type of Customer ID for which you want to provide values. For example, `email`. |
| `id`             | The ID used in the Experience Cloud Identity Service `setCustomerIDs` method. Mapped to `customerID.[customerIDType].id`. For example, `customerID.email.id` ↔︎ Customer Email. |
| `isMCSeed`       | An integer boolean that lets you use `customerID.[customerIDType].id` as the hit's identifier. Use `1` for true and `0` for false. |
| `authState`      | The `authState` used in the Experience Cloud Identity Service `setCustomerIDs` method. String values are not case-sensitive. The following values are supported: <ul><li> `0` or an empty string - Not logged in</li><li>`1` or `AUTHENTICATED` - Logged in </li><li>`2` or `LOGGED_OUT` - Logged out</li></ul> |

## Visitor and experience cloud IDs

See the Adobe Analytics documentation on [Visitor IDs](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en), and the order of preference in the event that multiple IDs are provided.

### Use Case 1: No prior Adobe Analytics implementation

If this is a brand new Adobe Analytics implementation, 100% server-side, you may use your own unique visitor ID, and pass it to the visitorID attribute in the connector. You need to decide what constitutes a suitable visitor ID, within the [constraints](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=en) set out by Adobe.

### Use Case 2: Migrating from existing Adobe Analytics client-side JavaScript

If you are migrating from a JavaScript-based Adobe Analytics tag to the server-side connector, you need to keep a consistent visitor ID to avoid "losing" visitors when/if you migrate fully. You also need to migrate the visitor IDs if you are implementing the Adobe Analytics connector as a secondary collection mechanism (where you are still using the JavaScript tag on your web pages or in your apps as the primary collection mechanism).

To migrate from existing Adobe Analytics client-side JavaScript, use the following steps:

#### Step 1: Configure the Adobe Experience Cloud ID tag

Follow [these instructions](https://docs.tealium.com/adobe-experience-cloud-id-service-tag/) to configure the Adobe Experience Cloud ID tag and set up the tag in iQ Tag Management.

#### Step 2: Store the Adobe visitor IDs in a first-party cookie

Storing the Adobe visitor IDs in a first-party cookie ensures that the value is transmitted to the server-side platform on each hit, without needing to re-request the value for the duration of the session.

1. In iQ Tag Management, go to the Data Layer tab, and create two (2) new First Party Cookie variables called `utag_main_adobe_mcid` and `utag_main_aa_vid`.  
    
<blockquote>
You may rename these variables if you want to, but be sure to retain the `utag_main_` prefix, which will save cookie space by stacking into the `utag_main` cookie. If you rename the variables, you will need to also update the JavaScript snippet below
</blockquote>

1. Create a JavaScript Code extension, scoped to the Adobe Experience Cloud ID Service tag, and paste in the following code:  
    ```
    if (typeof vAPI !== "undefined") {
      vAPI.getInstance(u.data.adobe_org_id,
        function (visitor) {
          var mcID = visitor.getMarketingCloudVisitorID(),
          analyticsID = visitor.getAnalyticsVisitorID(),
          sessionExpiry = ";exp-session";
          // store Adobe IDs for the session duration
          if (!mcID) {
            // something went wrong - the visitor IDs could not be retrieved
            utag.DB("MCID could not be returned");
          } else {
            utag.loader.SC("utag_main",{"adobe_mcid" : mcID + sessionExpiry, "aa_vid" : analyticsID + sessionExpiry});
            // optionally, trigger an empty utag.link call to trigger sending the cookie values to UDH
            // if utag.track call is omitted (default), values will be sent on the next utag.link or utag.view call anyway
            // utag.track is used to avoid calling other third-party tags; only the collect tag should respond
            // utag.track("adobe_vid_updated", {});
          }
        },
        u.clearEmptyKeys(u.data.config), u.data.customer_ids);
    }
    ```

    This creates a callback to the Adobe Visitor ID service that is called when the visitor ID(s) have been successfully retrieved from Adobe's servers, and stores the Visitor ID and Experience Cloud ID in Tealium's own first-party cookie (`utag_main`). The cookie expires at the end of the session in case the Visitor ID gets updated in future. To make the cookie persistent (non-expiring), set `sessionExpiry` to `""` in the above code.

1. Add the following condition to the JavaScript extension to prevent the code from running again during this session.  
  
      
      [
        [
          {
            "input": "utag_main_adobe_mcid",
            "operator": "is not defined"
          },
          {
            "input": "utag_main_aa_vid",
            "operator": "is not defined"
          }
        ]
      ]
      
  
#### Step 3: Configure server-side for AudienceStream and EventStream 
 
* **AudienceStream**: If you have AudienceStream, you may store the Adobe Visitor ID and Experience Cloud ID as visitor-level string attributes. Do not store them as Visitor ID attributes. For any actions triggered by an audience event, you may then map the new attribute to `visitorID` and `marketingCloudVisitorID` in the connector configuration.  
* **EventStream**: If you only have EventStream, you do not have the ability to store visitor ID variables, which is why we stored the value in a cookie.  
    * If you have already published your iQ Tag Management configuration from the previous step to Prod, you will find the new `utag_main_adobe_mcid` and `utag_main_aa_vid` values already present in your event attributes.  
    * If you have not published to Prod, you may manually add the event attributes, using the **First Party Cookie** string attribute type. After you have defined these attributes, you may now choose them in the Adobe Analytics connector and map them to `marketingCloudVisitorID` and `visitorID` , respectively.

## Debugging common issues

* To test the connector, we recommend using [trace](https://docs.tealium.com/about-trace/). While running a trace, look for the **HTTP Request Body** field, which shows a sample of the CSV header and the first line that will be sent to Adobe when the batch call is executed. You can compare the CSV output to the **Sample Connector Output** fields in the above tables to verify the output.
* Look for any errors in the response code being returned from Adobe. Anything other than HTTP Response Status: 200/Successful indicates that there was an error with the request.
    
<blockquote>
You do not need to enter the full URL value into the connector configuration; Tealium auto-generates the URL based on the Data Insertion Domain value. You will only see the full URL when running a Trace session.
</blockquote>

* If Adobe Analytics is not receiving data, go to **Admin > Report suites >  Edit Settings > General > Timestamp configuration** and change the [Timestamps option](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/timestamp-optional) from `Timestamps not allowed` to `Timestamps optional` or `Timestamps required`. If timestamp is required, be sure to map a valid timestamp.
* We highly recommend that you map to User Agent or Client Hints. Not mapping this value results in Adobe picking up the server's User Agent (for example, `Apache-HttpClient/4.5.5(Java/11.0.17`), which may be identified as bot traffic.

## Migrator tool

Using the Adobe Analytics 2.0 Migrator tool, you can migrate existing Adobe Analytics 1.4 connectors into the Adobe Analytics 2.0 connector.

Before using the Migrator Tool, note the following limitations:

* This tool does not migrate the 1.4 attributes that are unavailable in version 2.0. For more information, refer to the table of 1.4 and 2.0 attributes in the [Adobe Analytics 2.0 connector differences]() section.
* Lifecycle Event Attributes for mobile data-source attributes are unavailable in the 2.0 API, so the auto-mapping of these attributes will not be migrated.
* Adobe Analytics 2.0 does not support custom attributes; therefore, the attributes in this section of the 1.4 connectors will not be migrated.

To migrate Adobe Analytics 1.4 connectors, use the following steps:

1. Go to **Server-Side**, then open the Tealium Tools extension for Google Chrome.
1. In Tealium Tools, click the **Tool Catalogue** tab, then click **Adobe Analytics 2.0 Migrator**. For more information, see [Tealium Tools]().
1. Select how actions should be migrated.  
    * To disable existing Adobe Analytics 1.4 actions as part of the migration, select **Disable existing action**.
    * To migrate only active actions, select **Migrate only active actions**.
1. Select the scope of the migration from the list:
    * All Adobe Analytics 1.4 actions
    * Specific Adobe Analytics 1.4 action
    * Specific Adobe Analytics 1.4 connector
1. Enter the Adobe Analytics **Client ID** and **Client secret** for the project.
1. Click **Start**.  
  The Migrator tool automatically migrates existing Adobe Analytics 1.4 connectors to new Adobe Analytics 2.0 connectors. The name of the connector will be the same, with the suffix "2.0 (Migrated)".
1. Verify the new connector configurations and actions.
1. Save and publish your profile.