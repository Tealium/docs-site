---
title: データレイヤー
description: HTTP APIライブラリからのデータレイヤー変数について学びます。
url: https://docs.tealium.com/ja/platforms/http-api/data-layer/
---
## 標準パラメーター

Tealium Collectは、各リクエストで以下の標準パラメーターをサポートしています：

| パラメーター | 説明 |
| --- | --- |
| `tealium_account` | あなたのTealiumアカウントの名前です。 |
| `tealium_profile` | あなたのTealiumプロファイルの名前です。デフォルト値は `main` です。 |
| `tealium_datasource` | 任意。データソースキーです。詳細については、[データソース]()を参照してください。 |
| `tealium_event` | 推奨。トラッキング目的のイベント名です。 |
| `tealium_visitor_id` | Tealium AudienceStreamに必要です。イベントに関連付けられた訪問の匿名化された一意の識別子です |
| `tealium_trace_id` | 任意。[トレース]()で使用します。 |

リクエストの形式は使用されるHTTPメソッドによって異なります。以下の例ではプレースホルダー値が次の形式で中括弧で表されています：`{VALUE}`。

## カスタムイベントパラメーター

追加のイベント属性は、トラッキングニーズに応じてカスタムパラメーターとして送信されます。これらのパラメーターを[Tealium Customer Data Hubのイベント属性として定義]()してください。
