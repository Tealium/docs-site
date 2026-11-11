---
title: Amazon Bedrock AI コネクタ構成ガイド
description: Amazon Bedrock AI コネクタを構成し、Tealium のイベントデータと訪問データを基盤モデル、マネージドプロンプト、または複数ステップの Bedrock ワークフローに送信して、リアルタイムでエンリッチメントを行います。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-bedrock-ai-connector/
---

<blockquote>
AI コネクタの仕組みの概要と、AI コネクタまたは Tealium Functions を使用する状況についてのガイダンスは、[AI コネクタと Tealium Functions](https://docs.tealium.com/ai-connectors-and-functions/)を参照してください。
</blockquote>


## サポートされるモデル

Amazon Bedrock AI コネクタは、さまざまな基盤モデルをサポートしています。現在サポートされているモデルの一覧については、[Amazon Bedrock：Amazon Bedrock でサポートされる基盤モデル](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html)を参照してください。

一部の Bedrock モデルではプロビジョンドスループットが必要であり、オンデマンド推論を使用して呼び出すことはできません。オンデマンドスループットエラーが発生した場合は、`ON_DEMAND` 推論をサポートするモデルを使用するか、構成リストでプロビジョンドスループットまたは推論プロファイルの ARN を指定してください。

## IAM ロールと権限の作成

サーバーサイドコネクタから Amazon Bedrock に接続するには、AWS アカウントに IAM ロールと権限が必要です。接続を認証するには、次の 2 つの方法があります。

* [アクセスキーとシークレットアクセスキーを指定する](#access-key-and-secret-credentials)。
* [STS 認証情報を指定する](#sts-credentials)。

### アクセスキーとシークレットの認証情報

AWS アクセスキーとシークレットを作成するには、次の手順を実行します。

1. AWS マネジメントコンソールにログインし、**IAM**（Identity and Access Management）サービスに移動します。
1. **Users** をクリックし、次に **Add user** をクリックします。
1. ユーザー名を入力します。例：`TealiumBedrockUser`
1. ユーザーにポリシーをアタッチします。詳細については、[ポリシーのアタッチ](#attach-policies)を参照してください。
1. キーを作成します。
    * **Security credentials** タブに移動し、**Create Access Key** をクリックします。
    * **Access Key ID** と **Secret Access Key** をコピーし、安全に保存します。

### STS 認証情報

STS 認証情報を作成するには、次の手順を実行します。

1. AWS マネジメントコンソールにログインし、**IAM**（Identity and Access Management）サービスに移動します。
1. **Roles** をクリックし、次に **Create role** をクリックします。
1. **Trusted entity type** で AWS アカウントを選択します。
1. **Another AWS account** を選択し、Tealium アカウント ID `757913464184` を入力します。
1. （オプション）**Require external ID** チェックボックスを選択し、使用する外部 ID を指定します。外部 ID は最大 256 文字で、英数字（`A-Z`、`a-z`、`0-9`）と、ハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を使用できます。
1. ロールの名前を入力します。ロール名は `TealiumBedrock` で始まる必要があります。例：`TealiumBedrock-RoleName`
1. ロールにポリシーをアタッチします。詳細については、[ポリシーのアタッチ](#attach-policies)を参照してください。
1. 信頼ポリシーを作成します。
    * **Trust relationships** タブに移動し、**Edit trust relationship** をクリックします。
    * 作成したロールを特定の外部 ID が使用できるように信頼ポリシーが構成されていること、および Tealium の本番環境アカウント ID が `757913464184` であることを確認します。
    * Tealium への接続用に `EXTERNAL_ID` の値を構成します。ID は最大 256 文字で、英数字（`A-Z`、`a-z`、`0-9`）と、ハイフン（`-`）、アンダースコア（`_`）、ピリオド（`.`）などの記号を使用できます。

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

AWS マネジメントコンソールで、使用するコネクタアクションに必要なポリシーを入力します。各コネクタアクションには、次のポリシーが必要です。


<blockquote>
権限は、必要なフローおよび Lambda 関数の特定の ARN に制限することをお勧めします。
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



Lambda を使用している場合：

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

Lambda を使用していない場合：

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



ポリシーを入力してアタッチするには、次の手順を実行します。

1. AWS コンソールで **IAM > Policies** に移動し、**Create policy** をクリックします。
1. ポリシーエディタで **JSON** タブを選択し、コネクタアクション用のポリシーを貼り付け、検証の警告をすべて解決してから、**Next** をクリックします。
1. ポリシー名（例：`TealiumCustomAccessPolicy`）と、必要に応じて説明を入力し、**Create policy** をクリックします。
1. **IAM > Roles** に移動し、変更するロールを選択します。
1. **Permissions** タブで、**Add permissions > Attach policies** をクリックします。
1. カスタムポリシーを検索して選択し、**Attach policies** をクリックします。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **Authentication Type**：（必須）使用する認証の種類です。
    * **Access Key**
        * **Access Key**：（必須）IAM ユーザーのアクセスキーを指定します。関連付けられた IAM ポリシー（IAM ユーザーまたは引き受けたロールのいずれか）には、データを送信するストリームに加えて、`bedrock:PutRecord` 権限を付与する必要があります。
        * **Secret Key**：（必須）IAM ユーザーのシークレットキーを指定します。
    * **STS**
        * **STS - Assume Role: ARN**：（必須）引き受けるロールに割り当てられた Amazon リソースネームです。詳細については、[AWS：IAM ロールへの切り替え](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
        * **STS - Assume Role: Session Name**：（必須）引き受けたロールセッションの一意の識別子です。
        * **STS - Assume Role: External ID**：（オプション）第三者が顧客のアカウントでロールを引き受ける際に使用する一意の識別子です。詳細については、[AWS：第三者が所有する AWS アカウントへのアクセス](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html)を参照してください。
* **Region**：（必須）リージョンを選択します。

コネクタを構成したら、**Done** をクリックします。
## プロンプト情報

Tealium から送信する場合、Amazon Bedrock 内で管理する場合、またはフローで使用する場合のいずれであっても、Bedrock AI プロンプトは、Tealium がレスポンスを正しく処理できるよう、有効な JSON のみを返すように作成する必要があります。次のガイドラインに従ってください。

* マッピングされたパラメータを参照するには、二重中括弧を使用します。例：`{{tealium_account}}`、`{{tealium_profile}}`、`{{tealium_visitor_id}}`、`{{visitor_json}}`。
* 説明、Markdown、コードフェンス、および JSON の前後の余分なテキストを含めず、有効な JSON のみを返すようモデルに明確に指示します。
* 出力を安全に解析できるよう、想定する正確な JSON 構造（フィールド名、必須キー、値の型）を定義します。
* Tealium フィールド（`tealium_account`、`tealium_profile`、`tealium_visitor_id`、`tealium_event` など）を明示的に返すようモデルに指示します。
* プロンプト内で特定の属性を参照する必要がある場合は、その属性をベンダーパラメータにマッピングします。たとえば、`Last product viewed` を `last_product_viewed` にマッピングし、プロンプト内では `{{last_product_viewed}}` として参照します。
* 曖昧な指示は避けてください。呼び出しを繰り返しても同じ JSON スキーマが生成されるように、決定的なプロンプトを作成します。
* 最良の結果を得るには、次のような行を含めます。「説明文、バッククォート、追加の書式構成を一切含めず、単一の JSON オブジェクトのみを返してください。」

### プロンプトの例

```none
You are an AI assistant that must return only valid JSON.
Do not include explanations, markdown, code fences, or any text outside the JSON object.

Using the visitor data below, calculate a numeric score between 0 and 100 that represents
the visitor's likelihood to convert in this session.

Return a single JSON object only, with this exact structure:

{
  "tealium_account": "{{tealium_account}}",
  "tealium_profile": "{{tealium_profile}}",
  "tealium_visitor_id": "{{tealium_visitor_id}}",
  "tealium_event": "bedrock_ai_insight",
  "visitor_score": <integer between 0 and 100>
}

Visitor data:
{{visitor_json}}

Pay particular attention to the value of {{last_product_viewed}}.

```

レスポンスは次のようになります。

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

コネクタはレスポンスを受け取り、JSON イベントオブジェクトを Tealium Collect API エンドポイントに送信します。

## Amazon Bedrock Flows

Amazon Bedrock Flows は、プロンプト、ナレッジベース、Lambda 関数、条件ロジック、外部データを組み合わせて、再利用可能な単一のワークフローを構成するマルチステップの AI オーケストレーションです。フローでは、入力データがプロンプト、エンリッチメントステップ、ビジネスロジック、最終出力をどのように通過するかを定義し、複雑な AI による意思決定を単一の API エンドポイントとして利用できるようにします。

**Send Data to Bedrock Flow** アクションを使用するには、Tealium からの入力を受け取り、AI ステップで処理し、Lambda 関数を介して結果を Tealium に返すフローを Amazon Bedrock で作成します。

以下のセクションでは、フローの必須コンポーネントとオプションコンポーネントについて説明します。

### ステップ 1 - フロー入力を定義する

すべてのフローは入力ノードから始まります。このノードは、Tealium がフローに送信する JSON ドキュメントを表します。

Tealium は、マッピングされた属性を次の例のような形式で送信します。

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

フロー内では、`$.data.attribute_name` を使用してフィールドを参照します。前述の例に基づく参照方法は次のとおりです。

| Tealium 属性 | Bedrock の参照 | 例 |
| -----| ----- | ----- |
| `tealium_account` | `$.data.tealium_account` または `{{tealium_account}}` | `services-example` |
| `tealium_profile` | `$.data.tealium_profile` または `{{tealium_profile}}` | `ai` |
| `tealium_visitor_id` | `$.data.tealium_visitor_id` または `{{tealium_visitor_id}}` | `1234567890abc` |
| `visitor_profile` | `$.data.visitor_profile` |  `"visitor_profile": {"lifetime_value": "1200","total_orders": 5,...}` |

### ステップ 2 - データをプロンプトノードにマッピングする（必須）

次に、AI 出力（スコア、レコメンデーション、判断など）を生成するためのプロンプトノードを追加します。

プロンプトノード内で、次の操作を行います。

1. プロンプトテキストを構成します。
1. `{{fieldname}}` 形式を使用して変数を挿入します。例：`{{tealium_account}}`。
1. Bedrock モデルを選択します。
1. プロンプトの出力として有効な JSON を返します。

例については、上記の[プロンプトの例](#prompt-example)セクションを参照してください。

### ステップ 3 - （オプション）ナレッジベース検索を追加する

Amazon Bedrock Knowledge Bases を使用すると、AI ワークフローを Amazon S3、Amazon Redshift、Amazon OpenSearch Service などの外部データソースに接続できます。ナレッジベースはドキュメントを保存してインデックスを作成し、プロンプト実行時の検索やグラウンディングに利用できるようにします。フローにナレッジベースノードを追加すると、モデルはデータから関連情報を取得して使用し、より正確でコンテキストを考慮したレスポンスを生成できます。このステップはオプションですが、パーソナライゼーション、レコメンデーション、コンテキストに基づく意思決定に役立ちます。

ナレッジベースを接続した後、`{{$.kbResults}}` などのフィールドを使用して、ナレッジベースの結果をプロンプトに渡すことができます。

ナレッジベースの詳細については、[Amazon Bedrock：Amazon Bedrock Knowledge Bases でデータを取得し、AI レスポンスを生成する](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html)を参照してください。

ナレッジベースの作成方法については、[Amazon Bedrock：Amazon Bedrock Knowledge Bases でデータソースに接続してナレッジベースを作成する](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-create.html)を参照してください。

### ステップ 4 - 結果を Tealium に返すための Lambda ノードを追加する（Tealium との連携には必須）

プロンプトが構造化 JSON を生成したら、プロファイルをエンリッチするために、その結果を Tealium に返す必要があります。

次の処理を行う Lambda ノードを追加します。

* プロンプトの出力（プロンプトノードからの `$.data`）を受け取ります。
* JSON を解析します。
* Tealium Collect（`POST https://collect.tealiumiq.com/event`）に送信します。
* 次の項目を含めます。
  * `tealium_account`
  * `tealium_profile`
  * `tealium_visitor_id`
  * `tealium_event`（ユーザー定義）
  * AI の出力フィールド（例：`visitor_score`）

[提供されている Lambda の例](#lambda-example)を使用するか、独自に作成してください。

### ステップ 5 - フロー出力ノードを追加する

Tealium はフローの API レスポンスを処理しませんが、フローを完了するには出力ノードが必要です。

Lambda の出力を `FlowOutputNode` に接続しても Tealium の処理には影響しませんが、次のツールを使用してフローが正常に動作していることを確認できます。

* Bedrock コンソールでデバッグする。
* Lambda 関数からのエラーを確認する。
* 検証のために最終的な JSON 結果を調査する。
* Trace を使用して Tealium の出力を確認する。
#### Lambda の例

以下は、プロンプト出力を受け取り、JSON を解析し、そのデータを Tealium Collect エンドポイントに送信して、Tealium でのエンリッチメントとアクティベーションに使用する Lambda の例です。さまざまなデータ構造に対応するためのフォールバックが含まれています。必要に応じて書き換えてください。

指定したデータソースでサーバーサイドイベントを受け入れるように、アカウントとプロファイルを構成する必要があります。


<blockquote>
この例では、ランタイム環境として Node.js バージョン 18.x 以降が必要です。
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

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| Bedrock AI モデルにプロンプトを送信 | ✓ | ✓ |
| Bedrock AI マネージドプロンプトにデータを送信 | ✓ | ✓ |
| Bedrock AI ワークフローにデータを送信 | ✓ | ✓ |

### Bedrock AI モデルにプロンプトを送信

コネクタを通じて単一のモデルを呼び出し、応答を同期的に受け取るだけのシンプルな処理が必要な場合は、**Bedrock AI モデルにプロンプトを送信**を使用します。

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| モデル ID または推論プロファイル ARN | オンデマンド推論で使用する Amazon Bedrock モデルを選択するか、プロビジョンドスループットモデルの ARN または推論プロファイルの ARN を手動で入力します。<br>オンデマンド推論およびテキスト入出力をサポートするモデルのみが表示されます。<br>使用するモデルが表示されない場合は、そのモデルが AWS アカウントとリージョンで有効になっており、オンデマンド推論をサポートしていることを確認してください。<br><br><br>プロビジョンドスループットを使用する場合は、完全なモデル ARN（例：`arn:aws:bedrock:region:account-id:provisioned-model/...`）を入力します。<br>AWS アカウントで構成されている場合は、推論プロファイルの ARN も使用できます。<br>モデルの利用可否とサポートされる推論タイプは、AWS アカウントの権限とリージョン構成によって決まります。|
| プロンプトパラメータ | パラメータを、プロンプト内で置換するプレースホルダーにマッピングします。デフォルトでは、コネクタは `{{tealium_account}}`、`{{tealium_profile}}`、`{{tealium_visitor_id}}` にアクセスできます。これらはマッピングによって上書きできます。 |
| 訪問プロファイルを追加 | （オーディエンスアクションのみ）訪問プロファイルを変数 `{{visitor_profile}}` としてプロンプトテンプレートで使用できるようにするかどうかを指定します。 |
| 現在の訪問を追加 | （オーディエンスアクションのみ）現在の訪問データを `{{visitor_profile}}` オブジェクトに含めるかどうかを指定します。 |
| イベントペイロードを追加 | （イベントアクションのみ）イベントペイロードを変数 `{{event_payload}}` としてプロンプトテンプレートで使用できるようにするかどうかを指定します。 |
| プロンプト | <ul><li>マッピングされたパラメータを参照するには、二重中括弧を使用します。例：`{{tealium_account}}`、`{{visitor_id}}`、`{{event_value}}`。</li><li>訪問プロファイルをプロンプトに含めるには、`{{visitor_profile}}` を使用します。<br>説明、Markdown、コードフェンス、余分なテキストを含めず、有効な JSON のみを返すようモデルに明確に指示してください。</li><li>想定する正確な JSON 構造（フィールド名、必須キー、値の形式など）を定義します。</li><li>Tealium フィールドを含める必要がある場合は、プロンプト内で明示的に指定します。<br>曖昧な表現を避け、決定論的なプロンプトを記述してください。</li><li>「説明文、バッククォート、余分な書式を含めず、単一の JSON オブジェクトのみを返してください」のような直接的な指示を含めます。</li></ul> |
| デバッグモード | デバッグモードを有効にすると、コネクタは未加工の Bedrock 応答を Tealium Collect に送信せずに受け入れます。完全な処理を有効にする前に、Trace を使用して応答形式を検証してください。 |

#### 推論パラメータ

詳細については、[Amazon Bedrock API リファレンス：InferenceConfiguration](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent_InferenceConfiguration.html)を参照してください。

| パラメータ | 説明 |
| --- | --- |
| `maxTokens` | モデルが応答として生成できるトークンの最大数です。値を小さくすると出力が短くなり、レイテンシー、コスト、スロットリングのリスクを軽減できます。 |
| `temperature` | 出力のランダム性を制御します。値を小さくすると（`0.2` など）応答がより決定論的になり、値を大きくすると（`0.8` など）より創造的で多様な結果が生成されます。 |
| `topP` | 累積確率がこの値を超える最小のトークン集合にトークンの選択を制限する、核サンプリングのパラメータです。値を小さくすると出力の焦点が絞られ、値を大きくすると多様性が高まります。 |
| `stopSequences` | モデルが生成中に検出すると生成を停止する、1 つ以上の文字列です。応答を切り詰める場合や、構造化された出力の境界を適用する場合に役立ちます。 |
### Bedrock AI Managed Prompt にデータを送信

再利用可能でバージョン管理されたプロンプトを呼び出し、コネクタを介して同期的に応答を受け取る場合は、**Send Data to Bedrock AI Managed Prompt** を使用します。

| パラメータ | 説明 |
| --- | --- |
| Prompt ARN | （必須）Bedrock Prompt Management テンプレートの ARN を指定します。プロンプト ARN は、Bedrock のプロンプト詳細にある **Overview** セクションで確認できます。 |
| Prompt Data | <ul><li>Tealium は、マッピングされた属性を呼び出し時にプロンプトへ渡します。</li><li>コネクタは、変数 `tealium_account`、`tealium_profile`、`tealium_visitor_id` をプロンプトに含めます。これらはマッピングによって上書きできます。</li><li>説明、Markdown、コードフェンス、および JSON の前後に追加テキストを含めず、有効な JSON のみを返すよう、モデルに明確に指示するプロンプトを作成してください。</li><li>JSON に `tealium_account`、`tealium_profile`、`tealium_visitor_id` を含めて返すようモデルに指示する内容を、プロンプトに含める必要があります。</li><li>曖昧な表現は避けてください。出力を確実に解析できるよう、決定論的なプロンプトを作成してください。</li><li>最良の結果を得るには、「説明文、バッククォート、追加の書式構成を含めず、単一の JSON オブジェクトのみを返してください。」のような直接的な指示を含めます。</li></ul> |
| Add Visitor Profile | （オーディエンスアクションのみ）プロンプトテンプレートで訪問プロファイルを変数 `{{visitor_profile}}` として使用できるようにするかどうかを指定します。 |
| Add Current Visit | （オーディエンスアクションのみ）現在の訪問データを `{{visitor_profile}}` オブジェクトに含めるかどうかを指定します。 |
| Add Event Payload | （イベントアクションのみ）プロンプトテンプレートでイベントペイロードを変数 `{{event_payload}}` として使用できるようにするかどうかを指定します。 |
| Debug Mode | デバッグモードを有効にすると、コネクタは未加工の Bedrock 応答を Tealium Collect に送信せずに受け取ります。完全な処理を有効にする前に、Trace を使用して応答形式を検証してください。 |

### Bedrock AI Workflow にデータを送信

Lambda を介して非同期に実行される、複数ステップのオーケストレーションまたはナレッジベース検索が必要な場合は、**Send Data to Bedrock AI Workflow** を使用します。

| パラメータ | 説明 |
| --- | --- |
| Bedrock Flow Alias ARN | （必須）このアクションで呼び出す Bedrock Flow Alias の ARN を入力します。`live` などのエイリアスを作成し、その ARN をここで使用することをお勧めします。 |
| Flow Data | <ul><li>このコネクタを更新せずに、エイリアスが参照する Flow Version を AWS で変更できます。</li><li>コネクタは、マッピングされたフィールドを document という名前の JSON オブジェクトとして Flow に送信します。</li><li>Flow 内の Prompt、Lambda、またはその他のノードでは、`$.data.<fieldName>` を使用してこれらのフィールドを参照します。</li><li>デフォルトでは、`tealium_account`、`tealium_profile`、`tealium_visitor_id` が自動的に含まれます。必要に応じて、フィールドマッピングによって上書きできます。</li><li>Flow には `FlowOutputNode` を含める必要がありますが、Tealium はその出力を使用しません。</li><li>Collect エンドポイントを介して Tealium にデータを送り返すには、Lambda を使用します。</li><li>Bedrock コンソールで Flow をテストするときに成功／エラー情報を確認できるよう、Lambda の出力を `FlowOutputNode` に接続することをお勧めします。</li></ul> |
| Add Visitor Profile | （オーディエンスアクションのみ）完全な訪問プロファイルを `visitor_profile` JSON オブジェクトとして Flow の入力に含めるかどうかを指定します。 |
| Add Current Visit | （オーディエンスアクションのみ）現在の訪問データを `visitor_profile` JSON オブジェクトに含めるかどうかを指定します。 |
| Add Event Payload | （イベントアクションのみ）イベントペイロードを `event_payload` JSON オブジェクトとして Flow の入力に含めるかどうかを指定します。 |

## 一般的なエラーとトラブルシューティング

一般的なエラーコードと解決方法は次のとおりです。

### 一般的な AWS エラーコード：

* **`AccessDeniedException` または `NotAuthorized`**  
IAM ユーザーまたはロールに必要な権限（`bedrock:InvokeModel`、`bedrock:RenderPrompt`、`bedrock:InvokeFlow`、`bedrock:ListFoundationModels` など）がありません。  
解決するには、ロールまたはアクセスキーに関連付けられている IAM ポリシーを更新し、適切なリソースに対して必要な Bedrock アクションを許可します。

* **`InvalidClientTokenId`、`UnrecognizedClientException`、または `ExpiredTokenException`**  
構成されたアクセスキーまたは STS セッションが無効か、有効期限が切れています。  
解決するには、認証情報を更新してコネクタに再入力するか、STS ロールと外部 ID が正しく、有効期限が切れていないことを確認します。

* **`OptInRequired` または `FTUFormNotFilled`**  
AWS アカウントで Bedrock または特定のモデル（Anthropic など）が完全に有効化されていません。  
解決するには、AWS コンソールで Bedrock の有効化に必要な手順と、モデル固有のフォームまたは Marketplace サブスクリプションを完了します。

これらのエラーが表示された場合は、まず AWS で IAM またはアカウントの構成を修正してください。権限を修正するまで、コネクタアクションを再試行するだけでは成功しません。

### Bedrock API 呼び出しでよく発生するエラー

以下のエラーは、リクエストは Bedrock に到達したものの、サービスまたはモデルが正常に処理を完了できなかったことを示します。

* **`ValidationException` または `ValidationError`**  
リクエスト本文またはパラメータが、対象のモデルまたは API に対して無効です（モデル ID が間違っている、サポートされていないパラメータが指定されている、入力が大きすぎるなど）。  
解決するには、モデル ID、プロンプト ARN、Flow ARN を確認し、リクエスト本文がモデルで想定されているスキーマと一致していることを確認します。また、必要に応じてプロンプトのサイズまたは最大トークン数を減らします。

* **`ResourceNotFound` または `ResourceNotFoundException`**  
指定されたモデル、プロンプトバージョン、または Flow Alias ARN が存在しないか、そのリージョンでは利用できません。  
解決するには、コネクタ構成の ARN とリージョンが、Bedrock コンソールに表示されている値と一致しているか再確認します。

* **`ThrottlingException` または `ServiceQuotaExceededException`**  
呼び出しが Bedrock のクォータ（TPS やトークン制限など）を超えています。  
解決するには、呼び出し頻度を下げるか、AWS でクォータの引き上げをリクエストします。

* **`ServiceUnavailable`、`InternalFailure`、または `InternalServerException`**  
Bedrock 内で一時的なエラーまたは内部エラーが発生しています。  
解決するには、エラーが継続する場合、AWS Service Health Dashboard を確認するか、AWS Support のケースを作成します。

* **`ModelErrorException`、`ModelNotReadyException`、または `ModelTimeoutException`**（プロンプトまたはマネージドプロンプトのフロー）  
モデルで処理に失敗したか、モデルがまだウォームアップ中であるか、応答に時間がかかりすぎました。  
解決するには、しばらく待ってから再試行し、プロンプトを簡素化するかトークン使用量を減らします。また、モデルまたはプロビジョンドスループットが完全に有効になっていることを確認します。

これらすべてのエラーについて、Tealium は Bedrock から返された元の AWS エラーメッセージを表示します。トラブルシューティング時に、このメッセージを AWS ドキュメントと照合できます。