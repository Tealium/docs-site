---
title: 属性エンリッチメント
description: 望む属性を特定した後、それらをエンリッチメントで構成します。
url: https://docs.tealium.com/ja/server-side/getting-started/audiencestream-cdp/enrichments/
---
エンリッチメントは、属性の値をいつ、どのように更新するかを決定するビジネスルールです。各データタイプは、属性の値を操作するためのエンリッチメントの選択を提供します。例えば、数値属性は「数値の増減」エンリッチメントを提供し、数値を加算または減算します。

## エンリッチメント条件

各エンリッチメントは特定の時間に構成されます。これが **WHEN** 構成です。以下のオプションが各訪問と訪問属性に対して利用可能です：

* **新規訪問** – 訪問が初めてサイトに来たときに発生
* **新規訪問** – 訪問の新しい訪問時に発生
* **任意のイベント** – 任意のイベント時に発生
* **訪問終了** – 訪問が終了したときに発生

また、エンリッチメントが発生するタイミングを決定するカスタム条件、ルールを作成することもできます。

## 訪問属性の作成

![](https://docs.tealium.com/images/server-side/getting-started-audiencestream-lifetime-order-value.png)

例として、**Lifetime Order Value**（生涯注文価値）と呼ばれる人気のあるeコマース訪問属性を見てみましょう。これは、顧客が完了したすべての注文で費やした累積金額を計算する訪問属性です。この値を計算するには、購入がいつ発生するかとその購入額も知る必要がありますので、属性の依存関係は以下の通りです：

* `order_total` – 注文合計額のイベント属性。
* `purchase` – 完了した購入を追跡するイベント。

この属性を追加するための手順は以下の通りです：

1. **Transform > Visitor / Visit Attributes** に移動し、**Add Attribute** をクリックします。
1. スコープを **Visitor** に構成し、**Continue** をクリックします。
1. データタイプ **Number** を選択し、**Continue** をクリックします。
1. 属性の名前を `Lifetime Order Value` と入力します。
1. **Add Enrichment** をクリックし、**Increment or Decrement Number** を選択します。
1. 増加させる値を含む属性 (`order_total`) を選択します。
1. **WHEN** を **Any Event** に構成したまま、**Create a New Rule** をクリックします。
1. 購入イベントが発生したときを特定するルールを作成します。例えば：  
`tealium_event EQUALS purchase`
1. **Save** をクリックし、**Finish** をクリックします。

これで、完了した注文の合計金額を追跡するエンリッチメントを持つ訪問属性を作成しました。

![](https://docs.tealium.com/images/server-side/getting-started-audiencestream-enrichment.png)

次に、バッジと訪問IDと呼ばれるさらに特別な属性について学びます。