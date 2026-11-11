---
title: Criteo Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでCriteo Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/criteo-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に必要な訪問IDが使用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Criteo Cookie Matching Serviceを使用すると、購入者はTealium訪問を識別するCookieと、Criteoでユーザーを識別するCookieを関連付けることができます。

## タグに関するヒント

* 空白のままにすると、Tealiumアカウントとプロファイルが自動的に入力されます。
* 次のサーバーサイド属性をTealiumに送り返します。
  * `criteo_user_id`

Event StreamingでのCookieマッチングの詳細については、[Event Streamingにおける永続的Cookieマッチングについて](https://docs.tealium.com/about-persistent-cookie-matching/)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Tealiumアカウント**：（任意）Tealiumアカウント。
* **Tealiumプロファイル**：（任意）Tealiumプロファイル。
* **同期間隔（日数）**：（任意）IDを再確認する頻度。この値のデフォルトは7日です。
* **データソースキー**：（任意）サーバーサイド構成のデータソースキー。
* **`/event`エンドポイントを使用**：データを`/event`エンドポイントに送信します。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|Tealiumアカウント（`tealium_account`）|［文字列］|
|Tealiumプロファイル（`tealium_profile`）|［文字列］|
|同期間隔（日数）（`days_between_syncs`）|［数値］|
|データソースキー（`tealium_datasource`）|［文字列］|
|`/event`エンドポイントを使用（`use_event_endpoint`）|［ブール値］|