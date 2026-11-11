---
title: Dun & Bradstreet Web Visitor IDタグ構成ガイド
description: この記事では、Dun & Bradstreet Web Visitor IDタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/dun-amp-bradstreet-web-visitor-id-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* JavaScriptコード拡張機能を使用して、返されたデータを構成します。  
例：  
```javascript
window.tealium_dnbwvid = function(dnb_Data)
{
 // Set data here, ex: visitor_duns = dnb_Data.duns;
}
```

* Dun & Bradstreetのデータをサーバーサイド属性として使用できるようにするには（セッションごとに1回）：

  * **Tealiumに送信（サーバーサイド）**を`true`に構成します。
  * 空欄のままにすると、現在のアカウントとプロファイルがTealiumアカウントおよびTealiumプロファイルに自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **APIキー**
  * Dun & Bradstreetから提供されたAPIキー。
  * 例：`//API_KEY_HERE.d41.co/sync/`

* **データキー**
  * getData呼び出しで指定するAPIキー。
  * APIキーを使用する場合は空欄のままにします。
  * 例：`dnbvid.getData('DATA_KEY_HERE','json','T'... )`

* **Tealiumに送信（サーバーサイド）**
* **Tealiumアカウント**
  * （任意）サーバーサイドリクエストに使用する`tealium_account`を上書きします。

* **Tealiumプロファイル**
  * （任意）サーバーサイドリクエストに使用する`tealium_profile`を上書きします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---| ---|
|`api_key`|  <ul><li>Dun & Bradstreetから提供されたAPIキー。</li><li>例：`//API_KEY_HERE.d41.co/sync/`</li></ul> |
|`data_key`|  <ul><li>getData呼び出しで指定するAPIキー。</li><li>APIキーを使用する場合は空欄のままにします。</li><li>例：`dnbvid.getData('DATA_KEY_HERE','json','T'... )`</li></ul> |
|`send_to_tealium`|  <ul><li>Tealiumに送信</li><li>Dun & Bradstreetから受信したデータをTealiumのサーバーサイドで使用できるようにします。</li></ul> |
|`tealium_account`|  <ul><li>（任意）Tealiumアカウント</li><li>サーバーサイドリクエストに使用する`tealium_account`を上書きします。</li></ul> |
|`tealium_profile`|  <ul><li>（任意）Tealiumプロファイル</li><li>サーバーサイドリクエストに使用する`tealium_profile`を上書きします。</li></ul> |