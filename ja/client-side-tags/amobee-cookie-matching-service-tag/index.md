---
title: Amobee Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでAmobee Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amobee-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* 次のサーバーサイド属性をTealiumに返します。
  * `amobee_id`
* 空白のままにすると、Tealiumのアカウント名とプロファイル名が自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* Amobeeトークン（お客様のAmobeeトークン）
* Tealiumアカウント：
* Tealiumプロファイル

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`amobee_token`| <ul><li>Amobeeトークン</li><li>Amobeeから提供されたお客様のAmobeeトークン。</li></ul> |
|`tealium_account`| <ul><li>Tealiumアカウント名</li></ul> |
|`tealium_profile`| <ul><li>Tealiumプロファイル名</li></ul> |