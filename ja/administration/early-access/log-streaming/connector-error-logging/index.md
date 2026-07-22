---
title: コネクターエラーログ
description: この記事では、コネクターエラーログソースの構成方法、ログパラメータの確認方法、およびコネクターエラーのトラブルシューティング方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/log-streaming/connector-error-logging/
---

<blockquote>
ログストリーミングはEarly Accessであり、選ばれた顧客のみが利用可能です。この機能を試してみたい場合は、Tealiumサポート担当者に連絡してください。
</blockquote>


## 動作原理

監視されたコネクターアクションがエラーを返すと、Tealiumは構造化されたJSONログレコードを生成し、ログソースを通じて関連する宛先コネクターに転送します。宛先プラットフォームはこれらのレコードをダッシュボード、アラート、および分析のためにインデックス付けします。

宛先とログソースがどのように連携するかの概要については、[ログストリーミングについて](https://docs.tealium.com/about-log-streaming/)を参照してください。

## コネクターエラーログの構成

ログソースを作成するには、[ログソースの作成](https://docs.tealium.com/manage-log-streaming/#create-a-log-source)を参照してください。

**コネクターエラー**ログソースタイプを使用する場合：

* 監視するコネクターを選択します。
* すべてのアクションをログに記録するか、選択したアクションのみをログに記録するかを選択します。
* イベント属性を宛先で必要とされるパラメータにマッピングします。

各ログソースは以下の範囲で構成できます：

* すべてのコネクターとアクション
* 特定のコネクターやアクション、例えば単一のキャンペーンなど

ログ量を制限するために、コネクターのすべてのアクションをログに記録するのではなく、特定のアクションを選択します。
## コネクターエラーログソースの詳細を表示

宛先の**ログソース**テーブルで任意のコネクターエラーログソースをクリックしてその詳細を表示します：

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-log-source-details-overview.png)

### 概要タブ

**概要**タブには以下が表示されます：

* 基本情報（名前、メモ、UID、ラベル）
* 成功とエラーのトレンドチャート
* 選択した時間範囲の要約統計

以下のメトリックが表示されます：

* **総ボリューム**  
  選択した時間枠内に送信されたログイベントの総数。

* **リトライ**  
  失敗したログ配信のリトライ試行回数。

* **総成功**  
  成功裏に配信されたログイベントの数。

* **リトライ後の成功**  
  一回以上のリトライ後に成功裏に配信されたイベントの数。

* **総エラー**  
  配信に失敗したログイベントの数、リトライ後に成功したものを含む。

### コネクタータブ

**コネクター**タブには、ログソースによって監視されているコネクターがリストされています。これには以下が含まれます：

* 利用可能なアクションの総数
* 監視されているアクションの数
* ラベル

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-log-source-details-connectors.png)

各コネクター内で、個々のアクションを選択するか、構成されているすべてのアクションを監視することができます：

![](https://docs.tealium.com/images/early-access/log-streaming/log-streaming-select-connector-actions.png)

## ログを使用してコネクターエラーをトラブルシューティングする

コネクターエラーログによって生成されたログを使用して、コネクター実行の問題を特定、分類、解決します。

### 範囲と影響を確認する

* コネクターインターフェースで、過去1日、7日、30日の配信グラフ（成功 vs. エラー）を確認します。
* どのコネクターやアクションが影響を受けているか、エラーがいつ始まったかを特定します。
* 詳細な分析のためにメトリックとサンプルエラーをエクスポートします。

### エラータイプを分類する

ログを使用してエラーをカテゴリー分けします：

* **4xxエラー**（例：「無効なID」、「見つからない」）  
  通常、データまたは構成の問題を示します。

* **429または5xxエラー**  
  通常、ベンダーのレート制限または障害を示します。

* **タイムアウトエラー**  
  ベンダーが5秒以内に応答しない場合に発生します。タイムアウトエラーはリトライされません。

### 適切な修正を適用する

* データまたは構成のエラー：マッピングを修正し、IDを正しくし、必要な識別子が存在することを確認します。
* ベンダーの制限または障害：ベンダーと調整し、必要に応じて突発的なトラフィックを減らします。
* プラットフォームのスロットリング：根本的な問題を解決し、回復を監視します。

### 誤構成または不正なデータ

**典型的な原因：**
* トリガーにおける識別子の欠落または無効
* 不正なキャンペーンまたはアカウントID
* 必要なパラメータの欠落
* 権限またはポリシーの欠落（例：AWS IAM構成）

**解決策：**
* コネクターUIでエラーを確認します。
* 必要なデータが存在することを確認するための条件を追加します。
* ベンダーシステムに対してIDを検証します。
* 構成と権限を修正します。

### ベンダーのレート制限、タイムアウト、または障害

**典型的な原因：**
* HTTP 429、5xx、またはゲートウェイエラー
* ベンダータイムアウト（5秒以内に応答なし）
* ベンダーの容量を超えるトラフィックの急増

**プラットフォームの挙動：**
* Tealiumは429および5xxエラーを最大3回までリトライします。
* タイムアウトエラーはリトライされません。
* リトライ動作はコネクターごとに制御されます。

**解決策：**
* ベンダーログを確認します。
* ベンダーの制限または容量を増やします。
* 可能な場合は突発的なトラフィックを減らします。
* 時間をかけてエラー率を監視します。

### Tealiumの過負荷保護

**典型的な原因：**
* 高い失敗率の持続
* ベンダーの不安定さまたは構成の問題

**プラットフォームの挙動：**
* 失敗率が閾値を超えると、Tealiumはコネクターを一時停止またはスロットルする場合があります。
* エラー率が減少するにつれて、処理は徐々に再開されます。

**解決策：**
* 素早く根本原因を解決します。
* 回復動作を監視します。
* コネクターや地域をまたいで問題が持続する場合は、Tealiumサポートに連絡します。

## コネクターログパラメータ

以下の表は、コネクターエラーログで利用可能なすべてのパラメータをリストしています。マッピングでこれらのパラメータを参照する場合は、二重の中括弧を使用します（例：`{{connectorType}}`）。

| パラメータ | 説明 |
| ---- | ---- |
| `logger` | イベントを生成するために使用されるログ記録ユーティリティインスタンス |
| `account` | コネクターが構成されているアカウント |
| `profile` | コネクターが構成されているプロファイル |
| `customId` | コネクターアクションID。この値を見つけるには、コネクターをクリックし、次にアクションをクリックし、次に**詳細**をクリックします。 |
| `severityNumber` | 数値の重大度レベル |
| `severityText` | テキストの重大度レベル（例：ERROR） |
| `connectorType` | コネクターベンダー名 |
| `groupId` | 特定のコネクターアクション実行のログをグループ化するための識別子 |
| `result.executionTimeMs` | 実行時間（ミリ秒） |
| `result.status` | 実行結果：SUCCESSまたはFAILURE |
| `result.failure.code.name` | エラータイプ名（例：APIエラー） |
| `result.failure.code.id` | 数値のエラータイプ識別子 |
| `actionType` | コネクターアクションのタイプ（例：send_events） |
| `streamType` | EVENTまたはVISITOR |
| `result.failure.errorsCount` | 実行中のエラーの総数 |
| `result.failure.code.description` | 人間が読めるエラーの説明 |
| `recordSendDateTime` | ログレコードが送信された日時 |
| `actionsCount` | ログイベントで実行されたアクションの数 |
| `dimension` | エージェントが宛先に送信する前に構成した分類フィールド（例：LOG_LEVEL_ERROR） |
| `timestamp` | イベントが発生した時間 |
| `visitorId` | 訪問識別子（`tealium_visitor_id`）。バッチコネクターの場合、バッチからの訪問IDが1つだけ参照されます。 |
| `http.0.response.body` | HTTPレスポンスボディ |
| `result.failure.error.0.message` | 失敗を説明する具体的なエラーメッセージ |
| `http.0.response.statusCode` | HTTPレスポンスステータスコード（例：404、500） |
| `http.0.executionTimeMs` | HTTPリクエストの実行時間（ミリ秒） |
| `result.failure.error.0.count` | 特定のエラータイプの発生回数 |


<blockquote>
パラメータ名の数字（例：`http.0.executionTimeMs`）は、実行中に行われたHTTPコールの順序を表します。複数のコールが発生する場合、各リクエストに対して数字が増加します：最初のコールは`http.0`、2回目のコールは`http.1`、以降同様です。
</blockquote>

## 例示ログ

コネクタエラーログエントリは、[OpenTelemetry Protocol (OTLP)](https://opentelemetry.io/docs/specs/otlp/) ResourceLogs JSON形式を使用します。ペイロードは以下のように構成されています：

* `resourceLogs[].resource.attributes[]`: `account`、`profile`、`customId`など、ソースを識別するリソースレベルのフィールド。
* `resourceLogs[].scopeLogs[].logRecords[].attributes[]`: `connectorType`、`http.0.response.statusCode`、`result.failure.code.name`など、エラーの詳細を含むイベントレベルのフィールド。

各属性はキーと値のペアで、値には型があります（例：`stringValue`や`intValue`）。

以下にコネクタエラーログの例を示します：

```json
{
  "resourceLogs": [
    {
      "resource": {
        "attributes": [
          {
            "value": {
              "stringValue": "connector-errors"
            },
            "key": "logger"
          },
          {
            "value": {
              "stringValue": "ACCOUNT_NAME"
            },
            "key": "account"
          },
          {
            "value": {
              "stringValue": "PROFILE_NAME"
            },
            "key": "profile"
          },
          {
            "value": {
              "stringValue": "12345678-1234-1234-1234-123456789012"
            },
            "key": "customId"
          }
        ]
      },
      "scopeLogs": [
        {
          "scope": {},
          "logRecords": [
            {
              "severityNumber": 17,
              "severityText": "ERROR",
              "attributes": [
                {
                  "value": {
                    "stringValue": "webhook"
                  },
                  "key": "connectorType"
                },
                {
                  "value": {
                    "stringValue": "404 Not Found"
                  },
                  "key": "http.0.response.body"
                },
                {
                  "value": {
                    "stringValue": "Error: received non-successful http response status = 404"
                  },
                  "key": "result.failure.error.0.message"
                },
                {
                  "value": {
                    "stringValue": "e71684df-90e6-4c4d-8cb2-695da67402a0"
                  },
                  "key": "groupId"
                },
                {
                  "value": {
                    "intValue": "368"
                  },
                  "key": "result.executionTimeMs"
                },
                {
                  "value": {
                    "intValue": "1"
                  },
                  "key": "result.failure.error.0.count"
                },
                {
                  "value": {
                    "stringValue": "FAILURE"
                  },
                  "key": "result.status"
                },
                {
                  "value": {
                    "stringValue": "API Error"
                  },
                  "key": "result.failure.code.name"
                },
                {
                  "value": {
                    "intValue": "404"
                  },
                  "key": "http.0.response.statusCode"
                },
                {
                  "value": {
                    "intValue": "1"
                  },
                  "key": "result.failure.code.id"
                },
                {
                  "value": {
                    "stringValue": "send_events"
                  },
                  "key": "actionType"
                },
                {
                  "value": {
                    "intValue": "226"
                  },
                  "key": "http.0.executionTimeMs"
                },
                {
                  "value": {
                    "stringValue": "EVENT"
                  },
                  "key": "streamType"
                },
                {
                  "value": {
                    "intValue": "1"
                  },
                  "key": "result.failure.errorsCount"
                },
                {
                  "value": {
                    "stringValue": "An error occurred communicating with the vendor"
                  },
                  "key": "result.failure.code.description"
                },
                {
                  "value": {
                    "stringValue": "2024-12-03T19:26:44.921+0000"
                  },
                  "key": "recordSendDateTime"
                },
                {
                  "value": {
                    "intValue": "1"
                  },
                  "key": "actionsCount"
                },
                {
                  "value": {
                    "stringValue": "LOG_LEVEL_ERROR"
                  },
                  "key": "dimension"
                },
                {
                  "value": {
                    "stringValue": "2024-12-03T19:26:44.920978481Z"
                  },
                  "key": "timestamp"
                },
                {
                  "value": {
                    "stringValue": "5be887275efa4ea08137f3ea8b253e59"
                  },
                  "key": "visitorId"
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```