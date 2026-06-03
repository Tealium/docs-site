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

First, go to Tealium&#39;s tag marketplace and add the AT Internet SmartTag tag (Learn more about [how to add a tag]()).

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
  * Allows sending anonymous hits when the user is in &#34;OPT-OUT&#34; mode (first party).

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`window_var`|  &lt;ul&gt;&lt;li&gt;Window Tracker Name&lt;/li&gt;&lt;li&gt;Sets a window-level variable so tracker can be used outside of the tag template.&lt;/li&gt;&lt;/ul&gt; |
|`config.site`|  &lt;ul&gt;&lt;li&gt;AT Internet Site ID.&lt;/li&gt;&lt;li&gt;For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.&lt;/li&gt;&lt;/ul&gt; |
|`config.collectDomain`|  &lt;ul&gt;&lt;li&gt;AT Internet data collection domain.&lt;/li&gt;&lt;/ul&gt; |
|`config.collectDomainSSL`|  &lt;ul&gt;&lt;li&gt;AT Internet secured data collection domain.&lt;/li&gt;&lt;/ul&gt; |
|`config.log`|  &lt;ul&gt;&lt;li&gt;Log deprecated as of version 5.13.0&lt;/li&gt;&lt;/ul&gt; |
|`config.logSSL`|  &lt;ul&gt;&lt;li&gt;Deprecated as of version 5.13.0.&lt;/li&gt;&lt;li&gt;AT Internet Secure Log for this site ID.&lt;/li&gt;&lt;li&gt;For more information, see the AT Internet [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) documentation.&lt;/li&gt;&lt;li&gt;Refer to Tag Composer Subdomain for collector for secured pages&lt;/li&gt;&lt;/ul&gt; |
|`config.domain`|  &lt;ul&gt;&lt;li&gt;Deprecated as of version 5.13.0.&lt;/li&gt;&lt;li&gt;Collection Domain.&lt;/li&gt;&lt;li&gt;`xiti.com` or `ati-host.net`, depending on your AT Internet configuration.&lt;/li&gt;&lt;li&gt;You can use mappings to specify a custom collection domain.&lt;/li&gt;&lt;/ul&gt; |
|`config.pixelPath`|  &lt;ul&gt;&lt;li&gt;AT Internet pixel request URL path.&lt;/li&gt;&lt;li&gt;Defaults to `/hit.xiti`.&lt;/li&gt;&lt;/ul&gt; |
|`config.secure`|  &lt;ul&gt;&lt;li&gt;Enables the sending of information in a secure manner.&lt;/li&gt;&lt;/ul&gt; |
|`config.cookieSecure`|  &lt;ul&gt;&lt;li&gt;If set to **true**, enables you to add the option `secure` for the writing of tracker cookies (first).&lt;/li&gt;&lt;li&gt;Be aware that secure cookies only work on HTTPS pages.&lt;/li&gt;&lt;/ul&gt; |
|`config.disableCookie`|  &lt;ul&gt;&lt;li&gt;Disable Cookie.&lt;/li&gt;&lt;/ul&gt; |
|`config.cookieDomain`|  &lt;ul&gt;&lt;li&gt;Cookie Domain.&lt;/li&gt;&lt;li&gt;URL of your site.&lt;/li&gt;&lt;li&gt;Incorrect configuration may cause issues in the Unique Visitor calculation.&lt;/li&gt;&lt;/ul&gt; |
|`config.preview`|  &lt;ul&gt;&lt;li&gt;Preview.&lt;/li&gt;&lt;/ul&gt; |
|`config.sendHitWhenOptOut`|  &lt;ul&gt;&lt;li&gt;Allows sending anonymous hits when the user is in &#34;OPT-OUT&#34; mode (first party).&lt;/li&gt;&lt;/ul&gt; |

### Context

|Variable| Description|
|---| ---|
|`context.forcedCampaign`| Forced Campaign.|
|`context.forcedReferer`| Forced Referer.|

### E-Commerce - Events

For additional information, see [Cart Events (Sales Insights)](https://developers.atinternet-solutions.com/javascript-en/ecommerce-javascript-en/sales-insights-javascript-en/cart-events-sales-insights-javascript-fr/?kw=cartdisplay#cart-display_2).

|Variable| Description|
|---| ---|
|`order`|  &lt;ul&gt;&lt;li&gt;Order&lt;/li&gt;&lt;/ul&gt; |
|`cart`|  &lt;ul&gt;&lt;li&gt;Cart&lt;/li&gt;&lt;/ul&gt; |
|`prod`|  &lt;ul&gt;&lt;li&gt;Product View&lt;/li&gt;&lt;/ul&gt; |
|`aisle`|  &lt;ul&gt;&lt;li&gt;Aisle&lt;/li&gt;&lt;/ul&gt; |
|`transactionconfirm`|  &lt;ul&gt;&lt;li&gt;Transaction Confirmation&lt;/li&gt;&lt;/ul&gt; |
|`cartdisplay`|  &lt;ul&gt;&lt;li&gt;Cart Display&lt;/li&gt;&lt;/ul&gt; |
|`cartupdate`|  &lt;ul&gt;&lt;li&gt;Cart Update&lt;/li&gt;&lt;/ul&gt; |
|`displayshipping`|  &lt;ul&gt;&lt;li&gt;Display of Shipping Step&lt;/li&gt;&lt;/ul&gt; |
|`displaypayment`|  &lt;ul&gt;&lt;li&gt;Display of Payment Step&lt;/li&gt;&lt;/ul&gt; |
|`cartawaitingpayment`|  &lt;ul&gt;&lt;li&gt;Cart Awaiting Payment&lt;/li&gt;&lt;/ul&gt; |
|`productdisplay`|  &lt;ul&gt;&lt;li&gt;Product Display&lt;/li&gt;&lt;/ul&gt; |
|`productpagedisplay`|  &lt;ul&gt;&lt;li&gt;Product Page Display&lt;/li&gt;&lt;/ul&gt; |
|`productaddition`| &lt;ul&gt;&lt;li&gt;Product Addition&lt;/li&gt;&lt;/ul&gt; |
|`productremoval`|  &lt;ul&gt;&lt;li&gt;Product Removal&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;Order Total.&lt;/li&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Order Subtotal.&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Shipping amount.&lt;/li&gt;&lt;li&gt;Overrides `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax amount.&lt;/li&gt;&lt;li&gt;Overrides `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;Promo code.&lt;/li&gt;&lt;li&gt;Overrides `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Names.&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of SKUs.&lt;/li&gt;&lt;li&gt;Overrides `_csku`.&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Brands.&lt;/li&gt;&lt;li&gt;Overrides `_cbrand`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Categories.&lt;/li&gt;&lt;li&gt;Overrides `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_subcategory`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Sub Categories.&lt;/li&gt;&lt;li&gt;Overrides `_ccat2`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Discounts.&lt;/li&gt;&lt;li&gt;Overrides `_cpdisc`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID.&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |

### Visitor

|Variable| Description|
|---| ---|
|`visitor.id`|  &lt;ul&gt;&lt;li&gt;Customer ID.&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`visitor.category`|  &lt;ul&gt;&lt;li&gt;Category.&lt;/li&gt;&lt;/ul&gt; |
|`visitor.###`|  &lt;ul&gt;&lt;li&gt;Custom Property.&lt;/li&gt;&lt;/ul&gt; |

### On-Site Ads

|Variable| Description|
|---| ---|
|`promo.adId`|  &lt;ul&gt;&lt;li&gt;ID to be created.&lt;/li&gt;&lt;/ul&gt; |
| `promo.adId` |  &lt;ul&gt;&lt;li&gt;ID indicating the ad format.&lt;/li&gt;&lt;/ul&gt; |
|`promo.productId`|  &lt;ul&gt;&lt;li&gt;ID of associated product.&lt;/li&gt;&lt;/ul&gt; |
|`promo.###`|  &lt;ul&gt;&lt;li&gt;Custom Mapping.&lt;/li&gt;&lt;/ul&gt; |

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
|`dynlabel.pageId`|  &lt;ul&gt;&lt;li&gt;Dynamic Page ID&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.update`|  &lt;ul&gt;&lt;li&gt;Date of name change&lt;/li&gt;&lt;/ul&gt; |
| `dynlabel.chapter1` |  &lt;ul&gt;&lt;li&gt;Name of Chapter at level 1.&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.chapter2`|  &lt;ul&gt;&lt;li&gt;Name of Chapter at level 2.&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.chapter3`|  &lt;ul&gt;&lt;li&gt;Name of Chapter at level 3.&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.chapter#`|  &lt;ul&gt;&lt;li&gt;Name of Chapter at level #.&lt;/li&gt;&lt;/ul&gt; |

### Internal Search

|Variable| Description|
|---| ---|
|`intsearch.keyword`|  &lt;ul&gt;&lt;li&gt;Search keyword.&lt;/li&gt;&lt;/ul&gt; |
|`intsearch.resultPageNumber`|  &lt;ul&gt;&lt;li&gt;Search Result Page Number.&lt;/li&gt;&lt;/ul&gt; |
| `intsearch.resultPosition` |  &lt;ul&gt;&lt;li&gt;Search Result Position.&lt;/li&gt;&lt;/ul&gt; |

### MV (Multivariate) Testing

|Variable| Description|
|---| ---|
| `mvtesting.set.test` |  &lt;ul&gt;&lt;li&gt;Test ID and Name.&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.set.waveId`|  &lt;ul&gt;&lt;li&gt;Wave ID.&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.set.creation`|  &lt;ul&gt;&lt;li&gt;Creation ID and Name.&lt;/li&gt;&lt;/ul&gt; |
| `mvtesting.set.###` |  &lt;ul&gt;&lt;li&gt;Custom Set Mapping.&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.add.variable`|  &lt;ul&gt;&lt;li&gt;CSV/Array.&lt;/li&gt;&lt;li&gt;Test Variable.&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.add.version`|  &lt;ul&gt;&lt;li&gt;CSV/Array.&lt;/li&gt;&lt;li&gt;Test Version.&lt;/li&gt;&lt;/ul&gt; |
| `mvtesting.add.###` |  &lt;ul&gt;&lt;li&gt;Custom Add Mapping.&lt;/li&gt;&lt;/ul&gt; |

### Rich Media

|Variable| Description|
|---| ---|
|`richmedia.add.mediaType`|  &lt;ul&gt;&lt;li&gt;Media Type.&lt;/li&gt;&lt;li&gt;Values are:  &lt;ul&gt;&lt;li&gt;`video`&lt;/li&gt;&lt;li&gt;`audio`&lt;/li&gt;&lt;li&gt;`vpost`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|```richmedia.add.playerId```|  &lt;ul&gt;&lt;li&gt;Player ID.&lt;/li&gt;&lt;/ul&gt; |
| `richmedia.add.mediaLevel2` |  &lt;ul&gt;&lt;li&gt;Media Level 2.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.add.mediaLabel`|  &lt;ul&gt;&lt;li&gt;Media Label.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.add.isEmbedded`|  &lt;ul&gt;&lt;li&gt;Is Embedded.&lt;/li&gt;&lt;li&gt;Values are `int` or `ext`.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.add.broadcastMode`|  &lt;ul&gt;&lt;li&gt;Broadcast Mode.&lt;/li&gt;&lt;li&gt;Values are `live` or `clip`.&lt;/li&gt;&lt;/ul&gt; |
| `richmedia.add.webdomain` |  &lt;ul&gt;&lt;li&gt;Web Domain of External Placement&lt;/li&gt;&lt;/ul&gt; |
| `richmedia.add.duration` |  &lt;ul&gt;&lt;li&gt;Duration.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.action`|  &lt;ul&gt;&lt;li&gt;Send Action.&lt;/li&gt;&lt;li&gt;Values are:  &lt;ul&gt;&lt;li&gt;`play`&lt;/li&gt;&lt;li&gt;`pause`&lt;/li&gt;&lt;li&gt;`stop`&lt;/li&gt;&lt;li&gt;`info`&lt;/li&gt;&lt;li&gt;`move`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.playerId`|  &lt;ul&gt;&lt;li&gt;Player ID.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.mediaLabel`|  &lt;ul&gt;&lt;li&gt;Media Label.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.isBuffering`|  &lt;ul&gt;&lt;li&gt;Is Buffering.&lt;/li&gt;&lt;li&gt;Values are:  &lt;ul&gt;&lt;li&gt;`1` - start buffering&lt;/li&gt;&lt;li&gt;`0` - end buffering&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`richmedia.remove`|  &lt;ul&gt;&lt;li&gt;Remove Player.&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.removeAll`|  &lt;ul&gt;&lt;li&gt;Remove All Players&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |

### Mobile

|Variable| Description|
|---| ---|
|`mob.apvr`|  &lt;ul&gt;&lt;li&gt;App Version.&lt;/li&gt;&lt;/ul&gt; |
|`mob.ref`|  &lt;ul&gt;&lt;li&gt;Referrer.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc`|  &lt;ul&gt;&lt;li&gt;Object.&lt;/li&gt;&lt;li&gt;Life Cycle.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc`|  &lt;ul&gt;&lt;li&gt;Object.&lt;/li&gt;&lt;li&gt;Life Cycle.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.sessionId`|  &lt;ul&gt;&lt;li&gt;Session ID.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.fl`|  &lt;ul&gt;&lt;li&gt;First Launched.&lt;/li&gt;&lt;li&gt;Overrides `lifecycle_isfirstlaunch`.&lt;/li&gt;&lt;li&gt;Values are `0` or `1`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.flau`|  &lt;ul&gt;&lt;li&gt;First Launched Since Update.&lt;/li&gt;&lt;li&gt;Overrides `lifecycle_isfirstlaunchupdate`.&lt;/li&gt;&lt;li&gt;Values are `0` or `1`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lc`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Number of Launches.&lt;/li&gt;&lt;li&gt;Overrides `lifecycle_totallaunchcount`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.ldc`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Launches throughout the day.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lwc`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Launches throughout the week.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lmc`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Launches throughout the month.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lcsu`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Launches since last update.&lt;/li&gt;&lt;/ul&gt; |
| `mob.stc.lc.fld` |  &lt;ul&gt;&lt;li&gt;Date of first launch.&lt;/li&gt;&lt;li&gt;Overrides `lifecycle_firstlaunchdate`.&lt;/li&gt;&lt;li&gt;Date format is `yyyymmdd`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.dsfl`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Number of days since first launch.&lt;/li&gt;&lt;li&gt;Calculated from `lifecycle_firstlaunchdate`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.uld`|  &lt;ul&gt;&lt;li&gt;Date of first launch since last update.&lt;/li&gt;&lt;li&gt;Overrides `lifecycle_updatelaunchdate`.&lt;/li&gt;&lt;li&gt;Date format is `yyyymmdd`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.dsu`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Number of days since first launch since update.&lt;/li&gt;&lt;li&gt;Overrides `lifecycle_dayssinceupdate`.&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.dslu`|  &lt;ul&gt;&lt;li&gt;Number.&lt;/li&gt;&lt;li&gt;Days since app was last used.&lt;/li&gt;&lt;li&gt;Calculated from `lifecycle_lastlaunchdate`.&lt;/li&gt;&lt;/ul&gt; |

### Custom Tree Structure

|Variable| Description|
|---| ---|
|`customTreeStructure.category1`|  &lt;ul&gt;&lt;li&gt;Category Level 1&lt;/li&gt;&lt;/ul&gt; |
|`customTreeStructure.category2`|  &lt;ul&gt;&lt;li&gt;Category Level 2&lt;/li&gt;&lt;/ul&gt; |
|`customTreeStructure.category3`|  &lt;ul&gt;&lt;li&gt;Category Level 3&lt;/li&gt;&lt;/ul&gt; |

### Campaign

|Variable| Description|
|---| ---|
|`xtor`|  &lt;ul&gt;&lt;li&gt;Campaign ID.&lt;/li&gt;&lt;/ul&gt; |
