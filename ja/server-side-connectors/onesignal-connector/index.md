---
title: OneSignalコネクタ構成ガイド
description: この記事では、OneSignalコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/onesignal-connector/
---
## コネクタのアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|プレイヤーIDに基づくプッシュ通知の送信| ✓| ✗|
|プレイヤーIDに基づくメールの送信| ✓| ✗|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **REST APIキー**
  * 「Keys &amp; IDs」セクションに記載されている、アプリ固有の操作（アプリのユーザーの取得、ユーザーの変更、通知の取得、通知の送信）に使用するREST APIキー。
  * 詳細については、[OneSignalのチームとキー](https://documentation.onesignal.com/docs/accounts-and-keys#section-keys-ids)を参照してください。

## アクション構成 - パラメータとオプション

**Continue**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - プレイヤーIDに基づくプッシュ通知の送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリID| <ul><li>「Keys &amp; IDs」で確認できるOneSignalアプリケーションID。</li><li>詳細については、[通知の作成](https://documentation.onesignal.com/reference#create-notification)を参照してください。</li></ul> |
|プレイヤーID| 通知の送信先となる特定のプレイヤー。|
|テンプレートID| OneSignalアカウント内のプッシュ通知テンプレートのID。|

### アクション - プレイヤーIDに基づくメールの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリID| <ul><li>「Keys &amp; IDs」で確認できるOneSignalアプリケーションID。</li><li>詳細については、[通知の作成](https://documentation.onesignal.com/reference#create-notification)を参照してください。</li></ul> |
|プレイヤーID| 通知の送信先となる特定のプレイヤー。|
|メールの件名| メールの件名。|
|メール本文| メールの本文。|