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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**
  * あなたのAPIキーはSendwithusアカウントで見つけることができます。
  * 詳細については、[Sendwithus認証](https://support.sendwithus.com/api/#authentication&quot;&gt;https://support.sendwithus.com/api/#authentication)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - メールを送る

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|テンプレート|  <ul><li>送信するテンプレートのID。</li><li>詳細については、[Send API](https://support.sendwithus.com/api/#sendapi)を参照してください。</li></ul> |
|受信者のアドレス|  <ul><li>受信者のメールアドレス</li></ul> |
|受信者の名前|  <ul><li>受信者の名前。</li></ul> |
|送信者のアドレス|  <ul><li>送信者のメールアドレス。</li></ul> |
|返信先|  <ul><li>送信者の返信先アドレス。</li></ul> |
|送信者の名前|  <ul><li>送信者の名前。</li></ul> |
|テンプレートデータ|  <ul><li>メールテンプレートデータ。</li></ul> |
|ESPアカウント|  <ul><li>このメールを送信するESPアカウントのID。</li></ul> |
|ロケール|  <ul><li>送信するテンプレートのロケール。</li></ul> |
|バージョン名|  <ul><li>送信するテンプレートバージョンの名前。</li><li>A/Bテストを上書きします。</li></ul> |

### アクション - 新規顧客を作成する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  <ul><li>顧客のメールアドレス。</li><li>詳細については、[Customers API](https://support.sendwithus.com/api/#customersapi)を参照してください。</li></ul> |
|ロケール|  <ul><li>顧客のロケール。</li></ul> |

### アクション - 顧客を削除する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  <ul><li>削除する顧客のメールアドレス。</li><li>詳細については、[Customers API](https://support.sendwithus.com/api/#customersapi)を参照してください。</li></ul> |

### アクション - 顧客に対してドリップキャンペーンを有効にする

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ドリップキャンペーンID|  <ul><li>顧客に対して有効にするドリップキャンペーンのID。</li><li>詳細については、[Customers API](https://support.sendwithus.com/api/#customersapi)を参照してください。</li></ul> |
|受信者のアドレス|  <ul><li>受信者のメールアドレス。</li></ul> |
|受信者の名前|  <ul><li>受信者の名前。</li></ul> |
|送信者のアドレス|  <ul><li>送信者のメールアドレス。</li></ul> |
|返信先|  <ul><li>送信者の返信先アドレス。</li></ul> |
|メールデータ|  <ul><li>メールテンプレートデータ。</li></ul> |
|ESPアカウント|  <ul><li>このメールを送信するESPアカウントのID。</li></ul> |
|ロケール|  <ul><li>メールを送信するロケール。</li></ul> |
