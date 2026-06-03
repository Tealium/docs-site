---
title: Amazon Bedrock AIコネクタ構成ガイド
description: Amazon Bedrock AIコネクタを構成して、Tealiumのイベントデータと訪問データをリアルタイムでエンリッチするために、基盤モデル、管理されたプロンプト、または複数ステップのBedrockワークフローに送信します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-bedrock-ai-connector/
---
AIコネクタの動作概要とAIコネクタまたはTealium機能をいつ使用するかについてのガイダンスについては、[AIコネクタとTealium機能]()を参照してください。

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
      &#34;Version&#34;: &#34;2012-10-17&#34;,
      &#34;Statement&#34;: [
        {
          &#34;Effect&#34;: &#34;Allow&#34;,
          &#34;Principal&#34;: {
            &#34;AWS&#34;: &#34;arn:aws:iam::757913464184:root&#34;
          },
          &#34;Action&#34;: &#34;sts:AssumeRole&#34;,
          &#34;Condition&#34;: {
            &#34;StringEquals&#34;: {
              &#34;sts:ExternalId&#34;: &#34;EXTERNAL_ID&#34;
            }
          }
        }
      ]
    }
```

### ポリシーのアタッチ

AWS管理コンソールで、コネクタアクションに必要なポリシーを入力します。各コネクタアクションには次のポリシーが必要です：

必要なフローやLambda関数の特定のARNに対してのみ権限を制限することをお勧めします。




```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;ListModels&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:ListFoundationModels&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    },
    {
      &#34;Sid&#34;: &#34;InvokeModel&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:InvokeModel&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    }
  ]
}
```



```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;RenderManagedPrompt&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:RenderPrompt&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    }
  ]
}

```



Lambdaを使用する場合：

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;BedrockFlowInvoke&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:InvokeFlow&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:bedrock:&lt;REGION&gt;:&lt;ACCOUNT_ID&gt;:flow/&lt;flow_id&gt;/alias/&lt;alias_name&gt;&#34;
    },
    {
      &#34;Sid&#34;: &#34;LambdaInvokeFunction&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;lambda:InvokeFunction&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:lambda:&lt;REGION&gt;:&lt;ACCOUNT_ID&gt;:function:&lt;FUNCTION_NAME&gt;&#34;
    }
  ]
}
```

Lambdaを使用しない場合：

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;BedrockFlowInvoke&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:InvokeFlow&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:bedrock:&lt;REGION&gt;:&lt;ACCOUNT_ID&gt;:flow/&lt;flow_id&gt;/alias/&lt;alias_name&gt;&#34;
    }
  ]
}
```



ポリシーを入力してアタッチするには：

1. AWSコンソールで**IAM &gt; ポリシー**に移動し、**ポリシーの作成**をクリックします。
1. ポリシーエディタで**JSON**タブを選択し、コネクタアクション用のポリシーを貼り付け、検証警告を解決し、**次へ**をクリックします。
1. ポリシー名（例：`TealiumCustomAccessPolicy`）とオプションの説明を入力し、**ポリシーの作成**をクリックします。
1. **IAM &gt; ロール**に移動し、変更したいロールを選択します。
1. **権限**タブで**権限の追加 &gt; ポリシーのアタッチ**をクリックします。
1. カスタムポリシーを検索し、選択して**ポリシーのアタッチ**をクリックします。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法についての一般的な指示については、[コネクタについて]()を参照してください。

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
* 最良の結果を得るために、次のような行を含めます：&#34;プローズ、バックティック、追加のフォーマットなしで、単一のJSONオブジェクトのみを返します。&#34;

### プロンプト例

```none
あなたは、有効なJSONのみを返す必要があるAIアシスタントです。
説明、マークダウン、コードフェンス、またはJSONオブジェクトの外側のテキストを含めないでください。

以下の訪問データを使用して、このセッションでの訪問の変換可能性を表す0から100の間の数値スコアを計算します。

単一のJSONオブジェクトのみを返し、この正確な構造で：

{
  &#34;tealium_account&#34;: &#34;{{tealium_account}}&#34;,
  &#34;tealium_profile&#34;: &#34;{{tealium_profile}}&#34;,
  &#34;tealium_visitor_id&#34;: &#34;{{tealium_visitor_id}}&#34;,
  &#34;tealium_event&#34;: &#34;bedrock_ai_insight&#34;,
  &#34;visitor_score&#34;: &lt;0から100の間の整数&gt;
}

訪問データ：
{{visitor_json}}

{{last_product_viewed}}の値に特に注意してください。

```

レスポンスは以下のようになります：

```json
{
    &#34;metrics&#34;: {
        &#34;latencyMs&#34;: 1272
    },
    &#34;output&#34;: {
        &#34;message&#34;: {
            &#34;content&#34;: [
                {
                    &#34;text&#34;: &#34;{\&#34;tealium_account\&#34;:\&#34;your-account\&#34;,\&#34;tealium_profile\&#34;:\&#34;main\&#34;,\&#34;tealium_visitor_id\&#34;:\&#34;__your-account_main__5574_438850__\&#34;,\&#34;tealium_event\&#34;:\&#34;bedrock_ai_insight\&#34;,\&#34;visitor_score\&#34;:85}&#34;
                }
            ],
            &#34;role&#34;: &#34;assistant&#34;
        }
    },
    &#34;stopReason&#34;: &#34;end_turn&#34;,
    &#34;usage&#34;: {
        &#34;inputTokens&#34;: 8811,
        &#34;outputTokens&#34;: 65,
        &#34;serverToolUsage&#34;: {},
        &#34;totalTokens&#34;: 8876
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
&#34;document&#34;: {
    &#34;tealium_account&#34;: &#34;services-example&#34;,
    &#34;tealium_profile&#34;: &#34;ai&#34;,
    &#34;tealium_visitor_id&#34;: &#34;1234567890abc&#34;,
    &#34;visitor_profile&#34;: {
        &#34;lifetime_value&#34;: &#34;1200&#34;,
        &#34;total_orders&#34;: 5,
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
| `visitor_profile` | `$.data.visitor_profile` |  `&#34;visitor_profile&#34;: {&#34;lifetime_value&#34;: &#34;1200&#34;,&#34;total_orders&#34;: 5,...}` |

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

この例は、ランタイム環境としてNode.jsバージョン18.x以降が必要です。


```js
const COLLECT_URL = process.env.COLLECT_URL || &#34;https://collect.tealiumiq.com/event&#34;;
function extractInputByName(event, name) {
  const arr = event?.node?.inputs;
  if (Array.isArray(arr)) {
    const hit = arr.find(i =&gt; i?.name === name);
    if (hit &amp;&amp; typeof hit.value === &#34;string&#34;) return hit.value;
    if (hit &amp;&amp; typeof hit.value === &#34;object&#34;) return JSON.stringify(hit.value);
  }
  return undefined;
}
function extractJsonStringFromEvent(event) {
  const fromStandardPin = extractInputByName(event, &#34;codeHookInput&#34;);
  if (typeof fromStandardPin === &#34;string&#34;) return fromStandardPin;
  const anyString = event?.node?.inputs?.find?.(i =&gt; typeof i?.value === &#34;string&#34;)?.value;
  if (typeof anyString === &#34;string&#34;) return anyString;
  if (typeof event?.codeHookInput === &#34;string&#34;) return event.codeHookInput;
  if (typeof event?.document === &#34;string&#34;) return event.document;
  const doc = event?.fields?.[0]?.content?.document;
  if (typeof doc === &#34;string&#34;) return doc;
  if (typeof event === &#34;string&#34;) return event;
  throw new Error(&#34;Could not find JSON string in event&#34;);
}
export const handler = async (event) =&gt; {
  try {
    const jsonStr = extractJsonStringFromEvent(event);
    const obj = JSON.parse(jsonStr);  // Fixed: store parsed result
    const required = [&#34;tealium_account&#34;, &#34;tealium_profile&#34;, &#34;tealium_visitor_id&#34;];
    for (const key of required) {
      if (!Object.prototype.hasOwnProperty.call(obj, key)) {
        throw new Error(`Missing required field &#39;${key}&#39; in model output`);
      }
    }
    const r = await fetch(COLLECT_URL, {
      method: &#34;POST&#34;,
      headers: { &#34;Content-Type&#34;: &#34;application/json&#34; },
      body: jsonStr
    });
    if (!r.ok) {
      const txt = await r.text().catch(() =&gt; &#34;&#34;);
      throw new Error(`Collect failed ${r.status}: ${txt}`);
    }
    return jsonStr;
  } catch (err) {
    console.error(&#34;Shim error:&#34;, err);
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
| モデルIDまたは推論プロファイルARN | オンデマンド推論を使用するAmazon Bedrockモデルを選択するか、プロビジョニングスループットモデルARNまたは推論プロファイルARNを手動で入力します。&lt;br&gt;オンデマンド推論とテキスト入出力をサポートするモデルのみが表示されます。&lt;br&gt;希望のモデルが表示されない場合は、そのモデルがAWSアカウントとリージョンで有効になっているか確認してください。&lt;br&gt;&lt;br&gt;&lt;br&gt;プロビジョニングスループットを使用する場合は、完全なモデルARN（例：`arn:aws:bedrock:region:account-id:provisioned-model/...`）を入力します。&lt;br&gt;AWSアカウントで構成されている場合は、推論プロファイルARNも使用できます。&lt;br&gt;モデルの可用性とサポートされる推論タイプは、AWSアカウントの権限とリージョン構成によって決まります。|
| プロンプトパラメータ | プロンプト内のプレースホルダーにパラメータをマッピングします。デフォルトでは、コネクタは`{{tealium_account}}`、`{{tealium_profile}}`、`{{tealium_visitor_id}}`にアクセスできます。これらはマッピングで上書き可能です。 |
| 訪問プロファイルの追加 | (オーディエンスアクションのみ) プロンプトテンプレートで訪問プロファイルを変数`{{visitor_profile}}`として使用することを許可します。 |
| 現在の訪問の追加 | (オーディエンスアクションのみ) `{{visitor_profile}}`オブジェクトに現在の訪問データを含めるかどうか。 |
| イベントペイロードの追加 | (イベントアクションのみ) イベントペイロードをプロンプトテンプレートの変数`{{event_payload}}`として使用することを許可します。 |
| プロンプト | &lt;ul&gt;&lt;li&gt;マッピングされたパラメータを参照するには、二重の中括弧を使用します。例：`{{tealium_account}}`, `{{visitor_id}}`, `{{event_value}}`。&lt;/li&gt;&lt;li&gt;`{{visitor_profile}}`を使用して、訪問プロファイルをプロンプトに含めます。&lt;br&gt;モデルには、説明、マークダウン、コードフェンス、余分なテキストなしで有効なJSONのみを返すように明確に指示します。&lt;/li&gt;&lt;li&gt;期待される正確なJSON構造を定義します（例：フィールド名、必要なキー、値の形式）。&lt;/li&gt;&lt;li&gt;Tealiumフィールドを含める必要がある場合は、プロンプトで明確に指定します。&lt;br&gt;あいまいな表現を避けます。決定論的なプロンプトを書きます。&lt;/li&gt;&lt;li&gt;「プローズ、バックティック、余分なフォーマットなしで、単一のJSONオブジェクトのみを返す」という直接的な指示を含めます。&lt;/li&gt;&lt;/ul&gt; |
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
| プロンプトデータ | &lt;ul&gt;&lt;li&gt;Tealium は、それを呼び出すときにマッピングされた属性をプロンプトに渡します。&lt;/li&gt;&lt;li&gt;コネクタには `tealium_account`、`tealium_profile`、`tealium_visitor_id` の変数が含まれており、マッピングで上書きすることができます。&lt;/li&gt;&lt;li&gt;モデルに JSON のみを返すように明確に指示するプロンプトを記述してください。説明、マークダウン、コードフェンス、JSON の前後の追加テキストは含まないでください。&lt;/li&gt;&lt;li&gt;モデルが JSON で `tealium_account`、`tealium_profile`、`tealium_visitor_id` を返すように指示を含めてプロンプトを作成する必要があります。&lt;/li&gt;&lt;li&gt;あいまいな表現を避けてください。出力が確実に解析できるように決定論的なプロンプトを記述してください。&lt;/li&gt;&lt;li&gt;最良の結果を得るためには、「JSON オブジェクトのみを返し、散文、バックティック、余分なフォーマットは含まない」という直接的な指示を含めてください。&lt;/li&gt;&lt;/ul&gt; |
| 訪問プロファイルを追加 | (オーディエンスアクションのみ) プロンプトテンプレートで訪問プロファイルを `{{visitor_profile}}` 変数として使用することを許可するかどうか。 |
| 現在の訪問を追加 | (オーディエンスアクションのみ) `{{visitor_profile}}` オブジェクトに現在の訪問データを含めるかどうか。 |
| イベントペイロードを追加 | (イベントアクションのみ) プロンプトテンプレートでイベントペイロードを `{{event_payload}}` 変数として使用することを許可するかどうか。 |
| デバッグモード | デバッグモードが有効になっている場合、コネクタは Tealium Collect に送信することなく生の Bedrock 応答を受け入れます。完全な処理を有効にする前に応答形式を検証するために Trace を使用します。 |

### Bedrock AI ワークフローへデータを送信

**Bedrock AI ワークフローへデータを送信**を使用する場合は、Lambda を通じて非同期で実行されるマルチステップのオーケストレーションまたはナレッジベースの取得が必要なときに使用します。

| パラメータ | 説明 |
| --- | --- |
| Bedrock Flow Alias ARN | (必須) このアクションが呼び出す Bedrock Flow Alias の ARN を入力してください。`live` などのエイリアスを作成し、ここでその ARN を使用することをお勧めします。 |
| Flow データ | &lt;ul&gt;&lt;li&gt;AWS でエイリアスが指す Flow バージョンをこのコネクタを更新せずに変更します。&lt;/li&gt;&lt;li&gt;コネクタはマッピングされたフィールドを document という JSON オブジェクトとして Flow に送信します。&lt;/li&gt;&lt;li&gt;Flow 内で、これらのフィールドを Prompt、Lambda、または他のノードで `$.data.&lt;fieldName&gt;` を使用して参照します。&lt;/li&gt;&lt;li&gt;デフォルトでは、`tealium_account`、`tealium_profile`、および `tealium_visitor_id` が自動的に含まれ、必要に応じてフィールドマッピングを通じて上書きすることができます。&lt;/li&gt;&lt;li&gt;Flow には `FlowOutputNode` を含める必要がありますが、Tealium はその出力を使用しません。&lt;/li&gt;&lt;li&gt;Collect エンドポイントを通じて Tealium にデータを送り返すために Lambda を使用します。&lt;/li&gt;&lt;li&gt;Bedrock コンソールでフローをテストする際に成功/エラー情報を確認するために、Lambda の出力を `FlowOutputNode` に接続することをお勧めします。&lt;/li&gt;&lt;/ul&gt; |
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