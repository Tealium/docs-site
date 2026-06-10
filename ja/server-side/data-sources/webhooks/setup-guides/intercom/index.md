---
title: IntercomからのWebhook構成ガイド
description: この記事では、Intercomデータソースを使用してIntercomアカウントにWebhookを作成し、アクション可能なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/intercom/
---
## 前提条件

* [Intercomアカウント](https://app.intercom.com/admins/sign_in)
* EventStream/AudienceStreamアカウント

## 仕組み

Intercomは、指定したエンドポイントに対して送信リクエストを送る[Webhook API](https://developers.intercom.com/building-apps/docs/setting-up-webhooks)を提供しています。これらのリクエストは、Intercomアカウントで何が起こったかについてEventStreamに通知するようなプッシュ通知のように機能します。Customer Data Hub (CDH)にIntercomデータソースを追加すると、ユニークなエンドポイントが生成されます。このエンドポイントは、IntercomのWebhookを構成するために使用されます。構成が完了すると、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受け取ってユースケースを自動化し、情報を得て、生産性を向上させることができます。

## Intercomデータソース

Intercomデータソースは、Intercom構成のHTTP POST URLとして使用するためのユニークなURLを生成します。URLは次の形式で生成されます：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Tealium CDHプロファイルにIntercomデータソースを追加する方法については、[Data Sources]()を参照してください。データソースを追加し、接続した後は、プロファイルを保存して公開します。

## Intercomの構成

データソースエンドポイントを生成した後、以下の手順を使用してIntercomアカウントに移動し、Webhookを作成します。

1. [Intercomアカウント](https://app.intercom.io/a/apps/_/developer-hub)にログインします。
1. アプリケーションに移動します。
1. 構成したいアプリケーションを選択します。
1. **構成 &gt; Webhooks**に移動します。
1. Intercomデータソースに対して、前のセクションで説明したようにTealiumによって生成されたリクエストエンドポイントURLを指定します。
1. 通知を受け取りたいトピックを選択します。

## イベントと属性

すべての受信Intercomイベント属性は自動的に`intercom_`でプレフィックスされます。例えば、Intercomは`data.item.conversation_message.type`属性をTealiumに送信し、それは`intercom_data_item_conversation_message_type`（すべて小文字）に変換されます。

Intercomによって生成されるWebhookイベントと属性の完全なリストについては、[Intercom - Webhook Models](https://developers.intercom.com/building-apps/docs/webhook-model)を参照してください。

|**イベント属性**| **タイプ**| **例**|
|---| ---| ---|
|`intercom_type`| 文字列| &#34;notification_event&#34;|
|`intercom_id`| 文字列| &#34;notif_4e3504a3-ba3f-46dc-ab48-8e4d5bdfdf4e&#34;|
|`intercom_created_at`| 数値| &#34;1571080403&#34;|
|`intercom_topic`| 文字列| &#34;conversation.admin.closed&#34;|
|`intercom_data_type`| 文字列| &#34;notification_event_data&#34;|
|`intercom_data_item_type`| 文字列| 以下のいずれか: &lt;ul&gt;&lt;li&gt;&#34;conversation&#34;&lt;/li&gt;&lt;li&gt;&#34;user&#34;&lt;/li&gt;&lt;li&gt;&#34;contact&#34;&lt;/li&gt;&lt;li&gt;&#34;usertag&#34;&lt;/li&gt;&lt;li&gt;&#34;ead&#34;&lt;/li&gt;&lt;li&gt;&#34;contacttag&#34;&lt;/li&gt;&lt;li&gt;&#34;visitor&#34;&lt;/li&gt;&lt;li&gt;&#34;event&#34;&lt;/li&gt;&lt;li&gt;&#34;ping&#34;&lt;/li&gt;&lt;/ul&gt; |
|`intercom_data_item_id`| 文字列| &#34;24098479713&#34;|
|`intercom_data_item_user_type`| 文字列| &#34;user&#34;|
|`intercom_data_item_user_email`| 文字列| &#34;wz1996@gmail.com&#34;|
|`intercom_data_item_assignee_type`| 文字列| &#34;admin&#34;|
|`intercom_data_item_assignee_email`| 文字列| &#34;weibin.zhong@intercom.io&#34;|
|`intercom_data_item_conversation_message_subject`| 文字列| &#34;Hello&#34;|
|`intercom_data_item_conversation_message_body`| 文字列| &#34;&amp;lt;p&amp;gt;This is a new conversation&amp;lt;/p&amp;gt;&#34;|
|`intercom_data_item_conversation_parts_conversation_parts`| オブジェクトのリスト| &#34;[{&#34;type&#34;:&#34;conversation_part&#34;, &#34;id&#34;: &#34;3928295317&#34;},{&#34;type&#34;: &#34;conversation_part&#34;, &#34;id&#34;: &#34;3928295318&#34;}]&#34;|
|`intercom_data_item_tags_tags`| オブジェクトのリスト| &#34;{&#34;type&#34;: &#34;tag&#34;, &#34;id&#34;: &#34;2913705&#34;, &#34;name&#34;: &#34;API&#34;}, {&#34;type&#34;: &#34;tag&#34;, &#34;id&#34;: &#34;2914621&#34;, &#34;name&#34;: &#34;Feature request&#34;}]&#34;|
|`intercom_data_item_id`| 文字列| &#34;530370b477ad7120001d&#34;|
|`intercom_data_item_user_id`| 文字列| &#34;25&#34;|
|`intercom_data_item_email`| 文字列| &#34;wash@serenity.io&#34;|
|`intercom_data_item_phone`| 文字列| &#34;&#43;1123456789&#34;|
|`intercom_data_item_name`| 文字列| &#34;Hoban Washburne&#34;|
|`intercom_data_item_company_id`| 文字列| &#34;6&#34;|
|`intercom_data_item_event_name`| 文字列| &#34;invited-friend&#34;|

## ベンダーのドキュメンテーション

以下のドキュメンテーションを表示するには、[Intercomにログイン](https://app.intercom.com/admins/sign_in)します：

* [Intercom Developer Hub](https://app.intercom.io/a/apps/_/developer-hub)
* [Intercom: Webhooks概要](https://developers.intercom.com/building-apps/docs/webhooks)
* [Intercom: Webhooksの構成](https://developers.intercom.com/building-apps/docs/setting-up-webhooks)
* [Intercom: Authの構成 - 権限とスコープ](https://developers.intercom.com/building-apps/docs/setting-up-oauth#section-permissions)
* [Intercom: Webhook Models](https://developers.intercom.com/building-apps/docs/webhook-model)

