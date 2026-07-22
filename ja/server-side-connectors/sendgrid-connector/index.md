---
title: SendGridコネクタ構成ガイド
description: この記事では、SendGridコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/sendgrid-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|Upsert Contact| ✓| ✗|
|Remove Contact| ✓| ✗|
|Send Email| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要](https://docs.tealium.com/ja/server-side/connectors/manage/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**  
SendGridコネクタが使用するAPIキー。このコネクタはAPIキーに対して以下の権限が必要です：

  * **マーケティングキャンペーン:** フルアクセス
  * **メール送信:** フルアクセス
  * **テンプレートエンジン:** 読み取りアクセス

SendGrid APIキーに関する詳細情報は、次のドキュメンテーションを参照してください：[SendGrid APIキー](https://docs.sendgrid.com/ui/account-and-settings/api-keys)。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Upsert Contact

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Address Line 1|
|Address Line 2|
|Alternate Emails|
|City|
|Country|
|Email| (必須)|
|First Name|
|Last Name|
|Postal Code|
|State Province Region|
|Contact List Ids| 任意: リストID。このコンタクトが追加されるリストIDの文字列の配列。|

### アクション - Remove Contact

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Contact Id|
|Email|

### アクション - Send Email

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Name| (必須)|
|Send At|
|Send To All|
|Custom Unsubscribe Url|
|Editor|
|Generate Plain Content|
|HTML Content|
|Ip Pool|
|Plain Content|
|Subject|
|Categories| 任意: カテゴリ。このSingle Sendに関連付けるカテゴリ。最大アイテム数10。|
|Contact List Ids| 任意: コンタクトリストID。Single Sendを受け取る受信者リストID。最大アイテム数10。|
|Segments| 任意: セグメント。Single Sendを受け取る受信者セグメントID。最大アイテム数10。|
|Design Id| 任意: デザインID。**Html Content**、**Plain Content**、および/または**subject**の代わりにデザインIDを使用できます。|
|Sender Id| 任意: 送信者ID。確認済みの送信者のID。|
|Suppression Group Id| 任意: 抑制グループID。受信者が退会するための抑制グループのID — これまたは**Custom Unsubscribe Url**を提供する必要があります。|

