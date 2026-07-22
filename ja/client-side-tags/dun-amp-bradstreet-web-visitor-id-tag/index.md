---
title: Dun & Bradstreet Web Visitor IDタグ構成ガイド
description: この記事では、Dun & Bradstreet Web Visitor IDタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/dun-amp-bradstreet-web-visitor-id-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細は、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* マッピングを使用して標準の構成値を動的に上書きします。
* JavaScript Code拡張を使用して返されたデータを構成します。  
例：  
```javascript
window.tealium_dnbwvid = function(dnb_Data)
{
 // ここにデータを構成します。例：visitor_duns = dnb_Data.duns;
}
```

* Dun & Bradstreetのデータをサーバーサイドの属性として利用可能にする（セッションごとに一度）：

  * **Tealiumに送信（サーバーサイド）**を`true`に構成します
  * 空白の場合、Tealium AccountとTealium Profileは現在のアカウントとプロファイルで自動的に入力されます。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、D&B Web Visitor IDタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **APIキー**
  * Dun & Bradstreetから提供されるAPIキー。
  * 例：`//API_KEY_HERE.d41.co/sync/`

* **データキー**
  * getData呼び出しで提供されるAPIキー。
  * APIキーを使用する場合は空白にします。
  * 例：`dnbvid.getData('DATA_KEY_HERE','json','T'... )`

* **Tealiumに送信（サーバーサイド）**
* **Tealiumアカウント**
  * 任意。
  * サーバーサイドリクエストで使用される`tealium_account`を上書きします。

* **Tealiumプロファイル**
  * 任意。
  * サーバーサイドリクエストで使用される`tealium_profile`を上書きします。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`api_key`|  <ul><li>Dun & Bradstreetから提供されるAPIキー。</li><li>例：`//API_KEY_HERE.d41.co/sync/`</li></ul> |
|`data_key`|  <ul><li>getData呼び出しで提供されるAPIキー。</li><li>APIキーを使用する場合は空白にします。</li><li>例：`dnbvid.getData('DATA_KEY_HERE','json','T'... )`</li></ul> |
|`send_to_tealium`|  <ul><li>Tealiumに送信</li><li>Dun & Bradstreetから受け取ったデータがTealiumサーバーサイドに利用可能になります。</li></ul> |
|`tealium_account`|  <ul><li>Tealiumアカウント</li><li>任意。</li><li>サーバーサイドリクエストで使用される`tealium_account`を上書きします。</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル</li><li>任意。</li><li>サーバーサイドリクエストで使用される`tealium_profile`を上書きします。</li></ul> |
