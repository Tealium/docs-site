---
title: Data Layer Enrichment Public API について
description: Data Layer Enrichment Public API を使用すると、アクティブな訪問のプロファイルデータを取得できます。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/data-layer-enrichment-public-api/
---
## 仕組み

訪問がサイト上でイベントをトリガーした後、Data Layer Enrichment API を使用して訪問プロファイルを取得できます。API の訪問データは、訪問中の最後のアクティビティが Customer Data Platform（CDP）イベントとして受信されてから2分間利用できます。

返される CDP 訪問プロファイルは、一般的な訪問プロファイルと次の点で異なります。

* バッジとオーディエンスはオブジェクトとして返されます
* タイムラインとファネルは削除されています
* [制限付き属性](https://docs.tealium.com/data-layer-enrichment-object/)は返されません

アクティブな訪問の訪問プロファイルが GET リクエストの送信時点でまだ利用できない場合、API は空の JSON オブジェクトを返します。

JSON オブジェクトの詳細については、[Data Layer Enrichment API のオブジェクト](https://docs.tealium.com/data-layer-enrichment-object/)を参照してください。


<blockquote>
Data Layer Enrichment Public API と Profile Definition API は、データレイヤーエンリッチメント構成によって制御されます。データレイヤーエンリッチメントが無効になっている場合、どちらの API も `404` レスポンスを返します。詳細については、[サーバーサイドの Data Layer Enrichment を有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>



<blockquote>
ブラウザーから Data Layer Enrichment API を使用する場合は、許可リストの構成が必要になることがあります。詳細については、[ドメイン許可リスト](https://docs.tealium.com/enable-data-layer-enrichment/#domain-allow-list)を参照してください。
</blockquote>


### Profile Definition API との併用

API は、訪問に関連付けられたバッジ ID を含む訪問プロファイルを返します。これらのバッジに対応する名前を取得するには、[Profile Definition API](https://docs.tealium.com/get-profile-definition-api/)を使用します。


<blockquote>
Profile Definition API は、Tealium プロファイルに関連付けられたバッジとオーディエンスのデータを返すものであり、特定の訪問に限定されません。
</blockquote>


たとえば、2つのバッジが割り当てられている訪問プロファイルをリクエストすると、Data Layer Enrichment Public API から次の内容が返されます。

```json
{ 
  "badges" : {
    "8879": true
  }
}
```

Profile Definition API は、Tealium プロファイルで定義されているバッジ ID とその名前を返します。この例では、API は次の内容を返します。

```json
{
    "badges" : [
        {
            "id" : 24935,
            "name" : "Cart abandoner"
        },
        {
            "id" : 8879,
            "name" : "Frequent visitor"
        }
    ]
}
```