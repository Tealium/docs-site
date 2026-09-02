---
title: イベント仕様：データ品質
description: イベント仕様を定義した後、Live Eventsは受信データの品質を表示します。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/data-quality/
---
チャートのカラーコード付きバーは、データに対するイベント仕様の検証に応じて区切られています。

![](https://docs.tealium.com/images/server-side/getting-started-eventstream-live-events-all-filters.png)
<!-- GAP: replace getting-started-eventstream-live-events-all-filters.png with a screenshot of the live events chart showing all four segments: Valid (green), Warn (yellow), Invalid (red), and No Spec (blue) -->

イベント仕様検証付きのLive Events：

* **Valid (Green)**  
有効なイベントはイベント仕様の要件を満たしています。イベントには`tealium_event`属性の既知の値があり、必要な属性がすべて正しいデータ型で含まれています。

* **Warn (Yellow)**  
警告イベントはイベント仕様と一致し、必要な属性はすべて検証を通過しますが、1つ以上のオプション属性が欠落しているか、間違ったデータ型を持っています。

* **Invalid (Red)**  
無効なイベントはイベント仕様と一致しますが、少なくとも1つの必要な属性が欠けているか、間違ったデータ型を持っているか、構成されたデータ値ルールと一致しません。

* **No Spec (Blue)**  
**No Spec**とマークされたイベントは対応するイベント仕様がありません。イベントには`tealium_event`属性がないか、値に対応するイベント仕様がありません。

フィルターのいずれかをクリックして、その値の表示を切り替えてチャートの表示を調整します。

これでデータレイヤーのインストールと構成の基本が完了しました。次のチュートリアルでは、アクション可能なイベントフィードを作成する方法を示します。