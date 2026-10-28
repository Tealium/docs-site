---
title: AIコネクタとTealium Functionsの概要
description: AIコネクタとTealium Functionsの仕組み、およびLLMのアクティベーションにAIコネクタを使用する場合と、独自のモデルを呼び出すためにTealium Functionsを使用する場合について説明します。
url: https://docs.tealium.com/ja/guides/ai-connectors-and-functions/
---
Tealiumでは、AIモデルをリアルタイムのデータワークフローに統合するために、次の2つの方法をサポートしています。

* **AIコネクタ**：サポート対象のAIプロバイダーと統合し、プロンプトベースのLLMインタラクションまたはモデルエンドポイントの直接呼び出しを行います。
* **Tealium Functions**：独自のモデルを呼び出すか、カスタムエンドポイントを呼び出します。

このガイドでは、それぞれの方法の仕組みと、どのような場合に使用するかについて説明します。

## AIコネクタ

### 仕組み

AIコネクタは、サポート対象のプロバイダーが提供するホスト型AIサービスと統合します。次の2つのインタラクションパターンをサポートしています。

* **プロンプトベース（LLM）**：プロンプトとTealiumデータをLLMエンドポイントに送信します。モデルは構造化されたJSONレスポンスを返し、そのレスポンスはプロファイルのエンリッチメントのためにTealium Collectへ転送されます。
* **モデルエンドポイントの呼び出し**：Tealiumのイベント属性または訪問属性を、デプロイ済みのモデルエンドポイント（Snowflake Model Registryエンドポイントなど）に直接送信します。モデルは予測またはスコアを返し、それらはプロファイルのエンリッチメントのためにTealium Collectへ転送されます。

AIコネクタを使用するには、プロバイダーの認証資格情報と、リクエストおよびモデルに送信するTealiumデータを定義した、少なくとも1つの構成済みアクションが必要です。


<blockquote>
AIコネクタは、構造化された予測可能な出力を返すユースケース向けに設計されています。長文コンテンツやメディアの生成向けには設計されていません。ユースケースで自由形式の出力が必要な場合は、本番環境に移行する前に、組織のAIガバナンスプロセスに準拠していることを確認してください。
</blockquote>


### データフロー

![](https://docs.tealium.com/images/guides/ai-connectors-flow.png)

1. **トリガーが発火**：イベントまたはオーディエンスの変更によって、コネクタアクションがトリガーされます。
1. **リクエストを送信**：コネクタがプロンプトまたは入力データをAIモデルのエンドポイントに送信します。
1. **レスポンスを受信**：モデルが要求された値を生成し、JSONオブジェクトを返します。
1. **イベントを取り込み**：コネクタがレスポンスをTealium Collectに転送します。
1. **プロファイルをエンリッチ**：エンリッチメントルールがレスポンスの値を訪問プロファイル属性に書き込みます。
1. **オーディエンスをアクティベート**：オーディエンスルールが更新された属性を評価し、ダウンストリームコネクタが発火します。

### プロンプト

プロンプトでは、評価するコンテキストデータをモデルに指示し、具体的な質問を提示して、期待するレスポンスを定義します。ベンダーのコネクタによっては、レスポンス出力に関する具体的な指示を含める必要がある場合と、ない場合があります。詳細については、各コネクタの説明を参照してください。


<blockquote>
OpenAIの**OpenAIにプロンプトを送信**アクションなど、一部のコネクタでは、スキーマによってJSON構造が自動的に適用されます。そのようなコネクタでは、プロンプトにレスポンス形式の指示を含めないでください。以下の例は、レスポンス形式を手動で指定する必要があるコネクタに適用されます。
</blockquote>


#### コンテキストデータ

特定の属性、またはイベントや訪問のデータオブジェクト全体を、プロンプトのコンテキストとして含めることができます。

特定の属性を含めるには、コネクタアクションで属性をマッピングし、プロンプト内で参照します。たとえば、`product_review`をマッピングした場合、プロンプト内で`{{product_review}}`を参照できます。

データオブジェクト全体をプロンプトに含めるには、コネクタアクションの構成で**イベントペイロードを追加**または**訪問プロファイルを追加**を有効にしてから、プロンプト内で`{{event_payload}}`または`{{visitor_profile}}`を参照します。

オーディエンスアクションでは、**現在の訪問を追加**を有効にして、訪問プロファイルオブジェクト内に現在の訪問データを含めることもできます。

**重要**  
コネクタでコンテキストデータに関するプロンプト指示が必要な場合は、それをプロンプトの最初の行に含めます。次に例を示します。

```wrap
You receive a JSON object describing a customer event:
{{event_payload}}
```

コネクタでレスポンス形式に関するプロンプト指示が必要な場合は、それをプロンプトの末尾に含めます。次に例を示します。

```wrap
Return only a single JSON object on one line with the following structure: 
{
  "tealium_account": "{{tealium_account}}",
  "tealium_profile": "{{tealium_profile}}",
  "tealium_visitor_id": "{{tealium_visitor_id}}",
  "tealium_event":  "ai_response",
  "ai_review_sentiment": "<customer review sentiment>"
}
```

#### 質問

プロンプトでは、データの評価方法をモデルに指示し、1つ以上の具体的な値を生成するよう求めます。

たとえば、次のプロンプトでは、顧客レビューの感情を表すテキスト値を生成するよう求めています。

```wrap
Based on the provided product review event, classify the customer's sentiment as one of: "dissatisfied", "neutral", or "satisfied".
```

### レスポンスイベント

コネクタはAIレスポンスを解析してJSONオブジェクトを抽出し、イベントとしてTealium Collectに送り返します。

レスポンスイベントの例：

```json
{
  "tealium_account": "acme",
  "tealium_profile": "main",
  "tealium_visitor_id": "383...05d",
  "tealium_event": "ai_response",
  "ai_review_sentiment": "satisfied"
}
```

### 例

#### イベントトリガー

この例では、顧客が商品のレビューを送信した直後に、プロンプトがモデルに感情の評価を求めます。

**プロンプトの例**：

```wrap
You receive a JSON object describing a customer's product review:
{{event_payload}}

Based on the provided product review event, classify the customer's sentiment as one of: "dissatisfied", "neutral", or "satisfied".

Return only a single JSON object on one line with the following structure: 
{
  "tealium_account": "{{tealium_account}}",
  "tealium_profile": "{{tealium_profile}}",
  "tealium_visitor_id": "{{tealium_visitor_id}}",
  "tealium_event":  "ai_response",
  "ai_review_sentiment": "<customer review sentiment>"
}
```

**レスポンスイベントの例**：

```json
{
  "tealium_account": "acme",
  "tealium_profile": "main",
  "tealium_visitor_id": "383...05d",
  "tealium_event": "ai_response",
  "ai_review_sentiment": "satisfied"
}
```

#### オーディエンストリガー

この例では、顧客が「頻繁に閲覧するが購入しない」という名前のオーディエンスに参加し、プロンプトがモデルに顧客の意図を評価するよう求めます。

**プロンプトの例**：

```wrap
You receive a JSON object describing a retail visitor:
{{visitor_profile}}

Based on the customer data provided, classify their likely shopping intent as: "bargain hunting", "product comparison", "researching for later", or "not interested". If data is missing, make a best effort guess.

Return only a single JSON object on one line with the following structure: 
{
  "tealium_account": "{{tealium_account}}",
  "tealium_profile": "{{tealium_profile}}",
  "tealium_visitor_id": "{{tealium_visitor_id}}",
  "tealium_event":  "ai_response",
  "ai_shopping_intent": "<customer shopping intent>"
}
```

**レスポンスイベントの例**：

```json
{
  "tealium_account": "acme",
  "tealium_profile": "main",
  "tealium_visitor_id": "383...05d",
  "tealium_event": "ai_response",
  "ai_shopping_intent": "bargain hunting"
}
```

### アクティベーション

モデルが有効なJSONオブジェクトを返すと、コネクタはそれを受信イベントとしてTealium Collectに転送します。その後、エンリッチメントルールがレスポンスの値を訪問プロファイル属性に書き込みます。以降は、エンリッチされたプロファイルに基づいて、オーディエンスとダウンストリームコネクタがアクティベートされます。


<blockquote>
コネクタに固有の値を`tealium_event`に構成し、ユースケースに固有の名前をレスポンス属性に付けることで、これらのイベントに一致するイベントフィードやルールを簡単に作成できます。
</blockquote>


AIレスポンスイベントをアクティベートするルールの例：


[
  [
    {
      "input": "tealium_event",
      "operator": "equals",
      "filter": "ai_response"
    },
    {
      "input": "ai_review_sentiment",
      "operator": "is populated"
    }
  ]  
]

### テスト

本番環境で AI コネクタを有効化する前に、コネクタのマッピングで **デバッグモード**を有効にし、トレースを使用して構成をテストし、構成とプロンプトの動作を検証してください。デバッグモードを使用すると、本番環境でコストが発生したり、稼働中のデータに影響を与えたりする前に、エラーを検出してプロンプトを最適化できます。

デバッグモードでは、コネクタは AI リクエストを実行しますが、レスポンスイベントをアカウントに返さず、結果をログに記録します。トレースツールを使用してリクエストとレスポンスの全体を確認し、生成された出力を検証して、トリガー条件と属性マッピングが想定どおりに動作していることを確認してください。

### サポート対象ベンダー

認証、モデルの選択、プロンプトの要件、アクションパラメータなどの構成の詳細は、コネクタごとに異なります。

次の AI コネクタを利用できます。



## AI 向け Functions

### 仕組み

Tealium Functions は、独自モデルの呼び出し（IYOM）をコードベースで実現します。事前構成済みのコネクタを使用する代わりに、JavaScript を記述して、イベント関数または訪問関数から任意のモデルエンドポイントを直接呼び出します。ユースケースには、数値スコアを返す従来型の機械学習モデル、専用の AI コネクタがないプラットフォームでホストされている LLM、クラウドデータプラットフォーム上のエンドポイントなどがあります。

Tealium Functions は、イベントの処理後にトリガーされるイベント関数と、訪問プロファイルの更新後にトリガーされる訪問関数の両方をサポートしています。そのため、直近のイベントコンテキストまたは蓄積された訪問履歴のいずれかをスコアリングできます。

関数が実行されると、次の手順に従います。

1. イベント属性または訪問プロファイルデータを収集します。
1. モデルエンドポイントへのリクエストペイロードを構築します。
1. `fetch()` を使用してエンドポイントを呼び出します。
1. レスポンスを解析します。
1. `track()` を使用して予測結果を Tealium Collect に送信します。
1. エンリッチメントによって予測値を訪問プロファイルに書き込みます。

関数は訪問プロファイルを直接変更できないため、予測結果は Tealium Collect を経由し、エンリッチメントによってプロファイルに書き込む必要があります。

Functions は、同期および非同期の両方のモデル呼び出しをサポートしています。10 秒以内に応答するモデルには、標準の `await` パターンを使用します。応答に時間がかかるモデルには、ファイア・アンド・フォーゲットパターンを使用します。この場合、関数はリクエストを送信して直ちに終了します。推論が完了すると、モデルは結果をコールバック URL に POST します。

実装の詳細については、[AI アクティベーション用の関数の作成](https://docs.tealium.com/function-for-ai-activation/)を参照してください。

## コネクタと Functions の選択

### AI コネクタを使用する場合

* プロンプトベースの推論のために大規模言語モデルを呼び出す場合。
* リアルタイム推論のために、サポート対象プラットフォーム上（Snowflake Model Registry など）にデプロイされたモデルエンドポイントを呼び出す場合。
* ユースケースが、サポート対象のいずれかの AI プロバイダーに適合する場合。
* モデルが、Tealium イベントとして直接転送できる構造化出力を返す場合。
* コードを記述せずに、Tealium UI から統合を構成する場合。
* ユースケースが、ページビューなどの大量かつ価値の低いイベントではなく、対象を絞った価値の高いイベントまたはオーディエンスで構成される場合。


<blockquote>
AI コネクタは、事前定義されたリストに含まれる分類ラベル、信頼度、スコア、識別子など、構造化され予測可能な出力を返すユースケース向けに設計されています。長文コンテンツやメディアの生成向けには設計されていません。ユースケースで自由形式の出力が必要な場合は、本番環境に移行する前に、組織の AI ガバナンスプロセスに準拠してください。
</blockquote>


### Tealium Functions を使用する場合

* 専用の AI コネクタがないプラットフォームでモデルがホストされている場合。
* モデルに送信する前に、ペイロードにカスタムロジック、データ変換、または PII フィルタリングが必要な場合。
* 非同期のモデルレスポンスやカスタムネットワーク構成を処理する必要がある場合。

モデルにデータを送信する前に PII を削除またはトークン化する必要がある場合は、Tealium Functions を使用してカスタムフィルタリングを適用し、承認済みのフィールドのみをエンドポイントに送信してください。

## 比較の概要

| 考慮事項 | AI コネクタ | Tealium Functions |
|---------------|---------------|-------------------|
| セットアップ | UI で構成 | JavaScript コードを記述 |
| サポートされるモデルの種類 | サポート対象プラットフォーム上の LLM およびデプロイ済みモデルエンドポイント | 従来型の機械学習を含む、あらゆる ML または AI モデル |
| サポート対象プロバイダー | [サポート対象ベンダー](#supported-vendors)を参照 | 任意の HTTPS エンドポイント |
| プロンプトの制御 | 変数置換を使用するテンプレートベース | 完全にプログラム可能 |
| 認証 | コネクタ構成で管理 | Tealium Functions 内に認証トークンとして保存 |
| ペイロード構造 | イベントまたは訪問データに基づく固定構造 | 完全にカスタマイズ可能 |
| モデル呼び出し前の PII フィルタリング | プラットフォームレベルのみ（同意カテゴリおよび制限付き属性）。コネクタ内ではカスタム前処理コードを使用できません | モデルを呼び出す前に、JavaScript でフィルタリングと変換を完全にカスタマイズ可能 |
| レスポンス処理 | JSON の自動解析およびイベント転送 | コードによるカスタム解析 |
| 非同期サポート | 制限あり。Bedrock AI Workflow アクションは、Lambda コールバックを介した非同期レスポンスをサポート | ファイア・アンド・フォーゲットパターンおよびモデルから Tealium Collect へのコールバックを介してサポート |

## 一般的なユースケース

次の表に、一般的な AI ユースケースと、それぞれに推奨される統合アプローチを示します。

| ユースケース | 説明 | 推奨アプローチ |
|----------|-------------|----------------------|
| 感情分析 | 顧客のフィードバックまたはレビューイベントを肯定的、中立的、否定的のいずれかに分類します。 | AI コネクタ |
| 意図分類 | 閲覧履歴または購入履歴に基づいて、顧客の推定意図を特定します。 | AI コネクタ |
| ネクストベストアクション（プレイブックの選択） | 訪問のコンテキストに基づき、承認済みの有限のアクションまたはオファーから選択します。 | AI コネクタ |
| 傾向スコアリング | トレーニング済みの機械学習モデルを使用して、コンバージョン、離脱、または価値の高いアクションが発生する可能性を予測します。 | AI コネクタ（モデルがサポート対象プラットフォームにデプロイされている場合）または Tealium Functions |
| ネクストベストアクション（スコア最適化） | 数値モデルを使用して一連の候補アクションをスコアリングし、最もスコアの高いアクションを選択します。 | AI コネクタ（モデルがサポート対象プラットフォームにデプロイされている場合）または Tealium Functions |
| 特徴量ストアのルックアップ | アクティベーション用に、事前計算されたスコアまたは特徴量をデータプラットフォームから取得します。 | Tealium Functions |
| カスタムエンドポイント推論 | 専用の AI コネクタがないプラットフォームでホストされているモデルを呼び出します。 | Tealium Functions |