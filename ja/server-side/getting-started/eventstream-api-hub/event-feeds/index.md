---
title: イベントフィード
description: イベントフィードは、その属性に基づいた特定の条件に一致するイベントの集合です。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/event-feeds/
---
デフォルトのイベントフィードは `All Events` という名前で、すべての入力イベントを含んでいますが、その属性に基づいてイベントのサブセットを識別する新しいフィードを作成することができます。

## 仕組み

フィードは、ベンダーコネクタを使用してアクションを取るための最も重要なタイプのイベントを識別します。

以下がその仕組みです：

* **フィード名**  
イベントフィードには、コネクタアクションを構成する際など、インターフェース全体でそれを識別する名前があります。あなたとあなたのチームにとって意味のあるユーザーフレンドリーな名前を選んでください。  
例：`Purchases with Order Total Over $1,000`
* **条件**  
各フィードには、**All Events** フィードからフィルタリングするための1つ以上の条件が必要です。イベント属性の値を使用して、特定のタイプのイベントを識別するシンプルなルールを作成します。  
例：  
    ```none
    tealium_event EQUALS "purchase"
    AND
    order_total IS GREATER THAN 1000
    ```
* **Live Eventsで表示**  
フィードを作成した後、**Live Events** でそれを表示して、そのイベントのみを表示します。このインターフェースは、デバッグ、新しいイベント仕様の作成、またはフィードの健康状態の監視に役立ちます。
* **コネクタでの使用**  
イベントフィードが作成された後、それをコネクタで使用して、データをベンダーに送信します。これがAPIハブの動作です。

## 例

以下は、`search` イベントを識別し、その結果が `0` だったイベントフィードの例です。このフィードは、検索エンジンの健康状態を監視し、または検索機能を改善するのに役立つことができます。

フィードには2つの条件が含まれていることに注意してください：

* `tealium_event EQUALS "search"`
* `search_results EQUALS 0`

イベントフィードの例：**Search with No Results**

![](https://docs.tealium.com/images/server-side/getting-started-eventstream-event-feed-example.png)

次のチュートリアルでは、イベントフィードの追加方法を学びます。