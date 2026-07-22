---
title: Auth0からのWebhook構成ガイド
description: この記事では、Auth0データソースを使用してAuth0アカウントにWebhookを作成し、Tealiumに対して実行可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/auth0/
---
## 仕組み

Auth0データソースは、ユーザーがデータベースに追加された後、Auth0マーケットプレイスで利用可能なすべてのTealiumアクションからデータを受け取ります。

## 必要条件

Auth0からのWebhookには以下が必要です：

* Tealium EventStreamまたはTealium AudienceStream
* Auth0アカウント

### Auth0データソースの追加

Tealium Customer Data HubプロファイルにAuth0データソースを追加するには、[Data Sources](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加し、接続した後、プロファイルを保存して公開します。
Tealium Customer Data HubプロファイルにAuth0データソースを追加すると、Webhook構成で使用するためのユニークなURLとデータソースキーが生成されます。URLの形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

### Auth0の構成

Auth0をTealium Customer Data Hubプロファイルに接続した後、以下の手順でWebhookを構成します：

1. Auth0アカウントにログインします。
1. 左側のメニューから、**Actions > Library**を選択します。
1. **Create Action > Use a Marketplace Integration**をクリックします。
1. **Tealium Action**をライブラリに追加します。
1. アクションの**Tealium Account Name**、**Tealium Profile Name**、**Data Source key**を入力します。
1. 左側のメニューから、**Actions > Flow**を選択します。
1. 適切なフローを選択し、アクションをフローに追加します。

詳細については、[Auth0: Understand How Auth0 Actions Work](https://auth0.com/docs/customize/actions/actions-overview#what-can-you-do-with-actions-)を参照してください。

### イベントと属性

すべての受信Auth0イベント属性は`auth0_`で始まります。例えば、`user_id`属性の場合、Auth0は一致するEventStreamイベント属性`auth0_user_id`（すべて小文字）を送信します。Auth0 Webhook APIは、フラット化されたJSONオブジェクトをTealiumに送信します。

|キー| タイプ| 例|
|---| ---| ---|
|`tealium_event`| 文字列| `auth0_user_login`|
|`auth0_email_address`| 文字列| `user@example.com`|
|`auth0_user_id`| 数値| `8237572`|
|`auth0_phone_number`| 数値| `0123456789`|
|`auth0_ip`| 文字列| `255.255.255.255`|
|`auth0_city`| 文字列| `San Diego`|
|`auth0_last_name`| 文字列| `John`|
|`auth0_first_name`| 文字列| `Doe`|

詳細については、[Actions Triggers: post-user-registration - Event Object](https://auth0.com/docs/customize/actions/flows-and-triggers/post-user-registration-flow/event-object)を参照してください。

## ベンダーのドキュメンテーション

* [Auth0: Introduction to Integrating with Auth0](https://auth0.com/docs/customize/integrations/marketplace-partners/introduction-to-integrating-with-auth0)
* [Auth0: Understand How Auth0 Actions Work](https://auth0.com/docs/customize/actions/actions-overview#what-can-you-do-with-actions-)