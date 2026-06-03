---
title: レート制限
description: この記事では、Data Connectのレート制限について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/rate-limits/
---
Data Connectは以下のレート制限を使用します：

* Tealium Eventsアプリは以下の制限があります：
  * イベントのレート制限は500イベント/秒です。
  * レコードのレート制限は500レコード/秒です。大きなファイルサイズは、それぞれ500レコードのバッチに分割されます。 Data Connectの使用量が上記のレートを超えると、接続がスロットルされます。
* Workato JSONインポートファイルの最大サイズ：10 MB。
* Data Connectリクエストの最大サイズ：2.5 MB。

 コストを削減し、処理効率を向上させるために、上記の制限に従ってファイルバッチを最大化し、ビジネス目標を達成するために必要なWorkato [タスク]()の数を最小限に抑えます。
