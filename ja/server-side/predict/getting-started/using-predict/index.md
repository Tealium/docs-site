---
title: Predictの使用
description: この記事では、Tealium Predict MLのワークフロー、Predictの基本的な実装、およびデータを準備してモデルを作成するためのベストプラクティスの概要について説明します。
url: https://docs.tealium.com/ja/server-side/predict/getting-started/using-predict/
---
データ収集が有効になっているCustomer Data Platform（CDP）製品をご利用の場合は、Tealium Predictの使用を開始できます。達成しようとしている成果に対応するモデルを作成してトレーニングするのに十分なイベント量があることを確認するため、[前提条件]()を確認することをお勧めします。

![](https://docs.tealium.com/images/guides/predict/predict-workflow.png)

Predictの使用を開始するには、次の手順に従います。

1. **選択**  
予測したい訪問の行動を表す[ターゲット属性を選択](https://docs.tealium.com/decide-what-to-predict/)します。[ターゲット属性](https://docs.tealium.com/decide-what-to-predict/#target-attribute)には、CDP内の任意のバッジ属性またはブール属性を使用できます。ターゲット属性をモデリングに使用する準備ができていない場合は、[トレーニング用にデータを準備するための戦略]()を参照してください。
1. **トレーニング**  
ターゲット属性をモデリングに使用する準備ができたら、[モデルを作成]()してトレーニングを開始します。モデルを作成すると、デプロイ後にモデルの予測値を保存するための[出力属性](https://docs.tealium.com/decide-what-to-predict/#output-attributes)が自動的に作成されます。モデルのトレーニングでは、ユーザーが再訪してターゲット属性のアクションを完了する必要がある期間を定義します。
1. **確認**  
Predictの[モデルスコア]()と可視化を使用すると、モデルのパフォーマンスを確認し、モデルを[再トレーニング]()する必要があるかどうかを判断できます。
1. **デプロイ**  
モデルのパフォーマンスに満足したら、自信を持ってモデルを[デプロイ]()できます。デプロイされたモデルは、そのモデルの出力属性に[予測値](https://docs.tealium.com/deployed-model-health/)を保存します。
1. **作成**  
デプロイしたモデルでは、予測値を使用して[オーディエンスを作成]()し、訪問をより効果的にターゲティングして、ROI向上につながるパーソナライズされたエクスペリエンスを提供できます。