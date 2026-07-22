---
title: モデルの再訓練
description: この記事では、モデルを評価し、予測を改善するために必要な変更を決定した後、モデルを再訓練する方法について説明します。
url: https://docs.tealium.com/ja/server-side/predict/evaluate-models/retrain-a-model/
---
## 必要な変更を決定し、再訓練の準備をする

以下のセクションをガイドとして、モデルの再訓練の準備をします。訓練済みのモデルを編集したり、含まれている属性や除外されている属性を見るには、[モデルのレビュー](https://docs.tealium.com/review-your-model/)を参照してください。

## モデルの再訓練

モデルを再訓練するには3つの方法があります：

1. **モデルダッシュボード**から、**再訓練**をクリックします。  
      ![](https://docs.tealium.com/images/predict/predictv2-retrain.png)
1. 訓練が失敗した場合、**モデル詳細**画面からモデルを再訓練できます。  
      ![](https://docs.tealium.com/images/predict/predictv2-model-details-retrain.png)
1. **訓練詳細**画面から、訓練の詳細を確認した後、再訓練を選択できます。  
      ![](https://docs.tealium.com/images/predict/predictv2-training-details-retrain.png)

モデルの再訓練を選択した後、以下の手順を完了します：

1. 必要に応じて訓練オプションを調整します。例えば：
      * 訓練日付範囲
      * 除外する属性
1. **再訓練**をクリックします。あなたのモデルは現在、_バージョン2_で、ステータスは_公開が必要_です。
1. 変更を保存し、公開します。  
あなたのモデルは現在、_バージョン2_で、ステータスは_訓練中_です。

## デプロイの準備のために再訓練結果を見る

新しいバージョンが訓練された後、[訓練済みモデルの評価](https://docs.tealium.com/evaluate-trained-models/)のガイドラインに従って再訓練の結果を確認します。必要に応じてデータとモデルのプロパティをさらに洗練します。
