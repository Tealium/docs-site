---
title: Adobe Target Tag Setup Guide
description: This article describes how to set up the Adobe Target tag.
url: https://docs.tealium.com/client-side-tags/adobe-target/
---
Adobe Target gives marketers the necessary capabilities to continually make their online content and offers more relevant to their customers, yielding greater conversion.

## Tag tips

* This template requires utag version v4.26 or above. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* If you want to use the Adobe Experience Cloud ID Service,  add the Adobe Experience Cloud ID Service tag **BEFORE** this tag.
* Scope your [Adobe Target Extension]() to this tag.
* The **Timeout** setting is a failsafe in case the Target server may not be responding.  For best performance, do not set this value to less than 5000 ms.
* Unbundling is not supported in this tag. If you set **Bundle Flag** to `No`, the value is overwritten as `Yes`.
* Response objects received from `getOffers` are placed into the `u.offersReceived` array.

### getOffers response objects example

The contents of the response from `getOffers` resembles the following:

```
{
  &#34;prefetch&#34;: {
    &#34;mboxes&#34;: [{
      &#34;index&#34;: 0,
      &#34;name&#34;: &#34;a1-serverside-xt&#34;,
      &#34;options&#34;: [{
        &#34;content&#34;: &#34;&lt;img src=\&#34;http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&amp;fit=constrain&amp;hei=491&amp;wid=980&amp;fmt=png-alpha\&#34;/&gt;&#34;,
        &#34;type&#34;: &#34;html&#34;,
        &#34;eventToken&#34;: &#34;n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==&#34;,
        &#34;responseTokens&#34;: {
          &#34;profile.memberlevel&#34;: &#34;0&#34;,
          &#34;geo.city&#34;: &#34;anytown&#34;,
          &#34;activity.id&#34;: &#34;167169&#34;,
          &#34;experience.name&#34;: &#34;USA Experience&#34;,
          &#34;geo.country&#34;: &#34;countryname&#34;
        }
      }],
      &#34;analytics&#34;: {
        &#34;payload&#34;: {
          &#34;pe&#34;: &#34;tnt&#34;,
          &#34;tnta&#34;: &#34;167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100&#34;
        }
      }
    }]
  }
}
```

This response is placed in the `u.offersResponse` array. Then, the `u.applyOffers()` function is called to parse the `u.offersResponse` array, which calls Adobe Target&#39;s `aaplyOffers()` method to pass in each offer parsed.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Code Version**: The version of Adobe Target to use. To learn more, see [Adobe Target version details](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/target-atjs-versions.html).
* **Client Code**: The client name (for example, `mycompany` in the `mycompany.tt.omtrdc.net`)
* **Timeout**: Set this value to `5000` or greater.  This is time (in milliseconds) to wait for a response from Target before assuming the Target server is not responding.
* **Adobe Org ID**: Used with the visitor tracking across Adobe Target and Site Catalyst. Found in the `mbox.js` `var imsOrgId = &#39;XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg&#39;`
* **Library Endpoint Path**: The path variable in the library call (generally does not need changing).
* **Authoring Script URL**: If you are authoring targeted content, enter the authoring script URL (for example: `//cdn.tt.omtrdc.net/cdn/target-vec.j`).
* **Auto Create Global mbox**: Whether to automatically create the globally-hidden mbox. Only set this to `false` if you implement the mbox elsewhere.
* **Global mbox Name**: Adobe typically uses `target-global-mbox` for the name of the globally hidden mbox.  This tag automatically calls mboxCreate to create this mbox.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `config.clientCode` | | Client code.  |
|  `config.imsOrgId` | |  Adobe organization ID.  |
|  `config.serverDomain` | | Server domain. The domain where Adobe Target requests are sent.  |
|  `config.crossDomain` | | Enable cross domain.  |
|  `config.timeout` | | Target timeout.  |
|  `config.globalMboxName` | | Global Mbox name.  |
|  `config.globalMboxAutoCreate` | Boolean | Enable global Mbox creation.  |
| `config.endpoint` | | Library endpoint path.  | 
| `config.defaultContentHiddenStyle` | | Default content hidden style.  | 
| `config.defaultContentVisibleStyle` | | Default content visible style.  | 
| `config.bodyHiddenStyle` | | Body hidden style. A style to use when hiding the BODY element. The default value is `body{opacity:0}`. | 
|  `config.bodyHidingEnabled` | Boolean | Enbale body hidding. When you enable this setting, the BODY element is hidden to prevent window flickering. |
| `config.deviceIdLifetime` | Number | Device ID lifetime.  | 
| `config.sessionIdLifetime` | Number | Session ID lifetime.  | 
| `config.selectorsPollingTimeout` | Number | Selectors polling timeout.  | 
|  `config.visitorApiTimeout` | Number | Visitor API timeout.  |
|  `config.overrideMboxEdgeServer` | | Enable Mbox Edge Server override.  |
|  `config.overrideMboxEdgeServerTimeout` | Number | Override Mbox Edge Server timeout.  |
|  `config.optoutEnabled` | Boolean | Enable opt-out.  |
| `config.optinEnabled` | Boolean | Enable opt-in.  | 
| `config.secureOnly` | Boolean | Secure requests only.  | 
| `config.pageLoadEnabled` | Boolean | Enable page load.  | 
|  `config.viewsEnabled` | Boolean | Enable views.  |
| `config.authoringScriptUrl` | | Authoring script URL  | 
|`config.decisioningMethod` | | Decisioning method.  |
| `config.aepSandboxId` | String | Aep sandbox ID. |
| `config.aepSandboxName` | String | Aep sandbox name. |

### Track Events

| Variable | Type | Description |
|:---------|:------------|:------------|
| `evt.mbox` |String | Mbox name.  | 
|  `sevt.elector` |String |CSS selectors.  |
|  `evt.type` |String |HTML event type.  |
| `evt.preventDefault` |Boolean |Use prevent default.  | 
| `evt.params` | Object | Mbox parameters.   |
| `evt.params.###` | String | Mbox parameters item.  | 
| `evt.timeout` | Integer | Timeout.   | 
|  `evt.success` | Function | Success function.  |
|  `evt.error` | Function | Error function.  |

### Parameters

| Variable | Description |
|:---------|:------------|
| `mboxParams.###` |mboxParams.###  | 
| `targetPageParamsAll.###` |targetPageParamsAll.###  | 
|  `targetPageParams.###` |targetPageParams.###  |
| `targetPageParams.at_property` |targetPageParams.at_property  | 

### Multiple Offers and SPA

| Variable | Description |
|:---------|:------------|
|  `request_type`  | [prefetch or execute] Get Offers Request Type|
| `offers.fetchViews` |Fetch All Views  | 
|  `offers.consumerId` |Consumer ID  |
|  `offers.timeout` |Request Timeout  |
| `offers.id.tntId` |Request ID - tntId  | 
|  `offers.id.thirdPartyId` |Request ID - thirdPartyId  |
|  `offers.id.marketingCloudVisitorId` |Request ID - marketingCloudVisitorId  |
|  `offers.experienceCloud.analytics.logging` |Adobe Analytics Integration - Logging Type  |
|  `offers.views`  | Views Array - Array |
|  `offers.pageLoad`  | PageLoad Object - Object |
|  `offers.mboxes`  | Mboxes Array |
|  `offers.decisioningMethod` |Decisioning Method  |
|  `selector`  | CSS Selectors - Array |
| `offersResponse` |Response Object  |
| `viewName` |View Name  | 
|  `countPage`  | Increase Impression Count - Boolean |