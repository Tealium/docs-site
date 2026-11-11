---
title: DataXu Cookie Matching Serviceタグ構成ガイド
description: この記事では、DataXu Cookie Matching Serviceタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/dataxu-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* 空白のままにすると、現在のTiQアカウントとプロファイルがTealium AccountおよびTealium Profileに自動的に入力されます。
* 次のサーバーサイド属性をTealiumに送り返します。
  * `dataxuId`

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Tealium Account**
  * （任意）Tealium Account名。

* **Tealium Profile**:
  * （任意）Tealium Profile名。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`tealium_account`|Tealium Account|
|`tealium_profile`|Tealium Profile|