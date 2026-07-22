---
title: AT Internet SmartTag Setup Guide
description: This article describes how to set up the AT Internet SmartTag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/at-internet-smarttag/
---
## Tag Tips

* The `type` parameter must be populated to trigger Click event tracking.
* Current hosted version is 5.18.2
* As of version 5.13.0, the **Log**, **LogSSL**, and **Collection Domain** fields have been deprecated and replaced by the `collectDomain` and `collectDomainSSL` fields.
* For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#) documentation.
* Set a window-level variable name to be used for direct calls to AT Internet.
* Use mapping to dynamically override the standard configuration values.
* All options accept mapping of custom properties.
* Uses some of the E-Commerce variables (see mappings for details).

## Tag Configuration

First, go to Tealium's tag marketplace and add the AT Internet SmartTag tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Tag Version**
  * **Hosted** is the AT Internet tag directly embedded in Tealium.

* **AT Internet CDN**
  * You must configure your SmartTag and deploy it on AT Internet CDN. For more information, log into your AT Internet account and view the [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.

* **Window Tracker Name**
  * Sets a window-level variable so tracker can be used outside of the tag template.

* **Site ID**
  * AT Internet Site ID.
  * For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.

* **collectDomain**
  * AT Internet data collection domain.

* **collectDomainSSL**
  * AT Internet secured data collection domain.

* **Log**
  * Deprecated as of version 5.13.0.
  * AT Internet Log for this site ID.
  * For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) Subdomain for collector documentation.

* **LogSSL**
  * Deprecated as of version 5.13.0.
  * AT Internet Secure Log for this site ID.
  * For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.
  * Refer to Tag Composer Subdomain for collector for secured pages .

* **Collection Domain**
  * Deprecated as of version 5.13.0.
  * `xiti.com `or `ati-host.net`, depending on your AT Internet configuration.
  * You can use mappings to specify a custom collection domain.

* **Pixel Path**
  * AT Internet pixel request URL path.
  * Defaults to `/hit.xiti`.

* **Cookie Domain**
  * URL of your site.
  * Incorrect configuration may cause issues in the Unique Visitor calculation.

* **Secure**
  * Enables the sending of information in a secure manner.

* **Cookie Secure**
  * If set to `true`, enables you to add the option `secure` for the writing of tracker cookies (first).
  * Be aware that secure cookies only work on HTTPS pages.

* **First extension is settings**
  * Only enable if instructed to do so by an AT Internet or a Tealium representative.
  * Will take the first extension from the list of scoped extensions and run it BEFORE the other extensions and then use the configuration from the first extension to build the tracker.

* **Send Hit When OptOut**
  * Allows sending anonymous hits when the user is in "OPT-OUT" mode (first party).

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`window_var`|  <ul><li>Window Tracker Name</li><li>Sets a window-level variable so tracker can be used outside of the tag template.</li></ul> |
|`config.site`|  <ul><li>AT Internet Site ID.</li><li>For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.</li></ul> |
|`config.collectDomain`|  <ul><li>AT Internet data collection domain.</li></ul> |
|`config.collectDomainSSL`|  <ul><li>AT Internet secured data collection domain.</li></ul> |
|`config.log`|  <ul><li>Log deprecated as of version 5.13.0</li></ul> |
|`config.logSSL`|  <ul><li>Deprecated as of version 5.13.0.</li><li>AT Internet Secure Log for this site ID.</li><li>For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.</li><li>Refer to Tag Composer Subdomain for collector for secured pages</li></ul> |
|`config.domain`|  <ul><li>Deprecated as of version 5.13.0.</li><li>Collection Domain.</li><li>`xiti.com` or `ati-host.net`, depending on your AT Internet configuration.</li><li>You can use mappings to specify a custom collection domain.</li></ul> |
|`config.pixelPath`|  <ul><li>AT Internet pixel request URL path.</li><li>Defaults to `/hit.xiti`.</li></ul> |
|`config.secure`|  <ul><li>Enables the sending of information in a secure manner.</li></ul> |
|`config.cookieSecure`|  <ul><li>If set to **true**, enables you to add the option `secure` for the writing of tracker cookies (first).</li><li>Be aware that secure cookies only work on HTTPS pages.</li></ul> |
|`config.disableCookie`|  <ul><li>Disable Cookie.</li></ul> |
|`config.cookieDomain`|  <ul><li>Cookie Domain.</li><li>URL of your site.</li><li>Incorrect configuration may cause issues in the Unique Visitor calculation.</li></ul> |
|`config.preview`|  <ul><li>Preview.</li></ul> |
|`config.sendHitWhenOptOut`|  <ul><li>Allows sending anonymous hits when the user is in "OPT-OUT" mode (first party).</li></ul> |

### Context

|Variable| Description|
|---| ---|
|`context.forcedCampaign`| Forced Campaign.|
|`context.forcedReferer`| Forced Referer.|

### E-Commerce - Events

For additional information, see [Cart Events (Sales Insights)](https://developers.atinternet-solutions.com/javascript-en/ecommerce-javascript-en/sales-insights-javascript-en/cart-events-sales-insights-javascript-fr/?kw=cartdisplay#cart-display_2).

|Variable| Description|
|---| ---|
|`order`|  <ul><li>Order</li></ul> |
|`cart`|  <ul><li>Cart</li></ul> |
|`prod`|  <ul><li>Product View</li></ul> |
|`aisle`|  <ul><li>Aisle</li></ul> |
|`transactionconfirm`|  <ul><li>Transaction Confirmation</li></ul> |
|`cartdisplay`|  <ul><li>Cart Display</li></ul> |
|`cartupdate`|  <ul><li>Cart Update</li></ul> |
|`displayshipping`|  <ul><li>Display of Shipping Step</li></ul> |
|`displaypayment`|  <ul><li>Display of Payment Step</li></ul> |
|`cartawaitingpayment`|  <ul><li>Cart Awaiting Payment</li></ul> |
|`productdisplay`|  <ul><li>Product Display</li></ul> |
|`productpagedisplay`|  <ul><li>Product Page Display</li></ul> |
|`productaddition`| <ul><li>Product Addition</li></ul> |
|`productremoval`|  <ul><li>Product Removal</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID.</li><li>Overrides `_corder`.</li></ul> |
|`order_total`|  <ul><li>Order Total.</li><li>Overrides `_ctotal`.</li></ul> |
|`order_subtotal`|  <ul><li>Order Subtotal.</li><li>Overrides `_csubtotal`.</li></ul> |
|`order_shipping`|  <ul><li>Shipping amount.</li><li>Overrides `_cship`.</li></ul> |
|`order_tax`|  <ul><li>Tax amount.</li><li>Overrides `_ctax`.</li></ul> |
|`order_coupon_code`|  <ul><li>Promo code.</li><li>Overrides `_cpromo`.</li></ul> |
|`product_id`|  <ul><li>Array.</li><li>List of Product IDs.</li><li>Overrides `_cprod`</li></ul> |
|`product_name`|  <ul><li>Array.</li><li>List of Names.</li><li>Overrides `_cprodname`.</li></ul> |
|`product_sku`|  <ul><li>Array.</li><li>List of SKUs.</li><li>Overrides `_csku`.</li></ul> |
|`product_brand`|  <ul><li>Array.</li><li>List of Brands.</li><li>Overrides `_cbrand`.</li></ul> |
|`product_category`|  <ul><li>Array.</li><li>List of Categories.</li><li>Overrides `_ccat`.</li></ul> |
|`product_subcategory`|  <ul><li>Array.</li><li>List of Sub Categories.</li><li>Overrides `_ccat2`.</li></ul> |
|`product_quantity`|  <ul><li>Array.</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array.</li><li>List of Prices.</li><li>Overrides `_cprice`.</li></ul> |
|`product_discount`|  <ul><li>Array.</li><li>List of Discounts.</li><li>Overrides `_cpdisc`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID.</li><li>Overrides `_ccustid`.</li></ul> |

### Visitor

|Variable| Description|
|---| ---|
|`visitor.id`|  <ul><li>Customer ID.</li><li>Overrides `_ccustid`.</li></ul> |
|`visitor.category`|  <ul><li>Category.</li></ul> |
|`visitor.###`|  <ul><li>Custom Property.</li></ul> |

### On-Site Ads

|Variable| Description|
|---| ---|
|`promo.adId`|  <ul><li>ID to be created.</li></ul> |
| `promo.adId` |  <ul><li>ID indicating the ad format.</li></ul> |
|`promo.productId`|  <ul><li>ID of associated product.</li></ul> |
|`promo.###`|  <ul><li>Custom Mapping.</li></ul> |

### Custom Variables

|Variable| Description|
|---| ---|
|`param.###`|  setParam Value |
|--Custom Variables--| Custom Variables.|
| `cv.site.###` | Site Custom Variable.|
|`cv.page.###`|  Page Custom Variable. |
|`cv.###.###`| Custom Variable.|

### Dynamic Labels

|Variable| Description|
|---| ---|
|`dynlabel.pageId`|  <ul><li>Dynamic Page ID</li></ul> |
|`dynlabel.update`|  <ul><li>Date of name change</li></ul> |
| `dynlabel.chapter1` |  <ul><li>Name of Chapter at level 1.</li></ul> |
|`dynlabel.chapter2`|  <ul><li>Name of Chapter at level 2.</li></ul> |
|`dynlabel.chapter3`|  <ul><li>Name of Chapter at level 3.</li></ul> |
|`dynlabel.chapter#`|  <ul><li>Name of Chapter at level #.</li></ul> |

### Internal Search

|Variable| Description|
|---| ---|
|`intsearch.keyword`|  <ul><li>Search keyword.</li></ul> |
|`intsearch.resultPageNumber`|  <ul><li>Search Result Page Number.</li></ul> |
| `intsearch.resultPosition` |  <ul><li>Search Result Position.</li></ul> |

### MV (Multivariate) Testing

|Variable| Description|
|---| ---|
| `mvtesting.set.test` |  <ul><li>Test ID and Name.</li></ul> |
|`mvtesting.set.waveId`|  <ul><li>Wave ID.</li></ul> |
|`mvtesting.set.creation`|  <ul><li>Creation ID and Name.</li></ul> |
| `mvtesting.set.###` |  <ul><li>Custom Set Mapping.</li></ul> |
|`mvtesting.add.variable`|  <ul><li>CSV/Array.</li><li>Test Variable.</li></ul> |
|`mvtesting.add.version`|  <ul><li>CSV/Array.</li><li>Test Version.</li></ul> |
| `mvtesting.add.###` |  <ul><li>Custom Add Mapping.</li></ul> |

### Rich Media

|Variable| Description|
|---| ---|
|`richmedia.add.mediaType`|  <ul><li>Media Type.</li><li>Values are:  <ul><li>`video`</li><li>`audio`</li><li>`vpost`</li></ul> </li></ul> |
|```richmedia.add.playerId```|  <ul><li>Player ID.</li></ul> |
| `richmedia.add.mediaLevel2` |  <ul><li>Media Level 2.</li></ul> |
|`richmedia.add.mediaLabel`|  <ul><li>Media Label.</li></ul> |
|`richmedia.add.isEmbedded`|  <ul><li>Is Embedded.</li><li>Values are `int` or `ext`.</li></ul> |
|`richmedia.add.broadcastMode`|  <ul><li>Broadcast Mode.</li><li>Values are `live` or `clip`.</li></ul> |
| `richmedia.add.webdomain` |  <ul><li>Web Domain of External Placement</li></ul> |
| `richmedia.add.duration` |  <ul><li>Duration.</li></ul> |
|`richmedia.send.action`|  <ul><li>Send Action.</li><li>Values are:  <ul><li>`play`</li><li>`pause`</li><li>`stop`</li><li>`info`</li><li>`move`</li></ul> </li></ul> |
|`richmedia.send.playerId`|  <ul><li>Player ID.</li></ul> |
|`richmedia.send.mediaLabel`|  <ul><li>Media Label.</li></ul> |
|`richmedia.send.isBuffering`|  <ul><li>Is Buffering.</li><li>Values are:  <ul><li>`1` - start buffering</li><li>`0` - end buffering</li></ul> </li></ul> |
|`richmedia.remove`|  <ul><li>Remove Player.</li></ul> |
|`richmedia.removeAll`|  <ul><li>Remove All Players</li><li>Values are `true` or `false`.</li></ul> |

### Mobile

|Variable| Description|
|---| ---|
|`mob.apvr`|  <ul><li>App Version.</li></ul> |
|`mob.ref`|  <ul><li>Referrer.</li></ul> |
|`mob.stc`|  <ul><li>Object.</li><li>Life Cycle.</li></ul> |
|`mob.stc.lc`|  <ul><li>Object.</li><li>Life Cycle.</li></ul> |
|`mob.stc.lc.sessionId`|  <ul><li>Session ID.</li></ul> |
|`mob.stc.lc.fl`|  <ul><li>First Launched.</li><li>Overrides `lifecycle_isfirstlaunch`.</li><li>Values are `0` or `1`.</li></ul> |
|`mob.stc.lc.flau`|  <ul><li>First Launched Since Update.</li><li>Overrides `lifecycle_isfirstlaunchupdate`.</li><li>Values are `0` or `1`.</li></ul> |
|`mob.stc.lc.lc`|  <ul><li>Number.</li><li>Number of Launches.</li><li>Overrides `lifecycle_totallaunchcount`.</li></ul> |
|`mob.stc.lc.ldc`|  <ul><li>Number.</li><li>Launches throughout the day.</li></ul> |
|`mob.stc.lc.lwc`|  <ul><li>Number.</li><li>Launches throughout the week.</li></ul> |
|`mob.stc.lc.lmc`|  <ul><li>Number.</li><li>Launches throughout the month.</li></ul> |
|`mob.stc.lc.lcsu`|  <ul><li>Number.</li><li>Launches since last update.</li></ul> |
| `mob.stc.lc.fld` |  <ul><li>Date of first launch.</li><li>Overrides `lifecycle_firstlaunchdate`.</li><li>Date format is `yyyymmdd`.</li></ul> |
|`mob.stc.lc.dsfl`|  <ul><li>Number.</li><li>Number of days since first launch.</li><li>Calculated from `lifecycle_firstlaunchdate`.</li></ul> |
|`mob.stc.lc.uld`|  <ul><li>Date of first launch since last update.</li><li>Overrides `lifecycle_updatelaunchdate`.</li><li>Date format is `yyyymmdd`.</li></ul> |
|`mob.stc.lc.dsu`|  <ul><li>Number.</li><li>Number of days since first launch since update.</li><li>Overrides `lifecycle_dayssinceupdate`.</li></ul> |
|`mob.stc.lc.dslu`|  <ul><li>Number.</li><li>Days since app was last used.</li><li>Calculated from `lifecycle_lastlaunchdate`.</li></ul> |

### Custom Tree Structure

|Variable| Description|
|---| ---|
|`customTreeStructure.category1`|  <ul><li>Category Level 1</li></ul> |
|`customTreeStructure.category2`|  <ul><li>Category Level 2</li></ul> |
|`customTreeStructure.category3`|  <ul><li>Category Level 3</li></ul> |

### Campaign

|Variable| Description|
|---| ---|
|`xtor`|  <ul><li>Campaign ID.</li></ul> |
