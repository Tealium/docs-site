---
title: SendGrid受信Webhook構成ガイド
description: この記事では、SendGridデータソースを使用してSendGridアカウントにWebhookを作成し、Tealiumに対して実行可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/sendgrid/
---## 前提条件

* SendGridアカウント
* EventStream/AudienceStreamアカウント

## 仕組み

SendGridは、指定したエンドポイントに対して送信リクエストを送るWebhook APIを提供しています。これらのリクエストは、EventStreamに対するプッシュ通知のように機能し、SendGridアカウントで何が起こったかを通知します。UDHでSendGridデータソースを追加すると、SendGridアカウントでイベント通知を構成するために使用するユニークなエンドポイントが生成されます。

## SendGridデータソース

SendGridデータソースは、SendGrid構成でHTTP POST URLとして使用するためのユニークなURLを生成します。生成されたURLは以下の形式になります：

`<https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY>`

Tealium Customer Data HubプロファイルにSendGridデータソースを追加する方法については、[Data Sources](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加し、接続したら、プロファイルを保存して公開します。

## SendGridの構成

データソースエンドポイントを取得したら、SendGridアカウントに移動してWebhookを作成できます。

1. [SendGrid](https://app.sendgrid.com/)に移動し、[Settings &gt; Mail Settings](https://app.sendgrid.com/settings/mail_settings)に進みます。
1. イベント通知をオンにします。
1. HTTP POST URLフィールドにデータソースエンドポイントを貼り付けます。
1. 購読したいイベント通知を選択します。
1. 右上のチェックマークをクリックして、これらの更新を構成に保存します。

## イベントと属性

すべての受信SendGridイベントは自動的に`sendgrid_`でプレフィックスとアンダースコアが付けられたイベント属性に変換されます。例えば、SendGrid Webhookは`smpt-id`属性をTealiumに送信し、それが`sendgrid__smpt_id`（すべて小文字）に変換されます。

SendGridが生成するWebhookイベントと属性の完全なリストは以下を参照してください：

* [SendGrid Event Webhook Reference](https://sendgrid.com/docs/API_Reference/Event_Webhook/event.html)

|イベント属性| タイプ| 例|
|---| ---| ---|
|`sendgrid_asm_group_id`| 数値| 10|
|`sendgrid_attempt`| 文字列| "5"|
|`sendgrid_category`| 文字列| "cat facts"|
|`sendgrid_email`| 文字列| "example@test.com"|
|`sendgrid_event`| 文字列| "processed", "dropped", "delivered", "deferred", "bounce", "click", "spamreport", "unsubscribe", "group_resubscribe", or "group_unsubscribe"|
|`sendgrid_ip`| 文字列| "255.255.255.255"|
|`sendgrid_reason`| 文字列| "500 unknown recipient"|
|`sendgrid_response`| 文字列| "400 try again later"|
|`sendgrid_sg_event_id`| 文字列| "sg_event_id"|
|`sendgrid_sg_message_id`| 文字列| "sg_message_id"|
|`sendgrid_smtp_id`| 文字列| "&lt;14c5d75ce93.dfd.64b469@ismtpd-555&gt;"|
|`sendgrid_status`| 文字列| "5.0.0"|
|`sendgrid_timestamp`| 数値| 1513299569|
|`sendgrid_url`| 文字列| "<http://www.sendgrid.com/>"|
|`sendgrid_useragent`| 文字列| "Mozilla/4.0 (compatible; MSIE 6.1; Windows XP; .NET CLR 1.1.4322; .NET CLR 2.0.50727)"|
