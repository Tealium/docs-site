---
title: 2 段階検証パターンを使用してリアルタイムで PII を検出する
description: Tealium Functions と AWS Comprehend を使用したスケーラブルな 2 段階検証パターンにより、リアルタイムのイベントデータから個人識別情報（PII）を検出し、秘匿化します。
url: https://docs.tealium.com/ja/guides/two-stage-pii-detection/
---
2 段階検証パターンは、リアルタイムのイベントデータに含まれる個人識別情報（PII）を検出して管理するための、スケーラブルな方法です。サーバーサイド関数と AWS Comprehend を使用し、正規表現に基づく高速なフィルタリングと、高度な機械学習による検証を組み合わせます。

このガイドでは、以下について説明します。

* 高スループットのデータストリームで PII を検出するための実践的なアプローチ。
* Tealium EventStream、Functions、および AWS サービスを統合するための手順。
* データ変換関数、処理済みイベント関数、および AWS Lambda の実装例。

## 仕組み

2 段階検証パターンを使用して、リアルタイムかつ大容量のデータストリームに含まれる PII を識別し、管理します。このパターンでは、軽量で低レイテンシーのチェックと、より低速ながら高精度な機械学習（ML）による検証を分離することで、パフォーマンスを維持しながら処理コストを削減します。

このアプローチは、`message_text`、`form_input`、`user_comment` などの非構造化フィールドや自由記述テキストフィールドに含まれる PII の検出に適しています。

このパターンは、次の 2 つの段階で構成されます。

* **第 1 段階（正規表現フィルター）**：軽量なサーバーサイド関数が正規表現を使用して、PII が含まれている可能性のあるイベントを識別します。この関数は、`message_text`、`form_input`、`user_comment` などのフィールドをスキャンし、機密情報である可能性のあるデータを識別します。
* **第 2 段階（検証）**：Webhook は、フラグが構成されたイベントのみを AWS Comprehend に送信し、自然言語処理（NLP）に基づく検出と、必要に応じた秘匿化を実行します。

第 1 段階でフラグが構成されたイベントのみが第 2 段階に進むため、不要な API 呼び出しとレイテンシーを最小限に抑えられます。

### 主要コンポーネントについて

* **データ変換関数**  
  受信したイベントデータを評価し、軽量な正規表現を適用して潜在的な PII を識別するサーバーサイド関数です。必要に応じて、この関数は検出した値を転送前にハッシュ化できます。

* **派生属性**  
  データ変換関数の出力から派生するブール型のイベント属性です。関数は PII を検出すると、この属性を `true` に構成し、イベントにフラグを追加します。

* **AudienceStream イベントフィルター**  
  派生属性に基づいて受信イベントをフィルタリングし、PII を含まないイベントのみが訪問プロファイルをエンリッチするようにします。

* **イベントフィード**  
  フラグが構成されたイベントを派生属性に基づいてフィルタリングしたストリームです。さらに処理するために、コネクター、保存、または他の関数へ送信できます。

* **処理済みイベント関数**  
  エンリッチメントとフィルタリングの後に実行される関数です。フラグが構成されたイベントを外部エンドポイント（AWS Lambda と Comprehend など）へ送信し、高度な検証を行います。

## 利点

データがエンリッチ、保存、またはダウンストリームシステムと共有される前に、ガバナンスまたは秘匿化ポリシーを適用する必要がある場合は、2 段階検証パターンを使用します。

次のような利点があります。

* 軽量なパターンマッチングで大部分のイベントをフィルタリングすることにより、AWS Comprehend へのリクエスト数を削減します。
* フラグが構成されたイベントのみを第 2 段階の検証へルーティングすることで、イベント処理のリアルタイム性を維持できます。
* データが保存または分析される前に PII を検出し、秘匿化します。
* 少数のイベントのみで詳細な検証が必要となる他のワークフローにも適応できます。
* AI/ML パイプラインおよびコンプライアンスチェックのデータ品質を向上させます。

## ユースケース

ユーザーが誤って PII を入力する可能性のある非構造化データを収集する場合に、このパターンを使用します。  
次のような例があります。

* チャットメッセージ
* サポートフォーム
* 製品レビュー
* 検索フィールド

2 段階検証パターンは、メールアドレス、電話番号、クレジットカード情報などの機密データを、訪問プロファイル、分析ツール、または AI パイプラインに取り込まれる前に検出して管理します。

EventStream を流れるデータをフィルタリングして検証することにより、システム全体で使用される顧客データおよび行動データの正確性を維持しながら、コンプライアンス要件を満たすことができます。

## 要件

このパターンを実装するには、以下が必要です。

* EventStream
* Functions
* 以下を備えた AWS アカウント：
  * AWS Comprehend へのアクセス
  * デプロイ済みの Lambda 関数
  * （オプション）API Gateway または EventBridge との統合
* 以下に関する基本的な知識：
  * JavaScript（関数用）
  * 正規表現
  * HTTP API

## 統合手順

### 手順 1：潜在的な PII にフラグを構成するデータ変換関数を作成する

個人識別情報（PII）が含まれている可能性のあるイベントにフラグを構成し、必要に応じてハッシュ化するには、正規表現のパターンマッチングを使用するデータ変換関数を作成します。

[データ変換関数を作成する](https://docs.tealium.com/create-function/#create-a-data-transformation-function)手順に従い、このユースケースに次の構成を適用します。

#### トリガー条件を構成する

関数タイプとして **データ変換**を選択し、トリガー名を入力した後、関数を起動する条件を定義します。

未処理で機密情報が含まれている可能性のあるイベントのみが関数をトリガーするように、次の条件を追加します。

* メールアドレスなど、一般的な PII 形式を検出する正規表現パターンとイベントペイロードを照合する条件。
* 第 2 段階の検証をすでに通過したイベント（AWS Comprehend によってすでにフラグが構成されたイベントなど）をスキップする条件。

例：


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

**コード**タブで、デフォルトのロジックを、PII の疑いがあるイベントにフラグを追加し、必要に応じて機密フィールドをハッシュ化するコードに置き換えます。

```js
import CryptoES from "crypto-es";

// If you want to allow specific keys, define them here
const allowedPIIKeys = ["mid_email"];

// Email detection regex
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

このスクリプトは、以下の処理を実行します。

* イベントペイロードを再帰的にスキャンし、メールアドレスのパターンに一致する文字列を検索します。
* 明示的に許可されたキー（`mid_email` など）を除き、メールアドレスのパターンに一致する値をハッシュ化します。
* ダウンストリームでのフィルタリングとルーティングに使用するため、イベントに `potential_pii_detected: true` フラグを追加します。

![](https://docs.tealium.com/images/guides/data-transformation-function-code.png)

#### 保存、テスト、パブリッシュする

1. **テスト**タブを使用して、サンプルペイロードでロジックを検証します。
1. **構成**タブに移動し、**ステータス**を **オン**に構成します。
1. **完了**をクリックしてから、**保存してパブリッシュ**をクリックします。

### 手順 2：派生属性を使用して AudienceStream のエンリッチメントをフィルタリングする

データ変換関数を使用して潜在的な PII を含むイベントにフラグを構成した後、派生属性と AudienceStream イベントフィルターを使用して、それらのイベントによって訪問プロファイルがエンリッチされないようにします。
#### ブール型イベント属性を作成する

手順1で追加した `potential_pii_detected` フラグから値を取得するブール型イベント属性を作成します。

1. **Transform > Event Attributes > Add Attribute** に移動します。
1. **attribute type** で **Universal Variable** を選択します。
1. **Continue** をクリックします。
1. データ型として **Boolean** を選択します。
1. 属性に `Email_Check` などの名前を付けます。
1. **Enrichments** で、次のエンリッチメントを構成します。
    * すべてのイベントでデフォルトを `false` にする：
        * Boolean を `false` に構成
        * **WHEN**：`ANY EVENT`
    * PII のフラグが付けられたイベントを `true` に構成する：
        * Boolean を `true` に構成
        * **WHEN**：`ANY EVENT`
        * **AND**：

            
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
            

これにより、すべてのイベントに `true` または `false` の値が構成され、フラグが付けられたイベントのみが `true` としてマークされます。

![](https://docs.tealium.com/images/guides/email-check-attribute.png)

#### AudienceStream のイベントフィルターを使用してフラグ付きイベントを除外する

`Email_Check` 属性を使用して、フラグが付けられたイベントが AudienceStream のリアルタイム訪問プロファイルをエンリッチしないようにします。

1. **Server-Side Settings > General Settings** に移動します。
1. **Enable Customer Data Platform > Customer Data Platform - Event Filter** で、フィルターを次のように構成します。

   * **Attribute name**：`Email_Check`
   * **Value**：`false`

`Email_Check` が `false` のイベントのみが AudienceStream によって処理されます。潜在的な PII としてフラグが付けられたイベント（`Email_Check: true`）は、AudienceStream から除外されます。

![](https://docs.tealium.com/images/guides/audiencestream-event-filter.png)

### 手順3：フラグ付きイベントをルーティングするイベントフィードを作成する

イベントフィードを使用すると、属性条件に基づいてイベントをグループ化し、分離できます。この手順では、潜在的な PII が含まれているとしてフラグが付けられたイベントを収集するフィードを作成します。これにより、これらのイベントを個別に処理できます。たとえば、二次検証のために API に送信できます。

1. **Validate > Live Events** に移動し、**+ Add Event Feed** をクリックします。
1. **Title** を `Email_Check is True`、または任意のわかりやすい名前に構成します。
1. **Capture events that...** セクションで、次の条件を追加します。

    
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
    

これらの条件は、次のすべてに該当するイベントのみと一致します。

* データ変換関数によってフラグが付けられている（`potential_pii_detected`）
* `Email_Check = true` にエンリッチされている
* 第2段階の検証でまだ処理されていない

![](https://docs.tealium.com/images/guides/email-check-event-feed.png)


<blockquote>
このフィードをコネクタ、Webhook、または EventDB や EventStore などの保存ソリューションに接続して、さらに処理します。
</blockquote>


イベントフィードの詳細については、[about-event-feeds](https://docs.tealium.com/about-event-feeds/)を参照してください。

### 手順4：ペイロードを AWS に送信する処理済みイベント関数を構成する

処理済みイベント関数は、サーバーサイドデータパイプラインの最後に実行されます。この関数を使用して、フラグが付けられたイベントを AWS Lambda + Comprehend などの外部サービスに送信し、PII をさらに分析します。詳細については、[about-functions](https://docs.tealium.com/about-functions/)を参照してください。

イベントが手順3のイベントフィードで定義した条件に一致すると、この関数がトリガーされます。この関数は受信イベントから関連する値を抽出し、API Gateway を介して AWS Lambda に送信した後、PII 検出などの結果をイベントに追加します。

#### 処理済みイベント関数を作成する

1. **Transform > Functions** に移動します。
1. **+ Add Function** をクリックします。
1. 関数名を入力します。
1. **Processed Event** トリガーを選択し、**Continue** をクリックします。
1. `Check for PII` などのトリガー名を入力します。
1. トリガーを、手順3で作成したイベントフィード（`Email_Check is True` など）に構成します。
1. **Continue** をクリックします。

#### 関数コードを更新する

次のサンプルコードをコードエディターに貼り付けます。このコードは、`tealium_profile` や `tealium_event` などのデフォルト値を除外し、検査対象の属性を収集してペイロードを準備します。その後、API Gateway を介して AWS Lambda エンドポイントにペイロードを送信します。

```js
const url = "https://your-url"; // Replace with your actual API Gateway URL.

activate(async ({ event, helper }) => {
//Set default values through global variables to reduce code and errors.    


    // changes are applied through mutation of the original event
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
                tealium_account: "TEALIUM_ACCOUNT", // Replace with your Tealium account.
                tealium_profile: "TEALIUM_PROFILE", // Replace with your Tealium profile.
                tealium_datasource: "TEALIUM_DATASOURCE", // Replace with your Tealium datasource.
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

#### 関数をテストする

1. 関数エディターの **Test** タブに移動します。
1. **Test Payload** パネルを使用して、実際のサンプルイベントペイロードを読み込むか貼り付けます。
1. **Run Test** をクリックし、関数が実行されてデータが正しく送信されることを確認します。
1. 準備ができたら関数を有効にし、**Save and Publish** をクリックします。

送信リクエストと、レスポンスまたはエラーメッセージを確認できるログが表示されます。必要に応じて、ペイロードまたはコードを調整します。

詳細については、を参照してください。

#### 認証を構成する（任意）

API Gateway または Lambda エンドポイントで認証が必要な場合は、**Advanced** タブに移動し、関数で使用する認証トークンを構成します。

#### 結果

関数が公開されて有効になると、フィードの条件（`Email_Check = true` など）を満たすイベントによってこの関数がトリガーされ、ペイロードが Lambda サービスに送信されます。
### ステップ5：AWS LambdaとComprehendを構成する

このステップでは、フラグが付けられたイベントを分析し、個人を特定できる情報（PII）が含まれているかどうかを確認するためのAWSインフラストラクチャを構成します。これには、API Gatewayの構成、Lambda関数の作成、Amazon Comprehendを使用したエンティティ検出が含まれます。Lambdaは、後続処理でイベントのエンリッチメントやルーティングに使用できる結果を返します。

#### API Gatewayを構成する

Tealium Functionsからイベントを受信し、Lambda関数に転送するAPI Gatewayエンドポイントを作成します。このエンドポイントがPOSTリクエストを受け付け、Lambdaプロキシ統合を使用するように構成します。

詳しい手順については、[AWS Lambda：Amazon API Gatewayエンドポイントを使用したLambda関数の呼び出し](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)を参照してください。

#### PII検出用のLambda関数を作成する

受信したイベントペイロードを処理し、Amazon Comprehendを使用してPIIを確認したうえで、元のイベントと分析結果の両方を含むレスポンスを返すLambda関数を作成します。

Lambdaでは、次の処理を行う必要があります。

* Tealiumからイベントペイロード全体を受け取る。
* 分析対象のフィールド（例：`event.data`）を抽出する。
* AWS Comprehendを使用してPII（特にメールアドレス）を検出する。
* Comprehendの結果とともに元のペイロードを返す。

以下は、Node.jsによる実装例の概要です。

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

完全な例については、[Amazon Comprehend：AWS SDKまたはCLIでDetectPiiEntitiesを使用する](https://docs.aws.amazon.com/comprehend/latest/dg/example_comprehend_DetectPiiEntities_section.html)を参照してください。

#### レスポンス構造の例

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

このエンリッチメントは、追加処理、アラート、抑制などの後続ロジックで使用できます。


<blockquote>
処理中の問題を記録できるように、Lambdaにログ記録とエラー処理を追加してください。構造化ログを使用してイベントを追跡し、検出率やエラーに基づいてアラートを構成します。
</blockquote>


### ステップ6：確認してテストする

検証するには、次の操作を行います。

* PIIを含むサンプルテキストを使用してテストイベントを送信する。
* `potential_pii_detected`が正しく構成されていることを確認する。
* マスキングされたテキストがAWSから返されることを確認する。
* APIのパフォーマンスとレイテンシーについてログを確認する。
* 呼び出し回数を監視し、第2段階が必要な場合にのみ呼び出されていることを確認する。

### ステップ7：レスポンスを後続のルーティングと判断に使用する

AWS Lambdaからエンリッチされたイベントを受信した後、イベントペイロード内の`pii_analysis`オブジェクトを使用して追加のアクションを実行します。このステップでは、PIIが確認されたかどうかに基づいてイベントを解釈し、ルーティングする方法について説明します。

#### PIIの結果に基づいてシステムを更新する

返されたフィールド`pii_analysis.pii_detected`を使用して、異なる処理パスを開始します。例：

* `pii_detected`が`true`の場合：
  * マスキングワークフローに送信する。
  * パーソナライゼーションまたは分析パイプラインから除外する。
  * プライバシーチームに通知するか、監査を開始する。
* `pii_detected`が`false`の場合：
  * エンリッチメント、セグメンテーション、コネクタへの配信などの通常処理を再開する。

次のうち1つ以上を使用して、これらの判断を構成します。

* **Tealium Functions**：別の変換関数または処理済みイベント関数を使用して、結果に応じた処理を実行します。
* **AudienceStream**：検出ステータスを反映する訪問レベルまたはイベントレベルの属性を作成し、ルールやバッジで使用します。
* **イベントフィード**：PII分析結果に基づいて新しいフィードを作成し、コネクタまたはデータ保存（EventStore、EventDB）に対象を絞ってルーティングします。

## リソース

* [Functions](https://docs.tealium.com/about-functions/)
* [AWS Comprehend：個人を特定できる情報（PII）](https://docs.aws.amazon.com/comprehend/latest/dg/pii.html)
* [AWS Lambda：Amazon API Gatewayエンドポイントを使用したLambda関数の呼び出し](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)
* [Amazon API Gatewayとは](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
* [Amazon EventBridgeとは](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)
* [Amazon Comprehend：AWS SDKまたはCLIでDetectPiiEntitiesを使用する](https://docs.aws.amazon.com/comprehend/latest/dg/example_comprehend_DetectPiiEntities_section.html)