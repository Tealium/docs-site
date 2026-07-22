---
title: Piwik PRO Tag Setup Guide
description: This article describes how to set up the Piwik PRO tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/piwik-pro-tag/
---
## Tag tips

* The Track E-commerce Order Event fires when an Order ID is present.
* Use mapping to:
  * Dynamically override the standard configuration values
  * Setup event triggers
  * Set Custom Dimensions
  * Override the E-Commerce extension values
* Supports these E-Commerce extension parameters:
  * Order ID (`_corder` )
  * Order Total (`_ctotal` )
  * Sub Total (`_csubtotal` )
  * Shipping Amount (`_cship` )
  * Tax Amount (`_ctax` )
  * Cart or Order Type (`_ctype` )
  * Customer ID (`_ccustid` )
  * List of Product IDs (`_cprod` )
  * List of Names (`_cprodname` )
  * List of Categories (`_ccat` )
  * List of Quantities (`_cquan` )
  * List of Prices (`_cprice` )
  * List of Discounts (`_cpdisc` )

## Tag configuration

First, go to Tealium's tag marketplace and add the Piwik PRO tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **App ID**
  * PPAS application identifier (previously website ID, site ID or idSite).

* **Base URL**
  * PPAS instance URL without trailing slash.
  * Include `//` at the beginning.
  * Example: `//example.com`

* **Enable Download & Outlink tracking**

* **Tracking all content impressions within a page**  
To track content, it has to have the data-track-content attribute or `piwikTrackContent` CSS class attached to it.

* **Track All Visible Content Impressions**  
To track content, it has to have the data-track-content attribute or `piwikTrackContent` CSS class attached to it.

* **Check Impressions On Scroll**
  * Check new visible content impressions on the scroll event.
  * It will not detect content blocks placed in a scrollable element.

* **Visible Content Watch Interval**
  * Interval, in milliseconds, between checking for new visible content.
  * Periodic checks can be disabled for performance reasons by setting `0`.

* **Heartbeat Timer**
  * Time, in seconds, between cyclical heartbeat requests.

* **Track User Anonymously**
  * Track visitor anonymously (without consent).
  
* **Enable Heart Beat Timer**

* **Send Page View**
  * Page View events are automatically recorded your site. If you don’t want the snippet to send a Page View event, set the this option to `false`.

### Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

#### Standard

| Variable                             | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| `appId`                              | <ul><li>App ID.</li></ul>                                    |
| `base_url`                           | <ul><li>PPAS Instance Address.</li></ul>                     |
| `tracking_url`                       | <ul><li>Analytics Tracker URL.</li></ul>                     |
| `category`                           | <ul><li>Event Category.</li></ul>                            |
| `action`                             | <ul><li>Event Action.</li></ul>                              |
| `name`                               | <ul><li>Event Name.</li></ul>                                |
| `value`                              | <ul><li>Event Value.</li></ul>                               |
| `goal_name`                          | <ul><li>Goal Name.</li></ul>                                 |
| `goal_value`                         | <ul><li>Goal Value.</li></ul>                                |
| `title`                              | <ul><li>Custom Page Name/Document Title.</li></ul>           |
| `beat`                               | <ul><li>Time Between Heartbeat Requests.</li></ul>           |
| `keyword`                            | <ul><li>Keyword</li></ul>                                    |
| `searchCount`                        | <ul><li>Search Count</li></ul>                               |
| `isAnonymous`                        | <ul><li>Boolean</li><li>Enable Anonymous Tracking.</li></ul> |
| `CustomUrl`                          | <ul><li>Custom URL</li></ul>                                 |
| `ReferrerUrl`                        | <ul><li>Referrer URL.</li></ul>                              |
| `cookieDomain`                       | <ul><li>Cookie Domain.</li></ul>                             |
| `cookiePath`                         | <ul><li>Cookie Path.</li></ul>                               |
| `updateTimingDataOnPageLoadSampling` | <ul><li>Update Timing Data On Page Load Sampling.</li></ul>  |
| `enableHeartBeatTimer`               | <ul><li>Enable Heart Beat Timer.</li></ul>                   |
| `sendPageView`  | <ul><li>Boolean</li><li>Send Page View</li></ul>  |


#### Content Tracking

|Variable| Description|
|---| ---|
|`trackAllContentImpressions`|  <ul><li>Boolean</li><li>Track All Content Impressions.</li></ul> |
|`checkOnScroll`|  <ul><li>Boolean</li><li>Impression Check On Scroll.</li></ul> |
| `watchInterval` |  <ul><li>Impression WatchInterval.</li></ul> |
| `impressionDomNode` |  <ul><li>Impression Dom Node.</li></ul> |
|`domNode`|  <ul><li>Interaction Dom Node.</li></ul> |
| `contentInteraction` |  <ul><li>Content Interaction Name.</li></ul> |
|`contentName`|  <ul><li>Content Name.</li></ul> |
|`contentPiece`|  <ul><li>Content Piece.</li></ul> |
|`contentTarget`|  <ul><li>Content Target.</li></ul> |

#### Download and Outlink Tracking

|Variable| Description|
|---| ---|
|`link_tracking`|  <ul><li>Boolean</li><li>Enable Link Tracking.</li></ul> |
|`domains`|  <ul><li>Array</li><li>Ignore Alias Domains.</li></ul> |
|`outLinkClassName`|  <ul><li>Outlink Class Name.</li></ul> |
|`linkAddress`|  <ul><li>Link Address.</li></ul> |
|`addDownloadExtensions`|  <ul><li>Array</li><li>Add Download Extensions.</li></ul> |
|`setDownloadExtensions`|  <ul><li>Array</li><li>Replace Default Extensions.</li></ul> |
|`setDownloadClassName`|  <ul><li>Set Download ClassName.</li></ul> |
|`time`|  <ul><li>Link Tracking Delay.</li></ul> |
|`setIgnoreClasses`|  <ul><li>Array</li><li>Disable Outlink Tracking Classes.</li></ul> |

#### Events

|Variable| Description|
|---| ---|
|`trackEvent`|  <ul><li>Trigger Custom Event.</li></ul> |
|`trackGoal`|  <ul><li>Track Goal Conversion.</li></ul> |
|`addEcommerceItem`|  <ul><li>Add Ecommerce Item.</li></ul> |
|`trackEcommerceOrder`|  <ul><li>Track Ecommerce Order.</li></ul> |
|`trackEcommerceCartUpdate`|  <ul><li>Update Cart.</li></ul> |
|`setEcommerceView`|  <ul><li>Track Product / Category View.</li></ul> |
|`trackAllContentImpressions`|  <ul><li>Tracking all content impressions within a page.</li></ul> |
|`trackVisibleContentImpressions`|  <ul><li>Tracking all visible content impressions.</li></ul> |
|`trackContentImpressionsWithinNode`|  <ul><li>Tracking only content impressions for specific page part.</li></ul> |
|`trackContentInteractionNode`|  <ul><li>Track interactions manually with auto detection.</li></ul> |
|`trackContentImpression`|  <ul><li>Track impression manually.</li></ul> |
|`trackContentInteraction`|  <ul><li>Track user interaction manually.</li></ul> |
|`trackLink`|  <ul><li>Force Tracking download using JS function.</li></ul> |
|`setUserId`|  <ul><li>Set UserId.</li></ul> |
|`resetUserId`|  <ul><li>Reset UserId.</li></ul> |
|`setDocumentTitle`|  <ul><li>Set Custom Page Name.</li></ul> |
|`trackSiteSearch`|  <ul><li>Tracking Site Search.</li></ul> |
|`setUserIsAnonymous`|  <ul><li>Track User Anonymously.</li></ul> |
|`deanonymizeUser`|  <ul><li>Disable tracking user anonymously (after visitor consent).</li></ul> |

#### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID</li><li>Overrides `_corder`.</li></ul> |
|`order_total`|  <ul><li>Order Total</li><li>Overrides `_ctotal`.</li></ul> |
|`order_subtotal`|  <ul><li>Sub Total</li><li>Overrides `_csubtotal`.</li></ul> |
|`order_shipping`|  <ul><li>Shipping Amount</li><li>Overrides `_cship`.</li></ul> |
|`order_tax`|  <ul><li>Tax Amount</li><li>Overrides `_ctax`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID</li><li>Overrides `_ccustid` .</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs.</li><li>Overrides `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Names.</li><li>Overrides `_cprodname`.</li></ul> |
|`product_category`|  <ul><li>Array</li><li>List of Categories</li><li>Overrides `_ccat`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices.</li><li>Overrides `_cprice`.</li></ul> |
|`product_discount`|  <ul><li>Array</li><li>List of Discounts.</li><li>Overrides `_cpdisc`.</li></ul> |
