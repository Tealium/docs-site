---
title: 関数のトリガー
description: この記事では、各関数タイプのトリガーについて説明します。
url: https://docs.tealium.com/ja/server-side/functions/triggers/
---
関数は、関数タイプに応じて、データパイプライン内のさまざまな時点で発生するイベントによってトリガーされます。

## データ変換関数

データ変換関数には、関数の実行をトリガーする条件を指定するルールであるカスタムトリガーがあります。データ変換関数のトリガー条件が満たされると、次のデータパイプライン図に示すように、イベントまたはデータレコードがデータソースから収集された後、かつイベントまたはデータレコードが処理される前に、関数が呼び出されます。データ変換関数は、ファイルインポートイベントを除くすべてのイベントタイプをサポートします。

![](https://docs.tealium.com/images/server-side/functions-transform-data-pipeline.png)


<blockquote>
カスタムトリガーによってトリガーできる関数は1つだけです。イベントまたはデータレコードが複数の関数トリガーに一致する場合、**Date Modified**が最も古い関数だけがトリガーされます。
</blockquote>


詳細については、[データ変換関数について]()を参照してください。

## イベント関数と訪問関数
<!-- ## イベント関数、訪問関数、データレコード関数 -->

[イベント関数]()は、次のデータパイプライン図に示すように、イベントが処理された後に呼び出されます。

![](https://docs.tealium.com/images/server-side/functions-event-data-pipeline.png)

[訪問関数]()は、次のデータパイプライン図に示すように、訪問が処理された後に呼び出されます。

![](https://docs.tealium.com/images/server-side/functions-visit-visitor-data-pipeline.png)

<!-->

[Data Cloud Activationデータレコード関数]()は、次のデータパイプライン図に示すように、データレコードが処理された後に呼び出されます。

![](https://docs.tealium.com/images/server-side/functions-data-record-pipeline.png)

-->