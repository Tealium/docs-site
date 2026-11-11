---
title: Amazon Advertising Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでAmazon Advertising Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-advertising-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Amazon Advertising Cookie Matching Serviceを使用すると、Tealium訪問IDをAmazonシステム内のAmazon Cookie IDに関連付けることができます。その後、Tealium訪問IDをAmazon Advertising DSP Customer Data Platform（CDP）コネクタ構成の識別子として使用できます。

## タグに関するヒント

* このタグは、Tealium訪問セッションごとに1回だけ発火します。
* AmazonはTealium訪問IDを受信し、Amazon Cookie IDと照合します。その後、Tealium訪問IDをAmazon Advertising DSP CDPコネクタでCookie識別子として使用できます。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **リージョン**：データ収集の地理的リージョン。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `region` | 文字列 | リージョン |
| `tealium_visitor_id` | 文字列 | Tealium訪問ID |