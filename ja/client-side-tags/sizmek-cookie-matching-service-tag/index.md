---
title: Sizmek Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでSizmek Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sizmek-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## 仕組み

Sizmek Cookie Matching Serviceを使用すると、Tealium訪問を識別するCookieと、Sizmekでユーザーを識別するCookieを関連付けることができます。

## タグに関するヒント

* このタグは、Tealium訪問セッションごとに1回のみ配信されます。
* 空白のままにすると、Tealiumアカウントとプロファイルが自動的に入力されます。
* 次のサーバーサイド属性をTealiumに返します。
  * `sizmek_id`

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Sizmek UUID**
  * （必須）Sizmekから提供された一意のID。

* **Tealiumアカウント**
  * （必須）Tealiumアカウント名。

* **Tealiumプロファイル**
  * （必須）Tealiumプロファイル名。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`sizmek_uuid`|Sizmek ID|
|`tealium_account`|Tealiumアカウント名|
|`tealium_profile`|Tealiumプロファイル名|