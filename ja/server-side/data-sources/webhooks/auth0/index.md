---
title: Auth0受信Webhook構成ガイド
description: この記事では、Auth0データソースを使用してAuth0アカウントにWebhookを作成し、対応可能なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/auth0/
---
## 仕組み

ユーザーがデータベースに追加された後、Auth0データソースは、Auth0マーケットプレイスで利用可能なすべてのTealiumアクションからデータを受信します。

## 要件

Auth0受信Webhookには、以下が必要です。

* Event StreamingまたはCustomer Data Platform（CDP）
* Auth0アカウント

### Auth0データソースの追加

Tealium Customer Data HubプロファイルにAuth0データソースを追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存してパブリッシュします。

Tealium Customer Data HubプロファイルにAuth0データソースを追加すると、Webhookの構成で使用する一意のURLとデータソースキーが生成されます。URLの形式は次のとおりです。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

### Auth0の構成

Auth0をTealium Customer Data Hubプロファイルに接続した後、次の手順でWebhookを構成します。

1. Auth0アカウントにログインします。
1. 左側のメニューから、**Actions > Library**を選択します。
1. **Create Action > Use a Marketplace Integration**をクリックします。
1. **Tealium Action**をライブラリに追加します。
1. アクションの**Tealium Account Name**、**Tealium Profile Name**、および**Data Source key**を入力します。
1. 左側のメニューから、**Actions > Flow**を選択します。
1. 適切なフローを選択し、そのフローにアクションを追加します。

詳細については、[Auth0：Auth0 Actionsの仕組み](https://auth0.com/docs/customize/actions/actions-overview#what-can-you-do-with-actions-)を参照してください。

### イベントと属性

受信するすべてのAuth0イベント属性には、`auth0_`というプレフィックスがエンリッチメントされます。たとえば、`user_id`属性の場合、Auth0は対応するEvent Streamingイベント属性`auth0_user_id`（すべて小文字）を送信します。Auth0 Webhook APIは、フラット化されたJSONオブジェクトをTealiumに送信します。

|キー|型|例|
|---|---|---|
|`tealium_event`|文字列|`auth0_user_login`|
|`auth0_email_address`|文字列|`user@example.com`|
|`auth0_user_id`|数値|`8237572`|
|`auth0_phone_number`|数値|`0123456789`|
|`auth0_ip`|文字列|`255.255.255.255`|
|`auth0_city`|文字列|`San Diego`|
|`auth0_last_name`|文字列|`John`|
|`auth0_first_name`|文字列|`Doe`|

詳細については、[Actions Triggers：post-user-registration - Event Object](https://auth0.com/docs/customize/actions/flows-and-triggers/post-user-registration-flow/event-object)を参照してください。

## ベンダーのドキュメント

* [Auth0：Auth0との統合の概要](https://auth0.com/docs/customize/integrations/marketplace-partners/introduction-to-integrating-with-auth0)
* [Auth0：Auth0 Actionsの仕組み](https://auth0.com/docs/customize/actions/actions-overview#what-can-you-do-with-actions-)