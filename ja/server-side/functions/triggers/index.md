---
title: 関数トリガー
description: この記事では、各関数タイプのトリガーに関する情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/triggers/
---
関数は、関数タイプに応じて、データパイプラインの異なるポイントでイベントによってトリガーされます。

## データ変換関数

データ変換関数にはカスタムトリガーがあり、これは関数の実行をトリガーする条件を指定するルールです。データ変換関数のトリガー条件が満たされると、データソースからイベントまたはデータレコードが収集された後、そしてイベントまたはデータレコードが処理される前に、以下のデータパイプライン図に示されているように、関数が呼び出されます。データ変換関数は、ファイルインポートイベントを除くすべてのイベントタイプをサポートします。

![](https://docs.tealium.com/images/server-side/functions-transform-data-pipeline.png)


<blockquote>
カスタムトリガーによってトリガーされる関数は1つだけです。イベントまたはデータレコードが複数の関数トリガーに一致する場合、最も古い**Date Modified**を持つ関数のみがトリガーされます。
</blockquote>


詳細については、[データ変換関数について]()を参照してください。

## イベントと訪問関数

[イベント関数]()は、イベントが処理された後に呼び出されます。以下のデータパイプライン図に示されています：

![](https://docs.tealium.com/images/server-side/functions-event-data-pipeline.png)

[訪問関数]()は、訪問が処理された後に呼び出されます。以下のデータパイプライン図に示されています：

![](https://docs.tealium.com/images/server-side/functions-visit-visitor-data-pipeline.png)