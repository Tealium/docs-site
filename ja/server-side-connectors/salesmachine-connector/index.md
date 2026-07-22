---
title: Salesmachineコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでSalesmachineコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesmachine-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|連絡先の作成または更新| ✓| ✗|
|イベントの送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIトークン**  
SalesmachineプロジェクトのAPI資格情報は、Salesmachineダッシュボードの**管理 &gt; APIキー**で見つけることができます。詳細については、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#install)をご覧ください。
* **APIシークレット**  
SalesmachineプロジェクトのAPI資格情報は、Salesmachineダッシュボードの**管理 &gt; APIキー**で見つけることができます。詳細については、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#install)をご覧ください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 連絡先の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先UID|  <ul><li>連絡先を参照する一意の識別子。</li><li>データベースIDやメールアドレスなど、アプリケーション内の一意のIDと一致する必要があります。</li><li>このエンドポイントに関する詳細情報は、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#contact)をご覧ください。</li></ul> |
|属性|  <ul><li>追加または更新する連絡先の属性。</li><li>`Title`、`Registered At`、`Position`など、任意のパラメータを送信できます。</li></ul> |

### アクション - イベントの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先UID|  <ul><li>連絡先を参照する一意の識別子。</li><li>データベースIDやメールアドレスなど、アプリケーション内の一意のIDと一致する必要があります。</li><li>このエンドポイントに関する詳細情報は、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#event)をご覧ください。</li></ul> |
|イベントUID|  <ul><li>イベント名。</li></ul> |
|イベントデータ|  <ul><li>イベントに関連する追加の属性。</li><li>任意のパラメータを送信できます。Salesmachineはパラメータタイプを自動的に検出することに注意してください。</li><li>タイムスタンプには、Unixエポックからの秒数またはミリ秒数（整数）またはISO 8601の日付（文字列）を使用してください。</li></ul> |
