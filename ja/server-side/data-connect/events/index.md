---
title: データコネクトイベント
description: この記事では、データコネクトイベントの形式について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/events/
---
データコネクトは、Workatoの統合からリアルタイムの更新をキャプチャします。Workatoのレシピを使用してイベントトリガーを構成し、Tealium Eventsアプリを使用して統合データをTealiumイベント属性にマッピングします。

データコネクトは、レシピで構成したデータマッピングを使用して、JSON形式のイベントをTealiumに送信します。例えば、Salesforceの統合を構成して、コンタクトオブジェクトが更新されるたびに`customerStatusTypeID`という顧客フィールドをキャプチャし、その値をAudienceStreamの訪問属性として送信することができます。Tealium Event統合を使用して、Salesforceのフィールド`customerID`と`customerStatusTypeID`をTealiumのイベント属性`customer_id`と`customer_status`にそれぞれマッピングすることができます。

Salesforceが顧客フィールド`customerStatusTypeID`をキャプチャすると、Workatoのレシピがイベントをトリガーし、以下のイベントデータをTealiumに送信します：

```json
{
  tealium_event   : &#34;offline_account_update&#34;,
  customer_id     : &#34;123456&#34;,
  customer_status : &#34;Active&#34;
}
```

tealium_eventの名前`offline_account_update`は、各統合ごとにカスタマイズすることができます。

このイベントをTealium AudienceStreamでキャプチャするには、このイベントが発生するたびに`customer_status`を保存する訪問属性とエンリッチメントを作成します。
