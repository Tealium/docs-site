---
title: iSpot TV Cookie Matching Serviceタグ構成ガイド
description: この記事では、iSpot TV Cooke Matching Serviceタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/ispot-tv-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細は、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* このタグは、iSpot IDの取得に成功した場合、セッションごとに一度だけトリガーされます。
* 空白の場合、TealiumアカウントとTealiumプロファイルは、現在のアカウントとプロファイルで自動的に入力されます。
* 結果として生成されるサーバーサイドの呼び出しは、以下のパラメータを送信します：
  * `tealium_cookie_sync`: true
  * `tealium_account` : あなたのTealiumアカウント
  * `tealium_profile` : あなたのTealiumプロファイル
  * `tealium_visitor_id` : 訪問のTealium ID
  * `tealium_event` : `cookie_match_ispot`
  * `ispot_id` : 訪問のiSpot ID
  * `tealium_datasource` : 構成されている場合、TealiumデータソースID
  * `tealium_trace_id` : 構成されている場合、Tealium Trace ID

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Site ID**: iSpotから提供されるサイトID
* **Tealium Account**: (オプション) あなたのTealiumアカウント
* **Tealium Profile**: (オプション) あなたのTealiumプロファイル
* **Tealium Data Source ID**: (オプション) あなたのTealium Data Source ID

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|Site ID| (site\_id)|
|Tealium Account| (tealium\_account)|
|Tealium Profile| (tealium\_profile)|
|Tealium Data Source ID| (tealium\_datasource)|
