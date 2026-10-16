---
title: データレイヤーエンリッチメントパブリックAPIについて
description: データレイヤーエンリッチメントパブリックAPIを使用して、アクティブな訪問のプロファイルデータを取得できます。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/data-layer-enrichment-public-api/
---
## 動作原理

訪問がサイトでイベントをトリガーした後、データレイヤーエンリッチメントAPIを使用して訪問プロファイルを取得できます。API訪問データは、訪問中に最後のアクティビティがAudienceStreamイベントとして受信されてから2分間利用可能です。

返されるAudienceStream訪問プロファイルは、以下の点で通常の訪問プロファイルと異なります：

* バッジとオーディエンスはオブジェクトとして返されます
* タイムラインとファネルは削除されています
* [制限された属性](https://docs.tealium.com/data-layer-enrichment-object/)は返されません

アクティブな訪問のプロファイルがGETリクエストを送信した時点でまだ利用可能でない場合、APIは空のJSONオブジェクトを返します。

JSONオブジェクトについての詳細は、[データレイヤーエンリッチメントAPIオブジェクト](https://docs.tealium.com/data-layer-enrichment-object/)を参照してください。


<blockquote>
データレイヤーエンリッチメントパブリックAPIとプロファイル定義APIは、データレイヤーエンリッチメント構成によって制御されます。データレイヤーエンリッチメントが無効になっている場合、両方のAPIは`404`レスポンスを返します。詳細は、[サーバーサイドデータレイヤーエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>



<blockquote>
ブラウザからデータレイヤーエンリッチメントAPIを使用する場合、許可リストの構成が必要になる場合があります。詳細は、[ドメイン許可リスト](https://docs.tealium.com/enable-data-layer-enrichment/#domain-allow-list)を参照してください。
</blockquote>


### プロファイル定義APIとの組み合わせ

APIは訪問に関連付けられたバッジIDを含む訪問プロファイルを返します。これらのバッジの対応する名前を取得するには、[プロファイル定義API](https://docs.tealium.com/get-profile-definition-api/)を使用します。


<blockquote>
プロファイル定義APIはTealiumプロファイルに関連付けられたバッジとオーディエンスデータを返し、特定の訪問には制限されません。
</blockquote>


たとえば、2つのバッジが割り当てられた訪問プロファイルのリクエストは、データレイヤーエンリッチメントパブリックAPIを使用して次のように返されます：

```json
{ 
  "badges" : {
    "8879": true
  }
}
```

プロファイル定義APIは、Tealiumプロファイルで定義されたバッジIDとその名前を返します。この例では、APIは次のように返します：

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