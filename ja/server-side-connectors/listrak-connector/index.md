---
title: Listrakコネクタ構成ガイド
description: この記事では、Listrakコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/listrak-connector/
---
## 必要条件

* ListrakクライアントID
* Listrakクライアントシークレット

## サポートされているアクション

|**アクション名**| **オーディエンスにトリガー**| **ストリームにトリガー**|
|---| ---| ---|
|連絡先の作成または更新| ✓| ✗|
|連絡先の購読| ✓| ✗|
|連絡先の購読解除| ✓| ✗|
|トランザクションメッセージの送信| ✓| ✗|

## 構成の構成&lt;br&gt;

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[Connector Overview]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **クライアントID**
  * Listrakアカウントの統合に関連付けられたクライアントID。
  * クライアントIDは、Listrakダッシュボードの統合マネージャーで見つけることができます。
  * コネクタを完全に利用するためには、次のアクセスレベルが構成されていることを確認してください：`ListContactSegmentationMessageEvent`
  * 実装の詳細については、[Listrak Authentication](https://api.listrak.com/email#section/Authentication)を参照してください。

* **クライアントシークレット**
  * Listrakアカウントの統合に関連付けられたクライアントシークレット。
  * クライアントシークレットは、Listrakダッシュボードの**統合マネージャー**で見つけることができます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 連絡先の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;更新する場合は連絡先が所属するリスト、作成する場合は連絡先を追加するリスト。&lt;/li&gt;&lt;/ul&gt; |
|連絡先メール|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|ダブルオプトイン|  &lt;ul&gt;&lt;li&gt;新しい連絡先が作成される場合、ダブルオプトインメールを送信するかどうか。&lt;/li&gt;&lt;/ul&gt; |
|イベント|  &lt;ul&gt;&lt;li&gt;連絡先が作成または更新された後に発生するべきイベント。&lt;/li&gt;&lt;/ul&gt; |
|新しいメール|  &lt;ul&gt;&lt;li&gt;既存の連絡先を更新する場合、連絡先のメールアドレスはこの値に変更されます。&lt;/li&gt;&lt;/ul&gt; |
|更新タイプ|  &lt;ul&gt;&lt;li&gt;既存の連絡先を更新する場合、提出されたセグメンテーションフィールドに対して実行される更新のタイプ。&lt;/li&gt;&lt;li&gt;構成されていない場合、デフォルト値は`Update`です。&lt;/li&gt;&lt;/ul&gt; |
|セグメンテーショングループ|  &lt;ul&gt;&lt;li&gt;セグメンテーションフィールドのリストを含むセグメンテーショングループ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先の購読

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;連絡先が所属するリスト。&lt;/li&gt;&lt;/ul&gt; |
|連絡先メール|  &lt;ul&gt;&lt;li&gt;必須**。**&lt;/li&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|イベント|  &lt;ul&gt;&lt;li&gt;連絡先が購読した後に発生するべきイベント。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先の購読解除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先が所属するリスト。&lt;/li&gt;&lt;/ul&gt; |
|連絡先メール|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|イベント|  &lt;ul&gt;&lt;li&gt;連絡先が購読解除した後に発生するべきイベント。&lt;/li&gt;&lt;/ul&gt; |

### アクション - トランザクションメッセージの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|連絡先リスト|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先が所属するリスト。&lt;/li&gt;&lt;/ul&gt; |
|連絡先メール|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|トランザクションメッセージ|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;連絡先に送信するメッセージ。&lt;/li&gt;&lt;/ul&gt; |
|セグメンテーショングループ|  &lt;ul&gt;&lt;li&gt;セグメンテーションフィールドのリストを含むセグメンテーショングループ。&lt;/li&gt;&lt;/ul&gt; |

## ベンダー文書

* [Getting Started](https://api.listrak.com/email)

## APIs

* [Listrak Create or Update Contact HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak Subscribe HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak Unsubscribe HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak Send Transactional Message HTTP API](https://api.listrak.com/email#operation/TransactionalMessage_PostTransactionalMessageSend)

