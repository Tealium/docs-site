---
title: AIアクティベーション用の関数を作成する
description: イベントデータと訪問データを使用してリアルタイム予測を行い、訪問プロファイルをエンリッチするために外部AIモデルをTealium関数に接続します。
url: https://docs.tealium.com/ja/guides/function-for-ai-activation/
---
このガイドでは、リアルタイムアクティベーションのために外部AIモデルをTealium関数に統合する方法について説明します。モデルエンドポイントに安全に接続し、イベントデータと訪問データを使用してAI予測を呼び出し、モデル出力で訪問プロファイルを豊かにします。非同期応答と一般的な統合問題についても取り上げます。

Tealium関数またはAIコネクタを使用するタイミングについての情報は、[AIコネクタとTealium関数](https://docs.tealium.com/ai-connectors-and-functions/)を参照してください。

## 動作原理

機能を使用して、顧客離脱リスク、詐欺検出、傾向スコアリング、次の最適なアクションの推奨などのタスクのために外部AIモデルを呼び出します。機能はイベントデータと訪問プロファイル属性を収集し、ペイロードを構築し、モデルエンドポイントに送信し、予測を受け取り、アクティベーションのために訪問プロファイルを更新します。

リアルタイムモデル推論とアクティベーションのためのデータフローには、以下のステップが含まれます：

1. **顧客アクション**: ユーザーがアクションを実行します（例：商品を見る、カートに追加する、フォームを送信する）。
1. **機能トリガー**: イベントまたは訪問機能が構成されたトリガーに基づいて発火し、予測（スコア、分類、推奨）を返します。
1. **イベントを収集する**: 機能は予測データを`track()`メソッドを通じてTealium Collectに送信します。
1. **エンリッチメント処理**: 構成されたエンリッチメントが予測値を訪問プロファイル属性に書き込みます。
1. **ダウンストリームアクティベーション**: オーディエンスが評価し、更新されたプロファイル属性に基づいてコネクタが発火します。

機能は直接訪問プロファイルを変更することはできないため、予測はTealium Collectを通じてプロファイルに書き込まれる必要があります。

`track()`メソッドはイベントをTealium Collectに送信します。これらのイベント属性値を訪問プロファイル属性に書き込むためにエンリッチメントを構成する必要があります。

### 機能の種類

| 機能の種類 | トリガー | シグネチャ | 使用例 |
|-------------|----------------|------------|----------------|
| イベント機能 | 特定のイベントが処理された後に発火 | `{ event, helper }` | 即時のイベントコンテキストに基づいてスコアリング（例：商品閲覧時の商品推薦） |
| 訪問機能 | 訪問プロファイルが更新された後に発火 | `{ visitor, visit, helper }` | 蓄積されたプロファイルデータに基づいてスコアリング（例：エンゲージメント履歴に基づく顧客離脱予測） |

リアルタイム推論とアクティベーションのために外部AIモデルを呼び出すことで、以下のような複数の利点があります：

* 訪問の行動からリアルタイムで顧客離脱リスクを検出します。
* 高リスク訪問を特定することでリテンションキャンペーンのターゲティングを改善します。
* AIに基づく予測を使用してセグメンテーションによるパーソナライズされた体験をサポートします。
* モデル駆動の洞察によってプロファイルをエンリッチすることで、ダウンストリームアクティベーションの精度を向上させます。
* 高スループットデータストリームを処理してタイムリーな分析と対応を行います。
* マーケティング、アナリティクス、コンプライアンスのワークフローのデータ品質を向上させます。

### 前提条件

AIモデルを呼び出すための機能を作成する前に、以下のものを確保してください：

* REST APIエンドポイントにデプロイされた訓練済みのMLモデル、例えばSnowflake Cortex、Databricks Model Serving、AWS SageMaker、Google Vertex AI、Azure ML、Hugging Face Inference Endpoints、または任意のHTTPSエンドポイント。
* モデルエンドポイントのAPI認証情報、例えばAPIキー、ベアラートークン、またはJWT。
* プロファイルリージョンのTealium IPアドレスをデータクラウドの許可リストに追加します。詳細については、[許可するTealium IPアドレス]()を参照してください。
* モデルが期待するリクエストペイロードスキーマ。
* モデルが返すレスポンスペイロードスキーマ。

## AIに基づく顧客離脱リスク分析のための主要コンポーネント

* **データ変換機能**  
    受信イベントデータを評価し、正規表現を適用して顧客離脱リスクに関連する行動を特定します。

* **派生属性**  
    イベントデータから顧客離脱リスクスコアを計算します。この値は各イベントに対して機能によって構成されます。

* **AudienceStreamイベントフィルター**  
    顧客離脱リスクスコアを使用してイベントをフィルタリングします。高リスクのイベントのみが訪問プロファイルを豊かにします。

* **イベントフィード**  
    高リスクとフラグ付けされたイベントをコネクタ、保存、または他の機能によるさらなる処理のためにストリーミングします。

* **外部モデル呼び出し機能**  
    イベントまたはプロファイルデータを外部AIモデルエンドポイントに送信して高度な顧客離脱予測を行います。

* **エンリッチメント**  
    AIモデルの予測を訪問プロファイル属性に書き込み、アクティベーションとセグメンテーションのために使用します。

## 要件

このソリューションを実装するためには、以下が必要です：

* Tealiumの要件
    * AudienceStreamが有効になっていること
    * Tealiumの機能が有効になっていること
    * `track()`イベントを受信するための構成済みデータソース
    * 予測属性を訪問プロファイルに書き込むためのエンリッチメント
* モデルエンドポイントの要件
    * HTTPSプロトコルを使用すること
    * 10秒以内に応答すること。リアルタイムパーソナライゼーションのためには、応答時間が500ミリ秒未満であることを推奨します。
    * ベアラートークン、APIキー、またはヘッダーベースの認証を使用すること
    * JSON形式で応答すること。

## ステップ1: 機能を作成する

イベント機能または訪問機能を使用してAIアクティベーションロジックを実装できます。使用例とスコアリング時の利用可能なデータに最も適した機能タイプを選択します。

### コード参照

| オブジェクト/メソッド | 説明 |
| ---------- | ----------|
| `event.data.udo.*` | トリガーイベントからのイベント属性 |
| `visitor.properties.*` | 訪問プロファイルの文字列属性 |
| `visitor.metrics.*` | 訪問プロファイルの数値属性 |
| `visitor.audiences` | 訪問のオーディエンスメンバーシップ |
| `visitor.current_visit.*` | 訪問の現在のセッションからの訪問属性 |
| `helper.getAuth('name')` | 保存された認証トークンを取得 |
| `helper.getGlobalVariable('name')` | 保存されたグローバル変数を取得 |
| `track(data, config)` | Tealium Collectにイベントを送信（呼び出し毎に最大6回） |

### プラットフォーム固有の注意点

以下のコード例は一般的なREST APIパターンを示しています。実際の実装はプラットフォームによって異なります：

| プラットフォーム                | 注意点         |
|-------------------------|---------------|
| Snowflake Cortex        | Cortex機能はSnowflake SQL APIを使用してSQLステートメントを通じて呼び出されます。JWT認証が必要です。                                   |
| Databricks Model Serving| MLflowモデルはRESTエンドポイントとして公開されます。個人アクセストークン（PAT）認証を使用します。ジョブAPIを通じて非同期推論をサポートします。|
| AWS SageMaker           | エンドポイントはAWS署名バージョン4認証が必要です。認証を簡素化するためにLambdaプロキシの使用を検討してください。長時間実行されるジョブのための非同期推論エンドポイントをサポートします。 |
| Hugging Face            | 推論エンドポイントはベアラートークン認証を使用します。レスポンス形式はモデルタイプに依存します。                                                |
| GCP Vertex              | Vertex AIエンドポイントはOAuth 2.0またはサービスアカウント認証を使用します。                                                                          |
| Azure                   | Azure ML管理エンドポイントはAPIキーまたはAzure ADトークン認証を使用します。                                                                      |

プラットフォームのAPIドキュメントを参照して、リクエスト/レスポンス形式と認証要件について確認してください。
### イベント関数の例

次の例は、イベント関数から外部モデルAPIを呼び出す方法を示しています。ペイロードの構造とレスポンスの解析を、あなたのモデルのAPIに合わせて調整してください。


```js
activate(async ({ event, helper }) => {
  // 1. イベントデータから特徴ペイロードを組み立てる
  // これをモデルの期待する入力形式に合わせて調整してください
  const payload = {
    product_id: event.data.udo.product_id,
    category: event.data.udo.product_category,
    price: event.data.udo.product_price
  };
  // 2. モデルAPIを呼び出す
  const response = await fetch(
    helper.getGlobalVariable('MODEL_ENDPOINT_URL'),
    {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer ' + helper.getAuth('model_api_token'),
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(payload)
    }
  );
  if (!response.ok) {
    console.error('Model API error:', response.status);
    return;
  }
  const result = await response.json();
  // 3. Tealium Collectに予測を送信する
  // 属性名をモデルのレスポンスに合わせて調整してください
  track({
    tealium_event: 'model_prediction',
    prediction_score: result.score,
    prediction_label: result.label
  }, {
    tealium_account: event.account,
    tealium_profile: event.profile,
    tealium_datasource: helper.getGlobalVariable('DATASOURCE_KEY')
  });
});
```


### ビジター関数の例

ビジター関数は蓄積されたプロファイルデータにアクセスしてスコアリングが可能ですが、`event` オブジェクトにはアクセスできませんので、`account`、`profile`、および `datasource` の値にはグローバル変数を使用する必要があります。


```js
activate(async ({ visitor, visit, helper }) => {
  // ビジタープロファイル属性からペイロードを組み立てる
  const payload = {
    lifetime_value: visitor.metrics.lifetime_value,
    purchase_count: visitor.metrics.purchase_count,
    days_since_last_purchase: visitor.metrics.days_since_last_purchase,
    loyalty_tier: visitor.properties.loyalty_tier
  };
  const response = await fetch(
    helper.getGlobalVariable('MODEL_ENDPOINT_URL'),
    {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer ' + helper.getAuth('model_api_token'),
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(payload)
    }
  );
  if (!response.ok) {
    console.error('Model API error:', response.status);
    return;
  }
  const result = await response.json();
  // ビジター関数では、ルーティングにグローバル変数を使用する
  // イベントが正しいプロファイルに紐付けられるようにvisitor_idを含める
  track({
    tealium_event: 'churn_prediction',
    tealium_visitor_id: visitor.properties.visitor_id,
    churn_score: result.churn_probability,
    churn_risk_tier: result.risk_tier
  }, {
    tealium_account: helper.getGlobalVariable('TEALIUM_ACCOUNT'),
    tealium_profile: helper.getGlobalVariable('TEALIUM_PROFILE'),
    tealium_datasource: helper.getGlobalVariable('DATASOURCE_KEY')
  });
});
```


### モデル応答の遅延処理

モデル推論に10秒以上かかる場合は、非同期パターンを使用します。関数はリクエストを送信してすぐに終了します。処理が完了すると、モデルがTealiumにコールバックします。

1. 関数はビジターデータとコールバックURLをモデルエンドポイントに送信します
1. モデルエンドポイントは直ちに202 Acceptedを返します
1. 関数は終了します（タイムアウトなし）
1. モデルは非同期で推論を完了します
1. モデルはTealiumのHTTP APIに予測をPOSTします
1. エンリッチメントは予測をビジタープロファイルに書き込みます

#### モデルコールバック用のHTTP APIデータソースを作成する

モデルコールバックを受信するためのHTTP APIデータソースを作成します。詳細については、[データソースを作成する](https://docs.tealium.com/create-data-source/)を参照してください。

### 非同期関数コード

次の関数コードを使用します：


```js
activate(async ({ visitor, visit, helper }) => {
  const payload = {
    visitor_id: visitor.properties.visitor_id,
    lifetime_value: visitor.metrics.lifetime_value,
    purchase_count: visitor.metrics.purchase_count,
    callback_url: helper.getGlobalVariable('TEALIUM_CALLBACK_URL'),
    callback_datasource: helper.getGlobalVariable('DATASOURCE_KEY')
  };
  // 応答を待たずに発火 - レスポンスを待たない
  fetch(
    helper.getGlobalVariable('MODEL_ENDPOINT_URL'),
    {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer ' + helper.getAuth('model_api_token'),
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(payload)
    }
  ).catch(error => console.error('Request failed:', error.message));
  // 関数はすぐに終了 - モデルが準備ができたときにコールバックする
});
```


### モデルコールバックペイロード

モデルエンドポイントは、推論が完了するとTealium HTTP APIにPOSTする必要があります：

```
POST https://collect.tealiumiq.com/event?tealium_account={account}&tealium_profile={profile}&tealium_datasource={datasource_key}

{
  "tealium_event": "model_prediction_complete",
  "tealium_visitor_id": "original_visitor_id_from_request",
  "churn_score": 0.82,
  "churn_risk_tier": "high",
  "model_version": "v2.1"
}
```

`tealium_visitor_id`を含めることで、予測が正しいビジタープロファイルに紐付けられることが保証されます。ステップ3で説明されているように、これらの属性をプロファイルに書き込むためにエンリッチメントを構成します。

## ステップ2: MLプラットフォームの認証情報を構成する

モデルAPIの認証情報と構成をTealium関数に安全に保存します。

### MLプラットフォームの認証トークンを追加する

Tealiumプラットフォームの関数にAPI認証情報を保存するには、認証トークンを追加します。この例では、APIキーまたはトークンエンドポイントURLを`model_api_token`として保存します。詳細については、[認証を追加する](https://docs.tealium.com/add-authentication-to-function/)を参照してください。

関数でトークンを取得するには、次のコードを使用します：

```
    {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer ' + helper.getAuth('model_api_token'),
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(payload)
    }
```


<blockquote>
認証トークンは、HTTPリクエスト内の関数からのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。
</blockquote>


### MLプラットフォームのグローバル変数を追加する

関数のための構成情報、例えばモデルエンドポイントのURLや名前をグローバル変数として保存します。この例では、モデルエンドポイントのURLを`MODEL_ENDPOINT_URL`として保存します。詳細については、[グローバル変数を管理する](https://docs.tealium.com/manage-global-variables/)を参照してください。

関数で変数を取得するには、次のコードを使用します：

```
  const response = await fetch(
    helper.getGlobalVariable('MODEL_ENDPOINT_URL'),
...
    }
  );
```

## ステップ3: ビジタープロファイルにチャーンスコアを追加する

予測を下流システムで活用する前に、モデルの出力をビジタープロファイルに保存して処理するための属性とエンリッチメントを構成する必要があります。

### チャーンスコアプロファイル属性を作成する

ビジタープロファイルにモデルの予測を保存するための属性を作成します。この例では、`churn_score`という数値属性を作成します。

詳細については、[属性を作成する](https://docs.tealium.com/manage-as-attributes/#create-an-attribute)を参照してください。

作成した属性にモデルの予測をイベントからビジタープロファイルに書き込むためのエンリッチメントを作成します。エンリッチメントがなければ、予測はビジタープロファイルに表示されません。この例では、`tealium_event`が`model_prediction`（またはあなたのイベント名）と等しい場合に、`track()`コールから`prediction_score`イベント属性を`churn_score`ビジター属性に書き込むエンリッチメントを作成します。


[
  [
    {
      "input": "tealium_event",
      "operator": "equals (ignore case)",
      "filter": "model_prediction"
    }
  ] 
]


詳細については、[エンリッチメントを追加する](https://docs.tealium.com/add-enrichment/)を参照してください。

## ステップ4: 高リスクのチャーンオーディエンスを活性化する

予測属性を使用してオーディエンスを構築し、チャーンリスクに基づいてアクションをトリガーして活性化します。
### チャーンリスクオーディエンスの作成

予測属性に基づいてオーディエンスを作成します。この例では、`churn_score`が`0.7`を超える訪問のために`High Churn Risk`オーディエンスを作成します。


[
  [
    {
      "input": "churn_score",
      "operator": "greater than",
      "filter": "0.7"
    }
  ] 
]


詳細については、[オーディエンスの作成](https://docs.tealium.com/manage-audiences/#create-an-audience)を参照してください。

### コネクタの構成

予測値に基づいてオーディエンスにコネクタアクションをアタッチしてアクティベートします。この例では、高いチャーンリスクのためのリテンションメールをトリガーしたり、購買意向に基づいてユーザーをリマーケティングオーディエンスに追加することができます。

詳細については、[コネクタの追加](https://docs.tealium.com/add-connector/)を参照してください。

## デバッグ

### ログの表示

デバッグには`console.log()`を使用します：

```
console.log('Payload:', JSON.stringify(payload));
console.log('Response status:', response.status);
console.log('Result:', JSON.stringify(result));
```

ログを表示するには、関数エディターの**ログ**タブをクリックします。

### 一般的な問題

| 問題                        | 解決策                                                                                                   |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| 関数がタイムアウトする           | モデルが10秒以内に応答することを確認してください。専用またはプロビジョニングされたエンドポイントを使用してください。平均モデル応答時間に応じて非同期モデル呼び出しを検討してください。 |
| プロファイルに予測が表示されない  | エンリッチメントが構成されていることを確認してください。`tealium_datasource`の値をチェックしてください。                                       |
| 認証エラー                    | **認証トークン**でトークン値を確認してください。トークンの有効期限をチェックしてください。                                                 |
| `track()`が実行されない      | `track()`の前にエラーをチェックしてください。データソースがアクティブであることを確認してください。                                           |

## リソース

* [関数](https://docs.tealium.com/about-functions/)