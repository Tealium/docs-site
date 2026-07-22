---
title: Adobe Audience Managerタグ構成ガイド
description: この記事では、iQタグ管理アカウントでAdobe Audience Managerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-audience-manager-tag/
---
## タグのヒント

* **Use E-Commerce Variables**の下で**On**を選択して、OrderとCustomerのE-Commerceデータを`c_`データに追加します
* "Custom c_ Object"マッピングを使用して、自分のオブジェクトや追加のオブジェクトを`c_`データと一緒に送信します
* 現在のライブラリバージョン: 9.5

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Adobe Audience Managerタグを追加します([タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら)。

タグを追加したら、以下の構成を行います:

* **Visitor Service Namespace**: これはあなたのAdobe Org ID/Experience Cloud IDと同じです
* **Partner Name**: Audience Managementから提供されます
* **Use E-Commerce Variables**:

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです:

### 標準

| 変数                                                                   | 説明         |
|:---------------------------------------------------------------------------|:--------------------|
| Visitor Service Namespace                                                  | (`namespace`)         |
| Partner Name                                                               | (`partner`)           |
| Use E-Commerce Variables                                                   | (`use_ecommerce`)     |
| Container ID                                                               | (`containerNSID`)     |
| Data Partner ID                                                            | (`declaredId.dpid`)   |
| Unique User ID                                                             | (`declaredId.dpuuid`) |
| Defer Requests Until Page Load (`delayAllUntilWindowLoad`)                   | [Boolean]           |
| Disable UUID Cookie (`disableDeclaredUUIDCookie`)                            | [Boolean]           |
| Prevent Destination Publishing IFRAME (`disableDestinationPublishingIframe`) | [Boolean]           |
| Disable ID Synchronization (`disableIDSyncs`)                                | [Boolean]           |
| Enable Error Reporting (`enableErrorReporting`)                              | [Boolean]           |
| Enable Logging (`enableLogging`)                                             | [Boolean]           |
| Enable URL Destinations (`enableUrlDestinations`)                            | [Boolean]           |
| Enable Cookie Destinations (`enableCookieDestinations`)                      | [Boolean]           |
| Enable Akamai for HTTPS (`iframeAkamaiHTTPS`)                                | [Boolean]           |
| Remove Finished Scripts and Callbacks (`removeFinishedScriptsAndCallbacks`)   | [Boolean]           |
| Key Mappings Object (`mappings`)                                             | [Object]            |
| Cookie Name                                                                | (`uuidCookie.name`)   |
| Cookie Lifetime in Days                                                    | (`uuidCookie.days`)   |
| Cookie Path                                                                | (`uuidCookie.path`)   |
| Cookie Domain                                                              | (`uuidCookie.domain`) |
| Send Over HTTPS (`uuidCookie.secure`)                                        | [Boolean]           |

### 基本的な`c_`変数

| 変数             | 説明              |
|:---------------------|:-------------------------|
| Ad ID                | (`c.ad_id`)                |
| Content Author       | (`c.content_author`)       |
| Content Title        | (`c.content_title`)        |
| Content Publish Date | (`c.content_publish_date`) |
| Category ID          | (`c.category_id`)          |
| Category Name        | (`c.category_name`)        |
| Page Name            | (`c.page_name`)            |
| Page Number          | (`c.page_number`)          |
| Previous Page Name   | (`c.previous_page_name`)   |
| Search Category      | (`c.search_category`)      |
| Search Keyword       | (`c.search_keyword`)       |
| Search Results       | (`c.search_results`)       |
| Site Section         | (`c.site_section`)         |
| Sort By              | (`c.sort_by`)              |
| Sort Order           | (`c.sort_order`)           |
| Custom `c_` Variable   | (`c.custom`)               |
| Custom `c_` Object     | (`cobject.custom`)         |

### 基本的な`d_`変数

| 変数                               | 説明  |
|:---------------------------------------|:-------------|
| Caller                                 | (`d.caller`)   |
| Javascript Callback Function           | (`d.cb`)       |
| Data Provider ID                       | (`s`) (`d.cid`)  |
| Integration Code and User ID           | (`d.cid_ic`)   |
| Trait and Segment Return Type          | (`d.cts`)      |
| Return URL Destination                 | (`d.dst`)      |
| JSON Return Version                    | (`d.jsonv`)    |
| Name Space ID                          | (`d.nsid`)     |
| Return JSON                            | (`d.rtbd`)     |
| Score ID                               | (`d.sid`)      |
| Trait Data Source                      | (`d.tdpid`)    |
| Trait Data Source via Integration Code | (`d.tdpid_ic`) |
| Unique User ID                         | (`d.uuid`)     |
| Custom `_d` Variable                     | (`d.custom`)   |

### カスタム`h_`および`p_`変数

| 変数           | 説明 |
|:-------------------|:------------|
| Custom `_h` Variable | (`h.custom`)  |
| Custom `_p` Variable | (`p.custom`)  |

### E-Commerce

| 変数           | 説明                             |
|:-------------------|:----------------------------------------|
| Order ID           | (`order_id`) (Overrides `_corder`)          |
| Order Total        | (`order_total`) (Overrides `_ctotal`)       |
| Sub Total          | (`order_subtotal`) (Overrides `_csubtotal`) |
| Shipping Amount    | (`order_shipping`) (Overrides `_cship`)     |
| Tax Amount         | (`order_tax`) (Overrides `_ctax`)           |
| Store              | (`order_store`) (Overrides `_cstore`)       |
| Currency           | (`order_currency`) (Overrides `_ccurrency`) |
| Promo Code         | (`order_coupon_code`) (Overrides `_cpromo`) |
| Cart or Order Type | (`order_type`) (Overrides `_ctype`)         |
