---
title: Adition Cookie Matchingタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdition Cookie Matchingタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-cookie-matching-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* これはAditionのCookie Matchingバージョンで、TealiumとAdition間で訪問ID情報を同期することができます。
* このタグは別のAditionタグと連携して使用されます。
* 以下のサーバーサイド属性をTealiumに戻送します：
  * `adition_user_id`

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Adition Cookie Matchingタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

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

マッピングとは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  <ul><li>Tealiumアカウント</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル</li></ul> |