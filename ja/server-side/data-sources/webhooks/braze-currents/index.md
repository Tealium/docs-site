---
title: Braze Currentsデータソース構成ガイド
description: この記事では、Braze Currentsを使用して、実用的なイベントをEvent Streaming API HubおよびCDPに送信するために、Brazeをデータソースとして使用する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/braze-currents/
---
パートナー統合およびTealiumサーバーサイドデータソースの詳細については、[データソース](https://docs.tealium.com/partners/data-sources/#api)を参照してください。

## 前提条件

* Event StreamingまたはCustomer Data Platform（CDP）、あるいはその両方
* Currentsが有効になっているBrazeアカウント


<blockquote>
Currentsコネクタは、多くのBraze ProおよびEnterpriseレベルのパッケージにすでに含まれています。Currentsへのアクセス権がない場合は、Brazeのアカウントマネージャーにお問い合わせください。
</blockquote>


## 仕組み

Brazeプラットフォームは、分析、リターゲティング、およびシステム内のその他のユースケースに使用するため、Braze統合からさまざまなイベントデータを追跡します。BrazeをEvent StreamingまたはCDPに接続するには、[Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)を使用して、BrazeデータソースをTealiumアカウントに送信します。

Braze Currentsを構成すると、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受信することで、ユースケースの自動化、最新情報の把握、生産性の向上が可能になります。

### Braze Currentsデータソース

BrazeデータソースをTealium Customer Data Hubプロファイルに追加すると、Currents構成で使用する一意のURLが次の形式で生成されます。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

BrazeデータソースをTealium Customer Data Hubプロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存してパブリッシュします。

### Braze Currentsの構成

BrazeをTealium Customer Data Hubプロファイルに接続した後、次の手順でBraze Currentsを構成します。

1. Brazeアカウントにログインし、Brazeダッシュボードの**統合**セクションにある**Currents**ページに移動します。
1. **Currentを作成**メニューで、**Currentsコネクタ**または**パートナー**として**Tealium**を選択します。
1. BrazeデータソースをTealiumプロファイルに追加したときに作成されたカスタムエンドポイントURLを入力します。例：   
      ```
      https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
      ```

1. Tealiumに送信する[メッセージエンゲージメントイベント](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/)、[顧客行動](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)、および[ユーザーイベント](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)を選択します。
1. Currentを有効にして保存します。

### イベントと属性

Brazeイベントパラメータは、Currents構成で選択したエンゲージメント行動イベントまたは顧客行動イベントに基づいて事前定義されています。イベントはグループ化され、すべてのイベントを含むJSON配列としてカスタムエンドポイントに送信されます。たとえば、`{"events": [event1, event2, event3, etc...]}`のようになります。配列内の各要素は、1つのイベントを表すJSONオブジェクトです。

たとえば、Braze Canvasのメールがエンドユーザーの受信トレイに正常に配信されると、Brazeは次のJSONイベントオブジェクトを生成します。

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

受信するすべてのBrazeイベント属性には、`braze_`というプレフィックスが自動的にエンリッチメントされます。たとえば、Currentsが`id`を送信すると、対応するEvent Streamingイベント属性は`braze_id`（すべて小文字）になります。TealiumのBrazeデータソースは、次の例に示すように、イベントをカスタムJSONオブジェクトとしてフラット化します。

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

`tealium_event`属性は、Currentsの`event_type`パラメータの値を継承します。

次の画像は、Tealium Live Eventsツールに受信されたイベントの例で、メール配信イベントによって渡されたパラメータが含まれています。

![](https://docs.tealium.com/images/server-side/braze-currents-event-tealium-live-events-email-delivery.png)

サポートされているイベントの完全な一覧については、[Braze Currentsドキュメント](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)のCurrentsイベント用語集を参照してください。

## **ベンダーのドキュメント**

* [Currentsの構成](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/)
* [Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)
* [顧客行動イベント](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)
* [メッセージエンゲージメントイベント](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/)