---
title: データレイヤー
description: HTTP APIライブラリのデータレイヤー変数について説明します。
url: https://docs.tealium.com/ja/platforms/http-api/data-layer/
---
## 標準パラメータ

Tealium Collectは、各リクエストで次の標準パラメータをサポートしています。

| パラメータ | 説明 |
| --- | --- |
| `tealium_account` | Tealiumアカウントの名前。 |
| `tealium_profile` | Tealiumプロファイルの名前。デフォルト値は`main`です。 |
| `tealium_datasource` | （オプション）データソースキー。詳細については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。 |
| `tealium_event` | 推奨。トラッキングに使用するイベントの名前。 |
| `tealium_visitor_id` | Customer Data Platform（CDP）では必須。イベントに関連付けられた訪問を表す、匿名化された一意の識別子。 |
| `tealium_trace_id` | （オプション）[Trace](https://docs.tealium.com/manage-traces/)で使用します。 |

リクエストの形式は、使用するHTTPメソッドによって異なります。以下の例では、プレースホルダー値を`{VALUE}`の形式で中括弧を使用して表します。

## カスタムイベントパラメータ

トラッキングの要件に応じて、追加のイベント属性をカスタムパラメータとして送信します。これらのパラメータは、[Tealium Customer Data Hubのイベント属性](https://docs.tealium.com/add-enrichment/)として定義します。