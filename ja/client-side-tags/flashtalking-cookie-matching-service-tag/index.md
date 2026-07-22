---
title: Flashtalking Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFlashtalking Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/flashtalking-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50+へのアップグレード時のtealium_visitor_idの考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグのヒント

* 標準の構成値を上書きするためにマッピングを使用します。
* カスタムマッピングはTealiumへのクッキー同期リクエストに含まれます。
* このタグはセッションごとに一度だけ実行され、その実行は`utag_main_flashtalking_cms_<tag UID>`クッキーで制御されます。
* 以下のサーバーサイド属性をTealiumに戻します：
  * `flashtalking_id`

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Flashtalking Key**
  * あなたのFlashtalking Key。
* **Tealium Account**:
  * 任意
  * サーバーサイドリクエストに使用される`tealium_account`を上書きします。
* **Tealium Profile**:
  * 任意
  * サーバーサイドリクエストに使用される`tealium_profile`を上書きします。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`key`|  <ul><li>Flashtalking Key</li></ul> |
|`tealium_account`|  <ul><li>Tealium Account</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile</li></ul> |
|`tealium_event`|  <ul><li>Tealium Event</li></ul> |
