---
title: Taboola Cookie Matching Service タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Taboola Cookie Matching Service タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/taboola-cookie-matching-service-tag/
---
 このタグを `utag` バージョン 4.50 以降で使用する場合、`utag.js` の [`always_set_v_id` 構成]() を `true` に構成する必要があります。この構成により、訪問 ID が Cookie 同期のために利用可能になります。詳細については、[utag 4.50 リリースノート]() および [utag 4.50&#43; へのアップグレード時の tealium_visitor_id に関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-) を参照してください。

## タグのヒント

* このタグはデフォルトでサーバーサイド属性 `taboola_id` に Taboola ID を送信しますが、これはカスタマイズ可能です。
* ファーストパーティドメインをサポートします。
* このタグはセッションごとに一度だけ発火します。

EventStream での Cookie マッチングについての詳細は、[EventStream での永続的な Cookie マッチングについての理解]() を参照してください。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する一般的な手順については、[タグ概要]() の記事を読んでください。

タグを追加する際に、以下の構成を構成します：

* **Tealium アカウント**
    * Tealium Collect エンドポイントで使用されるアカウント。
    * Cookie 同期リクエストを別のアカウントに送る必要がある場合にこの値を構成します。
    * デフォルト：このタグが公開されているアカウント。
* **Tealium プロファイル**
    * Tealium Collect エンドポイントで使用されるプロファイル。
    * 複数のクライアントサイドプロファイルが単一のサーバーサイドプロファイルにデータを送信する場合にこの値を構成します。
    * デフォルト：このタグが公開されているプロファイル。
* **Tealium Collect エンドポイント**
    * Tealium との Cookie 同期に使用されるエンドポイント。
    * デフォルト値を上書きするためにカスタムドメインを入力します。この値は通常、`collect.yourdomain.com/event` のようなファーストパーティドメインに構成されます。
    * デフォルト：`collect.tealiumiq.com/event`
* **Taboola ID 属性名**
    * Taboola ID を含むサーバーサイド属性のカスタム名を構成します。
    * デフォルト：`taboola_id`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]() を参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信プロセスです。変数をタグ宛先にマッピングする方法についての指示は、[データマッピング](/ja/iq-tag-management/data-mappings/manage/) を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`| Tealium アカウント|
|`tealium_profile`| Tealium プロファイル|
|`taboola_id`| Taboola ID|
