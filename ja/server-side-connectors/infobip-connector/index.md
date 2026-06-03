---
title: Infobipコネクタ構成ガイド
description: この記事では、Infobipコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/infobip-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|SMSを送信| ✓| ✗|
|プッシュ通知を送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **ユーザー名**: あなたのInfobipのユーザー名。詳細については、[Infobipセキュリティと認証](https://dev.infobip.com/getting-started/security-and-authorization)を参照してください。
* **パスワード**: あなたのInfobipのパスワード。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - SMSを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|From|  &lt;ul&gt;&lt;li&gt;送信者IDを表し、英数字または数字であることができます。&lt;/li&gt;&lt;li&gt;英数字の送信者IDの長さは3から11文字の間である必要があります。&lt;/li&gt;&lt;li&gt;例：`CompanyName`。&lt;/li&gt;&lt;li&gt;数字の送信者IDの長さは3から14文字の間である必要があります。&lt;/li&gt;&lt;li&gt;詳細については、[Infobipのドキュメンテーション](https://dev.infobip.com/send-sms/single-sms-message)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|To|  &lt;ul&gt;&lt;li&gt;メッセージの宛先アドレス。&lt;/li&gt;&lt;li&gt;宛先アドレスは国際形式でなければなりません。&lt;/li&gt;&lt;li&gt;例：`41793026727`&lt;/li&gt;&lt;/ul&gt; |
|Text|  &lt;ul&gt;&lt;li&gt;送信されるメッセージのテキスト。&lt;/li&gt;&lt;/ul&gt; |

### アクション - プッシュ通知を送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|From|  &lt;ul&gt;&lt;li&gt;メッセージを送信するために使用するPUSHアプリケーションコード。&lt;/li&gt;&lt;li&gt;アプリケーションコードは、あなたのモバイルアプリケーションをInfobipプラットフォームで作成したアプリケーションプロファイルにリンクするアプリケーション識別子です。&lt;/li&gt;&lt;li&gt;モバイルアプリケーションにMobile Messaging SDKを実装したら、アプリケーションコードをMobile Messaging SDK構成に挿入する必要があります。詳細については、[シングルプッシュ通知を送信](https://dev.infobip.com/push-messaging/send-single-push-notification)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Push Registration ID|  &lt;ul&gt;&lt;li&gt;Push Registration Idは、アプリケーションインスタンスと特定のデバイスを識別する一意のIDです。&lt;/li&gt;&lt;li&gt;以下のうち**一つだけ**を含めてください：&lt;ul&gt;&lt;li&gt;Push Registration ID&lt;/li&gt;&lt;li&gt;External User ID&lt;/li&gt;&lt;li&gt;電話番号&lt;/li&gt;&lt;li&gt;メール&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|External User ID|  &lt;ul&gt;&lt;li&gt;ユーザープロファイルに構成された外部ユーザーID。&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;国際形式のMSISDN。&lt;/li&gt;&lt;li&gt;例：`41793026727`&lt;/li&gt;&lt;/ul&gt; |
|Email|  &lt;ul&gt;&lt;li&gt;ユーザープロファイルに提供されている場合のユーザーのメール。&lt;/li&gt;&lt;/ul&gt; |
|Text|  &lt;ul&gt;&lt;li&gt;送信されるメッセージのテキスト。&lt;/li&gt;&lt;/ul&gt; |
|Sent At|  &lt;ul&gt;&lt;li&gt;スケジュールされたプッシュ通知に使用されます。&lt;/li&gt;&lt;li&gt;メッセージはスケジュールされた時間に送信されます。&lt;/li&gt;&lt;/ul&gt; |
|Custom Payload|  &lt;ul&gt;&lt;li&gt;プッシュメッセージと一緒に配信できる追加のデータ。&lt;/li&gt;&lt;/ul&gt; |
|Notification Options|  &lt;ul&gt;&lt;li&gt;通知オプションを含むJSONオブジェクト。&lt;/li&gt;&lt;/ul&gt; |
|Validity Period|  &lt;ul&gt;&lt;li&gt;メッセージの有効期間、時間で表現されます。&lt;/li&gt;&lt;li&gt;期間が経過すると、メッセージの送信が許可されなくなるか、Cloud（APNSまたはFCM）で保留中のメッセージがキャンセルされます。&lt;/li&gt;&lt;li&gt;デフォルト値は48時間です。&lt;/li&gt;&lt;li&gt;最小値は30秒です。&lt;/li&gt;&lt;li&gt;最大値は72時間です。&lt;/li&gt;&lt;/ul&gt; |
|Notify URL|  &lt;ul&gt;&lt;li&gt;配信レポートが送信されるあなたのコールバックサーバー上のURL。&lt;/li&gt;&lt;li&gt;詳細については、[Infobipのドキュメンテーション](https://dev.infobip.com/push-messaging/delivery-reports-on-notify-url)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Callback Data|  &lt;ul&gt;&lt;li&gt;Notify URLに送信される追加のクライアントデータ。&lt;/li&gt;&lt;li&gt;最大値は200文字です。&lt;/li&gt;&lt;/ul&gt; |
|Target Only Primary Devices|  &lt;ul&gt;&lt;li&gt;`true`に構成すると、プライマリデバイスとしてマークされたプッシュデバイスにのみメッセージが送信されます。&lt;/li&gt;&lt;li&gt;デフォルトでは、メッセージはすべての対象デバイスに送信されます。これには、プライマリと非プライマリの両方が含まれます。&lt;/li&gt;&lt;/ul&gt; |