---
title: iSpot TV Cookie Matching Serviceタグ構成ガイド
description: この記事では、iSpot TV Cookie Matching Serviceタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/ispot-tv-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* iSpot IDが正常に取得された場合、このタグはセッションごとに1回だけトリガーされます。
* 空白のままにすると、現在のTealiumアカウントとTealiumプロファイルが自動的に構成されます。
* 生成されるサーバーサイド呼び出しでは、次のパラメータが送信されます。
  * `tealium_cookie_sync`: true
  * `tealium_account`：Tealiumアカウント
  * `tealium_profile`：Tealiumプロファイル
  * `tealium_visitor_id`：訪問のTealium ID
  * `tealium_event`：`cookie_match_ispot`
  * `ispot_id`：訪問のiSpot ID
  * `tealium_datasource`：構成されている場合はTealiumデータソースID
  * `tealium_trace_id`：構成されている場合はTealium Trace ID

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **サイトID**：iSpotから提供されたサイトID
* **Tealiumアカウント**：（任意）Tealiumアカウント
* **Tealiumプロファイル**：（任意）Tealiumプロファイル
* **TealiumデータソースID**：（任意）TealiumデータソースID

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|サイトID|（site\_id）|
|Tealiumアカウント|（tealium\_account）|
|Tealiumプロファイル|（tealium\_profile）|
|TealiumデータソースID|（tealium\_datasource）|