---
title: OneSignalコネクタ構成ガイド
description: この記事では、OneSignalコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/onesignal-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|プレイヤーIDに基づいてプッシュ通知を送信| ✓| ✗|
|プレイヤーIDに基づいてメールを送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **REST APIキー**
  * アプリ固有の操作（アプリのユーザーの取得、ユーザーの変更、通知の取得、通知の送信）のためのREST APIキーは、キー＆IDセクションに記載されています。
  * 詳細については、[OneSignalチームとキー](https://documentation.onesignal.com/docs/accounts-and-keys#section-keys-ids)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - プレイヤーIDに基づいてプッシュ通知を送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|App ID|  <ul><li>キー＆IDで見つけることができるOneSignalアプリケーションID。</li><li>詳細については、[通知の作成](https://documentation.onesignal.com/reference#create-notification)を参照してください。</li></ul> |
|Player ID| 通知を送信する特定のプレイヤー。|
|Template ID| OneSignalアカウント内のプッシュテンプレートのID。|

### アクション - プレイヤーIDに基づいてメールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|App ID|  <ul><li>キー＆IDで見つけることができるOneSignalアプリケーションID。</li><li>詳細については、[通知の作成](https://documentation.onesignal.com/reference#create-notification)を参照してください。</li></ul> |
|Player ID| 通知を送信する特定のプレイヤー。|
|Email Subject| メールの件名。|
|Email Body| メールの本文。|
