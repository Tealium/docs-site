---
title: Intercom 受信 Webhook セットアップガイド
description: この記事では、Intercom データソースを使用して Intercom アカウントに Webhook を作成し、実行可能なイベントを Tealium に送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/intercom/
---
## 前提条件

* [Intercom アカウント](https://app.intercom.com/admins/sign_in)
* Event Streaming および Customer Data Platform（CDP）アカウント

## 仕組み

Intercom は、指定したエンドポイントに送信リクエストを送る [Webhook API](https://developers.intercom.com/building-apps/docs/setting-up-webhooks) を提供しています。これらのリクエストは Event Streaming へのプッシュ通知として機能し、Intercom アカウントで発生した事象を通知します。Customer Data Hub（CDH）に Intercom データソースを追加すると、一意のエンドポイントが生成されます。このエンドポイントを使用して Intercom Webhook を構成します。構成後は、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受信することで、ユースケースの自動化、最新情報の把握、生産性の向上を実現できます。

## Intercom データソース

Intercom データソースは、Intercom の構成で HTTP POST URL として使用する一意の URL を生成します。URL は次の形式で生成されます。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Intercom データソースを Tealium CDH プロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存してパブリッシュします。

## Intercom のセットアップ

データソースのエンドポイントを生成したら、次の手順に従って Intercom アカウントに移動し、Webhook を作成します。

1. [Intercom アカウント](https://app.intercom.io/a/apps/_/developer-hub)にログインします。
1. アプリケーションに移動します。
1. 構成するアプリケーションを選択します。
1. **Configure > Webhooks** に移動します。
1. Intercom データソースに、前のセクションで説明した Tealium によって生成されたリクエストエンドポイント URL を指定します。
1. 通知を受け取るトピックを選択します。

## イベントと属性

受信するすべての Intercom イベント属性には、`intercom_` というプレフィックスが自動的にエンリッチメントされます。たとえば、Intercom は `data.item.conversation_message.type` 属性を Tealium に送信し、この属性は `intercom_data_item_conversation_message_type`（すべて小文字）に変換されます。

Intercom が生成する Webhook イベントと属性の完全な一覧については、[Intercom - Webhook モデル](https://developers.intercom.com/building-apps/docs/webhook-model)を参照してください。

|**イベント属性**| **型**| **例**|
|---| ---| ---|
|`intercom_type`| 文字列| "notification_event"|
|`intercom_id`| 文字列| "notif_4e3504a3-ba3f-46dc-ab48-8e4d5bdfdf4e"|
|`intercom_created_at`| 数値| "1571080403"|
|`intercom_topic`| 文字列| "conversation.admin.closed"|
|`intercom_data_type`| 文字列| "notification_event_data"|
|`intercom_data_item_type`| 文字列| 次のいずれか：<ul><li>"conversation"</li><li>"user"</li><li>"contact"</li><li>"usertag"</li><li>"ead"</li><li>"contacttag"</li><li>"visitor"</li><li>"event"</li><li>"ping"</li></ul> |
|`intercom_data_item_id`| 文字列| "24098479713"|
|`intercom_data_item_user_type`| 文字列| "user"|
|`intercom_data_item_user_email`| 文字列| "wz1996@gmail.com"|
|`intercom_data_item_assignee_type`| 文字列| "admin"|
|`intercom_data_item_assignee_email`| 文字列| "weibin.zhong@intercom.io"|
|`intercom_data_item_conversation_message_subject`| 文字列| "Hello"|
|`intercom_data_item_conversation_message_body`| 文字列| "&lt;p&gt;This is a new conversation&lt;/p&gt;"|
|`intercom_data_item_conversation_parts_conversation_parts`| オブジェクトのリスト| "[{"type":"conversation_part", "id": "3928295317"},{"type": "conversation_part", "id": "3928295318"}]"|
|`intercom_data_item_tags_tags`| オブジェクトのリスト| "{"type": "tag", "id": "2913705", "name": "API"}, {"type": "tag", "id": "2914621", "name": "Feature request"}]"|
|`intercom_data_item_id`| 文字列| "530370b477ad7120001d"|
|`intercom_data_item_user_id`| 文字列| "25"|
|`intercom_data_item_email`| 文字列| "wash@serenity.io"|
|`intercom_data_item_phone`| 文字列| "+1123456789"|
|`intercom_data_item_name`| 文字列| "Hoban Washburne"|
|`intercom_data_item_company_id`| 文字列| "6"|
|`intercom_data_item_event_name`| 文字列| "invited-friend"|

## ベンダーのドキュメント

次のドキュメントを表示するには、[Intercom にログイン](https://app.intercom.com/admins/sign_in)してください。

* [Intercom Developer Hub](https://app.intercom.io/a/apps/_/developer-hub)
* [Intercom：Webhook の概要](https://developers.intercom.com/building-apps/docs/webhooks)
* [Intercom：Webhook のセットアップ](https://developers.intercom.com/building-apps/docs/setting-up-webhooks)
* [Intercom：認証のセットアップ - 権限とスコープ](https://developers.intercom.com/building-apps/docs/setting-up-oauth#section-permissions)
* [Intercom：Webhook モデル](https://developers.intercom.com/building-apps/docs/webhook-model)