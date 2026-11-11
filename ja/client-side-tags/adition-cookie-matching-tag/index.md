---
title: Adition Cookie Matchingタグ構成ガイド
description: この記事では、タグ管理アカウントでAdition Cookie Matchingタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-cookie-matching-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* これはAditionのCookie Matchingバージョンであり、TealiumとAditionの間で訪問ID情報を同期できます。
* このタグは、別のAditionタグと組み合わせて使用します。
* 次のサーバーサイド属性をTealiumに返します。
  * `adition_user_id`

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Tealiumアカウント**
  * Tealiumアカウントの名前。
  * 正しいvdataエンドポイントにリダイレクトするために必要です。
  * デフォルトでは、タグ管理アカウント名が使用されます。

* **Tealiumプロファイル**
  * Tealiumプロファイルの名前。
  * 正しいvdataエンドポイントにリダイレクトするために必要です。
  * デフォルトでは、タグ管理プロファイル名が使用されます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`|  <ul><li>Tealiumアカウント</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル</li></ul> |