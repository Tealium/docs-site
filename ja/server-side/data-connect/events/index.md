---
title: Data Connectイベント
description: この記事では、Data Connectイベントの形式について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/events/
---
Data Connectは、Workatoインテグレーションからリアルタイムの更新を取得します。Workatoレシピを使用してイベントトリガーを構成し、Tealium Eventsアプリを使用してインテグレーションデータをTealiumのイベント属性にマッピングします。

Data Connectは、レシピで構成したデータマッピングを使用し、JSON形式でイベントをTealiumに送信します。たとえば、連絡先オブジェクトが更新されるたびに顧客フィールド`customerStatusTypeID`を取得し、その値を訪問属性としてCustomer Data Platform（CDP）に送信するよう、Salesforceインテグレーションを構成できます。Tealium Eventインテグレーションを使用すると、Salesforceフィールド`customerID`と`customerStatusTypeID`を、それぞれTealiumイベント属性`customer_id`と`customer_status`にマッピングできます。

Salesforceが顧客フィールド`customerStatusTypeID`を取得すると、Workatoレシピによってイベントがトリガーされ、次のイベントデータがTealiumに送信されます。

```json
{
  tealium_event   : "offline_account_update",
  customer_id     : "123456",
  customer_status : "Active"
}
```

tealium_event名`offline_account_update`は、インテグレーションごとにカスタマイズできます。

このイベントをCustomer Data Platform（CDP）で取得するには、このイベントが発生するたびに`customer_status`を保存する訪問属性とエンリッチメントを作成します。