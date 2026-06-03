---
title: Piano Analytics Tag Setup Guide
description: This article describes how to set up the Piano Analytics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/piano-analytics-tag/
---
## Tag tips

* Use mapping to override the standard configuration values dynamically.
* The **Set Consent Mode** parameter only accepts the values: `opt-in`, `essential`, or `opt-out`.

This tag is based on the following vendor SDK: [Piano Analytics: Javascript](https://developers.atinternet-solutions.com/piano-analytics/data-collection/sdks/javascript).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Site ID**: AT Internet Site ID.
* **Collection Domain**: AT Internet data collection domain.
* **Collection Path**: AT Internet pixel request URL path.
* **Add Event URL**: Automatically adds a `page_url` property to all events, containing the URL of the current page. The default value is `withoutQS`.
* **Require Consent**: To activate the Consents feature, set the `requireConsent` variable to `true`.
* **Send Event When Opt-out**: Do you want to send events when opted out? The default value is `true`.
* **Campaign Prefix**: Choose with an order of priority the type of campaign to be collected.
* **Enable UTM Tracking**: UTM parameters collected as properties. The default value is `true`.
* **Queue Name**: Use this field to overwrite the default `queueName` from `_pac`.
* **Privacy Default Mode**:  Select the default mode for privacy: `opt-in`, `essential`, or `opt-out`.
* **Automatically read from Tealium Consent Cookie**: Integrates with Tealium Consent Manager.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag configuration parameters

| Variable                  | Type      | Description             |
|:--------------------------|:----------|:------------------------|
|  `site`                   | String    | Site ID.                | 
|  `collectionDomain`       | String    | Collection domain.      | 
|  `collectionPath`         | String    | Collection path.        | 
|  `addEventURL`            | Boolean   | Add event URL.          | 
|  `sendEventWhenOptout`    | Boolean   | Send event when optout. | 
|  `campaignPrefix`         | String    | Campaign prefix.        | 
|  `enableUTMTracking`      | Boolean   | Enable UTM tracking.    | 
| `queueName`               | String    | Queue name.             | 

### Conversion parameters

| Variable    | Type        | Description |
|:------------|:------------|:------------|
| `goal_type` | String      | Goal type.  |

### Page parameters

| Variable        | Type      | Description     |
|:----------------|:----------|:----------------|
| `page`          | String    | Page.           |
| `page_chapter1` | String    | Page chapter 1. |
| `page_chapter2` | String    | Page chapter 2. |
| `page_chapter3` | String    | Page chapter 3. |

### Clicks parameters

| Variable         | Type      |Description       |
|:-----------------|:----------|:-----------------|
| `click`          | String    | Click.           |
| `click_chapter1` | String    | Click chapter 1. |
| `click_chapter2` | String    | Click chapter 2. |
| `click_chapter3` | String    | Click chapter 3. |

### On-site ads parameters

| Variable                       | Type    | Description                    |
|:-------------------------------|:--------|:-------------------------------|
|  `onsitead_type` (Required)    | String  | On site ad type.               |
|  `onsitead_advertiser`         | String  | On site ad advertiser.         |
|  `onsitead_campaign`           | String  | On site ad campaign.           |
|  `onsitead_category`           | String  | On site ad category.           |
|  `onsitead_creation`           | String  | On site ad creation.           |
|  `onsitead_detailed_placement` | String  | On site ad detailed placement. |
|  `onsitead_format`             | String  | On site ad format.             |
|  `onsitead_general_placement`  | String  | On site ad general placement.  |
|  `onsitead_url`                | String  | On site ad URL.                |
|  `onsitead_variant`            | String  | On site ad variant.            |

### ISE (internal search engine) parameters

| Variable         | Type    | Description     |
|:-----------------|:--------|:----------------|
| `ise_keyword`    | String  | ISE keyword.    |
| `ise_page`       | Number  | ISE page.       |
| `ise_click_rank` | Number  | ISE click rank. |

### MV (multivariate) testing parameters

| Variable      | Type   |Description   |
|:--------------|:-------|:-------------|
| `mv_creation` | String | Multivariate creation. |
| `mv_test`     | String | Multivariate test.     |
| `mv_wave`     | Number | Multivariate wave.     |

### Product parameters

| Variable                                         | Type              | Description                           |
|:-------------------------------------------------|:------------------|:--------------------------------------|
| `product_id` (Overrides `_cprod`)                | Array of strings  | Product ID.                           |
| `product` (Overrides `_cprodname`)               | Array of strings  | Product label.                        |
| `product_variant`                                | String            | Product variant.                      |
| `product_brand` (Overrides `_cbrand`)            | Array of strings  | Product brand.                        |
| `product_discount` (Overrides `_cpdisc`)         | Array of Booleans | Whether the product is discontinued.  |
| `product_pricetaxincluded` (Overrides `_cprice`) | Array of numbers  | Price, tax included.                  |
| `product_pricetaxfree`                           | Number            | Price, tax free.                      |
| `product_currency`                               | String            | Currency (ISO 4217).                  |
| `product_stock`                                  | Boolean           | Whether the product is in stock.      |
| `product_quantity` (Overrides `_cquan`)          | Array of numbers  | Product quantity.                     |
| `product_category1` (Overrides `_ccat`)          | Array of strings  | Level 1 category.                     |
| `product_category2` (Overrides `_ccat2`)         | Array of strings  | Level 2 category.                     |
| `product_category3`                              | String            | Level 3 category.                     |
| `product_category4`                              | String            | Level 4 category.                     |
| `product_cartcreation`                           | Boolean           | Whether the cart was created by this product addition. |

### Cart parameters

| Variable                                 | Type   | Description                                             |
|:-----------------------------------------|:-------|:--------------------------------------------------------|
| `cart_id` (Overrides `_corder`)          | String | Cart ID.                                                |
| `cart_currency` (Overrides `_ccurrency`) | String | Cart currency.                                          |
| `cart_turnovertaxincluded`               | Number | Turnover tax included.                                  |
| `cart_turnovertaxfree`                   | Number | Turnover tax free.                                      |
| `cart_creation_utc`                      | Number | Cart creation date in UTC seconds.                      |
| `cart_quantity` (Overrides `_ctotal`)    | Number | Number of products.                                     |
| `cart_nbdistinctproduct`                 | Number | Number of distinct products.                            |
| `cart_version`                           | Number | New unique version identifier associated with the cart. |

### Transaction parameters

| Variable                    | Type             |Description                                          |
|:----------------------------|:-----------------|:----------------------------------------------------|
| `transaction_id`            | String           | Transaction ID.                                     |
| `transaction_promocode`     | Array of strings | Promo code list.                                    |
| `transaction_firstpurchase` | Boolean          | Whether this is the first purchase by the customer. |

### Shipping and payment parameters

| Variable                   | Type   | Description                 |
|:---------------------------|:-------|:----------------------------|
| `shipping_delivery`        | String | Shipping type.              |
| `shipping_costtaxincluded` | Number | Shipping cost tax included. |
| `shipping_costtaxfree`     | Number | Shipping cost tax free.     |
| `payment_mode`             | String | Payment mode.               |

### User parameters

| Variable        | Type    | Description                                     |
|:----------------|:--------|:------------------------------------------------|
| `visitorId`     | String  | Custom visitor ID (GUID or 16 characters long). |
| `userId`        | String  | User ID.                                        |
| `userCategory`  | String  | User category.                                  |
| `enableStorage` | Boolean | Enable storage.                                 |

### Global parameters

| Variable              | Type    |Description |
|:----------------------|:------------|:------------|
| `cookieDomain`        | String  | The domain scope for tracking cookies set by the analytics script. |
| `cookieSameSite`      | String  | **SameSite** flag in cookies in client-side.                       |
| `cookieSecure`        | Boolean | **Secure** flag in cookies in client-side cookies.                 |
| `encodeStorageBase64` | Boolean | Whether the cookie is Base64-encoded.                              |

### Privacy and storage parameters

| Variable                 | Type    | Description                                          |
|:-------------------------|:--------|:-----------------------------------------------------|
| `privacyDefaultMode`     | String  | Privacy mode by default.                             |
| `mode`                   | String  | Consent mode.                                        |
| `requireConsent`         | String  | Require consent.                                     |
| `tealium_consent`        | Boolean | Tealium consent.                                     |
| `properties`             | Object  | Properties priority configuration.                   |
| `consent_events`         | Object  | Events priority configuration.                       |
| `storageLifetimePrivacy` | Number  | Lifetime storage privacy value.                      |
| `storageLifetimeUser`    | Number  | Lifetime storage user value.                         |
| `storageLifetimeVisitor` | Number  | Lifetime storage visitor value.                      |
| `visitorStorageMode`     | String  | Relative or fixed cookie lifetime value for visitor. |

### Visitor policy parameters

| Variable               | Type    | Description |
|:-----------------------|:--------|:------------|
|  `isVisitorClientSide` | Boolean | Whether the Visitor ID is stored on a cookie in the browser.&lt;ul&gt;&lt;li&gt;`true`: The Visitor ID is generated and stored in the browser.&lt;/li&gt;&lt;li&gt;`false`: The Visitor ID is managed by the server.&lt;/li&gt;&lt;/ul&gt; |

### Audio video parameters

| Variable                     | Type               | Description                        |
|:-----------------------------|:-------------------|:-----------------------------------|
| Playback session ID          | String             | Session ID of the playback.        |
| `heartbeatDuration`          | [Number or Object] | Delay between two heartbeats during playback, minimum delay is 5 seconds. |
| `bufferingHeartbeatDuration` | [Number or Object] | Delay between two heartbeats during buffering, minimum delay is 1 seconds.|
| `av_session_id`              | String             | Session ID, generated by the SDK.  |
| `av_content_id`              | String             | Content ID.                        |
| `av_content`                 | String             | Content label.                     |
| `av_content_type`            | String             | Content type.                      |
| `av_content_duration`        | Number             | Content duration, in milliseconds. |
| `av_content_linked`          | String             | Linked content label.              |
| `av_publication_date`        | Number             | Publication date, timestamp.       |
| `av_content_genre`           | Array of strings   | Content genres.                    |
| `av_show`                    | String             | Show label.                        |
| `av_show_season`             | String             | Show season label.                 |
| `av_episode_id`              | String             | Episode ID.                        |
| `av_episode`                 | String             | Episode label.                     |
| `av_channel`                 | String             | Channel label.                     |
| `av_author`                  | String             | Author name.                       |
| `av_content_version`         | String             | Content version.                   |
| `av_content_duration_range`  | String             | Duration range.                    |
| `av_broadcasting_type`       | String             | Broadcasting type.                 |
| `av_broadcaster`             | String             | Broadcaster name.                  |
| `av_ad_type`                 | String             | Ad type.                           |
| `av_player`                  | String             | Player label.                      |
| `av_player_version`          | String             | Player version.                    |
| `av_player_position`         | String             | Player position.                   |
| `av_auto_mode`               | Boolean            | Auto play mode.                    |
| `av_language`                | String             | Media language.                    |
| `av_subtitles`               | String             | Subtitles.                         |
| `av_launch_reason`           | String             | Launch reason.                     |

### Traffic source

| Variable             | Type   | Description             |
|:---------------------|:-------|:------------------------|
| `src`                | String | Source.                 |
| `src_details`        | String | Source details.         |
| `src_type`           | String | Campaign natural.       |
| `src_medium`         | String | Campaign type.          |
| `src_campaign`       | String | Campaign name.          |
| `src_se_category`    | String | Search engine category. |
| `src_portal_site_id` | String | Portal site ID.         |

### Enhanced marketing source detection

| Variable                  | Type    | Description            |
|:--------------------------|:--------|:-----------------------|
| `src_content`             | String  | Source Content.        |
| `src_creative_format`     | String  | Creative Format.       |
| `src_id`                  | String  | Source ID.             |
| `src_marketing_tactic`    | String  | Marketing Tactic.      |
| `src_source`              | String  | Source.                |
| `src_source_platform`     | String  | Source Platform.       |
| `src_term`                | String  | Source Term.           |
| `event_collection_auto`   | Boolean | Auto Event Collection. |
| `geo_country_code_alpha2` | String  | Country.               |

### Events

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/).

| Variable                         | Description                               |
|:---------------------------------|:------------------------------------------|
| `page.display`                   | Page display.                             |
| `click.action`                   | Click action.                             |
| `click.navigation`               | Click navigation.                         |
| `click.download`                 | Click download.                           |
| `click.exit`                     | Click exit.                               |
| `publisher.impression`           | Publisher impression.                     |
| `publisher.click`                | Publisher click.                          |
| `self_promotion.impression`      | Self-promotion impression.                |
| `self_promotion.click`           | Self-promotion click.                     |
| `internal_search_result.display` | Internal search result display.           |
| `internal_search_result.click`   | Internal search result display.           |
| `mv_test.display`                | MV test display.                          |
| `product.display`                | Product display.                          |
| `product.page_display`           | Product page display.                     |
| `product.add_to_cart`            | Product added to cart.                    |
| `product.remove_from_cart`       | Product removed from cart.                |
| `product.awaiting_payment`       | Product awaiting payment.                 |
| `product.purchased`              | Product purchased.                        |
| `cart.creation`                  | Cart created.                             |
| `cart.display`                   | Cart display.                             |
| `cart.update`                    | Cart updated.                             |
| `cart.delivery`                  | Cart delivery.                            |
| `cart.payment`                   | Cart payment.                             |
| `cart.awaiting_payment`          | Cart awaiting payment.                    |
| `transaction.confirmation`       | Transaction confirmation.                 |
| `setUser`                        | Set user.                                 |
| `getUser`                        | Get user.                                 |
| `deleteUser`                     | Delete user.                              |
| `getSessionID`                   | Get session ID.                           |
| `av.play`                        | AV play.                                  |
| `av.buffer.start`                | AV buffer start.                          |
| `av.buffer.heartbeat`            | AV buffer heartbeat.                      |
| `av.start`                       | AV start.                                 |
| `av.heartbeat`                   | AV heartbeat.                             |
| `av.pause`                       | AV pause.                                 |
| `av.rebuffer.start`              | AV rebuffer start.                        |
| `av.rebuffer.heartbeat`          | AV rebuffer heartbeat.                    |
| `av.resume`                      | AV resume.                                |
| `av.stop`                        | AV stop.                                  |
| `av.seek.start`                  | AV seek start.                            |
| `av.forward`                     | AV forward.                               |
| `av.backward`                    | AV backward.                              |
| `av.ad.click`                    | AV ad click.                              |
| `av.ad.skip`                     | AV ad skip.                               |
| `av.error`                       | AV error.                                 |
| `av.display`                     | AV display.                               |
| `av.close`                       | AV close.                                 |
| `av.volume`                      | AV volume.                                |
| `av.subtitle.on`                 | AV subtitle on.                           |
| `av.subtitle.off`                | AV subtitle off.                          |
| `av.fullscreen.on`               | AV full screen on.                        |
| `av.fullscreen.off`              | AV full screen off.                       |
| `av.quality`                     | AV quality.                               |
| `av.speed`                       | AV speed.                                 |
| `av.share`                       | AV share.                                 |
| `set.mode`                       | Set mode.                                 |
| `get.mode`                       | Get mode.                                 |
| `disableconsent`                 | Disable consent. Set `mode` to `opt-out`. |
| Custom                           | custom.                                   |

### Event-specific parameters

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/).

| Variable                         | Description                     |
|:---------------------------------|:--------------------------------|
| All Events                       | All events.                     |
| `page.display`                   | Page display.                   |
| `click.action`                   | Click action.                   |
| `click.navigation`               | Click navigation.               |
| `click.download`                 | Click download.                 |
| `click.exit`                     | Click exit.                     |
| `publisher.impression`           | Publisher impression.           |
| `publisher.click`                | Publisher click.                |
| `self_promotion.impression`      | Self-promotion impression.      |
| `self_promotion.click`           | Self-promotion click.           |
| `internal_search_result.display` | Internal search result display. |
| `internal_search_result.click`   | Internal search result display. |
| `mv_test.display`                | MV test display.                |
| `product.display`                | Product display.                |
| `product.page_display`           | Product page display.           |
| `product.add_to_cart`            | Product added to cart.          |
| `product.remove_from_cart`       | Product removed from cart.      |
| `product.awaiting_payment`       | Product awaiting payment.       |
| `product.purchased`              | Product purchased.              |
| `cart.creation`                  | Cart created.                   |
| `cart.display`                   | Cart display.                   |
| `cart.update`                    | Cart updated.                   |
| `cart.delivery`                  | Cart delivery.                  |
| `cart.payment`                   | Cart payment.                   |
| `cart.awaiting_payment`          | Cart awaiting payment.          |
| `transaction.confirmation`       | Transaction confirmation.       |
| `setUser`                        | Set user.                       |
| `getUser`                        | Get user.                       |
| `deleteUser`                     | Delete user.                    |
| `getSessionID`                   | Get session ID.                 |
| `av.play`                        | AV play.                        |
| `av.buffer.start`                | AV buffer start.                |
| `av.buffer.heartbeat`            | AV buffer heartbeat.            |
| `av.start`                       | AV start.                       |
| `av.heartbeat`                   | AV heartbeat.                   |
| `av.pause`                       | AV pause.                       |
| `av.rebuffer.start`              | AV rebuffer start.              |
| `av.rebuffer.heartbeat`          | AV rebuffer heartbeat.          |
| `av.resume`                      | AV resume.                      |
| `av.stop`                        | AV stop.                        |
| `av.seek.start`                  | AV seek start.                  |
| `av.forward`                     | AV forward.                     |
| `av.backward`                    | AV backward.                    |
| `av.ad.click`                    | AV ad click.                    |
| `av.ad.skip`                     | AV ad skip.                     |
| `av.error`                       | AV error.                       |
| `av.display`                     | AV display.                     |
| `av.close`                       | AV close.                       |
| `av.volume`                      | AV volume.                      |
| `av.subtitle.on`                 | AV subtitle on.                 |
| `av.subtitle.off`                | AV subtitle off.                |
| `av.fullscreen.on`               | AV full screen on.              |
| `av.fullscreen.off`              | AV full screen off.             |
| `av.quality`                     | AV quality.                     |
| `av.speed`                       | AV speed.                       |
| `av.share`                       | AV share.                       |
| Custom                           | Custom.                         |