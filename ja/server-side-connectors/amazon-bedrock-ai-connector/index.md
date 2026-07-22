---
title: Amazon Bedrock AIコネクタ構成ガイド
description: Amazon Bedrock AIコネクタを構成して、Tealiumのイベントデータと訪問データをリアルタイムでエンリッチするために、基盤モデル、管理されたプロンプト、または複数ステップのBedrockワークフローに送信します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-bedrock-ai-connector/
---

<blockquote>
AIコネクタの動作概要とAIコネクタまたはTealium機能をいつ使用するかについてのガイダンスについては、[AIコネクタとTealium機能](https://docs.tealium.com/ai-connectors-and-functions/)を参照してください。
</blockquote>


## サポートされているモデル

Amazon Bedrock AIコネクタは、幅広い基盤モデルをサポートしています。現在サポートされているモデルのリストについては、[Amazon Bedrock: Amazon Bedrockでサポートされている基盤モデル](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html)を参照してください。

一部のBedrockモデルはプロビジョニングされたスループットが必要であり、オンデマンド推論を使用して呼び出すことはできません。オンデマンドスループットエラーに遭遇した場合は、`ON_DEMAND`推論をサポートするモデルを使用するか、構成リストにプロビジョニングされたスループットまたは推論プロファイルARNを提供してください。

## IAMロールと権限の作成

Tealiumは、サーバーサイドコネクタからAmazon Bedrockに接続するために、AWSアカウント内のIAMロールと権限が必要です。接続を認証するには2つのオプションがあります：

* [アクセスキーとアクセスシークレットを提供する](#access-key-and-secret-credentials)。
* [STS認証情報を提供する](#sts-credentials)。

### アクセスキーとシークレット認証情報

AWSアクセスキーとシークレットを作成するには：

1. AWS管理コンソールにログインし、**IAM**（Identity and Access Management）サービスに移動します。
1. **ユーザー**をクリックし、**ユーザーを追加**をクリックします。
1. ユーザー名を入力します。例：`TealiumBedrockUser`。
1. ユーザーにポリシーをアタッチします。詳細については、[ポリシーのアタッチ](#attach-policies)を参照してください。
1. キーを作成します。
    * **セキュリティ認証情報**タブに移動し、**アクセスキーの作成**をクリックします。
    * **アクセスキーID**と**シークレットアクセスキー**をコピーし、安全に保存します。

### STS認証情報

STS認証情報を作成するには：

1. AWS管理コンソールにログインし、**IAM**（Identity and Access Management）サービスに移動します。
1. **ロール**をクリックし、**ロールの作成**をクリックします。
1. **信頼されたエンティティタイプ**で、AWSアカウントを選択します。
1. **別のAWSアカウント**を選択し、TealiumアカウントID：`757913464184`を入力します。
1. （オプション）**外部IDが必要**チェックボックスを選択し、使用する外部IDを指定します。外部IDは最大256文字で、英数字（`A-Z`, `a-z`, `0-9`）およびハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を含めることができます。
1. ロールの名前を入力します。ロール名は`TealiumBedrock`で始まる必要があります。例：`TealiumBedrock-RoleName`。
1. ロールにポリシーをアタッチします。詳細については、[ポリシーのアタッチ](#attach-policies)を参照してください。
1. 信頼ポリシーを作成します。
    * **信頼関係**タブに移動し、**信頼関係の編集**をクリックします。
    * 作成したロールを使用するために特定の外部IDを許可する信頼ポリシーがあることを確認し、Tealiumの本番アカウントIDが`757913464184`であることを確認します。
    * Tealiumとの接続に使用する`EXTERNAL_ID`値を構成します。IDは最大256文字で、英数字（`A-Z`, `a-z`, `0-9`）およびハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を含めることができます。

```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "AWS": "arn:aws:iam::757913464184:root"
          },
          "Action": "sts:AssumeRole",
          "Condition": {
            "StringEquals": {
              "sts:ExternalId": "EXTERNAL_ID"
            }
          }
        }
      ]
    }
```

### ポリシーのアタッチ

AWS管理コンソールで、コネクタアクションに必要なポリシーを入力します。各コネクタアクションには次のポリシーが必要です：


<blockquote>
必要なフローやLambda関数の特定のARNに対してのみ権限を制限することをお勧めします。
</blockquote>





```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListModels",
      "Effect": "Allow",
      "Action": [
        "bedrock:ListFoundationModels"
      ],
      "Resource": "*"
    },
    {
      "Sid": "InvokeModel",
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeModel"
      ],
      "Resource": "*"
    }
  ]
}
```



```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RenderManagedPrompt",
      "Effect": "Allow",
      "Action": [
        "bedrock:RenderPrompt"
      ],
      "Resource": "*"
    }
  ]
}

```



Lambdaを使用する場合：

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BedrockFlowInvoke",
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeFlow"
      ],
      "Resource": "arn:aws:bedrock:<REGION>:<ACCOUNT_ID>:flow/<flow_id>/alias/<alias_name>"
    },
    {
      "Sid": "LambdaInvokeFunction",
      "Effect": "Allow",
      "Action": [
        "lambda:InvokeFunction"
      ],
      "Resource": "arn:aws:lambda:<REGION>:<ACCOUNT_ID>:function:<FUNCTION_NAME>"
    }
  ]
}
```

Lambdaを使用しない場合：

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BedrockFlowInvoke",
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeFlow"
      ],
      "Resource": "arn:aws:bedrock:<REGION>:<ACCOUNT_ID>:flow/<flow_id>/alias/<alias_name>"
    }
  ]
}
```



ポリシーを入力してアタッチするには：

1. AWSコンソールで**IAM > ポリシー**に移動し、**ポリシーの作成**をクリックします。
1. ポリシーエディタで**JSON**タブを選択し、コネクタアクション用のポリシーを貼り付け、検証警告を解決し、**次へ**をクリックします。
1. ポリシー名（例：`TealiumCustomAccessPolicy`）とオプションの説明を入力し、**ポリシーの作成**をクリックします。
1. **IAM > ロール**に移動し、変更したいロールを選択します。
1. **権限**タブで**権限の追加 > ポリシーのアタッチ**をクリックします。
1. カスタムポリシーを検索し、選択して**ポリシーのアタッチ**をクリックします。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法についての一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します：

* **認証タイプ**：（必須）使用する認証のタイプ。
    * **アクセスキー**
        * **アクセスキー**：（必須）IAMユーザーのアクセスキーを提供します。関連するIAMポリシー（IAMユーザーまたは想定されるロール用）は、データを送信するストリームに対して`bedrock:PutRecord`権限を付与する必要があります。
        * **シークレットキー**：（必須）IAMユーザーのシークレットキーを提供します。
    * **STS**
        * **STS - Assume Role: ARN**：（必須）想定されるロールに割り当てられたAmazonリソース名。詳細については、[AWS: IAMロールへの切り替え](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
        * **STS - Assume Role: Session Name**：（必須）想定されるロールセッションの一意の識別子。
        * **STS - Assume Role: External ID**：（オプション）第三者が顧客のアカウントでロールを想定する際に使用する一意の識別子。詳細については、[AWS: 第三者によるAWSアカウントへのアクセス](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html)を参照してください。
* **リージョン**：（必須）リージョンを選択します。
## プロンプト情報

Tealiumから送信されたり、Amazon Bedrock内で管理されたり、フローで使用されたりするBedrock AIプロンプトは、Tealiumがレスポンスを正しく処理できるように、有効なJSONのみを返すように作成する必要があります。以下のガイドラインに従ってください：

* マップされたパラメータを参照するには二重中括弧を使用します。例：`{{tealium_account}}`、`{{tealium_profile}}`、`{{tealium_visitor_id}}`、`{{visitor_json}}`。
* モデルに対して、説明、マークダウン、コードフェンス、JSONの前後の余分なテキストなしで、有効なJSONのみを返すように明確に指示します。
* 出力を安全に解析できるように、期待する正確なJSON構造（フィールド名、必要なキー、値のタイプ）を定義します。
* Tealiumフィールドを明示的に返すようにモデルに指示します（例：`tealium_account`、`tealium_profile`、`tealium_visitor_id`、`tealium_event`）。
* プロンプトで特定の属性を参照する必要がある場合は、その属性をベンダーパラメータにマッピングします。例えば、`Last product viewed`を`last_product_viewed`にマッピングし、プロンプトで`{{last_product_viewed}}`として参照します。
* 曖昧な指示を避けます。繰り返し呼び出しても同じJSONスキーマを生成する決定論的なプロンプトを書きます。
* 最良の結果を得るために、次のような行を含めます："プローズ、バックティック、追加のフォーマットなしで、単一のJSONオブジェクトのみを返します。"

### プロンプト例

```none
あなたは、有効なJSONのみを返す必要があるAIアシスタントです。
説明、マークダウン、コードフェンス、またはJSONオブジェクトの外側のテキストを含めないでください。

以下の訪問データを使用して、このセッションでの訪問の変換可能性を表す0から100の間の数値スコアを計算します。

単一のJSONオブジェクトのみを返し、この正確な構造で：

{
  "tealium_account": "{{tealium_account}}",
  "tealium_profile": "{{tealium_profile}}",
  "tealium_visitor_id": "{{tealium_visitor_id}}",
  "tealium_event": "bedrock_ai_insight",
  "visitor_score": <0から100の間の整数>
}

訪問データ：
{{visitor_json}}

{{last_product_viewed}}の値に特に注意してください。

```

レスポンスは以下のようになります：

```json
{
    "metrics": {
        "latencyMs": 1272
    },
    "output": {
        "message": {
            "content": [
                {
                    "text": "{\"tealium_account\":\"your-account\",\"tealium_profile\":\"main\",\"tealium_visitor_id\":\"__your-account_main__5574_438850__\",\"tealium_event\":\"bedrock_ai_insight\",\"visitor_score\":85}"
                }
            ],
            "role": "assistant"
        }
    },
    "stopReason": "end_turn",
    "usage": {
        "inputTokens": 8811,
        "outputTokens": 65,
        "serverToolUsage": {},
        "totalTokens": 8876
    }
}
```

コネクタはレスポンスを受け取り、JSONイベントオブジェクトをTealium Collect APIエンドポイントに送信します。

## Amazon Bedrockフロー

Amazon Bedrockフローは、プロンプト、ナレッジベース、Lambda関数、条件ロジック、外部データを組み合わせた複数ステップのAIオーケストレーションです。フローは、複雑なAI意思決定を単一のAPIエンドポイントに変換するために、入力データがプロンプト、エンリッチメントステップ、ビジネスロジック、最終出力を通過する方法を定義します。

**Send Data to Bedrock Flow**アクションを使用するには、Tealiumから入力を受け取るAmazon Bedrockでフローを作成し、AIステップを処理して結果をLambda関数を通じてTealiumに返送します。

以下のセクションでは、フローの必須およびオプションのコンポーネントについて説明します。

### ステップ1 - フロー入力の定義

すべてのフローは入力ノードから始まります。このノードは、Tealiumがフローに送信するJSONドキュメントを表します。

Tealiumは、次の例に似た形式でマップされた属性を送信します：

```json
"document": {
    "tealium_account": "services-example",
    "tealium_profile": "ai",
    "tealium_visitor_id": "1234567890abc",
    "visitor_profile": {
        "lifetime_value": "1200",
        "total_orders": 5,
        ...
        }
}
```

フロー内でフィールドを参照するには、`$.data.attribute_name`を使用します。前の例に基づいて：

| Tealium属性 | Bedrock参照 | 例 |
| -----| ----- | ----- |
| `tealium_account` | `$.data.tealium_account` または `{{tealium_account}}` | `services-example` |
| `tealium_profile` | `$.data.tealium_profile` または `{{tealium_profile}}` | `ai` |
| `tealium_visitor_id` | `$.data.tealium_visitor_id` または `{{tealium_visitor_id}}` | `1234567890abc` |
| `visitor_profile` | `$.data.visitor_profile` |  `"visitor_profile": {"lifetime_value": "1200","total_orders": 5,...}` |

### ステップ2 - プロンプトノードにデータをマッピングする（必須）

次に、AI出力（スコア、推奨事項、または決定など）を生成するためのプロンプトノードを追加します。

プロンプトノード内で：

1. プロンプトテキストを構成します。
1. `{{fieldname}}`形式を使用して変数を挿入します。例：`{{tealium_account}}`。
1. Bedrockモデルを選択します。
1. プロンプトの出力として有効なJSONを返します。

例については、上記の[プロンプト例](#prompt-example)セクションを参照してください。

### ステップ3 - （オプション）ナレッジベースの取得を追加する

Amazon Bedrockナレッジベースを使用すると、AIワークフローをAmazon S3、Amazon Redshift、またはAmazon OpenSearch Serviceなどの外部データソースに接続できます。ナレッジベースはドキュメントを保存およびインデックス化し、プロンプト実行中の取得および接地に使用できるようにします。このステップはオプションですが、パーソナライゼーション、レコメンデーション、またはコンテキストに基づいた意思決定には価値があります。

ナレッジベースを接続した後、`{{$.kbResults}}`のようなフィールドを使用して、ナレッジベースの結果をプロンプトに渡すことができます。

ナレッジベースに関する詳細は、[Amazon Bedrock: Retrieve data and generate AI responses with Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html)を参照してください。

ナレッジベースの作成に関する詳細は、[Amazon Bedrock: Create a knowledge base by connecting to a data source in Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-create.html)を参照してください。

### ステップ4 - Tealiumとの統合に必要なLambdaノードを追加する

プロンプトが構造化されたJSONを生成した後、その結果をプロファイルエンリッチメントのためにTealiumに戻す必要があります。

Lambdaノードを追加します：

* プロンプトノードからの出力（`$.data`）を受け取ります。
* JSONを解析します。
* Tealium Collectに投稿します：`POST https://collect.tealiumiq.com/event`。
* 次のものを含みます：
  * `tealium_account`
  * `tealium_profile`
  * `tealium_visitor_id`
  * `tealium_event`（ユーザー定義）
  * AI出力フィールド（例：`visitor_score`）

[提供されたLambda例](#lambda-example)を使用するか、独自のものを構築します。

### ステップ5 - フロー出力ノードを追加する

TealiumはフローのAPIレスポンスを処理しませんが、出力ノードはフローを完了するために必要です。

Lambda出力を`FlowOutputNode`に接続することはTealiumの処理に影響を与えませんが、次のツールを使用してフローが機能していることを確認するのに役立ちます：

* Bedrockコンソールでのデバッグ。
* Lambda関数からのエラーの表示。
* 検証のための最終JSON結果の検査。
* Traceを使用したTealiumでの出力の表示。
#### Lambdaの例

以下は、プロンプト出力を受け入れ、JSONを解析し、TealiumのCollectエンドポイントにデータを送信してTealiumでエンリッチメントとアクティベーションを行うLambdaの例です。さまざまなデータ構造を考慮したフォールバックが含まれています。必要に応じて書き換えてください。

アカウントとプロファイルは、指定されたデータソースでサーバーサイドイベントを受け入れるように構成する必要があります。


<blockquote>
この例は、ランタイム環境としてNode.jsバージョン18.x以降が必要です。
</blockquote>



```js
const COLLECT_URL = process.env.COLLECT_URL || "https://collect.tealiumiq.com/event";
function extractInputByName(event, name) {
  const arr = event?.node?.inputs;
  if (Array.isArray(arr)) {
    const hit = arr.find(i => i?.name === name);
    if (hit && typeof hit.value === "string") return hit.value;
    if (hit && typeof hit.value === "object") return JSON.stringify(hit.value);
  }
  return undefined;
}
function extractJsonStringFromEvent(event) {
  const fromStandardPin = extractInputByName(event, "codeHookInput");
  if (typeof fromStandardPin === "string") return fromStandardPin;
  const anyString = event?.node?.inputs?.find?.(i => typeof i?.value === "string")?.value;
  if (typeof anyString === "string") return anyString;
  if (typeof event?.codeHookInput === "string") return event.codeHookInput;
  if (typeof event?.document === "string") return event.document;
  const doc = event?.fields?.[0]?.content?.document;
  if (typeof doc === "string") return doc;
  if (typeof event === "string") return event;
  throw new Error("Could not find JSON string in event");
}
export const handler = async (event) => {
  try {
    const jsonStr = extractJsonStringFromEvent(event);
    const obj = JSON.parse(jsonStr);  // Fixed: store parsed result
    const required = ["tealium_account", "tealium_profile", "tealium_visitor_id"];
    for (const key of required) {
      if (!Object.prototype.hasOwnProperty.call(obj, key)) {
        throw new Error(`Missing required field '${key}' in model output`);
      }
    }
    const r = await fetch(COLLECT_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: jsonStr
    });
    if (!r.ok) {
      const txt = await r.text().catch(() => "");
      throw new Error(`Collect failed ${r.status}: ${txt}`);
    }
    return jsonStr;
  } catch (err) {
    console.error("Shim error:", err);
    return JSON.stringify({ ok: false, error: String(err.message || err) });
  }
};
```


## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Bedrock AIモデルへのプロンプト送信 | ✓ | ✓ |
| Bedrock AI管理プロンプトへのデータ送信 | ✓ | ✓ |
| Bedrock AIワークフローへのデータ送信 | ✓ | ✓ |


### Bedrock AIモデルへのプロンプト送信

**Bedrock AIモデルへのプロンプト送信**を使用する場合、コネクタを通じて同期的にレスポンスを返すシンプルな単一モデルコールが必要です。

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| モデルIDまたは推論プロファイルARN | オンデマンド推論を使用するAmazon Bedrockモデルを選択するか、プロビジョニングスループットモデルARNまたは推論プロファイルARNを手動で入力します。<br>オンデマンド推論とテキスト入出力をサポートするモデルのみが表示されます。<br>希望のモデルが表示されない場合は、そのモデルがAWSアカウントとリージョンで有効になっているか確認してください。<br><br><br>プロビジョニングスループットを使用する場合は、完全なモデルARN（例：`arn:aws:bedrock:region:account-id:provisioned-model/...`）を入力します。<br>AWSアカウントで構成されている場合は、推論プロファイルARNも使用できます。<br>モデルの可用性とサポートされる推論タイプは、AWSアカウントの権限とリージョン構成によって決まります。|
| プロンプトパラメータ | プロンプト内のプレースホルダーにパラメータをマッピングします。デフォルトでは、コネクタは`{{tealium_account}}`、`{{tealium_profile}}`、`{{tealium_visitor_id}}`にアクセスできます。これらはマッピングで上書き可能です。 |
| 訪問プロファイルの追加 | (オーディエンスアクションのみ) プロンプトテンプレートで訪問プロファイルを変数`{{visitor_profile}}`として使用することを許可します。 |
| 現在の訪問の追加 | (オーディエンスアクションのみ) `{{visitor_profile}}`オブジェクトに現在の訪問データを含めるかどうか。 |
| イベントペイロードの追加 | (イベントアクションのみ) イベントペイロードをプロンプトテンプレートの変数`{{event_payload}}`として使用することを許可します。 |
| プロンプト | <ul><li>マッピングされたパラメータを参照するには、二重の中括弧を使用します。例：`{{tealium_account}}`, `{{visitor_id}}`, `{{event_value}}`。</li><li>`{{visitor_profile}}`を使用して、訪問プロファイルをプロンプトに含めます。<br>モデルには、説明、マークダウン、コードフェンス、余分なテキストなしで有効なJSONのみを返すように明確に指示します。</li><li>期待される正確なJSON構造を定義します（例：フィールド名、必要なキー、値の形式）。</li><li>Tealiumフィールドを含める必要がある場合は、プロンプトで明確に指定します。<br>あいまいな表現を避けます。決定論的なプロンプトを書きます。</li><li>「プローズ、バックティック、余分なフォーマットなしで、単一のJSONオブジェクトのみを返す」という直接的な指示を含めます。</li></ul> |
| デバッグモード | デバッグモードが有効になっている場合、コネクタはTealium Collectに送信する前に生のBedrockレスポンスを受け入れます。完全な処理を有効にする前に、Traceを使用してレスポンス形式を検証します。 |

#### 推論パラメータ

詳細については、[Amazon Bedrock API Reference: InferenceConfiguration](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent_InferenceConfiguration.html)を参照してください。

| パラメータ | 説明 |
| --- | --- |
| `maxTokens` | モデルがレスポンスで生成可能なトークンの最大数。値が低いほど出力が短くなり、レイテンシ、コスト、スロットリングリスクが低減します。 |
| `temperature` | 出力のランダム性を制御します。値が低い（例：`0.2`）とレスポンスがより決定論的になり、値が高い（例：`0.8`）とより創造的で多様な結果が得られます。 |
| `topP` | トークン選択をこの値を超える累積確率を持つ最小セットに制限する核サンプリングパラメータ。値が低いほど出力が集中し、値が高いほど多様性が許容されます。 |
| `stopSequences` | モデルが遭遇したときに生成を停止する一つまたは複数の文字列。レスポンスの切り捨てや構造化された出力境界の強制に役立ちます。 |
### Bedrock AI 管理プロンプトへデータを送信

**Bedrock AI 管理プロンプトへデータを送信**を使用する場合は、プロンプトがコネクタを通じて同期的に応答を返す、再利用可能でバージョン管理された呼び出しを行いたいときに使用します。

| パラメータ | 説明 |
| --- | --- |
| プロンプト ARN | (必須) Bedrock プロンプト管理テンプレートの ARN を提供してください。プロンプト ARN は Bedrock のプロンプト詳細の **概要** セクションで見つけることができます。 |
| プロンプトデータ | <ul><li>Tealium は、それを呼び出すときにマッピングされた属性をプロンプトに渡します。</li><li>コネクタには `tealium_account`、`tealium_profile`、`tealium_visitor_id` の変数が含まれており、マッピングで上書きすることができます。</li><li>モデルに JSON のみを返すように明確に指示するプロンプトを記述してください。説明、マークダウン、コードフェンス、JSON の前後の追加テキストは含まないでください。</li><li>モデルが JSON で `tealium_account`、`tealium_profile`、`tealium_visitor_id` を返すように指示を含めてプロンプトを作成する必要があります。</li><li>あいまいな表現を避けてください。出力が確実に解析できるように決定論的なプロンプトを記述してください。</li><li>最良の結果を得るためには、「JSON オブジェクトのみを返し、散文、バックティック、余分なフォーマットは含まない」という直接的な指示を含めてください。</li></ul> |
| 訪問プロファイルを追加 | (オーディエンスアクションのみ) プロンプトテンプレートで訪問プロファイルを `{{visitor_profile}}` 変数として使用することを許可するかどうか。 |
| 現在の訪問を追加 | (オーディエンスアクションのみ) `{{visitor_profile}}` オブジェクトに現在の訪問データを含めるかどうか。 |
| イベントペイロードを追加 | (イベントアクションのみ) プロンプトテンプレートでイベントペイロードを `{{event_payload}}` 変数として使用することを許可するかどうか。 |
| デバッグモード | デバッグモードが有効になっている場合、コネクタは Tealium Collect に送信することなく生の Bedrock 応答を受け入れます。完全な処理を有効にする前に応答形式を検証するために Trace を使用します。 |

### Bedrock AI ワークフローへデータを送信

**Bedrock AI ワークフローへデータを送信**を使用する場合は、Lambda を通じて非同期で実行されるマルチステップのオーケストレーションまたはナレッジベースの取得が必要なときに使用します。

| パラメータ | 説明 |
| --- | --- |
| Bedrock Flow Alias ARN | (必須) このアクションが呼び出す Bedrock Flow Alias の ARN を入力してください。`live` などのエイリアスを作成し、ここでその ARN を使用することをお勧めします。 |
| Flow データ | <ul><li>AWS でエイリアスが指す Flow バージョンをこのコネクタを更新せずに変更します。</li><li>コネクタはマッピングされたフィールドを document という JSON オブジェクトとして Flow に送信します。</li><li>Flow 内で、これらのフィールドを Prompt、Lambda、または他のノードで `$.data.<fieldName>` を使用して参照します。</li><li>デフォルトでは、`tealium_account`、`tealium_profile`、および `tealium_visitor_id` が自動的に含まれ、必要に応じてフィールドマッピングを通じて上書きすることができます。</li><li>Flow には `FlowOutputNode` を含める必要がありますが、Tealium はその出力を使用しません。</li><li>Collect エンドポイントを通じて Tealium にデータを送り返すために Lambda を使用します。</li><li>Bedrock コンソールでフローをテストする際に成功/エラー情報を確認するために、Lambda の出力を `FlowOutputNode` に接続することをお勧めします。</li></ul> |
| 訪問プロファイルを追加 | (オーディエンスアクションのみ) Flow 入力に完全な訪問プロファイルを `visitor_profile` JSON オブジェクトとして含めるかどうか。 |
| 現在の訪問を追加 | (オーディエンスアクションのみ) `visitor_profile` JSON オブジェクトに現在の訪問データを含めるかどうか。 |
| イベントペイロードを追加 | (イベントアクションのみ) Flow 入力にイベントペイロードを `event_payload` JSON オブジェクトとして含めるかどうか。 |

## 一般的なエラーとトラブルシューティング

以下は一般的なエラーコードと解決策です：

### 一般的な AWS エラーコード：

* **`AccessDeniedException` または `NotAuthorized`**   
IAM ユーザーまたはロールに必要な権限がありません（例：`bedrock:InvokeModel`, `bedrock:RenderPrompt`, `bedrock:InvokeFlow`, `bedrock:ListFoundationModels`）。  
これを解決するには、ロールまたはアクセスキーに添付されている IAM ポリシーを更新して、必要な Bedrock アクションを正しいリソースに含めてください。

* **`InvalidClientTokenId`, `UnrecognizedClientException`, または `ExpiredTokenException`**  
構成されたアクセスキーまたは STS セッションが無効または期限切れです。  
これを解決するには、コネクタで資格情報を回転させて再入力するか、STS ロールと外部 ID が正しく、期限切れでないことを確認してください。

* **`OptInRequired` または `FTUFormNotFilled`**  
AWS アカウントが Bedrock または特定のモデル（例：Anthropic）で完全に有効化されていません。  
これを解決するには、AWS コンソールで必要な Bedrock 有効化手順と任意のモデル固有のフォームまたはマーケットプレースのサブスクリプションを完了してください。

これらのエラーが表示された場合は、まず AWS で IAM またはアカウント構成を解決してください。権限が修正されるまでコネクタアクションを再試行しても成功しません。

### Bedrock API 呼び出しからの一般的なエラー

以下のエラーは、リクエストが Bedrock に到達したが、サービスまたはモデルが正常に完了できなかったことを意味します。

* **`ValidationException` または `ValidationError`**  
リクエスト本体またはパラメータがターゲットモデルまたは API に対して無効です（例：間違ったモデル ID、サポートされていないパラメータ、入力が大きすぎる）。  
これを解決するには、モデル ID / プロンプト ARN / フロー ARN を確認し、リクエスト本体がモデルの期待するスキーマに一致していることを確認し、必要に応じてプロンプトのサイズや最大トークン数を減らしてください。

* **`ResourceNotFound` または `ResourceNotFoundException`**   
指定されたモデル、プロンプトバージョン、または Flow エイリアス ARN が存在しないか、その地域で利用できません。  
これを解決するには、コネクタ構成の ARN と地域を Bedrock コンソールに表示されている値と照らし合わせて再確認してください。

* **`ThrottlingException` または `ServiceQuotaExceededException`**  
呼び出しが Bedrock のクォータを超えています（例：TPS またはトークン制限）。  
これを解決するには、呼び出し頻度を減らすか、AWS でクォータ増加をリクエストしてください。

* **`ServiceUnavailable`, `InternalFailure`, または `InternalServerException`**  
Bedrock 内の一時的または内部エラーです。  
これを解決するには、エラーが持続する場合は AWS Service Health Dashboard を確認するか、AWS サポートケースを開いてください。

* **`ModelErrorException`, `ModelNotReadyException`, または `ModelTimeoutException`** (プロンプトまたは管理プロンプトフロー)  
モデルが失敗した、まだウォーミングアップ中、または応答に時間がかかりすぎました。  
これを解決するには、待って再試行し、プロンプトを簡素化するかトークン使用を減らし、モデルまたはプロビジョニングされたスループットが完全にアクティブであることを確認してください。

これらのエラーについては、Tealium は Bedrock からの元の AWS エラーメッセージを表示するため、トラブルシューティング時に AWS のドキュメントと照らし合わせることができます。