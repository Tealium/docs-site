---
title: Sendwithusコネクタ構成ガイド
url: https://docs.tealium.com/ja/server-side-connectors/sendwithus-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|メールを送る| ✓| ✗|
|新規顧客を作成する| ✓| ✗|
|顧客を削除する| ✓| ✗|
|顧客に対してドリップキャンペーンを有効にする| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**
  * あなたのAPIキーはSendwithusアカウントで見つけることができます。
  * 詳細については、[Sendwithus認証](https://support.sendwithus.com/api/#authentication&amp;quot;&amp;gt;https://support.sendwithus.com/api/#authentication)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - メールを送る

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|テンプレート|  &lt;ul&gt;&lt;li&gt;送信するテンプレートのID。&lt;/li&gt;&lt;li&gt;詳細については、[Send API](https://support.sendwithus.com/api/#sendapi)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|受信者のアドレス|  &lt;ul&gt;&lt;li&gt;受信者のメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|受信者の名前|  &lt;ul&gt;&lt;li&gt;受信者の名前。&lt;/li&gt;&lt;/ul&gt; |
|送信者のアドレス|  &lt;ul&gt;&lt;li&gt;送信者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|返信先|  &lt;ul&gt;&lt;li&gt;送信者の返信先アドレス。&lt;/li&gt;&lt;/ul&gt; |
|送信者の名前|  &lt;ul&gt;&lt;li&gt;送信者の名前。&lt;/li&gt;&lt;/ul&gt; |
|テンプレートデータ|  &lt;ul&gt;&lt;li&gt;メールテンプレートデータ。&lt;/li&gt;&lt;/ul&gt; |
|ESPアカウント|  &lt;ul&gt;&lt;li&gt;このメールを送信するESPアカウントのID。&lt;/li&gt;&lt;/ul&gt; |
|ロケール|  &lt;ul&gt;&lt;li&gt;送信するテンプレートのロケール。&lt;/li&gt;&lt;/ul&gt; |
|バージョン名|  &lt;ul&gt;&lt;li&gt;送信するテンプレートバージョンの名前。&lt;/li&gt;&lt;li&gt;A/Bテストを上書きします。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 新規顧客を作成する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  &lt;ul&gt;&lt;li&gt;顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;詳細については、[Customers API](https://support.sendwithus.com/api/#customersapi)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|ロケール|  &lt;ul&gt;&lt;li&gt;顧客のロケール。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 顧客を削除する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  &lt;ul&gt;&lt;li&gt;削除する顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;詳細については、[Customers API](https://support.sendwithus.com/api/#customersapi)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 顧客に対してドリップキャンペーンを有効にする

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ドリップキャンペーンID|  &lt;ul&gt;&lt;li&gt;顧客に対して有効にするドリップキャンペーンのID。&lt;/li&gt;&lt;li&gt;詳細については、[Customers API](https://support.sendwithus.com/api/#customersapi)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|受信者のアドレス|  &lt;ul&gt;&lt;li&gt;受信者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|受信者の名前|  &lt;ul&gt;&lt;li&gt;受信者の名前。&lt;/li&gt;&lt;/ul&gt; |
|送信者のアドレス|  &lt;ul&gt;&lt;li&gt;送信者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|返信先|  &lt;ul&gt;&lt;li&gt;送信者の返信先アドレス。&lt;/li&gt;&lt;/ul&gt; |
|メールデータ|  &lt;ul&gt;&lt;li&gt;メールテンプレートデータ。&lt;/li&gt;&lt;/ul&gt; |
|ESPアカウント|  &lt;ul&gt;&lt;li&gt;このメールを送信するESPアカウントのID。&lt;/li&gt;&lt;/ul&gt; |
|ロケール|  &lt;ul&gt;&lt;li&gt;メールを送信するロケール。&lt;/li&gt;&lt;/ul&gt; |
