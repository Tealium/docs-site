---
title: Braze Currents データソース構成ガイド
description: この記事では、Brazeをデータソースとして使用し、Braze Currentsを使用してTealium EventStream API HubとTealium AudienceStream CDPにアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/braze-currents/
---
パートナー統合やTealium Server-Sideデータソースに関する追加情報については、[Data Sources](/ja/partners-and-industries/partner-with-us/data-sources/#api)を参照してください。

## 前提条件

* Tealium EventStream および/または Tealium AudienceStream
* Currentsが有効化されたBrazeアカウント

Currentsコネクタは、多くのBraze pro-およびエンタープライズレベルのパッケージにすでに含まれています。まだCurrentsへのアクセスがない場合は、Brazeアカウントマネージャーに連絡してください。

## 仕組み

Brazeプラットフォームは、分析、リターゲティング、およびシステム内の他のユースケースのために、Braze統合からさまざまなイベントデータを追跡します。BrazeをTealium EventStreamまたはTealium AudienceStreamに接続するには、[Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)を使用してBrazeデータソースをTealiumアカウントに送信します。

Braze Currentsを構成した後、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受け取ることで、ユースケースを自動化し、情報を得て、生産性を向上させることができます。

### Braze Currentsデータソース

Tealium Customer Data HubプロファイルにBrazeデータソースを追加すると、Currents構成で使用するためのユニークなURLが生成されます。その形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

BrazeデータソースをTealium Customer Data Hubプロファイルに追加する方法については、[Data Sources]()を参照してください。データソースを追加し、接続した後は、プロファイルを保存して公開します。

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

Brazeイベントパラメータは、Currents構成で選択したエンゲージメント行動または顧客行動イベントに基づいて事前に定義されています。イベントはグループ化され、すべてのイベントを含むJSON配列としてカスタムエンドポイントに送信されます。例えば、`{&#34;events&#34;: [event1, event2, event3, etc...]}`、配列内の各要素は単一のイベントを表すJSONオブジェクトです。

例えば、Braze Canvasのメールがエンドユーザーの受信トレイに正常に届いたとき、Brazeは次のJSONイベントオブジェクトを生成します：

```json
users.messages.email.Delivery
{
    &#34;event_type&#34;: &#34;users.messages.email.Delivery&#34;,
    &#34;id&#34;: &#34;663628f0-3f46-484e-8b6c-51d0a67764e0&#34;,
    &#34;time&#34;: 1646162118,
    &#34;timezone&#34;: &#34;America/Chicago&#34;,
    &#34;user&#34;: {
        &#34;external_user_id&#34;: &#34;62181fc031c9ba304eecb255&#34;
    },
    &#34;properties&#34;: {
        &#34;canvas_id&#34;: &#34;c176e77e-33ba-44d6-809c-c89483d1e3d7&#34;,
        &#34;canvas_name&#34;: &#34;My Cool Canvas&#34;,
        &#34;canvas_step_name&#34;: &#34;Initial Email&#34;,
        &#34;canvas_variation_id&#34;: &#34;31234567-89ab-cdef-0123-456789abcdef&#34;,
        &#34;canvas_variation_name&#34;: &#34;Variant 1&#34;,
        &#34;canvas_step_id&#34;: &#34;d8e31e8e-0584-43dd-8e4e-b657707df800&#34;,
        &#34;dispatch_id&#34;: &#34;621e70c403115018b55ee12cc214a515&#34;,
        &#34;email_address&#34;: &#34;test1@tealium.com&#34;,
        &#34;sending_ip&#34;: &#34;167.89.14.251&#34;,
        &#34;subscription_group_id&#34;: &#34;41234567-89ab-cdef-0123-456789abcdef&#34;
    }
}
```

すべての着信Brazeイベント属性は自動的に`braze_`でプレフィックスされます。例えば、Currentsが`id`を送信すると、対応するEventStreamイベント属性は`braze_id`（すべて小文字）となります。Tealium Brazeデータソースは、次の例に示すように、イベントをカスタムJSONオブジェクトとしてフラット化します：

```json
{
    &#34;tealium_event&#34;: &#34;users.messages.email.Delivery&#34;,
    &#34;braze_event_type&#34;: &#34;users.messages.email.Delivery&#34;,
    &#34;braze_id&#34;: &#34;663628f0-3f46-484e-8b6c-51d0a67764e0&#34;,
    &#34;braze_time&#34;: 1646162118,
    &#34;braze_timezone&#34;: &#34;America/Chicago&#34;,
    &#34;braze_user_external_user_id&#34;: &#34;62181fc031c9ba304eecb255&#34;,
    &#34;braze_properties_canvas_id&#34;: &#34;c176e77e-33ba-44d6-809c-c89483d1e3d7&#34;,
    &#34;braze_properties_canvas_name&#34;: &#34;My Cool Canvas&#34;,
    &#34;braze_properties_canvas_step_name&#34;: &#34;Initial Email&#34;,
    &#34;braze_properties_canvas_variation_id&#34;: &#34;31234567-89ab-cdef-0123-456789abcdef&#34;,
    &#34;braze_properties_canvas_variation_name&#34;: &#34;Variant 1&#34;,
    &#34;braze_properties_canvas_step_id&#34;: &#34;d8e31e8e-0584-43dd-8e4e-b657707df800&#34;,
    &#34;braze_properties_dispatch_id&#34;: &#34;621e70c403115018b55ee12cc214a515&#34;,
    &#34;braze_properties_email_address&#34;: &#34;test1@tealium.com&#34;,
    &#34;braze_properties_sending_ip&#34;: &#34;167.89.14.251&#34;,
    &#34;braze_properties_subscription_group_id&#34;: &#34;41234567-89ab-cdef-0123-456789abcdef&#34;
}
```

`tealium_event`属性は、Currentsからの`event_type`パラメータの値を継承します。

以下の画像は、Tealium Live Eventsツールへの着信イベントの例であり、メール配信イベントによって渡されたパラメータを含んでいます：

![](/images/server-side/braze-currents-event-tealium-live-events-email-delivery.png)

サポートされるイベントの完全なリストについては、[Braze Currents documentation](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)のCurrents Event Glossaryを参照してください。

## **ベンダーのドキュメンテーション**

* [Setting up Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/)
* [Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)
* [Customer Behavior Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)
* [Message Engagement Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/)
