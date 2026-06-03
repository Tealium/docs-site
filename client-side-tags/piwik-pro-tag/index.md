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

First, go to Tealium&#39;s tag marketplace and add the Piwik PRO tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **App ID**
  * PPAS application identifier (previously website ID, site ID or idSite).

* **Base URL**
  * PPAS instance URL without trailing slash.
  * Include `//` at the beginning.
  * Example: `//example.com`

* **Enable Download &amp; Outlink tracking**

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

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

#### Standard

| Variable                             | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| `appId`                              | &lt;ul&gt;&lt;li&gt;App ID.&lt;/li&gt;&lt;/ul&gt;                                    |
| `base_url`                           | &lt;ul&gt;&lt;li&gt;PPAS Instance Address.&lt;/li&gt;&lt;/ul&gt;                     |
| `tracking_url`                       | &lt;ul&gt;&lt;li&gt;Analytics Tracker URL.&lt;/li&gt;&lt;/ul&gt;                     |
| `category`                           | &lt;ul&gt;&lt;li&gt;Event Category.&lt;/li&gt;&lt;/ul&gt;                            |
| `action`                             | &lt;ul&gt;&lt;li&gt;Event Action.&lt;/li&gt;&lt;/ul&gt;                              |
| `name`                               | &lt;ul&gt;&lt;li&gt;Event Name.&lt;/li&gt;&lt;/ul&gt;                                |
| `value`                              | &lt;ul&gt;&lt;li&gt;Event Value.&lt;/li&gt;&lt;/ul&gt;                               |
| `goal_name`                          | &lt;ul&gt;&lt;li&gt;Goal Name.&lt;/li&gt;&lt;/ul&gt;                                 |
| `goal_value`                         | &lt;ul&gt;&lt;li&gt;Goal Value.&lt;/li&gt;&lt;/ul&gt;                                |
| `title`                              | &lt;ul&gt;&lt;li&gt;Custom Page Name/Document Title.&lt;/li&gt;&lt;/ul&gt;           |
| `beat`                               | &lt;ul&gt;&lt;li&gt;Time Between Heartbeat Requests.&lt;/li&gt;&lt;/ul&gt;           |
| `keyword`                            | &lt;ul&gt;&lt;li&gt;Keyword&lt;/li&gt;&lt;/ul&gt;                                    |
| `searchCount`                        | &lt;ul&gt;&lt;li&gt;Search Count&lt;/li&gt;&lt;/ul&gt;                               |
| `isAnonymous`                        | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Enable Anonymous Tracking.&lt;/li&gt;&lt;/ul&gt; |
| `CustomUrl`                          | &lt;ul&gt;&lt;li&gt;Custom URL&lt;/li&gt;&lt;/ul&gt;                                 |
| `ReferrerUrl`                        | &lt;ul&gt;&lt;li&gt;Referrer URL.&lt;/li&gt;&lt;/ul&gt;                              |
| `cookieDomain`                       | &lt;ul&gt;&lt;li&gt;Cookie Domain.&lt;/li&gt;&lt;/ul&gt;                             |
| `cookiePath`                         | &lt;ul&gt;&lt;li&gt;Cookie Path.&lt;/li&gt;&lt;/ul&gt;                               |
| `updateTimingDataOnPageLoadSampling` | &lt;ul&gt;&lt;li&gt;Update Timing Data On Page Load Sampling.&lt;/li&gt;&lt;/ul&gt;  |
| `enableHeartBeatTimer`               | &lt;ul&gt;&lt;li&gt;Enable Heart Beat Timer.&lt;/li&gt;&lt;/ul&gt;                   |
| `sendPageView`  | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Send Page View&lt;/li&gt;&lt;/ul&gt;  |


#### Content Tracking

|Variable| Description|
|---| ---|
|`trackAllContentImpressions`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Track All Content Impressions.&lt;/li&gt;&lt;/ul&gt; |
|`checkOnScroll`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Impression Check On Scroll.&lt;/li&gt;&lt;/ul&gt; |
| `watchInterval` |  &lt;ul&gt;&lt;li&gt;Impression WatchInterval.&lt;/li&gt;&lt;/ul&gt; |
| `impressionDomNode` |  &lt;ul&gt;&lt;li&gt;Impression Dom Node.&lt;/li&gt;&lt;/ul&gt; |
|`domNode`|  &lt;ul&gt;&lt;li&gt;Interaction Dom Node.&lt;/li&gt;&lt;/ul&gt; |
| `contentInteraction` |  &lt;ul&gt;&lt;li&gt;Content Interaction Name.&lt;/li&gt;&lt;/ul&gt; |
|`contentName`|  &lt;ul&gt;&lt;li&gt;Content Name.&lt;/li&gt;&lt;/ul&gt; |
|`contentPiece`|  &lt;ul&gt;&lt;li&gt;Content Piece.&lt;/li&gt;&lt;/ul&gt; |
|`contentTarget`|  &lt;ul&gt;&lt;li&gt;Content Target.&lt;/li&gt;&lt;/ul&gt; |

#### Download and Outlink Tracking

|Variable| Description|
|---| ---|
|`link_tracking`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Enable Link Tracking.&lt;/li&gt;&lt;/ul&gt; |
|`domains`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Ignore Alias Domains.&lt;/li&gt;&lt;/ul&gt; |
|`outLinkClassName`|  &lt;ul&gt;&lt;li&gt;Outlink Class Name.&lt;/li&gt;&lt;/ul&gt; |
|`linkAddress`|  &lt;ul&gt;&lt;li&gt;Link Address.&lt;/li&gt;&lt;/ul&gt; |
|`addDownloadExtensions`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Add Download Extensions.&lt;/li&gt;&lt;/ul&gt; |
|`setDownloadExtensions`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Replace Default Extensions.&lt;/li&gt;&lt;/ul&gt; |
|`setDownloadClassName`|  &lt;ul&gt;&lt;li&gt;Set Download ClassName.&lt;/li&gt;&lt;/ul&gt; |
|`time`|  &lt;ul&gt;&lt;li&gt;Link Tracking Delay.&lt;/li&gt;&lt;/ul&gt; |
|`setIgnoreClasses`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Disable Outlink Tracking Classes.&lt;/li&gt;&lt;/ul&gt; |

#### Events

|Variable| Description|
|---| ---|
|`trackEvent`|  &lt;ul&gt;&lt;li&gt;Trigger Custom Event.&lt;/li&gt;&lt;/ul&gt; |
|`trackGoal`|  &lt;ul&gt;&lt;li&gt;Track Goal Conversion.&lt;/li&gt;&lt;/ul&gt; |
|`addEcommerceItem`|  &lt;ul&gt;&lt;li&gt;Add Ecommerce Item.&lt;/li&gt;&lt;/ul&gt; |
|`trackEcommerceOrder`|  &lt;ul&gt;&lt;li&gt;Track Ecommerce Order.&lt;/li&gt;&lt;/ul&gt; |
|`trackEcommerceCartUpdate`|  &lt;ul&gt;&lt;li&gt;Update Cart.&lt;/li&gt;&lt;/ul&gt; |
|`setEcommerceView`|  &lt;ul&gt;&lt;li&gt;Track Product / Category View.&lt;/li&gt;&lt;/ul&gt; |
|`trackAllContentImpressions`|  &lt;ul&gt;&lt;li&gt;Tracking all content impressions within a page.&lt;/li&gt;&lt;/ul&gt; |
|`trackVisibleContentImpressions`|  &lt;ul&gt;&lt;li&gt;Tracking all visible content impressions.&lt;/li&gt;&lt;/ul&gt; |
|`trackContentImpressionsWithinNode`|  &lt;ul&gt;&lt;li&gt;Tracking only content impressions for specific page part.&lt;/li&gt;&lt;/ul&gt; |
|`trackContentInteractionNode`|  &lt;ul&gt;&lt;li&gt;Track interactions manually with auto detection.&lt;/li&gt;&lt;/ul&gt; |
|`trackContentImpression`|  &lt;ul&gt;&lt;li&gt;Track impression manually.&lt;/li&gt;&lt;/ul&gt; |
|`trackContentInteraction`|  &lt;ul&gt;&lt;li&gt;Track user interaction manually.&lt;/li&gt;&lt;/ul&gt; |
|`trackLink`|  &lt;ul&gt;&lt;li&gt;Force Tracking download using JS function.&lt;/li&gt;&lt;/ul&gt; |
|`setUserId`|  &lt;ul&gt;&lt;li&gt;Set UserId.&lt;/li&gt;&lt;/ul&gt; |
|`resetUserId`|  &lt;ul&gt;&lt;li&gt;Reset UserId.&lt;/li&gt;&lt;/ul&gt; |
|`setDocumentTitle`|  &lt;ul&gt;&lt;li&gt;Set Custom Page Name.&lt;/li&gt;&lt;/ul&gt; |
|`trackSiteSearch`|  &lt;ul&gt;&lt;li&gt;Tracking Site Search.&lt;/li&gt;&lt;/ul&gt; |
|`setUserIsAnonymous`|  &lt;ul&gt;&lt;li&gt;Track User Anonymously.&lt;/li&gt;&lt;/ul&gt; |
|`deanonymizeUser`|  &lt;ul&gt;&lt;li&gt;Disable tracking user anonymously (after visitor consent).&lt;/li&gt;&lt;/ul&gt; |

#### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;Order Total&lt;/li&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub Total&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Shipping Amount&lt;/li&gt;&lt;li&gt;Overrides `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax Amount&lt;/li&gt;&lt;li&gt;Overrides `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid` .&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names.&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Categories&lt;/li&gt;&lt;li&gt;Overrides `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Discounts.&lt;/li&gt;&lt;li&gt;Overrides `_cpdisc`.&lt;/li&gt;&lt;/ul&gt; |
