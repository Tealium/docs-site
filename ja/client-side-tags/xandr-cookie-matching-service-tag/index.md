---
title: Xandr Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでXandr Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/xandr-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Xandr Cookie Matching Serviceを使用すると、購入者はTealium訪問を識別するCookieと、Xandrのユーザーを識別するCookieを関連付けることができます。

## タグに関するヒント

* このタグは、Tealium訪問セッションごとに一度だけ実行されます。
* 次のサーバー側属性をTealiumに返します。
    * `adnxs_uid`
* 空白のままにすると、TealiumアカウントとTealiumプロファイルが自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* Tealiumアカウント
* Tealiumプロファイル

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
| `tealium_account` | Tealiumアカウント|
| `tealium_profile` | Tealiumプロファイル|