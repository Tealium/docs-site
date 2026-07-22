---
title: Airshipインカミングウェブフック構成ガイド
description: この記事では、Airshipデータソースを使用してAirshipアカウントにウェブフックを作成し、アクション可能なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/airship/
---

## 前提条件

* Tealium EventStream および/または Tealium AudienceStream
* Airshipアカウント

## 仕組み

AirshipをTealium EventStreamまたはTealium AudienceStreamに接続するには、[Airship Webhook API](https://docs.airship.com/guides/messaging/user-guide/data/data-streaming/data-streaming/)を使用して、TealiumアカウントのカスタムAirshipデータソースエンドポイントに送信リクエストを送ります。

ウェブフックを構成した後、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受け取ってユースケースを自動化し、情報を得て、生産性を向上させることができます。

## Airshipデータソース

Tealium Customer Data HubプロファイルにAirshipデータソースを追加すると、ウェブフック構成で使用するためのユニークなURLが生成されます。その形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Tealium Customer Data HubプロファイルにAirshipデータソースを追加する方法については、[Data Sources](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加し、接続したら、プロファイルを保存して公開します。

## Airshipの構成

AirshipをTealium Customer Data Hubプロファイルに接続した後、以下の手順でウェブフックを構成します：

1. Airshipアカウントにログインし、**構成 &gt; プロジェクト構成**に移動し、**管理**をクリックしてリアルタイムデータストリーミングの統合を構成します。
1. **リアルタイムデータストリーミング**の下で**Tealium**をクリックします。  
      
<blockquote>
以前に構成した統合は**有効な統合**の下にリストされます。
</blockquote>


1. 名前と説明を入力します。
1. TealiumプロファイルにAirshipデータソースを追加して作成したカスタムエンドポイントURLを入力します。例えば

      ```
      https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
      ```

1. 匿名の訪問をTealiumに送信するかどうかを選択します。
1. Tealiumに送信するイベントタイプを選択します。
1. **保存**をクリックします。

## イベントと属性

すべての受信Airshipイベント属性は`airship_`で始まります。例えば、Airshipは`id`属性をTealiumに送信し、それは`airship_id`（すべて小文字）に変換されます。

AirshipウェブフックAPIは、以下のAirship Email Subscriptionイベントの例に示すように、フラット化されたJSONオブジェクトをTealiumに送信します：

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

Airshipが生成するウェブフックイベントと属性の完全なリストについては、[Airship Events Documentation](https://docs.airship.com/api/connect/#schema-tag-events)を参照してください。

## ベンダーのドキュメンテーション

* [Airship Real-Time Data Streaming Documentation](https://docs.airship.com/guides/messaging/user-guide/data/data-streaming/data-streaming/)
* [Airship Events Documentation](https://docs.airship.com/api/connect/#schema-tag-events)

