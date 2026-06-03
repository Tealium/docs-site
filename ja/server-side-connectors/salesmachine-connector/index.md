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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIトークン**  
SalesmachineプロジェクトのAPI資格情報は、Salesmachineダッシュボードの**管理 &amp;gt; APIキー**で見つけることができます。詳細については、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#install)をご覧ください。
* **APIシークレット**  
SalesmachineプロジェクトのAPI資格情報は、Salesmachineダッシュボードの**管理 &amp;gt; APIキー**で見つけることができます。詳細については、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#install)をご覧ください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 連絡先の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先UID|  &lt;ul&gt;&lt;li&gt;連絡先を参照する一意の識別子。&lt;/li&gt;&lt;li&gt;データベースIDやメールアドレスなど、アプリケーション内の一意のIDと一致する必要があります。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#contact)をご覧ください。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;追加または更新する連絡先の属性。&lt;/li&gt;&lt;li&gt;`Title`、`Registered At`、`Position`など、任意のパラメータを送信できます。&lt;/li&gt;&lt;/ul&gt; |

### アクション - イベントの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先UID|  &lt;ul&gt;&lt;li&gt;連絡先を参照する一意の識別子。&lt;/li&gt;&lt;li&gt;データベースIDやメールアドレスなど、アプリケーション内の一意のIDと一致する必要があります。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、[Salesmachineのドキュメンテーション](https://docs.salesmachine.io/#event)をご覧ください。&lt;/li&gt;&lt;/ul&gt; |
|イベントUID|  &lt;ul&gt;&lt;li&gt;イベント名。&lt;/li&gt;&lt;/ul&gt; |
|イベントデータ|  &lt;ul&gt;&lt;li&gt;イベントに関連する追加の属性。&lt;/li&gt;&lt;li&gt;任意のパラメータを送信できます。Salesmachineはパラメータタイプを自動的に検出することに注意してください。&lt;/li&gt;&lt;li&gt;タイムスタンプには、Unixエポックからの秒数またはミリ秒数（整数）またはISO 8601の日付（文字列）を使用してください。&lt;/li&gt;&lt;/ul&gt; |
