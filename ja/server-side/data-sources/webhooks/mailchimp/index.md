---
title: Mailchimp 受信 Webhook セットアップガイド
description: この記事では、Mailchimp データソースを使用して Mailchimp アカウントに Webhook を作成し、対応可能なイベントを Tealium に送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/mailchimp/
---## 前提条件

* Mailchimp アカウント
* Customer Data Platform（CDP）アカウント

## 仕組み

Mailchimp は、指定したエンドポイントに送信リクエストを送る Webhook API を提供しています。これらのリクエストにより、Mailchimp アカウント内のアクティビティが CDP に通知されます。Mailchimp データソースを追加すると一意のエンドポイントが生成され、これを使用して Mailchimp Webhook を構成します。

## Mailchimp データソース

Mailchimp データソースは、Mailchimp の構成で HTTP POST URL として使用する一意の URL を生成します。生成される URL の形式は次のとおりです。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Mailchimp データソースを Tealium Customer Data Hub プロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続したら、プロファイルを保存してパブリッシュします。

## Mailchimp のセットアップ

データソースのエンドポイントを取得したら、Mailchimp アカウントで Webhook を作成できます。

1. [Mailchimp アカウント](https://login.mailchimp.com/)にログインします。
1. **Lists** に移動します。
1. 構成するリストを選択します。
1. **Settings** メニューオプションをクリックし、**Webhooks** を選択します。
1. **Create New Webhook** をクリックし、データソースのエンドポイントを貼り付けます。

## イベントと属性

受信するすべての Mailchimp イベント属性には、接頭辞として `mailchimp_` が自動的に追加され、アンダースコア区切りに変換されます。たとえば、Mailchimp が `data[merges][EMAIL]` 属性を Tealium に送信すると、`mailchimp_data_merges_email`（すべて小文字）に変換されます。

Mailchimp によって生成される Webhook イベントと属性の完全な一覧については、以下を参照してください。

* [Webhook について - 開発者ガイド - Mailchimp](https://developer.mailchimp.com/documentation/mailchimp/guides/about-webhooks/)

|イベント属性|型|例|
|---|---|---|
|`mailchimp_data_action`|文字列| "unsub"|
|`mailchimp_data_campaign_id`|文字列| "4fjk2ma9xd"|
|`mailchimp_data_email`|文字列| "api@mailchimp.com"|
|`mailchimp_data_email_type`|文字列| "html"|
|`mailchimp_data_id`|文字列| "8a25ff1d98"|
|`mailchimp_data_ip_opt`|文字列| "10.20.10.30"|
|`mailchimp_data_ip_signup`|文字列| "10.20.10.30"|
|`mailchimp_data_list_id`|文字列| "a6b5da1054"|
|`mailchimp_data_merges_email`|文字列| "api@mailchimp.com"|
|`mailchimp_data_merges_fname`|文字列| "Mailchimp"|
|`mailchimp_data_merges_interests`|配列| "Group1,Group2"|
|`mailchimp_data_merges_lname`|文字列| "API"|
|`mailchimp_data_new_email`|文字列| "api+new@mailchimp.com"|
|`mailchimp_data_new_id`|文字列| "51da8c3259"|
|`mailchimp_data_old_email`|文字列| "api+old@mailchimp.com"|
|`mailchimp_data_reason`|文字列| "Some reason"|
|`mailchimp_data_status`|文字列| "sent"|
|`mailchimp_data_subject`|文字列| "Test Campaign Subject"|
|`mailchimp_fired_at`|文字列| "2009-03-26 21:40:57"|
|`mailchimp_type`|文字列| "subscribe", "unsubscribe", "upemail", "profile", "cleaned", または "campaign"|