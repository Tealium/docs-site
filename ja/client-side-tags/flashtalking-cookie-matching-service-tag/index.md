---
title: Flashtalking Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでFlashtalking Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/flashtalking-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* マッピングを使用して、標準の構成値を上書きします。
* カスタムマッピングは、TealiumへのCookie同期リクエストに含まれます。
* このタグはセッションごとに1回だけ実行されます。その実行の制御には`utag_main_flashtalking_cms_<tag UID>` Cookieが使用されます。
* 次のサーバーサイド属性をTealiumに送信します。
  * `flashtalking_id`

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **Flashtalkingキー**
  * Flashtalkingキー。
* **Tealiumアカウント**：
  * 任意
  * サーバーサイドリクエストで使用される`tealium_account`を上書きします。
* **Tealiumプロファイル**：
  * 任意
  * サーバーサイドリクエストで使用される`tealium_profile`を上書きします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`key`|  <ul><li>Flashtalkingキー</li></ul> |
|`tealium_account`|  <ul><li>Tealiumアカウント</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル</li></ul> |
|`tealium_event`|  <ul><li>Tealiumイベント</li></ul> |