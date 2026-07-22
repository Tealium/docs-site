---
title: Criteo Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでCriteo Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/criteo-cookie-matching-service-tag/
---

<blockquote>
このタグを `utag` バージョン4.50以降で使用する場合、`utag.js` の [`always_set_v_id` 構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を `true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)と[utag 4.50+へのアップグレード時のtealium_visitor_idの考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Criteo Cookie Matching Serviceは、Tealiumの訪問を識別するクッキーと、Criteoのユーザーを識別するクッキーを関連付けることを可能にします。

## タグのヒント

* 空白の場合、Tealiumアカウントとプロファイルは自動的に入力されます。
* 以下のサーバーサイド属性をTealiumに戻します：
  * `criteo_user_id`

EventStreamでのクッキーマッチングについての詳細は、[EventStreamでのPersistent Cookie Matchingの理解](https://docs.tealium.com/about-persistent-cookie-matching/)を参照してください。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法についての一般的な指示については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Tealiumアカウント**：（オプション）あなたのTealiumアカウント。
* **Tealiumプロファイル**：（オプション）あなたのTealiumプロファイル。
* **同期間隔**：（オプション）IDを再確認する頻度。この値はデフォルトで7日間に構成されています。
* **データソースキー**：（オプション）サーバーサイド構成からのデータソースキー。
* **`/event`エンドポイントを使用**：`/event`エンドポイントにデータを送信します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|Tealiumアカウント (`tealium_account`)| [文字列]|
|Tealiumプロファイル (`tealium_profile`)| [文字列]|
|同期間隔 (`days_between_syncs`)| [数値]|
|データソースキー (`tealium_datasource`)| [文字列]|
|`/event`エンドポイントを使用 (`use_event_endpoint`)| [ブール値]|
