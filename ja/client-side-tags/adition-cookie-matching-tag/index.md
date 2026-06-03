---
title: Adition Cookie Matchingタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdition Cookie Matchingタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-cookie-matching-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* これはAditionのCookie Matchingバージョンで、TealiumとAdition間で訪問ID情報を同期することができます。
* このタグは別のAditionタグと連携して使用されます。
* 以下のサーバーサイド属性をTealiumに戻送します：
  * `adition_user_id`

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Adition Cookie Matchingタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Tealiumアカウント**
  * あなたのTealiumアカウントの名前。
  * 正しいvdataエンドポイントにリダイレクトするために必要です。
  * デフォルトでは、あなたのTealium iQアカウント名になります。

* **Tealiumプロファイル**
  * あなたのTealiumプロファイルの名前。
  * 正しいvdataエンドポイントにリダイレクトするために必要です。
  * デフォルトでは、あなたのTealium iQプロファイル名になります。

## データマッピング

マッピングとは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealiumアカウント&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル&lt;/li&gt;&lt;/ul&gt; |