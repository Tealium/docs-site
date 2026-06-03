---
title: Dun & Bradstreet Web Visitor IDタグ構成ガイド
description: この記事では、Dun & Bradstreet Web Visitor IDタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/dun-amp-bradstreet-web-visitor-id-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細は、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

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

* Dun &amp; Bradstreetのデータをサーバーサイドの属性として利用可能にする（セッションごとに一度）：

  * **Tealiumに送信（サーバーサイド）**を`true`に構成します
  * 空白の場合、Tealium AccountとTealium Profileは現在のアカウントとプロファイルで自動的に入力されます。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、D&amp;B Web Visitor IDタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **APIキー**
  * Dun &amp; Bradstreetから提供されるAPIキー。
  * 例：`//API_KEY_HERE.d41.co/sync/`

* **データキー**
  * getData呼び出しで提供されるAPIキー。
  * APIキーを使用する場合は空白にします。
  * 例：`dnbvid.getData(&#39;DATA_KEY_HERE&#39;,&#39;json&#39;,&#39;T&#39;... )`

* **Tealiumに送信（サーバーサイド）**
* **Tealiumアカウント**
  * 任意。
  * サーバーサイドリクエストで使用される`tealium_account`を上書きします。

* **Tealiumプロファイル**
  * 任意。
  * サーバーサイドリクエストで使用される`tealium_profile`を上書きします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`api_key`|  &lt;ul&gt;&lt;li&gt;Dun &amp; Bradstreetから提供されるAPIキー。&lt;/li&gt;&lt;li&gt;例：`//API_KEY_HERE.d41.co/sync/`&lt;/li&gt;&lt;/ul&gt; |
|`data_key`|  &lt;ul&gt;&lt;li&gt;getData呼び出しで提供されるAPIキー。&lt;/li&gt;&lt;li&gt;APIキーを使用する場合は空白にします。&lt;/li&gt;&lt;li&gt;例：`dnbvid.getData(&#39;DATA_KEY_HERE&#39;,&#39;json&#39;,&#39;T&#39;... )`&lt;/li&gt;&lt;/ul&gt; |
|`send_to_tealium`|  &lt;ul&gt;&lt;li&gt;Tealiumに送信&lt;/li&gt;&lt;li&gt;Dun &amp; Bradstreetから受け取ったデータがTealiumサーバーサイドに利用可能になります。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealiumアカウント&lt;/li&gt;&lt;li&gt;任意。&lt;/li&gt;&lt;li&gt;サーバーサイドリクエストで使用される`tealium_account`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル&lt;/li&gt;&lt;li&gt;任意。&lt;/li&gt;&lt;li&gt;サーバーサイドリクエストで使用される`tealium_profile`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
