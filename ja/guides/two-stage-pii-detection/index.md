---
title: リアルタイムで個人識別情報（PII）を検出するための2段階検証パターンの使用
description: Tealiumの機能とAWS Comprehendを使用して、リアルタイムイベントデータ内の個人識別情報（PII）を検出し、修正するためのスケーラブルな2段階検証パターンを使用します。
url: https://docs.tealium.com/ja/guides/two-stage-pii-detection/
---
2段階検証パターンは、リアルタイムイベントデータ内の個人識別情報（PII）を検出し管理するためのスケーラブルな方法を提供します。これは、サーバーサイドの機能とAWS Comprehendを使用して、高速な正規表現ベースのフィルタリングと高度な機械学習検証を組み合わせています。

このガイドには以下が含まれます：

* 高スループットデータストリームでPIIを検出する実用的なアプローチ。
* Tealium EventStream、機能、およびAWSサービスを統合するためのステップバイステップの指示。
* データ変換機能、処理済みイベント機能、およびAWS Lambdaの例の実装。

## 仕組み

リアルタイムで高容量のデータストリームでPIIを識別し管理するために、2段階検証パターンを使用します。このパターンは、軽量で低遅延のチェックをより遅い、より正確な機械学習（ML）検証から分離して、パフォーマンスを維持し処理コストを削減します。

このアプローチは、`message_text`、`form_input`、または`user_comment`などの非構造化またはフリーテキストフィールドでPIIを検出するのに理想的です。

パターンには2つの段階があります：

* **ステージ1（正規表現フィルター）**：軽量のサーバーサイド機能は正規表現を使用してPIIを含む可能性のあるイベントを識別します。この機能は、`message_text`、`form_input`、または`user_comment`などのフィールドをスキャンして潜在的にセンシティブなデータを識別します。
* **ステージ2（検証）**：Webhookは、自然言語処理（NLP）ベースの検出およびオプションの修正のために、フラグが付けられたイベントのみをAWS Comprehendに送信します。

ステージ1でフラグが付けられたイベントのみがステージ2に進みます。これにより、不要なAPI呼び出しと遅延が最小限に抑えられます。

### 主要コンポーネントを理解する

* **データ変換機能**  
  サーバーサイドの機能で、受信イベントデータを評価し、潜在的なPIIを識別するために軽量の正規表現を適用します。オプションで、この機能は検出された値をハッシュ化して転送することができます。

* **派生属性**  
  データ変換機能の出力から派生したブールイベント属性です。機能はPIIを検出すると、イベントにフラグを追加して`true`に構成します。

* **AudienceStreamイベントフィルター**  
  派生属性に基づいて受信イベントをフィルタリングし、PIIを含まないイベントのみが訪問プロファイルを豊かにします。

* **イベントフィード**  
  派生属性に基づいてフィルタリングされたフラグ付きイベントのストリームで、コネクタ、保存、または他の機能に送信することができます。

* **処理済みイベント機能**  
  エンリッチメントとフィルタリングの後に実行される機能です。フラグが付けられたイベントを外部エンドポイント（AWS Lambda + Comprehendなど）に送信して、高度な検証を行います。

## 利点

データがエンリッチメントされたり、保存されたり、下流システムと共有される前にガバナンスまたは修正ポリシーを適用する必要がある場合に、2段階検証パターンを使用します。

利点には以下が含まれます：

* 軽量なパターンマッチを使用してほとんどのイベントをフィルタリングすることにより、AWS Comprehendへのリクエスト数を減らします。
* フラグが付けられたイベントのみをステージ2検証にルーティングすることで、イベント処理を300ミリ秒未満に保ちます。
* データが保存または分析される前にPIIを検出し修正します。
* 詳細な検証が必要なイベントの小さなサブセットのみに適応します。
* AI/MLパイプラインおよびコンプライアンスチェックのためのデータ品質を向上させます。

## 使用例

ユーザーが誤ってPIIを含む可能性のある非構造化入力を収集する場合にこのパターンを使用します。
例には以下が含まれます：

* チャットメッセージ
* サポートフォーム
* 製品レビュー
* 検索フィールド

2段階検証パターンは、訪問プロファイル、分析ツール、またはAIパイプラインに入る前に、電子メールアドレス、電話番号、クレジットカードの詳細などの機密データを検出し管理します。

EventStreamを通じてデータをフィルタリングおよび検証することで、コンプライアンス要件を満たしながら、システム全体で使用される顧客および行動データの正確性を保持することができます。

## 要件

このパターンを実装するには、以下が必要です：

* EventStream
* 機能
* AWSアカウントで：
  * AWS Comprehendへのアクセス
  * デプロイされたLambda関数
  * （オプション）API GatewayまたはEventBridge統合
* 基本的な知識：
  * JavaScript（機能用）
  * 正規表現
  * HTTP API

## 統合手順

### ステップ1：潜在的なPIIをフラグするためのデータ変換機能を作成する

個人識別情報（PII）を含む可能性のあるイベントをフラグし、オプションでハッシュするために、正規表現パターンマッチングを使用するデータ変換機能を作成します。

[データ変換機能を作成する](https://docs.tealium.com/create-function/#create-a-data-transformation-function)の手順に従い、このユースケースに対する次の構成を適用します：

#### トリガー条件を構成する

**データ変換**を機能タイプとして選択し、トリガー名を入力した後、機能をアクティブにする条件を定義します。

機能がトリガーされるように、次の条件を追加します：

* イベントペイロードが電子メールアドレスなどの一般的なPII形式を検出する正規表現パターンに一致する条件。
* すでにステージ2検証を通過したイベント（AWS Comprehendによってすでにフラグが付けられたイベントなど）をスキップする条件。

例えば：


[
  [
    {
    "input": "$.data",
    "operator": "matches regex",
    "filter": "/\\b[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}\\b/im"
    },
    {
    "input": "$.data.udo.tealium_event",
    "operator": "does not equal",
    "filter": "pii_detected"
    }
  ]  
]


![](https://docs.tealium.com/images/guides/data-transformation-function.png)

#### 変換コードを追加する

**コード**タブの下で、疑わしいPIIを含むイベントにフラグを追加し、オプションで機密フィールドをハッシュするコードでデフォルトのロジックを置き換えます。

```js
import CryptoES from "crypto-es";

// 特定のキーを許可したい場合は、ここでそれらを定義します
const allowedPIIKeys = ["mid_email"];

// メール検出用の正規表現
const emailRegex = /\b[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}\b/im;

function findAndHashEmailKeys(jsonData, hashFunction) {
  function traverse(obj, currentPath = "") {
    for (const key in obj) {
      const newPath = `${currentPath}.${key}`;
      if (typeof obj[key] === "string" && emailRegex.test(obj[key]) && !allowedPIIKeys.includes(key)) {
        obj[key] = hashFunction(obj[key]).toString();
      } else if (typeof obj[key] === "object" && obj[key] !== null) {
        traverse(obj[key], newPath);
      }
    }
  }
  traverse(jsonData);
}

transform((event) => {
  findAndHashEmailKeys(event.data, CryptoES.SHA256);
  event.data.udo["potential_pii_detected"] = true;
});
```

このスクリプトは次のことを行います：

* イベントペイロードを再帰的にスキャンして、メールパターンに一致する文字列を検出します。
* 明示的に許可されたキー（`mid_email`など）を除いて、メールパターンに一致する値をハッシュします。
* ダウンストリームのフィルタリングおよびルーティングで使用するために、イベントに`potential_pii_detected: true`フラグを追加します。

![](https://docs.tealium.com/images/guides/data-transformation-function-code.png)

#### 保存、テスト、公開

1. **テスト**タブを使用して、サンプルペイロードでロジックを検証します。
1. **構成**タブに移動し、**ステータス**を**ON**に構成します。
1. **完了**をクリックし、**保存して公開**をクリックします。

### ステップ2: 派生属性を使用してAudienceStreamエンリッチメントをフィルタリングする

データ変換機能を使用して潜在的なPIIを含むイベントをフラグした後、派生属性とAudienceStreamイベントフィルターを使用して、それらのイベントが訪問プロファイルをエンリッチするのを防ぎます。
#### ブール型イベント属性の作成

ステップ1で追加された `potential_pii_detected` フラグからその値を導出するブール型イベント属性を作成します。

1. **Transform > Event Attributes > Add Attribute** に移動します。
1. **属性タイプ** で **Universal Variable** を選択します。
1. **Continue** をクリックします。
1. データタイプとして **Boolean** を選択します。
1. 属性の名前を `Email_Check` のように構成します。
1. **Enrichments** の下で、以下のエンリッチメントを構成します：
    * すべてのイベントに対してデフォルトで `false` に構成：
        * ブール値を `false` に構成
        * **WHEN**: `ANY EVENT`
    * フラグ付きPIIイベントに対して `true` に構成：
        * ブール値を `true` に構成
        * **WHEN**: `ANY EVENT`
        * **AND**:

            
            [
              [
                {
                "input": "potential_pii_detected",
                "operator": "is true"
                },
                {
                "input": "tealium_event",
                "operator": "does not equal",
                "filter": "pii_detected"
                }
              ]  
            ]
            

これにより、すべてのイベントに `true` または `false` の値が構成され、フラグ付きイベントのみが `true` とマークされます。

![](https://docs.tealium.com/images/guides/email-check-attribute.png)

#### AudienceStream イベントフィルターを使用してフラグ付きイベントを除外

`Email_Check` 属性を使用して、AudienceStreamでリアルタイム訪問プロファイルのエンリッチメントからフラグ付きイベントを防ぎます。

1. **Server-Side Settings > General Settings** に移動します。
1. **Activate AudienceStream > Event Filter** の下で、フィルターを構成します：

   * **属性名**: `Email_Check`
   * **値**: `false`

`Email_Check` が `false` のイベントのみが AudienceStream によって処理されます。AudienceStreamは潜在的なPII（`Email_Check: true`）としてフラグ付けされたイベントを除外します。

![](https://docs.tealium.com/images/guides/audiencestream-event-filter.png)

### ステップ3: フラグ付きイベントをルーティングするためのイベントフィードの作成

イベントフィードを使用すると、属性条件に基づいてイベントをグループ化して分離することができます。このステップでは、潜在的なPIIを含むとフラグ付けされたイベントを収集するフィードを作成します。これにより、それらを別々に処理することができます。たとえば、二次検証のためにAPIに送信します。

1. **Validate > Live Events** に移動し、**+ Add Event Feed** をクリックします。
1. **Title** を `Email_Check is True` またはお好みの説明的な名前に構成します。
1. **Capture events that...** セクションに以下の条件を追加します：

    
    [
      [
        {
        "input": "Email_Check",
        "operator": "is true"
        },
        {
        "input": "tealium_event",
        "operator": "does not equal (ignore case)",
        "filter": "pii_detected"
        }
      ]  
    ]
    

これらの条件は、次のイベントにのみ一致します：

* データ変換関数によってフラグが付けられたイベント（`potential_pii_detected`）
* `Email_Check = true` にエンリッチされたイベント
* まだ二段階検証によって処理されていないイベント

![](https://docs.tealium.com/images/guides/email-check-event-feed.png)


<blockquote>
このフィードをコネクタ、ウェブフック、または EventDB や EventStore などの保存ソリューションに接続して、さらなる処理を行います。
</blockquote>


イベントフィードについての詳細は、[about-event-feeds](https://docs.tealium.com/about-event-feeds/) を参照してください。

### ステップ4: 処理済みイベント関数を構成してペイロードをAWSに送信

処理済みイベント関数は、サーバーサイドデータパイプラインの最後に実行されます。この関数を使用して、フラグ付きイベントをAWS Lambda + Comprehendなどの外部サービスに送信して、さらなるPII分析を行います。詳細については、[about-functions](https://docs.tealium.com/about-functions/) を参照してください。

イベントフィードで定義された基準に一致するイベントが発生すると（ステップ3）、この関数がトリガーされます。この関数は、受信イベントから関連する値を抽出し、API Gatewayを通じてAWS Lambdaに送信し、その後イベントに結果（PII検出など）を追加します。

#### 処理済みイベント関数の作成

1. **Server-Side > Transform > Functions** に移動します。
1. **+ Add Function** をクリックします。
1. 関数の名前を入力します。
1. **Processed Event** トリガーを選択し、**Continue** をクリックします。
1. トリガー名を `Check for PII` のように構成します。
1. トリガーをステップ3で作成したイベントフィードに構成します（例：`Email_Check is True`）。
1. **Continue** をクリックします。

#### 関数コードの更新

コードエディタに以下のサンプルコードを貼り付けます。このコードは、`tealium_profile` や `tealium_event` などのデフォルトを除外して属性を収集し、ペイロードを準備し、API Gatewayを通じてAWS Lambdaエンドポイントに送信します。

```js
const url = "https://your-url"; // 実際のAPI Gateway URLに置き換えてください。

activate(async ({ event, helper }) => {
//グローバル変数を使用してデフォルト値を構成し、コードとエラーを減らします。    


    // 元のイベントの変更はミューテーションによって適用されます
    const IGNORE = ['tealium_profile', 'tealium_account', 'tealium_event']
    var TOCHECK = ""

    function preparePayload(o){
        var str = ""
        for(var i in o ){
            if(!IGNORE.includes(i))
                //console.log(i)
                TOCHECK += o[i] + "\n"
        }
        
    }
   
    preparePayload(event.data.udo)
    preparePayload(event.data.firstparty_tealium_cookies)
    
        //console.log(str)
        
        const response = await fetch(url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({"text" : JSON.stringify(TOCHECK)})
        });
        //console.log("Status :" + response.status);
        
        if(response.status == 200){
            var tempSet = new Set()
            var toReturn = {}
            var result = JSON.parse(response._bodyInit);
            var rr = JSON.parse(result['body'])
            for(var j in rr){
                var type = rr[j]['Type']
                if(type == 'EMAIL'){
                    var text = rr[j]['Text']
                    var score = rr[j]['Score']
                    tempSet.add(type+"__"+score+"__"+text)
                }
            }
            toReturn['tealium_event'] = 'pii_detected'
            toReturn['tealium_visitor_id'] = event['visitor_id']
            toReturn['tealium_firstparty_visitor_id'] = event['visitor_id']
            toReturn['pii_type_value'] = Array.from(tempSet)

            track(toReturn, {
                tealium_account: "TEALIUM_ACCOUNT", // Tealiumアカウントに置き換えてください。
                tealium_profile: "TEALIUM_PROFILE", // Tealiumプロファイルに置き換えてください。
                tealium_datasource: "TEALIUM_DATASOURCE", // Tealiumデータソースに置き換えてください。
            })
            .then(response => {
                if(!response.ok){
                    throw new Error(`Network response was not ok. Status code: ${response.status}.`);
                }
                return response.text();
            })
            
           
            console.log("200 : ", JSON.stringify(result['body']))
        }else {
           console.log('FAILED : ', JSON.stringify(response))
        }

});
```

![](https://docs.tealium.com/images/guides/check-for-pii-processed-event-function.png)

#### 関数のテスト

1. 関数エディタの **Test** タブに移動します。
1. **Test Payload** パネルを使用して、実際のサンプルイベントペイロードを読み込むか貼り付けます。
1. **Run Test** をクリックして、関数が正しく実行されデータが送信されることを確認します。
1. 準備ができたら、関数を有効にして **Save and Publish** をクリックします。

送信されたリクエストと受信した応答またはエラーメッセージを確認するログが表示されます。必要に応じてペイロードまたはコードを調整します。

詳細については、 を参照してください。

#### 認証の構成（オプション）

API GatewayまたはLambdaエンドポイントが認証を要求する場合、**Advanced** タブに移動して関数で使用する認証トークンを構成します。

#### 結果

関数がライブで公開されると、フィードの基準を満たすイベント（例：`Email_Check = true`）がこの関数をトリガーし、ペイロードをLambdaサービスに送信します。
### ステップ5: AWS LambdaとComprehendの構成

このステップでは、個人を特定できる情報（PII）が含まれているイベントを分析するためのAWSインフラを構成します。これには、API Gatewayの構成、Lambda関数の作成、およびエンティティ検出を行うためのAmazon Comprehendの使用が含まれます。Lambdaは、下流でイベントを豊かにし、ルーティングするために使用できる結果を返します。

#### API Gatewayの構成

Tealium関数からイベントを受け取り、Lambda関数に転送するAPI Gatewayエンドポイントを作成します。エンドポイントはPOSTリクエストを受け入れ、Lambdaプロキシ統合で構成する必要があります。

詳細な手順については、[AWS Lambda: Amazon API Gatewayエンドポイントを使用してLambda関数を呼び出す](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)を参照してください。

#### PII検出用のLambda関数を作成

受信イベントペイロードを処理し、Amazon Comprehendを使用してPIIをチェックし、元のイベントと分析結果を含むレスポンスを返すLambda関数を作成します。

Lambdaは以下を行う必要があります:

* Tealiumからの完全なイベントペイロードを受け入れる。
* 分析のための関連フィールドを抽出する（例：`event.data`）。
* AWS Comprehendを使用してPII（特にメールアドレス）を検出する。
* Comprehendの結果とともに元のペイロードを返す。

こちらはNode.jsでのサンプル実装の概要です:

```js
const AWS = require("aws-sdk");
const comprehend = new AWS.Comprehend();

exports.handler = async (event) => {
  const inputText = JSON.stringify(event.data); // Or a specific field
  const languageCode = "en";

  try {
    const piiResponse = await comprehend.detectPiiEntities({
      Text: inputText,
      LanguageCode: languageCode,
    }).promise();

    const piiEntities = piiResponse.Entities || [];
    const piiDetected = piiEntities.length > 0;

    return {
      ...event,
      pii_analysis: {
        pii_detected: piiDetected,
        entities: piiEntities,
      },
    };
  } catch (err) {
    console.error("PII detection failed:", err);
    return {
      ...event,
      pii_analysis: {
        pii_detected: false,
        error: "Comprehend error",
      },
    };
  }
};
```

完全な例については、[Amazon Comprehend: AWS SDKまたはCLIを使用してDetectPiiEntitiesを使用する](https://docs.aws.amazon.com/comprehend/latest/dg/example_comprehend_DetectPiiEntities_section.html)を参照してください。

#### 例のレスポンス構造

```json
{
  "data": {
    "udo": {
      "potential_pii_detected": true,
      ...
    }
  },
  "pii_analysis": {
    "pii_detected": true,
    "entities": [
      {
        "Type": "EMAIL",
        "Score": 0.98,
        "BeginOffset": 13,
        "EndOffset": 35
      }
    ]
  }
}
```

このエンリッチメントは、追加の処理、アラート、または抑制のための下流ロジックで使用できます。


<blockquote>
処理中の問題をキャプチャするために、Lambdaにログ記録とエラーハンドリングを追加します。検出率やエラーに基づいてアラートを構成するために、構造化されたログを使用してイベントを追跡します。
</blockquote>


### ステップ6: レビューとテスト

確認するために:

* PIIを含むサンプルテキストでテストイベントを送信します。
* `potential_pii_detected`が正しく構成されていることを確認します。
* AWSから返された赤字テキストを確認します。
* APIのパフォーマンスとレイテンシのログをレビューします。
* ステージ2が必要な場合にのみ呼び出されることを確認するために、呼び出し回数を監視します。

### ステップ7: レスポンスを下流のルーティングと決定に使用する

AWS Lambdaからエンリッチされたイベントを受け取った後、イベントペイロードの`pii_analysis`オブジェクトを使用してさらなるアクションを取ります。このステップは、PIIが確認されたかどうかに基づいてイベントを解釈し、ルーティングする方法に焦点を当てています。

#### PII結果に基づいてシステムを更新する

返されたフィールド`pii_analysis.pii_detected`を使用して、異なる処理パスをトリガーします。例えば:

* `pii_detected`が`true`の場合:
  * 赤字化ワークフローに送信します。
  * 個人化または分析パイプラインから抑制します。
  * プライバシーチームにアラートを送信するか、監査をトリガーします。
* `pii_detected`が`false`の場合:
  * エンリッチメント、セグメント化、またはコネクタ配信などの通常の処理を再開します。

これらの決定を以下のいずれかを使用して構成します:

* **Tealium関数**: 結果に基づいて別の変換または処理されたイベント関数を使用します。
* **AudienceStream**: 検出ステータスを反映する訪問またはイベントレベルの属性を作成し、ルールやバッジで使用します。
* **イベントフィード**: PII分析結果に基づいて新しいフィードを作成し、コネクタやデータ保存（EventStore、EventDB）へのターゲットルーティングを行います。

## リソース

* [関数](https://docs.tealium.com/about-functions/)
* [AWS Comprehend: 個人を特定できる情報 (PII)](https://docs.aws.amazon.com/comprehend/latest/dg/pii.html)
* [AWS Lambda: Amazon API Gatewayエンドポイントを使用してLambda関数を呼び出す](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)
* [Amazon API Gatewayとは何か？](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
* [Amazon EventBridgeとは何か？](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)
* [Amazon Comprehend: AWS SDKまたはCLIを使用してDetectPiiEntitiesを使用する](https://docs.aws.amazon.com/comprehend/latest/dg/example_comprehend_DetectPiiEntities_section.html)

