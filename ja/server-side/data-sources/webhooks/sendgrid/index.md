---
title: SendGrid受信Webhook構成ガイド
description: この記事では、SendGridデータソースを使用してSendGridアカウントにWebhookを作成し、対応可能なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/sendgrid/
---## 前提条件

* SendGridアカウント
* Event StreamingおよびCustomer Data Platform（CDP）アカウント

## 仕組み

SendGridは、指定したエンドポイントに送信リクエストを送るWebhook APIを提供しています。これらのリクエストはEvent Streamingへのプッシュ通知として機能し、SendGridアカウントで発生した事象を通知します。UDHにSendGridデータソースを追加すると、一意のエンドポイントが生成されます。このエンドポイントを使用して、SendGridアカウントでイベント通知を構成します。

## SendGridデータソース

SendGridデータソースは、SendGridの構成でHTTP POST URLとして使用する一意のURLを生成します。生成されるURLの形式は次のとおりです。

`<https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY>`

SendGridデータソースをTealium Customer Data Hubプロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存してパブリッシュします。

## SendGridの構成

データソースのエンドポイントを取得したら、SendGridアカウントでWebhookを作成できます。

1. [SendGrid](https://app.sendgrid.com/)で、[Settings &gt; Mail Settings](https://app.sendgrid.com/settings/mail_settings)に移動します。
1. Event Notificationを有効にします。
1. HTTP POST URLフィールドに、データソースのエンドポイントを貼り付けます。
1. サブスクライブするイベント通知を選択します。
1. 上隅にあるチェックマークをクリックして、これらの更新を構成に保存します。

## イベントと属性

受信したすべてのSendGridイベントは、先頭に`sendgrid_`がエンリッチメントされ、アンダースコア形式のイベント属性に自動的に変換されます。たとえば、SendGrid Webhookが`smpt-id`属性をTealiumに送信すると、`sendgrid__smpt_id`（すべて小文字）に変換されます。

SendGridによって生成されるWebhookイベントと属性の完全なリストについては、以下を参照してください。

* [SendGrid Event Webhookリファレンス](https://sendgrid.com/docs/API_Reference/Event_Webhook/event.html)

|イベント属性|型|例|
|---|---|---|
|`sendgrid_asm_group_id`|数値|10|
|`sendgrid_attempt`|文字列|"5"|
|`sendgrid_category`|文字列|"cat facts"|
|`sendgrid_email`|文字列|"example@test.com"|
|`sendgrid_event`|文字列|"processed"、"dropped"、"delivered"、"deferred"、"bounce"、"click"、"spamreport"、"unsubscribe"、"group_resubscribe"、または"group_unsubscribe"|
|`sendgrid_ip`|文字列|"255.255.255.255"|
|`sendgrid_reason`|文字列|"500 unknown recipient"|
|`sendgrid_response`|文字列|"400 try again later"|
|`sendgrid_sg_event_id`|文字列|"sg_event_id"|
|`sendgrid_sg_message_id`|文字列|"sg_message_id"|
|`sendgrid_smtp_id`|文字列|"&lt;14c5d75ce93.dfd.64b469@ismtpd-555&gt;"|
|`sendgrid_status`|文字列|"5.0.0"|
|`sendgrid_timestamp`|数値|1513299569|
|`sendgrid_url`|文字列|"<http://www.sendgrid.com/>"|
|`sendgrid_useragent`|文字列|"Mozilla/4.0 (compatible; MSIE 6.1; Windows XP; .NET CLR 1.1.4322; .NET CLR 2.0.50727)"|