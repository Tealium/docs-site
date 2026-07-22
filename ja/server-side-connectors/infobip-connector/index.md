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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
|From|  <ul><li>送信者IDを表し、英数字または数字であることができます。</li><li>英数字の送信者IDの長さは3から11文字の間である必要があります。</li><li>例：`CompanyName`。</li><li>数字の送信者IDの長さは3から14文字の間である必要があります。</li><li>詳細については、[Infobipのドキュメンテーション](https://dev.infobip.com/send-sms/single-sms-message)を参照してください。</li></ul> |
|To|  <ul><li>メッセージの宛先アドレス。</li><li>宛先アドレスは国際形式でなければなりません。</li><li>例：`41793026727`</li></ul> |
|Text|  <ul><li>送信されるメッセージのテキスト。</li></ul> |

### アクション - プッシュ通知を送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|From|  <ul><li>メッセージを送信するために使用するPUSHアプリケーションコード。</li><li>アプリケーションコードは、あなたのモバイルアプリケーションをInfobipプラットフォームで作成したアプリケーションプロファイルにリンクするアプリケーション識別子です。</li><li>モバイルアプリケーションにMobile Messaging SDKを実装したら、アプリケーションコードをMobile Messaging SDK構成に挿入する必要があります。詳細については、[シングルプッシュ通知を送信](https://dev.infobip.com/push-messaging/send-single-push-notification)を参照してください。</li></ul> |
|Push Registration ID|  <ul><li>Push Registration Idは、アプリケーションインスタンスと特定のデバイスを識別する一意のIDです。</li><li>以下のうち**一つだけ**を含めてください：<ul><li>Push Registration ID</li><li>External User ID</li><li>電話番号</li><li>メール</li></ul> </li></ul> |
|External User ID|  <ul><li>ユーザープロファイルに構成された外部ユーザーID。</li></ul> |
|Phone Number|  <ul><li>国際形式のMSISDN。</li><li>例：`41793026727`</li></ul> |
|Email|  <ul><li>ユーザープロファイルに提供されている場合のユーザーのメール。</li></ul> |
|Text|  <ul><li>送信されるメッセージのテキスト。</li></ul> |
|Sent At|  <ul><li>スケジュールされたプッシュ通知に使用されます。</li><li>メッセージはスケジュールされた時間に送信されます。</li></ul> |
|Custom Payload|  <ul><li>プッシュメッセージと一緒に配信できる追加のデータ。</li></ul> |
|Notification Options|  <ul><li>通知オプションを含むJSONオブジェクト。</li></ul> |
|Validity Period|  <ul><li>メッセージの有効期間、時間で表現されます。</li><li>期間が経過すると、メッセージの送信が許可されなくなるか、Cloud（APNSまたはFCM）で保留中のメッセージがキャンセルされます。</li><li>デフォルト値は48時間です。</li><li>最小値は30秒です。</li><li>最大値は72時間です。</li></ul> |
|Notify URL|  <ul><li>配信レポートが送信されるあなたのコールバックサーバー上のURL。</li><li>詳細については、[Infobipのドキュメンテーション](https://dev.infobip.com/push-messaging/delivery-reports-on-notify-url)を参照してください。</li></ul> |
|Callback Data|  <ul><li>Notify URLに送信される追加のクライアントデータ。</li><li>最大値は200文字です。</li></ul> |
|Target Only Primary Devices|  <ul><li>`true`に構成すると、プライマリデバイスとしてマークされたプッシュデバイスにのみメッセージが送信されます。</li><li>デフォルトでは、メッセージはすべての対象デバイスに送信されます。これには、プライマリと非プライマリの両方が含まれます。</li></ul> |