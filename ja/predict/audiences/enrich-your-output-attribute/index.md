---
title: Predictを使用してオーディエンスを作成する
description: この記事では、予測を使用して1つ以上のオーディエンスを作成する方法について説明します。
url: https://docs.tealium.com/ja/predict/audiences/enrich-your-output-attribute/
---
モデルがデプロイされ、予測を行っている後、一般的な次のステップは、予測を使用して1つ以上のオーディエンスを作成することです。

デプロイされたすべてのモデルで、訪問スコープの出力属性を生成します。デフォルトでは出力属性は各訪問後に持続しないため、この属性を訪問スコープにすることを検討するかもしれません。訪問スコープの出力属性を使用すると、[Visitor Lookup Tool]()や[Audience Discovery]()などの追加ツールを使用できます。

Tealium Predictによって生成された出力属性をエンリッチするには、次の手順を完了します：

1. **Predict &amp;gt; Deployed Model Dashboard**に移動します。
1. 出力属性を豊かにしたいモデルに関連付けられた**Model Details**をクリックします。
1. モデルの**Live Performance**画面で、出力属性をクリックします。  
![](/images/predict/predict-output-attribute.png)
1. **Visitor/Visit Attributes**画面で、豊かにしたい出力属性の名前をメモします。
1. **&#43; Add Attribute**をクリックします。
1. **Visitor**スコープを選択し、**Continue**をクリックします。
1. **Number**属性を選択し、**Continue**をクリックします。
1. 属性を次の構成で構成します：
      1. **Title**フィールドに、訪問スコープのNumber属性の名前を入力します。例えば、&#34;Most recent score for \{your output attribute name\}&#34;。
      1. **Type**フィールドで、**Decimal (default)**を選択します。
      1. **Add Enrichment**をクリックし、**Set Number**の豊かさを選択します。
      1. 豊かさを訪問スコープの出力属性の名前に構成します。
      1. この豊かさを各訪問の終了時に実行するように構成します。**WHEN**フィールドで**Visit ended**を選択します  
    ![](/images/predict/predict-visitor-scoped-attribute-properties.png)
1. **Finish**をクリックします。
1. プロファイルを保存し、公開します。
