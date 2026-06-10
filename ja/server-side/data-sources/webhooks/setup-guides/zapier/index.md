---
title: ZapierからのWebhook構成ガイド
description: この記事では、Zapierデータソースを使用してZapierアカウントにWebhookを作成し、Tealiumに対して実行可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/zapier/
---
## 前提条件

* Zapierアカウント
* Tealium AudienceStreamアカウント

## 仕組み

Zapierは、指定したエンドポイントにZapsからWebhookを送信することができます。これらのリクエストは、ZapierアカウントのアクティビティについてTealium AudienceStreamに通知します。Zapierデータソースを追加すると、ZapierのWebhookを構成するために使用するユニークなエンドポイントが生成されます。

## Zapierデータソース

Zapierデータソースは、Zapier Webhook構成で使用するためのユニークなURLを生成します。また、データソースはZapierのWebhookのためのクエリストリングパラメータも生成します。

WebhookのURLは以下の通りです：

```
https://collect.tealiumiq.com/event
```

Zapierの構成で必要なクエリストリングパラメータは以下の通りです：

```
tealium_acount=ACCOUNT
tealium_profile=PROFILE
tealium_datasource=DATA_SOURCE_KEY
tealium_event=EVENT_NAME
```

ZapierデータソースをTealiumプロファイルに追加するには、[Data Sources]()を参照してください。データソースを追加し、接続したら、プロファイルを保存して公開します。

## Zapierの構成

データソースのエンドポイントを取得したら、Zapierアカウントに移動してWebhookを作成します。ZapierのWebhookを作成する際には、データソースのURLとクエリストリングパラメータを使用し、必要な追加のイベント属性を続けて入力します。ZapierのイベントがAudienceStream内の訪問プロファイルをエンリッチすることを目指している場合、ユーザーIDを含めるようにしてください。

![](/images/server-side/zapierwebhooksetup-png.png)

Zapier Webhooksの構成については、[Send Webhooks in Zaps](https://help.zapier.com/hc/en-us/articles/8496326446989-Send-webhooks-in-Zaps)を参照してください。