---
title: Marketo、Google Analytics、AudienceStreamを使用してリードスコアリングモデルを作成する方法
description: この記事では、Marketo、Google Analytics、AudienceStreamを使用してリードスコアリングモデルを作成する方法について説明します。
url: https://docs.tealium.com/ja/guides/lead-scoring-model/
---## はじめに

* **タグベンダー**  
Google Analytics (Universal) &#43; Google Measurement Protocol
* **ユースケース**  
AudienceStreamからGoogle Analyticsへリードスコアをプッシュ
* **主要属性**
    * **リードスコア** ([数値]())  
    カスタムイベントの相互作用に基づく数値。この値は新しい訪問に対してゼロに初期化され、その訪問がクライアントのウェブサイト上の特定のアセットとの相互作用に基づいて増減されます。
    * **訪問価値** ([文字列]())  
    リードスコア値に基づく文字列。この値は新しい訪問に対して`Standard Visitor`に初期化されます。その訪問は、指定されたリードスコアの閾値を超えた後に`High Value Visitor`にアップグレードされることができます。さらに、その訪問のリードスコアがその閾値を下回ると`Standard Visitor`に戻ることがあります。このユースケースでは、初期値は2つだけですが、訪問間の階層をさらに作成するために追加することができます。

* **ユースケース**  
Google Analyticsに`GET URL`コールをトリガーして、そのリードスコアが彼らを置くオーディエンスに基づいて訪問が`Standard Visitor`または`High Value Visitor`かを識別します。このプロセスは、データを送信するために[Google Analytics Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/)を活用します。
* **サンプルシナリオ**  
作成されるオーディエンスは、Marketo内で構築されたサンプルクライアントのスコアリングモデルからの要素に関連しています。Marketoのスコアリングモデルは、訪問がトリガーする各イベントにポイントを与え、それによってMarketo内のMQL（マーケティング資格リード）スコアを増加させます。AudienceStreamで同じイベントをキャプチャしてオーディエンスを作成することにより、カスタムディメンションに値を送信してGoogle Analyticsをエンリッチすることができます。これらのカスタムディメンションは、閲覧行動のルックバック分析に受動的に使用することも、Google Analyticsでリマーケティングリストを構築してGoogle広告にインポートし、Google Display Network内で広告目的に使用することもできます。

## ステップ1: Google Analytics訪問IDの取得 (Tealium iQ)

WebhookからのヒットをGoogle Analyticsが適切に保存するためには、[Webhook]()でGoogle Analytics訪問IDを提供する必要があります。これはTealium iQでクッキー`_ga`を解析し、クッキー値の最後の2つの長い数字をデータレイヤー変数に保存することによって行われます。`_ga`を**First Party Cookie**として、`google_visitorid`を`UDO Variable`として**Data Layer**タブで宣言します。次に、以下に示すように[Set Data Values extension]()を作成します。

以下のコードとスクリーンショットの例を参照してください：

```js
b[&#34;cp._ga&#34;].split(&#34;.&#34;).splice(2,2).join(&#34;.&#34;)
```

![](/images/server-side/google-analytics-visitor-id.png)

その後、`google_visitorid`値を文字列として保存できます。

![](/images/server-side/set-string-to-google-visitorid.png)

データが存在するかどうかを確認するために[Boolean]()を構成します。これは、`google_visitorid`に保存された値がGoogle Analyticsによってコネクタから受信したデータを保存するために必要であるため重要です。

![](/images/server-side/set-boolean-google-visitor-id.png)

最後に、Google Analytics用に構築するWebhookの`cid`パラメータにデータをマッピングします。

![](/images/server-side/map-to-cid.png)

## ステップ2: イベント情報のキャプチャ (Tealium iQ)

Tealium iQでリードスコアメトリックを調整するイベントを構成します。このステップでは、クリックされたり操作されたりした特定のウェブサイトアセットに`utag.link()`を呼び出すことが含まれます。このために、jQueryの`onHandler()`拡張機能またはJavaScriptコード拡張機能を使用するオプションがあります。これらはどちらもデータをGoogle AnalyticsとAudienceStreamに送信します。

このユースケースでは、[Javascript Code extension]()を使用し、jQueryを使用してすべてのイベントをキャプチャしました。このユースケースからの肯定的なイベントの例には、ケーススタディ、ホワイトペーパー、ビデオ、ウェビナーなどのアセットとの相互作用が含まれます。また、サポートなどの否定的なイベントも含まれ、これによりリードスコアが減少するかゼロにリセットされます。

![](/images/server-side/no-title-160ica6f830d8bd7a1ce.png)

## ステップ3: ルールと属性の作成 (AudienceStream)

### リードスコア

すべての新しい訪問に対して**リードスコア**をゼロに初期化します。これは、**Lifetime Event Count Number**を使用してゼロであるかどうかを確認することによって行われます。

![](/images/server-side/lead-score-lifetime.png)

肯定的なポイントを持つすべてのイベントについて、望む値で**リードスコア**を増加させます。

![](/images/server-side/increment-decrement-lead-score.png)

すべての否定的なイベントについて、モデルに合った方法で否定的なクレジットを適用します。**サポート**の場合、スコアをゼロにリセットします。

![](/images/server-side/lead-score-support-user.png)

スコアリングモデルがまだ洗練されている場合（このユースケースのように）、初期に小さな値を使用してください。そうすることで、モデルをより高い値で洗練するときに、初期の低いリードスコア値を持つ訪問がオーディエンスを歪めることがありません。

### ルール

`リードスコア &gt; 3`または`リードスコア &gt;= 3`。これらは次に訪問価値文字列を割り当てるために使用されます。

![](/images/server-side/ls-greater-equal-3.png)

### 訪問価値

このユースケースでは、初期の重要な**リードスコア**の閾値は`3`です。**リードスコア**が`3`未満の場合は`Standard Visitor`に構成します。**リードスコア**が`3`以上の場合は`High Value Visitor`に構成します。

![](/images/server-side/string-visitor-value.png)

## ステップ4: オーディエンスの作成 (AudienceStream)

### ハイバリュービジター

**訪問価値**が`High Value Visitor`の場合、訪問はこのオーディエンスのメンバーです。

![](/images/server-side/high-value-audience.png)

### スタンダードビジター

**訪問価値**が`Standard Visitor`の場合、訪問はこのオーディエンスのメンバーです。

![](/images/server-side/standard-audience.png)

## ステップ5: Webhookの構成 (Google AnalyticsとAudienceStream)

### カスタムディメンション

Google Analyticsで[Webhook]()が入力する**カスタムディメンション**を作成します。

![](/images/server-side/no-title-168i3748718d3d7cc6ec.png)

### Webhookの例

Google Analyticsにデータをトリガーするために使用される以下の例の構成です。

![](/images/server-side/google-analytics-configurations.png)


### 必須パラメータ

以下の表は、Google Analyticsで正しくデータを保存するために入力が必要な主要なフィールドを示しています。

Googleのドキュメントに基づいて`t`と`ni`は必須ではありませんが、Webhookが直帰率に影響を与えたりページビューを増加させたりしないように、それぞれ`event`と`1`に構成する必要があります。

| フィールド              | 説明                                                                                                                                                                     |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **t**=event        | ヒットタイプを識別します。ページビューまたはイベントのいずれかになります。ページが実際に表示されていないため、イベントを使用するのが最適です。 |
| **cid**=12345.6789 | Tealium iQによって解析された訪問IDです。                                                                                                                                    |
| **tid**=UA-12345-1 | Google Analyticsアカウント番号です。                                                                                                                                    |
| **v**=1            | Google測定プロトコルのバージョン1を示します。                                                                                                                    |
| **ni**=1           | ヒットが非インタラクションイベントであるかを識別します。`1`に構成することで、直帰率に影響を与えません。                                                                  |

### オプションパラメータ

以下の表は必須ではないが、Google AnalyticsでWebhookイベントを他のイベントから分離する方法に追加のコンテキストを提供するパラメータをリストしています。

| フィールド                  | 説明         |
|:-----------------------|:--------------------|
| **ec**=ASConnector     | イベントカテゴリ名 |
| **ea**=VisitorValue    | イベントアクション名   |
| **el**=StandardVisitor | イベントラベル名    |
| **dp**=/webhook/       | ドキュメントパス       |
| **dt**=Webhook         | ドキュメントタイトル      |

### AudienceStream動的パラメータ

このユースケースでは、以前に構成された属性から以下の値が入力されます。

| フィールド                                                      | 説明                                                                                                                     |
|:-----------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| **cd1**=id:123-ABC-456&amp;amp;token:\_mch-site.com-123456-789 | カスタムディメンション1の値。このシナリオでは`theMarketoID`です。                                                               |
| **cd2**=StandardVisitor                                    | カスタムディメンション2の値。このシナリオでは訪問の価値が`Standard Visitor`または`High Value Visitor`です。 |

### コネクタ

2つのコネクタが構成されます。それぞれが訪問が`Standard Visitor`または`High Value Visitor`のオーディエンスに参加または変更するときに発火します。

![](/images/server-side/two-connectors.png)

新しい訪問は、最初のページビューで`Standard Visitor`としてフラグを立てるためにコネクタを発火させます。この最初のコネクタは、Google Analyticsがカスタムディメンションに`NULL`値を自動的に割り当てないために必要です。カスタムディメンションにデフォルト値が必要な場合、何らかの値で入力する必要があります。彼らが最終的に`High Value Visitor`オーディエンスに参加すると、2番目のコネクタが発火して彼らを`High Value Visitor`にアップグレードします。その訪問がそのオーディエンスを離れて`Standard Visitor`オーディエンスに再参加する場合、コネクタは再び発火します。

## ステップ 6: 実行

### 例: カスタムレポート

![](/images/server-side/no-title-171i447e852b607fbd60.png)

### 例: High Value Visitorに基づくリマーケティングリスト

![](/images/server-side/no-title-172i85ee1c061f359fca.png)

Google Analyticsは、既存のディスプレイ広告キャンペーンと統合して、訪問をターゲットにすることができます。