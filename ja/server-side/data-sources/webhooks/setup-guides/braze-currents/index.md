---
title: Braze Currents データソース構成ガイド
description: この記事では、Brazeをデータソースとして使用し、Braze Currentsを使用してTealium EventStream API HubとTealium AudienceStream CDPにアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/braze-currents/
---
パートナー統合やTealium Server-Sideデータソースに関する追加情報については、[Data Sources](https://docs.tealium.com/ja/partners-and-industries/partner-with-us/data-sources/#api)を参照してください。

## 前提条件

* Tealium EventStream および/または Tealium AudienceStream
* Currentsが有効化されたBrazeアカウント


<blockquote>
Currentsコネクタは、多くのBraze pro-およびエンタープライズレベルのパッケージにすでに含まれています。まだCurrentsへのアクセスがない場合は、Brazeアカウントマネージャーに連絡してください。
</blockquote>


## 仕組み

Brazeプラットフォームは、分析、リターゲティング、およびシステム内の他のユースケースのために、Braze統合からさまざまなイベントデータを追跡します。BrazeをTealium EventStreamまたはTealium AudienceStreamに接続するには、[Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)を使用してBrazeデータソースをTealiumアカウントに送信します。

Braze Currentsを構成した後、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受け取ることで、ユースケースを自動化し、情報を得て、生産性を向上させることができます。

### Braze Currentsデータソース

Tealium Customer Data HubプロファイルにBrazeデータソースを追加すると、Currents構成で使用するためのユニークなURLが生成されます。その形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

BrazeデータソースをTealium Customer Data Hubプロファイルに追加する方法については、[Data Sources](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加し、接続した後は、プロファイルを保存して公開します。

### Braze Currentsの構成

Tealium Customer Data HubプロファイルにBrazeを接続した後、以下の手順でBraze Currentsを構成します：

1. Brazeアカウントにログインし、Brazeダッシュボードの**Integrations**セクションの**Currents**ページに移動します。
1. **Create Current**メニューから、**Currents connector**または**Partner**として**Tealium**を選択します。
1. TealiumプロファイルにBrazeデータソースを追加して作成されたカスタムエンドポイントURLを入力します。例えば、   
      ```
      https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
      ```

1. [Message Engagement Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/)、[Customer Behavior](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)、および[User Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)をTealiumに送信するよう選択します。
1. Currentを有効化し、保存します。

### イベントと属性

Brazeイベントパラメータは、Currents構成で選択したエンゲージメント行動または顧客行動イベントに基づいて事前に定義されています。イベントはグループ化され、すべてのイベントを含むJSON配列としてカスタムエンドポイントに送信されます。例えば、`{"events": [event1, event2, event3, etc...]}`、配列内の各要素は単一のイベントを表すJSONオブジェクトです。

例えば、Braze Canvasのメールがエンドユーザーの受信トレイに正常に届いたとき、Brazeは次のJSONイベントオブジェクトを生成します：

```json
users.messages.email.Delivery
{
    "event_type": "users.messages.email.Delivery",
    "id": "663628f0-3f46-484e-8b6c-51d0a67764e0",
    "time": 1646162118,
    "timezone": "America/Chicago",
    "user": {
        "external_user_id": "62181fc031c9ba304eecb255"
    },
    "properties": {
        "canvas_id": "c176e77e-33ba-44d6-809c-c89483d1e3d7",
        "canvas_name": "My Cool Canvas",
        "canvas_step_name": "Initial Email",
        "canvas_variation_id": "31234567-89ab-cdef-0123-456789abcdef",
        "canvas_variation_name": "Variant 1",
        "canvas_step_id": "d8e31e8e-0584-43dd-8e4e-b657707df800",
        "dispatch_id": "621e70c403115018b55ee12cc214a515",
        "email_address": "test1@tealium.com",
        "sending_ip": "167.89.14.251",
        "subscription_group_id": "41234567-89ab-cdef-0123-456789abcdef"
    }
}
```

すべての着信Brazeイベント属性は自動的に`braze_`でプレフィックスされます。例えば、Currentsが`id`を送信すると、対応するEventStreamイベント属性は`braze_id`（すべて小文字）となります。Tealium Brazeデータソースは、次の例に示すように、イベントをカスタムJSONオブジェクトとしてフラット化します：

```json
{
    "tealium_event": "users.messages.email.Delivery",
    "braze_event_type": "users.messages.email.Delivery",
    "braze_id": "663628f0-3f46-484e-8b6c-51d0a67764e0",
    "braze_time": 1646162118,
    "braze_timezone": "America/Chicago",
    "braze_user_external_user_id": "62181fc031c9ba304eecb255",
    "braze_properties_canvas_id": "c176e77e-33ba-44d6-809c-c89483d1e3d7",
    "braze_properties_canvas_name": "My Cool Canvas",
    "braze_properties_canvas_step_name": "Initial Email",
    "braze_properties_canvas_variation_id": "31234567-89ab-cdef-0123-456789abcdef",
    "braze_properties_canvas_variation_name": "Variant 1",
    "braze_properties_canvas_step_id": "d8e31e8e-0584-43dd-8e4e-b657707df800",
    "braze_properties_dispatch_id": "621e70c403115018b55ee12cc214a515",
    "braze_properties_email_address": "test1@tealium.com",
    "braze_properties_sending_ip": "167.89.14.251",
    "braze_properties_subscription_group_id": "41234567-89ab-cdef-0123-456789abcdef"
}
```

`tealium_event`属性は、Currentsからの`event_type`パラメータの値を継承します。

以下の画像は、Tealium Live Eventsツールへの着信イベントの例であり、メール配信イベントによって渡されたパラメータを含んでいます：

![](https://docs.tealium.com/images/server-side/braze-currents-event-tealium-live-events-email-delivery.png)

サポートされるイベントの完全なリストについては、[Braze Currents documentation](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)のCurrents Event Glossaryを参照してください。

## **ベンダーのドキュメンテーション**

* [Setting up Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/)
* [Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)
* [Customer Behavior Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)
* [Message Engagement Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/)
