---
title: AI アクティベーション用の関数を作成する
description: 外部 AI モデルを Tealium 関数に接続し、イベントデータと訪問データを使用してリアルタイム予測を呼び出し、訪問プロファイルをエンリッチします。
url: https://docs.tealium.com/ja/guides/function-for-ai-activation/
---
このガイドでは、リアルタイムアクティベーションを実現するために、外部 AI モデルを Tealium 関数と統合する方法について説明します。モデルエンドポイントに安全に接続し、イベントデータと訪問データを使用して AI 予測を呼び出し、そのモデル出力によって訪問プロファイルをエンリッチします。また、非同期レスポンスと一般的な統合上の問題についても説明します。

ユースケースに応じて Tealium 関数と AI コネクタのどちらを使用すべきかについては、[AI コネクタと Tealium 関数](https://docs.tealium.com/ai-connectors-and-functions/)を参照してください。

## 仕組み

関数を使用して外部 AI モデルを呼び出し、解約リスク、不正検出、傾向スコアリング、ネクストベストアクションのレコメンデーションなどのタスクを実行します。関数は、イベントデータと訪問プロファイル属性を収集してペイロードを作成し、モデルエンドポイントに送信して予測を受け取り、アクティベーションに使用する訪問プロファイルを更新します。

リアルタイムのモデル推論とアクティベーションにおけるデータフローには、次の手順が含まれます。

1. **顧客アクション**：ユーザーがアクション（製品の表示、カートへの追加、フォームの送信など）を実行します。
1. **関数トリガー**：構成されたトリガーに基づいてイベント関数または訪問関数が実行され、予測（スコア、分類、レコメンデーション）を返します。
1. **Collect へのイベント送信**：関数が `track()` メソッドを使用して予測データを Tealium Collect に送信します。
1. **エンリッチメント処理**：構成されたエンリッチメントが、予測値を訪問プロファイル属性に書き込みます。
1. **ダウンストリームアクティベーション**：更新されたプロファイル属性に基づいてオーディエンスが評価され、コネクタが実行されます。

関数は訪問プロファイルを直接変更できないため、予測は Tealium Collect を経由し、エンリッチメントを通じてプロファイルに書き込む必要があります。

`track()` メソッドはイベントを Tealium Collect に送信します。これらのイベント属性値を訪問プロファイル属性に書き込むには、エンリッチメントを構成する必要があります。

### 関数の種類

| 関数の種類 | トリガー | シグネチャ | ユースケース |
|-------------|----------------|------------|----------------|
| イベント関数 | 特定のイベントが処理された後に実行 | `{ event, helper }` | 直近のイベントコンテキストに基づくスコアリング（製品表示時の製品レコメンデーションなど） |
| 訪問関数 | 訪問プロファイルが更新された後に実行 | `{ visitor, visit, helper }` | 蓄積されたプロファイルデータに基づくスコアリング（エンゲージメント履歴に基づく解約予測など） |

関数を使用して外部 AI モデルを呼び出し、リアルタイムの推論とアクティベーションを行うことで、次のようなメリットが得られます。

* 訪問の行動から顧客の解約リスクをリアルタイムで検出できます。
* リスクの高い訪問を特定し、リテンションキャンペーンのターゲティングを改善できます。
* AI ベースの予測をセグメンテーションに使用し、パーソナライズされたエクスペリエンスを提供できます。
* モデルに基づくインサイトでプロファイルをエンリッチし、ダウンストリームアクティベーションの精度を高められます。
* スループットの高いデータストリームを処理し、タイムリーな分析と対応を実現できます。
* マーケティング、分析、コンプライアンスのワークフローにおけるデータ品質を改善できます。

### 前提条件

AI モデルを呼び出す関数を作成する前に、次のものが用意されていることを確認してください。

* Snowflake Cortex、Databricks Model Serving、AWS SageMaker、Google Vertex AI、Azure ML、Hugging Face Inference Endpoints、または任意の HTTPS エンドポイントなど、REST API エンドポイントにデプロイされた学習済み ML モデル。
* API キー、Bearer トークン、JWT など、モデルエンドポイントの API 認証情報。
* プロファイルのリージョンに対応する Tealium の IP アドレスを、データクラウドの許可リストに追加します。詳細については、[許可する Tealium IP アドレス]()を参照してください。
* モデルが想定するリクエストペイロードのスキーマ。
* モデルが返すレスポンスペイロードのスキーマ。

## AI ベースの解約リスク分析の主要コンポーネント

* **データ変換関数**  
    受信したイベントデータを評価し、正規表現を適用して、解約リスクに関連する行動を特定します。

* **派生属性**  
    イベントデータから解約リスクスコアを計算します。関数は各イベントにこの値を構成します。

* **AudienceStream イベントフィルター**  
    解約リスクスコアを使用してイベントをフィルタリングします。リスクの高いイベントのみが訪問プロファイルをエンリッチします。

* **イベントフィード**  
    フラグが構成された高リスクイベントを、コネクタ、保存、またはその他の関数による追加処理に向けてストリーミングします。

* **外部モデル呼び出し関数**  
    エンリッチされたイベントデータまたはプロファイルデータを外部 AI モデルのエンドポイントに送信し、高度な解約予測を実行します。

* **エンリッチメント**  
    AI モデルの予測を訪問プロファイル属性に書き込み、アクティベーションとセグメンテーションに使用できるようにします。

## 要件

このソリューションを実装するには、次のものが必要です。

* Tealium の要件
    * AudienceStream が有効になっていること
    * Tealium 関数が有効になっていること
    * `track()` イベントを受信するよう構成されたデータソース
    * 予測属性を訪問プロファイルに書き込むためのエンリッチメント
* モデルエンドポイントの要件
    * HTTPS プロトコルを使用すること
    * 10 秒以内に応答すること。リアルタイムパーソナライゼーションでは、500 ミリ秒未満の応答時間を推奨します。
    * Bearer トークン、API キー、またはヘッダーベースの認証を使用すること
    * JSON 形式で応答すること

## ステップ 1：関数を作成する

AI アクティベーションロジックは、イベント関数または訪問関数のいずれかを使用して実装できます。ユースケースとスコアリング時に利用できるデータに最も適した関数の種類を選択してください。

### コードリファレンス

| オブジェクト／メソッド | 説明 |
| ---------- | ----------|
| `event.data.udo.*` | トリガーとなったイベントのイベント属性 |
| `visitor.properties.*` | 訪問プロファイルの文字列属性 |
| `visitor.metrics.*` | 訪問プロファイルの数値属性 |
| `visitor.audiences` | 訪問が属するオーディエンス |
| `visitor.current_visit.*` | 訪問の現在のセッションにおける訪問属性 |
| `helper.getAuth('name')` | 保存されている認証トークンを取得 |
| `helper.getGlobalVariable('name')` | 保存されているグローバル変数を取得 |
| `track(data, config)` | イベントを Tealium Collect に送信（1 回の呼び出しにつき最大 6 回） |

### プラットフォーム固有の注意事項

次のコード例は、一般的な REST API パターンを示しています。実際の実装はプラットフォームによって異なります。

| プラットフォーム | 注意事項 |
|-------------------------|---------------|
| Snowflake Cortex | Cortex 関数は、Snowflake SQL API を使用して SQL ステートメントから呼び出します。JWT 認証が必要です。 |
| Databricks Model Serving | MLflow モデルは REST エンドポイントとして公開されます。パーソナルアクセストークン（PAT）認証を使用します。Jobs API を通じた非同期推論をサポートします。 |
| AWS SageMaker | エンドポイントには AWS Signature Version 4 認証が必要です。認証を簡素化するには、Lambda プロキシの使用を検討してください。長時間実行されるジョブ向けの非同期推論エンドポイントをサポートします。 |
| Hugging Face | Inference Endpoints は Bearer トークン認証を使用します。レスポンス形式はモデルの種類によって異なります。 |
| GCP Vertex | Vertex AI エンドポイントは OAuth 2.0 またはサービスアカウント認証を使用します。 |
| Azure | Azure ML マネージドエンドポイントは、API キーまたは Azure AD トークン認証を使用します。 |

リクエスト／レスポンス形式と認証要件については、使用しているプラットフォームの API ドキュメントを参照してください。
### イベント関数の例

次の例は、イベント関数から外部モデル API を呼び出す方法を示しています。モデルの API に合わせて、ペイロード構造とレスポンスの解析処理を調整してください。


```js
activate(async ({ event, helper }) => {
  // 1. Assemble feature payload from event data
  // Adapt this to match your model's expected input format
  const payload = {
    product_id: event.data.udo.product_id,
    category: event.data.udo.product_category,
    price: event.data.udo.product_price
  };
  // 2. Call your model API
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
  // 3. Send prediction to Tealium Collect
  // Adapt the attribute names to match your model's response
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


### 訪問関数の例

訪問関数では、蓄積されたプロファイルデータにアクセスしてスコアリングできます。ただし、訪問関数は `event` オブジェクトにアクセスできないため、`account`、`profile`、および `datasource` の値にはグローバル変数を使用する必要があります。


```js
activate(async ({ visitor, visit, helper }) => {
  // Assemble payload from visitor profile attributes
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
  // For Visitor Functions, use Global Variables for routing
  // Include visitor_id to ensure the event stitches to the correct profile
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


### モデルのレスポンスが遅い場合の処理

モデルの推論に 10 秒以上かかる場合は、非同期パターンを使用します。関数はリクエストを送信し、直ちに終了します。処理が完了すると、モデルが Tealium にコールバックします。

1. 関数が訪問データとコールバック URL をモデルエンドポイントに送信する
1. モデルエンドポイントが直ちに 202 Accepted を返す
1. 関数が終了する（タイムアウトなし）
1. モデルが非同期で推論を完了する
1. モデルが予測結果を Tealium の HTTP API に POST する
1. エンリッチメントによって予測結果が訪問プロファイルに書き込まれる

#### モデルのコールバック用 HTTP API データソースを作成する

モデルのコールバックを受信するための HTTP API データソースを作成します。詳細については、[データソースの作成](https://docs.tealium.com/create-data-source/)を参照してください。

### 非同期関数のコード

次の関数コードを使用します。


```js
activate(async ({ visitor, visit, helper }) => {
  const payload = {
    visitor_id: visitor.properties.visitor_id,
    lifetime_value: visitor.metrics.lifetime_value,
    purchase_count: visitor.metrics.purchase_count,
    callback_url: helper.getGlobalVariable('TEALIUM_CALLBACK_URL'),
    callback_datasource: helper.getGlobalVariable('DATASOURCE_KEY')
  };
  // Fire and forget - don't await the response
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
  // Function exits immediately - model will callback when ready
});
```


### モデルのコールバックペイロード

推論が完了したら、モデルエンドポイントから Tealium HTTP API に POST する必要があります。

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

`tealium_visitor_id` を含めることで、予測結果が正しい訪問プロファイルに結合されます。これらの属性をプロファイルに書き込むには、ステップ 3 の説明に従ってエンリッチメントを構成します。

## ステップ 2：ML プラットフォームの認証情報を構成する

安全にアクセスできるように、モデル API の認証情報と構成を Tealium 関数に保存します。

### ML プラットフォームの認証トークンを追加する

Tealium プラットフォーム上の関数に API 認証情報を保存するには、認証トークンを追加します。この例では、API キーまたはトークンを `model_api_token` として保存します。詳細については、[認証の追加](https://docs.tealium.com/add-authentication-to-function/)を参照してください。

次のコードを使用して、関数内でトークンを取得します。

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
認証トークンは、HTTP リクエスト内でのみ関数から参照できます。HTTP リクエストの外部でトークンを参照しようとすると、トークンは UUID プレースホルダーに置き換えられます。
</blockquote>


### ML プラットフォームのグローバル変数を追加する

モデルエンドポイントの URL や名前など、関数の構成情報をグローバル変数として保存します。この例では、モデルエンドポイントの URL を `MODEL_ENDPOINT_URL` として保存します。詳細については、[グローバル変数の管理](https://docs.tealium.com/manage-global-variables/)を参照してください。

次のコードを使用して、関数内で変数を取得します。

```
  const response = await fetch(
    helper.getGlobalVariable('MODEL_ENDPOINT_URL'),
    {
...
    }
  );
```

## ステップ 3：訪問プロファイルにチャーンスコアを追加する

ダウンストリームシステムで予測結果をアクティベートするには、まず訪問プロファイルにモデルの出力を保存して処理するための属性とエンリッチメントを構成する必要があります。

### チャーンスコアのプロファイル属性を作成する

モデルの予測結果を訪問プロファイルに保存するための属性を作成します。この例では、数値属性 `churn_score` を作成します。

詳細については、[属性の作成](https://docs.tealium.com/manage-as-attributes/#create-an-attribute)を参照してください。

作成した属性をエンリッチし、イベントのモデル予測結果を訪問プロファイルに書き込みます。エンリッチメントがない場合、予測結果は訪問プロファイルに表示されません。この例では、`tealium_event` が `model_prediction`（または使用するイベント名）と等しい場合に、`track()` 呼び出しのイベント属性 `prediction_score` を訪問属性 `churn_score` に書き込むエンリッチメントを作成します。


[
  [
    {
      "input": "tealium_event",
      "operator": "equals (ignore case)",
      "filter": "model_prediction"
    }
  ] 
]


詳細については、[エンリッチメントの追加](https://docs.tealium.com/add-enrichment/)を参照してください。

## ステップ 4：チャーンリスクの高いオーディエンスをアクティベートする

予測属性を使用してオーディエンスを構築し、アクションをトリガーしてチャーンリスクに対応します。
### チャーンリスクオーディエンスの作成

予測属性に基づいてオーディエンスを作成します。この例では、`churn_score` が `0.7` より大きい訪問を対象とする `High Churn Risk` オーディエンスを作成します。


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

コネクタアクションをオーディエンスに関連付け、予測値に基づいてアクティブ化します。この例では、チャーンリスクが高いユーザーにリテンションメールを送信したり、購入意向に基づいてユーザーをリマーケティングオーディエンスに追加したりできます。

詳細については、[コネクタの追加](https://docs.tealium.com/add-connector/)を参照してください。

## デバッグ

### ログの表示

デバッグには `console.log()` を使用します。

```
console.log('Payload:', JSON.stringify(payload));
console.log('Response status:', response.status);
console.log('Result:', JSON.stringify(result));
```

ログを表示するには、関数エディターの **Logs** タブをクリックします。

### よくある問題

| 問題 | 解決策 |
|---|---|
| 関数がタイムアウトする | モデルが10秒以内に応答することを確認します。専用エンドポイントまたはプロビジョニング済みエンドポイントを使用してください。モデルの平均応答時間に応じて、非同期でのモデル呼び出しを検討してください。 |
| 予測がプロファイルに表示されない | エンリッチメントが構成されていることを確認します。`tealium_datasource` の値を確認してください。 |
| 認証エラー | **Auth Tokens** でトークンの値を確認します。トークンの有効期限を確認してください。 |
| `track()` が実行されない | `track()` より前にエラーが発生していないか確認します。データソースが有効であることを確認してください。 |

## リソース

* [関数](https://docs.tealium.com/about-functions/)