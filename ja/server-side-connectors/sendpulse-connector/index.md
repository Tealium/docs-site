---
title: SendPulseコネクタ構成ガイド
description: この記事では、SendPulseコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/sendpulse-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|メーリングリストにメールを追加（シングルオプトイン）| ✓| ✗|
|メーリングリストにメールを追加（ダブルオプトイン）| ✓| ✗|
|メーリングリストからメールを削除| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **クライアントID**
  * SendPulseのAPIドキュメンテーションの[認証セクション](https://sendpulse.com/integrations/api)で、OAuth2認証情報についての情報を参照してください。

* **クライアントシークレット**
  * 必須。
  * あなたのウェブアプリケーションクライアントシークレットを提供します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - メーリングリストにメールを追加（シングルオプトイン）

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;ユーザーを追加するメーリングリストのID。&lt;/li&gt;&lt;li&gt;詳細については、[SendPulseのドキュメンテーション](https://sendpulse.com/integrations/api/bulk-email)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;リストに追加するユーザーのメールアドレス。&lt;/li&gt;&lt;/ul&gt; |

### アクション - メーリングリストにメールを追加（ダブルオプトイン）

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;ユーザーを追加するメーリングリストのID。&lt;/li&gt;&lt;li&gt;詳細については、[SendPulseのドキュメンテーション](https://sendpulse.com/integrations/api/bulk-email)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|送信者メール|  &lt;ul&gt;&lt;li&gt;あなたの送信者メール。&lt;/li&gt;&lt;li&gt;送信者メールアドレスは、SendPulseアカウントの**メール &gt; サービス構成 &gt; 送信元アドレス**メニューで有効化する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;リストに追加するユーザーのメールアドレス。&lt;/li&gt;&lt;/ul&gt; |

### アクション - メーリングリストからメールを削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;連絡先を削除するリストのID。&lt;/li&gt;&lt;li&gt;詳細については、[SendPulseのドキュメンテーション](https://sendpulse.com/integrations/api/bulk-email)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;リストから削除するメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
