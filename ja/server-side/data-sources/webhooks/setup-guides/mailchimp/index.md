---
title: Mailchimp受信Webhook構成ガイド
description: この記事では、MailchimpアカウントでWebhookを作成し、Tealiumにアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/mailchimp/
---## 前提条件

* Mailchimpアカウント
* Tealium AudienceStreamアカウント

## 動作原理

Mailchimpは、指定したエンドポイントに送信されるWebhook APIを提供します。これらのリクエストは、MailchimpアカウントのアクティビティについてTealium AudienceStreamに通知します。Mailchimpデータソースを追加すると、Mailchimp Webhookを構成するために使用する一意のエンドポイントが生成されます。

## Mailchimpデータソース

Mailchimpデータソースは、Mailchimp構成でHTTP POST URLとして使用する一意のURLを生成します。生成されるURLの形式は以下の通りです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Tealium Customer Data HubプロファイルにMailchimpデータソースを追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存して公開します。

## Mailchimpの構成

データソースエンドポイントを取得したら、MailchimpアカウントでWebhookを作成することができます。

1. [Mailchimpアカウント](https://login.mailchimp.com/)にログインします。
1. **リスト**に移動します。
1. 構成するリストを選択します。
1. **構成**メニューオプションをクリックし、**Webhooks**を選択します。
1. **新しいWebhookを作成**をクリックし、データソースエンドポイントを貼り付けます。

## イベントと属性

すべての受信Mailchimpイベント属性は、`mailchimp_`で自動的に接頭辞が付けられ、アンダースコアが付きます。たとえば、Mailchimpは`data[merges][EMAIL]`属性をTealiumに送信し、それは`mailchimp_data_merges_email`（すべて小文字）に変換されます。

Mailchimpによって生成されるWebhookイベントと属性の完全なリストを見るには：

* [Webhooksについて - 開発者ガイド - Mailchimp](https://developer.mailchimp.com/documentation/mailchimp/guides/about-webhooks/)

|イベント属性| タイプ| 例|
|---| ---| ---|
|`mailchimp_data_action`| 文字列| "unsub"|
|`mailchimp_data_campaign_id`| 文字列| "4fjk2ma9xd"|
|`mailchimp_data_email`| 文字列| "api@mailchimp.com"|
|`mailchimp_data_email_type`| 文字列| "html"|
|`mailchimp_data_id`| 文字列| "8a25ff1d98"|
|`mailchimp_data_ip_opt`| 文字列| "10.20.10.30"|
|`mailchimp_data_ip_signup`| 文字列| "10.20.10.30"|
|`mailchimp_data_list_id`| 文字列| "a6b5da1054"|
|`mailchimp_data_merges_email`| 文字列| "api@mailchimp.com"|
|`mailchimp_data_merges_fname`| 文字列| "Mailchimp"|
|`mailchimp_data_merges_interests`| 配列| "Group1,Group2"|
|`mailchimp_data_merges_lname`| 文字列| "API"|
|`mailchimp_data_new_email`| 文字列| "api+new@mailchimp.com"|
|`mailchimp_data_new_id`| 文字列| "51da8c3259"|
|`mailchimp_data_old_email`| 文字列| "api+old@mailchimp.com"|
|`mailchimp_data_reason`| 文字列| "Some reason"|
|`mailchimp_data_status`| 文字列| "sent"|
|`mailchimp_data_subject`| 文字列| "Test Campaign Subject"|
|`mailchimp_fired_at`| 文字列| "2009-03-26 21:40:57"|
|`mailchimp_type`| 文字列| "subscribe", "unsubscribe", "upemail", "profile", "cleaned", or "campaign"|
