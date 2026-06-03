---
title: Tealium Collectタグの追加と構成
description: この記事では、データレイヤーのエンリッチメントを有効にするためにTealium Collectタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/tealium-collect-dle/
---
詳細な手順については、[Tealium Collectタグ構成ガイド]()を参照してください。

![](/images/server-side/whiteui-datalayerenrichment-tealiumcollecttagconfiguration.png)

## データエンリッチメントの頻度

データレイヤーエンリッチメントを有効にするためにTealium Collectタグを構成する際、属性情報でデータレイヤーをどのくらいの頻度で更新するかを決定する必要があります。以下のオプションがあります：

* **なし**（デフォルト）
  * データレイヤーエンリッチメントは行われません。
* **まれ**
  * データレイヤーエンリッチメントは訪問（セッション）ごとに一度行われます。
  * 取得した顧客データはローカル保存に保存され、セッション中の後続のトラッキングコールで使用されます。
* **頻繁**（推奨）
  * データレイヤーエンリッチメントはトラッキングコールごとに行われます。セッション中に変更された顧客データはリアルタイムでユニバーサルデータオブジェクト（UDO）に反映されます。  
  このオプションはページごとに追加のHTTPリクエストを発生させます。

## ロードルールの選択

Tealium Collectタグについては、デフォルトの**すべてのページでロード**ルールを選択したままにすることをお勧めします。データレイヤーに必要な属性が含まれるように、最も関連性の高いデータでそれを満たしてください。

### Tealium iQでAudienceStream属性を使用する

AudienceStreamの属性はTealium iQでインポートされた変数として扱われます。これらの変数は編集や削除ができません。AudienceStream属性を削除または変更するには、AudienceStreamプロファイルで変更を行います。属性は[プロファイルライブラリ]()にはインポートできず、通常のプロファイルにのみインポートできます。

![](/images/server-side/whiteui-datalayerenrichment-editaudiencestreamvariables.png)

### どのようなAudienceStream属性タイプがインポートされますか？

以下の属性タイプがTealium iQにインポートされ、データレイヤーで利用可能になります：

* バッジ
* 数値
* 文字列
* ブール値
* 日付  

日付属性はデータレイヤーにインポートされ、UDOで表示されますが、ロードルールやタグマッピングで使用することはできません。

## ロードルールの構築

サポートされている属性を使用してロードルールを作成できます。ロードルールで使用可能なルール演算子は、バッジに対して以下の通りです。

* **バッジが割り当てられている**  
`True` は、バッジ属性が訪問に割り当てられている場合です。  
      ![](/images/server-side/whiteui-datalayerenrichment-badgeisorisnotassigned.png)
* **バッジが割り当てられていない**  
`False` は、バッジ属性が訪問に割り当てられていない場合です。

AudienceStreamから属性を削除すると、Tealium iQのデータレイヤースクリーンから自動的に削除されます。ただし、削除された属性を参照するロードルールは自動的に更新されません。削除された属性をまだ参照しているロードルールを手動で更新する必要があります。

## コールバック関数

データレイヤーエンリッチメントリクエストは、レスポンスに基づいてコードを実行することができるコールバックメソッド `window.tealium_enrichment()` を提供します。

コールバック関数を使用するには、次のコードを含む[JavaScript Code extension]()をPre Loaderにスコープ構成して作成します：

```js
window.tealium_enrichment = function(data) {
    console.log(&#34;Data Layer Enrichment Callback&#34;);
    // ここにコードを記述...
};
```