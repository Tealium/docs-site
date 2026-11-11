---
title: Listrakコネクタ構成ガイド
description: この記事では、Listrakコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/listrak-connector/
---
## 要件

* ListrakクライアントID
* Listrakクライアントシークレット

## サポートされているアクション

|**アクション名**| **オーディエンスでのトリガー**| **ストリームでのトリガー**|
|---| ---| ---|
|連絡先の作成または更新| ✓| ✗|
|連絡先の購読登録| ✓| ✗|
|連絡先の購読解除| ✓| ✗|
|トランザクションメッセージの送信| ✓| ✗|

## 構成<br>

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

* **クライアントID**
  * Listrakアカウントのインテグレーションに関連付けられたクライアントID。
  * クライアントIDは、ListrakダッシュボードのIntegration Managerで確認できます。
  * コネクタの機能をすべて利用できるように、次のアクセスレベルが構成されていることを確認してください：`ListContactSegmentationMessageEvent`
  * 実装の詳細については、[Listrakの認証](https://api.listrak.com/email#section/Authentication)を参照してください。

* **クライアントシークレット**
  * Listrakアカウントのインテグレーションに関連付けられたクライアントシークレット。
  * クライアントシークレットは、Listrakダッシュボードの**Integration Manager**で確認できます。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — 連絡先の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  <ul><li>（必須）更新する場合は連絡先が属するリスト、作成する場合は連絡先を追加するリスト。</li></ul> |
|連絡先のメールアドレス|  <ul><li>（必須）連絡先のメールアドレス。</li></ul> |
|ダブルオプトイン|  <ul><li>新しい連絡先を作成する場合に、ダブルオプトインメールを送信するかどうか。</li></ul> |
|イベント|  <ul><li>連絡先の作成または更新後に発生させるイベント。</li></ul> |
|新しいメールアドレス|  <ul><li>既存の連絡先を更新する場合、連絡先のメールアドレスがこの値に変更されます。</li></ul> |
|更新タイプ|  <ul><li>既存の連絡先を更新する場合、送信されたセグメンテーションフィールドに対して実行する更新のタイプ。</li><li>構成されていない場合、デフォルト値は`Update`です。</li></ul> |
|セグメンテーショングループ|  <ul><li>セグメンテーションフィールドのリストを含むセグメンテーショングループ。</li></ul> |

### アクション — 連絡先の購読登録

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  <ul><li>（必須）連絡先が属するリスト。</li></ul> |
|連絡先のメールアドレス|  <ul><li>（必須）連絡先のメールアドレス。</li></ul> |
|イベント|  <ul><li>連絡先の購読登録後に発生させるイベント。</li></ul> |

### アクション — 連絡先の購読解除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  <ul><li>（必須）連絡先が属するリスト。</li></ul> |
|連絡先のメールアドレス|  <ul><li>（必須）連絡先のメールアドレス。</li></ul> |
|イベント|  <ul><li>連絡先の購読解除後に発生させるイベント。</li></ul> |

### アクション — トランザクションメッセージの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  <ul><li>（必須）連絡先が属するリスト。</li></ul> |
|連絡先のメールアドレス|  <ul><li>（必須）連絡先のメールアドレス。</li></ul> |
|トランザクションメッセージ|  <ul><li>（必須）連絡先に送信するメッセージ。</li></ul> |
|セグメンテーショングループ|  <ul><li>セグメンテーションフィールドのリストを含むセグメンテーショングループ。</li></ul> |

## ベンダーのドキュメント

* [はじめに](https://api.listrak.com/email)

## API

* [Listrak連絡先作成または更新HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak購読登録HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak購読解除HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrakトランザクションメッセージ送信HTTP API](https://api.listrak.com/email#operation/TransactionalMessage_PostTransactionalMessageSend)