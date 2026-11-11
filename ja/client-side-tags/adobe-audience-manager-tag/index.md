---
title: Adobe Audience Managerタグ構成ガイド
description: この記事では、タグ管理アカウントでAdobe Audience Managerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-audience-manager-tag/
---
## タグ構成のヒント

* **Use E-Commerce Variables**で**On**を選択すると、注文および顧客のEコマースデータが`c_`データに追加されます
* 「Custom c_ Object」マッピングを使用すると、独自のオブジェクトや追加のオブジェクトを`c_`データとともに送信できます
* 現在のライブラリバージョン：9.5

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **Visitor Service Namespace**：Adobe Org ID／Experience Cloud IDと同じ値です
* **Partner Name**：Audience Managementから提供されます
* **Use E-Commerce Variables**：

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数                                                                       | 説明                  |
|:---------------------------------------------------------------------------|:----------------------|
| Visitor Service Namespace                                                  | (`namespace`)         |
| Partner Name                                                               | (`partner`)           |
| Use E-Commerce Variables                                                   | (`use_ecommerce`)     |
| Container ID                                                               | (`containerNSID`)     |
| Data Partner ID                                                            | (`declaredId.dpid`)   |
| Unique User ID                                                             | (`declaredId.dpuuid`) |
| ページ読み込みまでリクエストを延期（`delayAllUntilWindowLoad`）             | [Boolean]             |
| UUID Cookieを無効化（`disableDeclaredUUIDCookie`）                          | [Boolean]             |
| Destination Publishing IFRAMEを防止（`disableDestinationPublishingIframe`） | [Boolean]             |
| ID同期を無効化（`disableIDSyncs`）                                          | [Boolean]             |
| エラー報告を有効化（`enableErrorReporting`）                                | [Boolean]             |
| ロギングを有効化（`enableLogging`）                                         | [Boolean]             |
| URL Destinationを有効化（`enableUrlDestinations`）                          | [Boolean]             |
| Cookie Destinationを有効化（`enableCookieDestinations`）                    | [Boolean]             |
| HTTPSでAkamaiを有効化（`iframeAkamaiHTTPS`）                                | [Boolean]             |
| 完了したスクリプトとコールバックを削除（`removeFinishedScriptsAndCallbacks`） | [Boolean]           |
| キーマッピングオブジェクト（`mappings`）                                   | [Object]              |
| Cookie名                                                                   | (`uuidCookie.name`)   |
| Cookieの有効期間（日数）                                                    | (`uuidCookie.days`)   |
| Cookieパス                                                                 | (`uuidCookie.path`)   |
| Cookieドメイン                                                             | (`uuidCookie.domain`) |
| HTTPS経由で送信（`uuidCookie.secure`）                                      | [Boolean]             |

### 基本的な`c_`変数

| 変数             | 説明                       |
|:-----------------|:---------------------------|
| 広告ID           | (`c.ad_id`)                |
| コンテンツ作成者 | (`c.content_author`)       |
| コンテンツタイトル | (`c.content_title`)      |
| コンテンツ公開日 | (`c.content_publish_date`) |
| カテゴリーID     | (`c.category_id`)          |
| カテゴリー名     | (`c.category_name`)        |
| ページ名         | (`c.page_name`)            |
| ページ番号       | (`c.page_number`)          |
| 前のページ名     | (`c.previous_page_name`)   |
| 検索カテゴリー   | (`c.search_category`)      |
| 検索キーワード   | (`c.search_keyword`)       |
| 検索結果         | (`c.search_results`)       |
| サイトセクション | (`c.site_section`)         |
| 並べ替え基準     | (`c.sort_by`)              |
| 並べ替え順序     | (`c.sort_order`)           |
| カスタム`c_`変数 | (`c.custom`)               |
| カスタム`c_`オブジェクト | (`cobject.custom`)  |

### 基本的な`d_`変数

| 変数                                   | 説明           |
|:---------------------------------------|:---------------|
| 呼び出し元                             | (`d.caller`)   |
| JavaScriptコールバック関数             | (`d.cb`)       |
| データプロバイダーID                   | (`s`) (`d.cid`) |
| 統合コードとユーザーID                 | (`d.cid_ic`)   |
| TraitおよびSegmentの戻り値の型          | (`d.cts`)      |
| 戻り先URL Destination                  | (`d.dst`)      |
| JSON戻り値のバージョン                  | (`d.jsonv`)    |
| Namespace ID                           | (`d.nsid`)     |
| JSONを返す                             | (`d.rtbd`)     |
| スコアID                               | (`d.sid`)      |
| Traitデータソース                      | (`d.tdpid`)    |
| 統合コード経由のTraitデータソース      | (`d.tdpid_ic`) |
| 一意のユーザーID                       | (`d.uuid`)     |
| カスタム`_d`変数                       | (`d.custom`)   |

### カスタム`h_`変数および`p_`変数

| 変数             | 説明         |
|:-----------------|:-------------|
| カスタム`_h`変数 | (`h.custom`) |
| カスタム`_p`変数 | (`p.custom`) |

### Eコマース

| 変数                 | 説明                                      |
|:---------------------|:------------------------------------------|
| 注文ID               | (`order_id`)（`_corder`を上書き）         |
| 注文合計             | (`order_total`)（`_ctotal`を上書き）      |
| 小計                 | (`order_subtotal`)（`_csubtotal`を上書き） |
| 配送料               | (`order_shipping`)（`_cship`を上書き）    |
| 税額                 | (`order_tax`)（`_ctax`を上書き）          |
| ストア               | (`order_store`)（`_cstore`を上書き）      |
| 通貨                 | (`order_currency`)（`_ccurrency`を上書き） |
| プロモーションコード | (`order_coupon_code`)（`_cpromo`を上書き） |
| カートまたは注文タイプ | (`order_type`)（`_ctype`を上書き）      |