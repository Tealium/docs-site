---
title: Airship 受信 Webhook セットアップガイド
description: この記事では、Airship データソースを使用して Airship アカウントに Webhook を作成し、対応可能なイベントを Tealium に送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/airship/
---

## 前提条件

* Event Streaming または Customer Data Platform（CDP）、あるいはその両方
* Airship アカウント

## 仕組み

Airship を Event Streaming または CDP に接続するには、[Airship Webhook API](https://docs.airship.com/guides/messaging/user-guide/data/data-streaming/data-streaming/) を使用して、Tealium アカウント内のカスタム Airship データソースエンドポイントに送信リクエストを送ります。

Webhook を構成すると、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受信して、ユースケースの自動化、最新情報の把握、生産性の向上を実現できます。

## Airship データソース

Airship データソースを Tealium Customer Data Hub プロファイルに追加すると、Webhook の構成で使用する次の形式の一意の URL が生成されます。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Airship データソースを Tealium Customer Data Hub プロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続したら、プロファイルを保存してパブリッシュします。

## Airship のセットアップ

Airship を Tealium Customer Data Hub プロファイルに接続した後、次の手順で Webhook を構成します。

1. Airship アカウントにログインし、**Settings &gt; Project Configuration** に移動して、**Manage** をクリックし、Real-Time Data Streaming 統合を構成します。
1. **Real-Time Data Streaming** で、**Tealium** をクリックします。  
      
<blockquote>
以前に構成した統合は、**Enabled Integrations** に表示されます。
</blockquote>


1. 名前と説明を入力します。
1. Airship データソースを Tealium プロファイルに追加したときに作成されたカスタムエンドポイント URL を入力します。例：

      ```
      https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
      ```

1. 匿名訪問を Tealium に送信するかどうかを選択します。
1. Tealium に送信するイベントタイプを選択します。
1. **Save** をクリックします。

## イベントと属性

受信するすべての Airship イベント属性には、プレフィックス `airship_` がエンリッチメントされます。たとえば、Airship は `id` 属性を Tealium に送信し、その属性は `airship_id`（すべて小文字）に変換されます。


Airship Webhook API は、次の Airship メールサブスクリプションイベントの例に示すように、フラット化された JSON オブジェクトを Tealium に送信します。

```json
{
  "airship_id": "62f3b7ac-4048-4f22-a0b5-22c01ef172a9",
  "airship_offset": "1000022265027",
  "airship_occurred": "2021-10-01T16:52:07.131Z",
  "airship_processed": "2019-04-01T13:00:23.456Z",
  "airship_device_channel": "6b46c724-494b-4491-9fe7-1b903d266110",
  "airship_device_device_type": "EMAIL",
  "airship_device_named_user_id": "Tealium",
  "airship_device_delivery_address": "test1@tealium.com",
  "airship_body_event_type": "registration",
  "airship_body_identifiers_address": "new.subscription@emaildomain.com",
  "airship_body_properties_commercial_opted_in": "2019-01-04T20:56:00.000Z",
  "airship_body_properties_transactional_opted_in": "2019-01-04T20:56:00.000Z",
  "airship_type": "SUBSCRIPTION",
  "tealium_timestamp_epoch": 1634740696399,
  "tealium_event": "airship_subscription"
}
```

Airship によって生成される Webhook イベントと属性の完全なリストについては、[Airship イベントのドキュメント](https://docs.airship.com/api/connect/#schema-tag-events)を参照してください。

## ベンダーのドキュメント

* [Airship Real-Time Data Streaming のドキュメント](https://docs.airship.com/guides/messaging/user-guide/data/data-streaming/data-streaming/)
* [Airship イベントのドキュメント](https://docs.airship.com/api/connect/#schema-tag-events)