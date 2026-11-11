---
title: Zapier受信Webhook構成ガイド
description: この記事では、Zapierデータソースを使用してZapierアカウントにWebhookを作成し、対応可能なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/zapier/
---
## 前提条件

* Zapierアカウント
* Customer Data Platform（CDP）アカウント

## 仕組み

Zapierでは、Zapから指定したエンドポイントにWebhookを送信できます。これらのリクエストにより、ZapierアカウントでのアクティビティがCDPに通知されます。Zapierデータソースを追加すると、Zapier Webhookの構成に使用する一意のエンドポイントが生成されます。

## Zapierデータソース

Zapierデータソースは、Zapier Webhookの構成で使用する一意のURLを生成します。また、Zapier Webhook用のクエリ文字列パラメータも生成します。

Webhook URLは次のとおりです。

```
https://collect.tealiumiq.com/event
```

Zapierの構成では、次のクエリ文字列パラメータが必要です。

```
tealium_acount=ACCOUNT
tealium_profile=PROFILE
tealium_datasource=DATA_SOURCE_KEY
tealium_event=EVENT_NAME
```

ZapierデータソースをTealiumプロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存してパブリッシュします。

## Zapierの構成

データソースのエンドポイントを取得したら、Zapierアカウントに移動してWebhookを作成します。Zapier Webhookを作成する際は、データソースのURLとクエリ文字列パラメータに続けて、必要な追加イベント属性を指定します。Zapierイベントを使用してCustomer Data Platform（CDP）内の訪問プロファイルをエンリッチする場合は、必ずユーザーIDを含めてください。

![](https://docs.tealium.com/images/server-side/zapierwebhooksetup-png.png)

Zapier Webhookの構成については、[ZapでWebhookを送信する](https://help.zapier.com/hc/en-us/articles/8496326446989-Send-webhooks-in-Zaps)を参照してください。