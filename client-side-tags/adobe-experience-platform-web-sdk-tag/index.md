---
title: Adobe Experience Platform Web SDK Tag Setup Guide
description: This article describes how to set up the Adobe Experience Platform Web SDK tag.
url: https://docs.tealium.com/client-side-tags/adobe-experience-platform-web-sdk-tag/
---
Adobe Experience Platform Web SDK (Adobe Alloy) is a client-side JavaScript library that allows customers of the Adobe Experience Cloud to interact with the various services in the Experience Cloud through the Adobe Experience Platform Edge Network.

## Tag tips

* Use mappings to override standard config values and set custom parameters.
* If you are configuring multiple instances, you must provide a unique **Datastream ID** and **Org ID** for each instance. Provide multiple values in a comma-separated list.

## How it works

Mapping destinations are represented with a dot notation. The final API payload consists of a series of nested JSON objects based on the dot notation represented in the tag.

The Adobe Experience Platform Web SDK tag includes the following mappings specific to the Adobe application you are using and include XDM and non-XDM data mappings. XDM data is an object whose content and structure matches a schema you have created within Adobe Experience Platform.

* XDM Event triggers: Use to trigger events with a specific `eventType` value. 
* Event-specific parameters: Use to map both XDM and non-XDM attributes for specific events.
* Analytics XDM data: Use to map data to be passed in the XDM object. 
* Target Data: Use to map non-XDM attributes to be passed in the data object to update a Target profile or send Target Recommendations attributes.

For more information about sending XDM and non-XDM data to Adobe, see [Track Events](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) in the Adobe documentation.

### Event example

Configure Adobe Experience Platform Web SDK events by selecting a variable that maps to an event and then specifying a trigger. Events are triggered when the variable is equal to a specific value, passing the chosen event name as `eventType`. 

#### Use case: Purchase event with XDM Event Triggers

To set up a purchase event:

1. Navigate to the **Data Mappings** screen of the Adobe Experience Platform Web SDK tag configuration.
1. Select `tealium_event` from the variable drop-down list and click **Select a Destination**.
1. In the **Category** section, select **XDM Event Triggers**.
1. Set the **When mapped variable equals** field to **Purchase**. This is the value `tealium_event` must equal to trigger a purchase.
1. In the **Trigger event** drop-down list, select **Purchases** `(commerce.purchases)` under the **sendEvent: Commerce Events** section. This is the event that is triggered when `tealium_event` equals a purchase event.

![](/images/client-side-tags/adobe-experience-web-sdk-mappings-example.png)

#### Use case: Purchase event with Event-specific Parameters

If you need to send data with the purchase event that is not already included in the existing E-Commerce extension mappings, use **Event-specific Parameters**. Select an attribute from the list or enter a custom destination. Ensure you follow the specific dot notation for the given event and attribute.

The following example passes `purchaseOrderNumber` as XDM data with the purchase event:

1. Navigate to the **Data Mappings** screen of the Adobe Experience Platform Web SDK tag configuration.
1. Select `po_number` (or the relevant client-specific data layer element) from the variable drop-down list and click **Select a Destination**.
1. In the **Category** section, select **Event-specific Parameters**.
1. Because `purchaseOrderNumber` is not one of the default destinations, you must enter a **Custom Parameter**. Select **Custom** from the **Parameter** drop-down and enter the full dot notation path for the destination: `commerce.purchases.xdm.commerce.order.purchaseOrderNumber`.
1. In the **For event** drop-down list, select the event **Purchases**.
1. Click **Add** to add the parameter

#### Use case: Non-XDM data/Adobe Target data

Non-XDM, or Target data, can also be set using event mapping. In this use case, we will also send `product_brand` for use in Adobe Target.

1. Navigate to the **Data Mappings** screen of the Adobe Experience Platform Web SDK tag configuration.
1. Select `product_brand` from the variable drop-down list and click **Select a Destination**.
1. In the **Category** section, select **Target Data**.
1. Select `entity.brand` as the mapping destination.
1. The purchase event sent to the Adobe Web SDK will now include `data.__adobe.target.entity.brand` in the payload.

The following examples shows the resulting Adobe Web SDK call, including some default mappings from the E-Commerce extension. This example shows how the Adobe dot notation is broken out into a nested object for `commerce.purchases.xdm.commerce.order.purchaseOrderNumber`.

```javascript
alloy(&#34;sendEvent&#34;,{
  &#34;xdm&#34;:{
    &#34;commerce&#34;:{
      &#34;order&#34;:{
        &#34;purchaseID&#34;:&#34;123456789&#34;,
        &#34;currencyCode&#34;:&#34;USD&#34;,
        &#34;priceTotal&#34;:39.98,
        &#34;purchaseOrderNumer&#34;:&#34;A1234&#34;
      }
    },
    &#34;productListItems&#34;:[
      {
        &#34;SKU&#34;:&#34;HT105&#34;,
        &#34;name&#34;:&#34;The Big Floppy Hat&#34;,
        &#34;priceTotal&#34;:29.99,
        &#34;quantity&#34;:1
      }
    ]
  },
  &#34;data&#34;:{
    __adobe: {
      target: {
        &#34;entity.brand&#34;: &#34;Acme&#34;
      }
    }
  }
});
```

## Manage Flicker with Adobe Target

Loading the Adobe Experience Platform Web SDK asynchronously can cause content flicker, as previously loaded content could be updated by Adobe Target. To minimize flicker, Adobe recommends adding a prehiding snippet. Add this snippet to the `utag.sync.js` template with a [JavaScript extension]().

For more information about `utag.sync.js`, see [How `utag.sync.js` works]().

For information about the prehiding snippet, see [Manage Flicker](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html).

### Blank page error when using a Cookie Management Solution

When using a cookie management solution (CMS) to ensure that tags are not triggered until the user has consented to different cookie categories, the prehiding snippet loads, rendering a blank page until it times out (3-7 seconds). The reason for this behavior is that the Adobe Experience Platform Web SDK tag cannot be loaded until the user accepts consent.

The solution consists of checking if consent has been given and, based on consent, triggering the prehiding snippet or not.

If you use a custom CMS external to Tealium, manage consent checking through that CMS platform.

If you use the Tealium JavaScript extension, update the logic so that the function is triggered only if the consent cookie contains a specific value, representing the user consent for the cookie category to which the AEP Web SDK tag belongs (for example, the functional cookie&#39;s category).

#### Example

In this example, the CMS sets a cookie called `mycms_cookie` that contains the value `functional:1` if the user has accepted the usage of the functional cookies or `all:1` if the user has accepted all the cookies.

The following code checks for those values to trigger the prehiding snippet.

 There are comments in the example that identify lines of code that need to be modified for your configuration. 

```javascript
!function(e,a,n,t){
  if (a) return;
  //Check if the cookie exists, and if it does, get its value. Update the mycms_cookie bit with the actual name of your CMS&#39;s cookie.
  var cms_cookie_value = (document.cookie.match(/^(?:.*;)?\s*mycms_cookie\s*=\s*([^;]&#43;)(?:.*)?$/)||[,null])[1];
  if(cms_cookie_value){
    //Add the accepted values to an array. In the example below, the cookie value must contain either all:1 or functional:1 to trigger the prehidding snippet.     
    var accepted_values = [&#39;all:1&#39;,&#39;functional:1&#39;];
    for(var i=0;i&lt;accepted_values.length;i&#43;&#43;){
      if(cms_cookie_value.includes(accepted_values[i])){
        var x=e.head;
        if(x){
          var o=e.createElement(&#34;style&#34;);
          o.id=&#34;alloy-prehiding&#34;;
          o.innerText=n;
          x.appendChild(o);
          setTimeout(function(){o.parentNode&amp;&amp;o.parentNode.removeChild(o)},t);
          return;
        }
      }
    }
  }
}

(document, document.location.href.indexOf(&#34;adobe_authoring_enabled&#34;) !== -1, &#34;body { opacity: 0 !important }&#34;, 3000);
```

Update the `&#34;body { opacity: 0 !important }&#34;` code with the element to target, such as a specific `div`. Otherwise, the default behavior of the code is to hide the whole body of the content.

## Adobe Analytics migration guide

The Adobe Analytics tag is a legacy tag replaced by the Adobe Experience Platform Web SDK tag. The Adobe Experience Platform Web SDK tag sends data to Adobe Analytics by translating the Experience Data Model (XDM) into an Adobe Analytics format.

The Adobe Experience Platform Web SDK tag supports legacy variables, properties, and events.

### Code comparison

The following examples show the structural differences between calls in Adobe Analytics and Adobe Experience Platform Web SDK:

#### Adobe Analytics

```javascript
// Load the AppMeasurement library
var s = new AppMeasurement();
// Set the report suite ID
s.account = &#34;example-rsid&#34;;
// Set the page name
s.pageName = &#34;Home Page&#34;;
// Set other variables as needed
s.prop1 = &#34;value1&#34;;
s.eVar1 = &#34;value2&#34;;
s.hellow = &#34;value3&#34;;
// Send the data to Adobe Analytics servers
var s_code = s.t();
if (s_code) document.write(s_code);
```

#### Adobe Experience Platform Web SDK

```javascript
window.alloy(&#34;sendEvent&#34;, {
    // Set the type of event
    type: &#34;viewStart&#34;,
    // Set the data for Adobe Analytics
    xdm: {
      web: {
        webPageDetails: {
          // Set the page name
          name: &#34;Home Page&#34;
        }
      },
      _experience: {
        analytics: {
          customDimensions: {
            props: {
              prop1: &#34;value1&#34;
            },
            eVars: {
              eVar1: &#34;value2&#34;
            }
          }
        }
      },
    },
    data: {
      // Set other variables as needed
      hellow: &#34;value3&#34;,
    }
  });
```

### Migrate the Adobe Analytics tag using Tealium Tools

Using the Adobe Experience Platform Web SDK Migrator tool, you can migrate existing Adobe Analytics AppMeasurement tags into the Adobe Experience Platform Web SDK tag. 

Before using the Migrator Tool, note the following limitations:

* This tool does not migrate doPlugins or extensions. If your configuration uses doPlugins or extensions, you will need to migrate those manually. For instructions on migrating these elements, see the [Migrate events globally](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally) section of the Adobe documentation). 
* The `link_name` and `link_trackvars` variables are not supported.
* `products` variables must to be split into different attributes before they can be manually mapped as per Adobe specifications in the Adobe Experience Platform Web SDK tag. For more information, see [products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) in the Adobe documentation.
* Any events and attributes that do not automatically migrate with the tool will have an empty mapping. You can manually map these empty attributes using the [Migrate the Adobe Analytics tag manually](#migrate-the-adobe-analytics-tag-manually) guide.

Complete the following steps to migrate your Adobe Analytics tag using Tealium Tools:

1. Add the Adobe Experience Platform Web SDK Migrator to your Tealium Tools using the JSON definition at the following URL: https://solutions.tealium.net/hosted/tealiumTools/aep_migrate/aep_migrate.json. For more information about adding custom tools, see [Manage Custom Tools]().
1. Go to **Tag Management &gt; Tags** and launch the Adobe Experience Platform Web SDK Migrator tool.
1. To disable your existing Adobe Analytics tag as part of the migration, select **Disable existing tag**.
1. Select the scope for the migration:
    * All AppMeasurement Tags
    * All Active AppMeasurement Tags
    * Specific AppMeasurement Tag (You will need to add the tag UID for the tag you want to migrate.)
1. Click **Start**.  
The Migrator tool will automatically migrate existing Adobe Analytics AppMeasurement tags into the Adobe Experience Platform Web SDK tag.
1. Save and publish your profile.

If your configuration uses doPlugins or extensions, you will need to migrate those manually (see below). 

### Migrate the Adobe Analytics tag manually

To migrate from the Adobe Analytics tag to the Adobe Experience Platform Web SDK tag manually, complete the following steps.

This migration guide uses the following example data mappings in the Adobe Analytics tag:

![](/images/client-side-tags/adobe-analytics-migration-example1.png)

![](/images/client-side-tags/adobe-analytics-migration-example2.png)

1. Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().
1. Configure the following tag settings in Tealium:
    * **Org ID**: Your Adobe-assigned Experience Cloud organization ID. For example, `XXX@AdobeOrg`.
    * **Datastream ID**: Your Adobe-assigned datastream ID, which links the SDK to the appropriate accounts and configuration. Also referred to as the `edgeConfigId`.
1. Configure the following settings in Adobe Experience Platform: 
    1. Go to **Datastreams** and select the datastream you want to use in the migration.
    1. In your Datastream **Configure** screen, note the **Event Schema** used in your datastream and click **Save**. ![](/images/client-side-tags/adobe-experience-platform-datastreams.png)
    1. In the Datastream details screen, ensure your Adobe Analytics service is enabled and select the service. ![](/images/client-side-tags/adobe-experience-platform-service.png)
    1. In the **Adobe Analytics service** screen, enter the Adobe **Report Suite ID** that points to the appropriate data stores.![](/images/client-side-tags/adobe-experience-platform-aa-enable.png)
    1. Go to **Data Management &gt; Schemas** and select the **Event Schema** that is linked to your datastream. 
    1. Ensure that **Field Groups** includes the **Adobe Analytics ExperienceEvent Template** field group. ![](/images/client-side-tags/adobe-experience-platform-schemas.png)
1. In this example, you would map the following legacy attributes, properties, and events to the Adobe Experience Platform Web SDK tag in Tealium. For more information, see [About data mappings]().
    1. In the Adobe Experience Platform Web SDK tag, go to **Data Mappings**.
    1. Select the **sf (js)** variable and map it to **Analytics eVars &gt; evar181** then click **Done**.
    1. Select the **page_category (js)** variable and map to **Analytics Props &gt; prop5** and lick **Done**.
    1. Select the **medallia_custom_event(js)** variable and **XDM Event Trigger**. Configure the mapping using the following values and click **Done**:
        * Add `MDigital_Invite_Displayed:_experience.analytics.event101to200` as a custom destination.
        * When mapped variables equals: **MDigital_Invite_Displayed**
        * Trigger event: **Experience Analytics Events 101-200 (\_experience.analytics.event101to200)**
        * Custom event name: **200**
    1. Select the **page_category (js)** variable and configure the mapping using the following values and click **Done**:
        * Add `xdm._experience.analytics.customDimension` and `data.channel` as custom destinations. 
        * Go to **Non-XDM/Custom Schema** and for **Non-XDM/Custom Schema Path** enter **channel**.
1. Click **Finish**.
1. Disable your **Adobe Analytics tag**.
1. Save and publish.

For more information about configuring Adobe Experience Platform Datastream, services, and schemas, see the following articles in the Adobe documentation:

* [Configure a Datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [Create and edit schemas in the UI](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Analytics settings](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#analytics)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tag Version**: Select the appropriate tag version. The default is the latest version.
* **Instance Name**: The namespace for your SDK. The default is `alloy`.
* **Org ID**: Your Adobe-assigned Experience Cloud organization ID. For example, `XXX@AdobeOrg`.
* **Edge Domain**: The domain that will be used to interact with Adobe services. Update the default setting if you mapped one of your first-party domains (using CNAME) to an Adobe-provisioned domain.
* **Datastream ID**: Your Adobe-assigned datastream ID, which links the SDK to the appropriate accounts and configuration. Also referred to as the `edgeConfigId`.
* **Debug Enabled**: Enables debugging messages to be displayed in the browser’s JavaScript console.
* **Edge Base Path**: Configured in your Adobe account. The default is `ee`.
* **Auto Pageview Tracking**: Fires the `web.webpagedetails.pageViews` event automatically for every page view.
* **Auto Purchase Tracking**: Fires the `commerce.purchases` event automatically whenever an order ID is present.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
| --- | --- | --- |
| `library_version`  | String | The tag version. |
| `context`  | Array | The context. |
| `debugEnabled`  | Boolean | Debug enabled. |
| `decisionScopes`  | Array | The decision scopes. |
| `defaultConsent`  | String | The default consent. |
| `downloadLinkQualifier`  | String | The download link qualifier. |
| `edgeConfigId`  | String | The datastream ID. |
| `edgeDomain`  | String | The edge domain. |
| `edgeBasePath`  | String | The edge base path. |
| `auto_page_tracking`  | Boolean | Auto page tracking. |
| `auto_purchase_tracking`  | Boolean | Auto purchase tracking. |
| `event_type`  | String | The event type. |
| `errorsEnabled`  | Boolean | Errors enabled. |
| `hasHidingSnippet`  | Boolean | Adobe target pre-hiding snippet. |
| `instanceName`  | String | The instance name. |
| `orgId`  | String | The organization ID. |
| `renderDecisions`  | Boolean | Render decisions .|
| `documentUnloading`  | Boolean | Document unloading. |
| `custom.##` | - | Custom data.  | 
| `commandCallback`  | Function | `commandCallback` function. |

### Data Collection

| Variable | Type | Description |
| ---| --- | --- |
| `clickCollectionEnabled`  | Boolean | Click collection enabled. |
| `onBeforeEventSend`  | Function | onBeforeEventSend function. |
| `onBeforeLinkClickSend`  | Function | onBeforeLinkClickSend function. |
| `internalLinkEnabled` | Boolean | Internal link enabled. |
| `downloadLinkEnabled` | Boolean | Download link enabled. |
| `externalLinkEnabled` | Boolean | External link enabled. |
| `eventGroupingEnabled` | Boolean | Event grouping enabled. |
| `sessionStorageEnabled` | Boolean | Session storage enabled. |
| `filterClickDetails` | Function | Filter click details. |

### Streaming Media

| Variable | Type | Description |
|:---------|:-----|:------------|
| `channel` | String | (Required) The name of the channel where streaming media collection occurs. For example, Video channel. |
| `playerName` | String | (Required) The name of the media player. |
| `appVersion` | String | The version of the media player application. |
| `mainPingInterval` | Integer | Frequency of pings for main content, in seconds. The default value is 10. Values can range from 10 to 50 seconds. If no value is specified, the default value is used when using automatically tracked sessions. For more information, see [Data Collection: Create an automatically-tracked media session](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/createmediasession#automatic). |
| `adPingInterval` | Integer | Frequency of pings for ad content, in seconds. The default value is 10. Values can range from 1 to 10 seconds. If no value is specified, the default value is used when using automatically tracked sessions. For more information, see [Data Collection: Create an automatically-tracked media session](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/createmediasession#automatic). |

### E-Commerce

| Variable | Type | Description |
|:---------| --- | :------------|
| `purchaseID` (Overrides `_corder`) | String | The order ID.  | 
| `priceTotal` (Overrides `_ctotal`) | String | The order total.  | 
| `currencyCode` (Overrides `_ccurrency`) | String | The currency.  | 
| `product.name` (Overrides `_cprodname`)  | Array | List of names. |
| `product.SKU` (Overrides `_csku`)  | Array | List of SKUs. |
| `product.quantity` (Overrides `_cquan`)  | Array | List of quantities. |
| `product.priceTotal` (Overrides `_cprice`)  | Array | List of prices. |
| `product.lineItemId` (Overrides `_ccat`)  | Array | List of line item IDs. |
| `payment.transactionID`  | Array | Payment transaction ID. |
| `payment.paymentAmount`  | Array | The payment amount. |
| `payment.paymentType`  | Array | The payment type. |
| `payment.currencyCode`  | Array | Payment currency code. |

### Privacy Options

| Variable | Type | Description |
|:---------| ---| :------------|
| `defaultConsent`  | String | The default consent. |


### Personalization Options

| Variable | Type | Description |
|:---------| --- | :------------|
| `prehidingStyle`  | String | Pre-hiding style. |
|`targetMigrationEnabled`  | Boolean |  Target migration enabled. |


### Audiences Options

| Variable | Type | Description |
|:---------| --- | :------------|
| `cookieDestinationsEnabled`  | Boolean | Cookie destinations enabled. |
| `urlDestinationsEnabled`  | Boolean | URL destinations enabled. |


### Identity Options

| Variable | Type | Description |
|:---------| --- | :------------|
| `idMigrationEnabled`  | Boolean | ID migration enabled. |
| `thirdPartyCookiesEnabled`  | Boolean | Third party cookies enabled. |
| `identityMap`  | String | The identity map. |

### identityMap Parameters

| Variable | Type | Description |
|:---------| ---- | :------------|
| `id_namespace`  | [Array, String] | The ID namespace. |
| `id`  | [Array, String] | The ID. |
| `authenticatedState`  | [Array, String] | Authenticated state. |
| `primary`  | [Array, String] | Primary. |

### Datastream Overrides

| Variable | Type | Description |
|:---------| ---- | :------------|
| `edgeConfigOverrides.com_adobe_experience_platform.datasets.event.datasetId`  | String | Experience Platform Event Dataset. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets.profile.datasetId`  | String | Experience Platform Profile Dataset. |
| `edgeConfigOverrides.com_adobe_analytics.reportSuites`  | [Array, String] | Adobe Analytics Report Suites. |
| `edgeConfigOverrides.com_adobe_identity.idSyncContainerId`  | Number | Audience Manager ID Sync Container. |
| `edgeConfigOverrides.com_adobe_target.propertyToken`  | String | Adobe Target Property Token. |
| `edgeConfigOverrides.datastreamId`  | String | &lt;ul&gt;&lt;li&gt;Data Stream ID.&lt;/li&gt;&lt;li&gt;You can map multiple datastream IDs separated by a comma.&lt;/li&gt;&lt;li&gt;Each time a sendEvent call is made, the tag verifies if there are multiple datastream IDs in this variable.&lt;/li&gt;&lt;li&gt;If there are multiple datastream IDs, a separate sendEvent call is made for each datastream ID.&lt;/li&gt;&lt;li&gt;Note that `edgeConfigOverrides.datastreamId` overrides `edgeConfigID`, which overrides the datastream ID set in the configuration step.&lt;/li&gt;&lt;/l&gt; |

### XDM Event Triggers 

| Variable | Description |
|:---------|:------------|
| `advertising.clicks` | Clicks |
| `advertising.completes` | Completes |
| `advertising.conversions` | Conversions |
| `advertising.federated` | Federated |
| `advertising.firstQuartiles` | First Quartiles |
| `advertising.impressions` | Impressions |
| `advertising.midpoints` | Midpoints |
| `advertising.starts` | Starts |
| `advertising.thirdQuartiles` | Third Quartiles |
| `advertising.timePlayed` | Time Played |
| `application.close` | Close |
| `application.launch` | Launch |
| `commerce.checkouts` | Checkouts |
| `commerce.productListAdds` | Product List Adds |
| `commerce.productListOpens` | Product List Opens |
| `commerce.productListRemovals` | Product List Removals |
| `commerce.productListReopens` | Product List Reopens |
| `commerce.productListViews` | Product List Views |
| `commerce.productViews` | Product Views |
| `commerce.purchases` | Purchases |
| `commerce.saveForLaters` | Save For Laters |
| `decisioning.propositionDisplay` | Proposition Display |
| `decisioning.propositionInteract` | Proposition Interact |
| `delivery.feedback` | Feedback |
| `directMarketing.emailBounced` | Email Bounced |
| `directMarketing.emailBouncedSoft` | Email BouncedSoft |
| `directMarketing.emailClicked` | Email Clicked |
| `directMarketing.emailDelivered` | Email Delivered |
| `directMarketing.emailOpened` | Email Opened |
| `directMarketing.emailUnsubscribed` | Email Unsubscribed |
| `inappmessageTracking.dismiss` | Dismiss |
| `inappmessageTracking.display` | Display |
| `inappmessageTracking.interact` | Interact |
| `leadOperation.callWebhook` | Call Webhook |
| `leadOperation.convertLead` | Convert Lead |
| `leadOperation.interestingMoment` | Interesting Moment |
| `leadOperation.newLead` | New Lead |
| `leadOperation.scoreChanged` | Score Changed |
| `leadOperation.statusInCampaignProgressionChanged ` | Status In Campaign Progression Changed |
| `listOperation.addToList` | Add To List |
| `listOperation.removeFromList` | Remove From List |
| `message.feedback` | Feedback |
| `message.tracking` | Tracking |
| `opportunityEvent.addToOpportunity` | Add To Opportunity |
| `opportunityEvent.opportunityUpdated` | Opportunity Updated |
| `opportunityEvent.removeFromOpportunity` | Remove From Opportunity |
| `pushTracking.applicationOpened` | Application Opened |
| `pushTracking.customAction` | Custom Action |
| `web.webinteraction.linkClicks` | Link Clicks |
| `web.webpagedetails.pageViews` | Page Views |
| `web.formFilledOut` | Form Filled Out |
| `identityMap` | identityMap |
| `Custom._experience.analytics.event1to100 ` | Experience Analytics Events 1-100 |
| `Custom._experience.analytics.event101to200` | Experience Analytics Events 101-200  |
| `Custom._experience.analytics.event201to300` | Experience Analytics Events 201-300  |
| `Custom._experience.analytics.event301to400` | Experience Analytics Events 301-400  |
| `Custom._experience.analytics.event401to500` | Experience Analytics Events 401-500  |
| `Custom._experience.analytics.event501to600` | Experience Analytics Events 501-600 |
| `Custom._experience.analytics.event601to700` | Experience Analytics Events 601-700  |
| `Custom._experience.analytics.event701to800` | Experience Analytics Events 701-800  |
| `Custom._experience.analytics.event801to900` | Experience Analytics Events 801-900 |
| `Custom._experience.analytics.event901to1000` | Experience Analytics Events 901-1000  |
| Custom | Custom |

### Analytics XDM Data

| Variable | Type | Description |
|:---------|---|:------------|
| `xdm.timestamp`  | String | xdm.timestamp |
| `xdm.application.isClose`  | String | xdm.application.isClose |
| `xdm.application.isInstall`  | String | xdm.application.isInstall |
| `xdm.application.isLaunch`  | String | xdm.application.isLaunch |
| `xdm.application.closeType`  | String | xdm.application.closeType |
| `xdm.application.name`  | String | xdm.application.name |
| `xdm.application.isUpgrade`  | String | xdm.application.isUpgrade |
| `xdm.application.version`  | String | xdm.application.version |
| `xdm.application.sessionLength`  | String | xdm.application.sessionLength |
| `xdm.web.webInteraction.URL`  | String | web.webInteraction.URL |
| `xdm.web.webInteraction.name`  | String | web.webInteraction.name |
| `xdm.web.webInteraction.type`  | String | web.webInteraction.type |
| `xdm.web.webPageDetails.URL`  | String | web.webPageDetails.URL |
| `xdm.web.webPageDetails.name`  | String | web.webPageDetails.name |
| `xdm.web.webPageDetails.isErrorPage`  | String | web.webPageDetails.isErrorPage |
| `xdm.web.webPageDetails.server`  | String | web.webPageDetails.server |
| `xdm.web.webPageDetails.siteSection`  | String | web.webPageDetails.siteSection |
|`xdm.web.webPageDetails.viewName`  | String |  web.webPageDetails.viewName |
| `xdm.web.webReferrer.URL`  | String | web.webReferrer.URL |
| `xdm.commerce.checkouts.id`  | String | xdm.commerce.checkouts.id |
| `xdm.commerce.checkouts.value`  | String | xdm.commerce.checkouts.value |
| `xdm.commerce.order.currencyCode`  | String | xdm.commerce.order.currencyCode |
| `xdm.commerce.order.purchaseID`  | String | xdm.commerce.order.purchaseID |
| `xdm.commerce.order.transactionID`  | String | xdm.commerce.order.transactionID |
| `xdm.commerce.productListAdds.id`  | String | xdm.commerce.productListAdds.id |
| `xdm.commerce.productListAdds.value`  | String | xdm.commerce.productListAdds.value |
| `xdm.commerce.productListOpens.id`  | String | xdm.commerce.productListOpens.id |
| `xdm.commerce.productListOpens.value`  | String | xdm.commerce.productListOpens.value |
| `xdm.commerce.productListRemovals.id`  | String | xdm.commerce.productListRemovals.id |
| `xdm.commerce.productListRemovals.value`  | String | xdm.commerce.productListRemovals.value |
| `xdm.commerce.productListViews.id`  | String | xdm.commerce.productListViews.id |
| `xdm.commerce.productListViews.value`  | String | xdm.commerce.productListViews.value |
| `xdm.commerce.productViews.id`  | String | xdm.commerce.productViews.id |
| `xdm.commerce.productViews.value`  | String | xdm.commerce.productViews.value |
| `xdm.commerce.purchases.value`  | String | xdm.commerce.purchases.value |
| `xdm.device.model`  | String | device.model |
| `xdm.device.colorDepth`  | String | device.colorDepth |
| `xdm.device.screenHeight`  | String | device.screenHeight |
| `xdm.device.screenWidth`  | String | device.screenWidth |
| `xdm.device.type`  | String | device.type |
| `xdm.environment.browserDetails.acceptLanguage`  | String | environment.browserDetails.acceptLanguage |
| `xdm.environment.browserDetails.cookiesEnabled`  | String | environment.browserDetails.cookiesEnabled |
| `xdm.environment.browserDetails.javaEnabled`  | String | environment.browserDetails.javaEnabled |
| `xdm.environment.browserDetails.userAgent`  | String | environment.browserDetails.userAgent |
| `xdm.environment.browserDetails.viewportHeight`  | String | environment.browserDetails.viewportHeight |
| `xdm.environment.browserDetails.viewportWidth`  | String | environment.browserDetails.viewportWidth |
| `xdm.environment.carrier`  | String | environment.carrier |
| `xdm.environment.connectionType`  | String | environment.connectionType |
| `xdm.environment.ipV4`  | String | environment.ipV4 |
| `xdm.environment.language`  | String | environment.language |
| `xdm.environment.operatingSystem`  | String | environment.operatingSystem |
| `xdm.environment.operatingSystemVersion`  | String | environment.operatingSystemVersion |
| `xdm.xdm.identityMap.ECID`  | Array | identityMap.ECID |
| `xdm.marketing.trackingCode`  | String | marketing.trackingCode |
| `xdm.media.mediaTimed.completes.value`  | String | media.mediaTimed.completes.value |
| `xdm.media.mediaTimed.dropBeforeStart.value`  | String | media.mediaTimed.dropBeforeStart.value |
| `xdm.media.mediaTimed.federated.value`  | String | media.mediaTimed.federated.value |
| `xdm.media.mediaTimed.firstQuartiles.value`  | String | media.mediaTimed.firstQuartiles.value |
| `xdm.media.mediaTimed.mediaSegmentView.value`  | String | media.mediaTimed.mediaSegmentView.value |
| `xdm.media.mediaTimed.midpoints.value`  | String | media.mediaTimed.midpoints.value |
| `xdm.media.mediaTimed.pauseTime.value`  | String | media.mediaTimed.pauseTime.value |
| `xdm.media.mediaTimed.pauses.value`  | String | media.mediaTimed.pauses.value |
| `xdm.media.mediaTimed.primaryAssetReference.@id`  | String | media.mediaTimed.primaryAssetReference.@id |
| `xdm.media.mediaTimed.primaryAssetReference.dc:title`  | String | media.mediaTimed.primaryAssetReference.dc:title |
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name` | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator\[N\].iptc4xmpExt:Name|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number`  | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number |
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue` | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating| N.iptc4xmpExt:RatingValue|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number`  | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name`  | String | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name|
|  `xdm.media.mediaTimed.primaryAssetReference.showType`  | String | media.mediaTimed.primaryAssetReference.showType|
|  `xdm.media.mediaTimed.primaryAssetReference.xmpDM:duration` | String | media.mediaTimed.primaryAssetReference.xmpDM:duration|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.@id`  | String | media.mediaTimed.primaryAssetViewDetails.@id
|  `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastChannel`  | String | media.mediaTimed.primaryAssetViewDetails.broadcastChannel|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastContentType`  | String | media.mediaTimed.primaryAssetViewDetails.broadcastContentType|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastNetwork`  | String | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork|
| `xdm.media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value`  | String | media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value |
|  `xdm.media.mediaTimed.primaryAssetViewDetails.playerName`  | String | media.mediaTimed.primaryAssetViewDetails.playerName|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version`  | String | media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.sourceFeed`  | String | media.mediaTimed.primaryAssetViewDetails.sourceFeed|
| `xdm.media.mediaTimed.primaryAssetViewDetails.streamFormat`  | String |  media.mediaTimed.primaryAssetViewDetails.streamFormat|
|  `xdm.media.mediaTimedxdm..progress10.value`  | String | media.mediaTimed.progress10.value|
|  `xdm.media.mediaTimed.progress95.value`  | String | media.mediaTimed.progress95.value|
|  `xdm.media.mediaTimed.resumes.value`  | String | media.mediaTimed.resumes.value|
|  `xdm.media.mediaTimed.starts.value`  | String | media.mediaTimed.starts.value|
|  `xdm.media.mediaTimed.thirdQuartiles.value`  | String | media.mediaTimed.thirdQuartiles.value|
|  `xdm.media.mediaTimed.timePlayed.value`  | String | media.mediaTimed.timePlayed.value|
|  `xdm.media.mediaTimed.totalTimePlayed.value`  | String | media.mediaTimed.totalTimePlayed.value|
|  `xdm.placeContext.geo.latitude`  | String |placeContext.geo.latitude|
| `xdm.placeContext.geo.longitude`  | String | placeContext.geo.longitude|
|  `xdm.placeContext.geo.postalCode`  | String | placeContext.geo.postalCode|
|  `xdm.placeContext.geo.stateProvince`  | String | placeContext.geo.stateProvince|
|  `xdm.placeContext.localTime`  | String | placeContext.localTime|
| `xdm.productListItems.lineItemId`  | Array | productListItems.lineItemId |
|  `xdm.productListItems.name`  | Array | productListItems.name|
|  `xdm.productListItems.priceTotal`  | Array | productListItems.priceTotal|
| `xdm.productListItems.quantity`  | Array | productListItems.quantity |
| `xdm.productListItems.SKU`  | Array | productListItems.SKU |
|  `xdm._experience.analytics.customDimensions.hierarchies.hier1` | String |  _experience.analytics.customDimensions.hierarchies.hier1|
|   `xdm._experience.analytics.customDimensions.hierarchies.hier2` | String | _experience.analytics.customDimensions.hierarchies.hier2|
|   `xdm._experience.analytics.customDimensions.hierarchies.hier3`  | String | _experience.analytics.customDimensions.hierarchies.hier3|
|   `xdm._experience.analytics.customDimensions.hierarchies.hier4` | String | _experience.analytics.customDimensions.hierarchies.hier4|
|  `xdm._experience.analytics.customDimensions.hierarchies.hier5` | String |_experience.analytics.customDimensions.hierarchies.hier5|
|   `xdm._experience.analytics.customDimensions.listProps.prop1.delimiter` | String | _experience.analytics.customDimensions.listProps.prop1.delimiter|
|   `xdm._experience.analytics.customDimensions.listProps.prop1.values` | Array | _experience.analytics.customDimensions.listProps.prop1.values|
|   `xdm._experience.analytics.customDimensions.lists.list1.list` | Array | _experience.analytics.customDimensions.lists.list1.list|
|   `xdm._experience.analytics.customDimensions.lists.list2.list` | Array | _experience.analytics.customDimensions.lists.list2.list|
|  `xdm._experience.analytics.customDimensions.lists.list3.list` | Array | _experience.analytics.customDimensions.lists.list3.list  |
|  `xdm._experience.analytics.event1to100.event1.id` | String |  _experience.analytics.event1to100.event1.id|
|  `xdm._experience.analytics.event1to100.event1.value` | String | _experience.analytics.event1to100.event1.value |

### Target Data (non-XDM, data object)

| Variable | Type | Description |
|:---------| --- | :------------|
| `data.__adobe.target.entity.id`  | String | entity.id |
| `data.__adobe.target.entity.name`  | String | entity.name |
| `data.__adobe.target.entity.categoryId`  | String | entity.categoryId |
| `data.__adobe.target.entity.pageUrl`  | String | entity.pageUrl |
| `data.__adobe.target.entity.thumbnailUrl`  | String | entity.thumbnailUrl |
| `data.__adobe.target.entity.message`  | String | entity.message |
| `data.__adobe.target.entity.value`  | String | entity.value |
| `data.__adobe.target.entity.inventory`  | String | entity.inventory |
| `data.__adobe.target.entity.brand`  | String | entity.brand |
| `data.__adobe.target.entity.margin`  | String | entity.margin |
| `data.__adobe.target.entity.event.detailsOnly`  | String | entity.event.detailsOnly |
| `data.__adobe.target.entity.yourCustomAttributeName`  | String | entity.yourCustomAttributeName |
| `data.__adobe.target.excludedIds`  | String | entity.excludedIds |
| `data.__adobe.target.cartIds`  | String | entity.cartIds  |
| `data.__adobe.target.productPurchasedId`  | String | entity.productPurchasedId |
| `data.__adobe.target.user.categoryId`  | String | entity.user.categoryId |
| `data.__adobe.target.profile.age`  | String | entity.profile.age |
| `data.__adobe.target.profile.gender`  | String | entity.profile.gender |

### Analytics eVars

This connector supports direct mapping for `eVar1`-`eVar250`. For example, mapping destinations will expand to `_experience.analytics.customDimensions.eVars.eVar1-250`.

### Analytics Props

This connector supports direct mapping for `prop1`-`prop75`. For example, mapping destinations will expand to `_experience.analytics.customDimensions.props.prop1-75`

### XDM (Legacy)

| Variable | Type| Description |
|:---------| --- |:------------|
| `account_name`  | String |Account Name | 
|  `pageName`  | String |Page Name |
|  `clientID`  | String | Client ID |


### Adobe Audience Manager Config (Legacy)

| Variable | Type | Description |
|:---------| ---| :------------|
| `cookieDestinationsEnabled`  | Boolean | Cookie Destinations Enabled |
|  `urlDestinationsEnabled`  | Boolean | URL Destinations Enabled|