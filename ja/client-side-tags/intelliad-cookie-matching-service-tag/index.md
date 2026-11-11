---
title: intelliAd Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでintelliAd Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/intelliad-cookie-matching-service-tag/
---
intelliAd Cookie Matching Serviceは、Tealium訪問IDをintelliAdユーザーIDに関連付けます。


<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* このタグは、Tealium訪問セッションごとに1回のみ発火します。
* 次のサーバーサイド属性をTealiumに送り返します。
  * `intelliad_uid`
* 空白のままにすると、現在のアカウントとプロファイルがTealiumアカウントおよびTealiumプロファイルに自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Tealiumアカウント**
  * （任意）サーバーサイドリクエストに使用される`tealium_account`を上書きします。
* **Tealiumプロファイル**：
  * （任意）サーバーサイドリクエストに使用される`tealium_profile`を上書きします。
* **データレイヤーに保存**
  * ユーザーのintelliAd IDを、現在のWebページのデータレイヤーオブジェクトに`intelliad_uid`として保存します。
* **Tealiumに送信（サーバーサイド）**
  * `intelliad_uid` intelliAd IDをサーバーサイド属性として使用できるようにします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`tealium_account`| <ul><li>Tealiumアカウント</li></ul> |
|`tealium_profile`| <ul><li>Tealiumプロファイル</li></ul> |
|`store_in_datalayer`| <ul><li>データレイヤーに保存</li><li>値は**yes**または**no**です。</li></ul> |
|`send_to_tealium`| <ul><li>Tealiumに送信</li><li>値は**yes**または**no**です。</li></ul> |