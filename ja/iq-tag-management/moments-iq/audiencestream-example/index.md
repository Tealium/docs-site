---
title: Moments iQの専門知識とAudienceStreamの例
description: この記事では、訪問の専門知識を評価し、この情報で訪問プロファイルをエンリッチするMoments iQの体験の例を提供します。
url: https://docs.tealium.com/ja/iq-tag-management/moments-iq/audiencestream-example/
---
以下の例では、電子機器のサイトに体験を埋め込み、訪問にその専門知識レベルについて尋ねます。訪問の回答はその後、訪問プロファイルで豊かにされます。これにより、製品ラインに対する彼らの精通度を判断するのに役立ち、ホームインストールサービス、スピーカーケーブル、または延長保証などの追加サービスや製品のパーソナライズされた推薦に使用できます。

## 要件

この例には以下が必要です：

* Moments iQ。
* Tealium AudienceStream。
* 最新バージョンの [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/)。

## ステップ 1: タグを作成する

以下の体験はホームページに表示されます。

[Create a Moments iQ experience](https://docs.tealium.com/manage-moments-iq/#create-a-moments-iq-tag) を使用して、以下のプロパティを持つTealium Moments iQタグを追加することで、訪問との最初のエンゲージメントを作成します：

* **タイトル**: `訪問の専門知識`
* **体験の配置**: `中央`
* **体験のタイプ**: `埋め込み`
* **体験の位置**: `開始後`
* **リダイレクトがタブを開く**: `False`
* **ヘッダーテキスト**: `専門知識`
* **メインテキスト**: `あなたを知るためのお手伝いをしてください`
* **質問テキスト**: `ホームシアター機器に関するあなたの経験レベルは何ですか？`
* **回答タイプ**: `ラジオボタン`
* **回答**: `プロフェッショナル|上級|基本|なし`

**配置セレクター**に、体験をロードしたいCSSプロパティを入力します（例：`div.col-main`）。

### ロードルールを作成する

体験をホームページでのみロードするために、以下のルールを作成します：


[
  [
    {
      "input": "js.page_type",
      "operator": "equals (ignore case)",
      "filter": "home"
    }
  ] 
]



## ステップ 2: AudienceStream属性を作成する

体験からの値で属性をエンリッチするためにAudienceStreamを構成するには、以下のステップを使用します：

1. まだ存在しない場合、以下の属性を作成します：
    * **Customer_Expertise** は、`momentsiq_answer1`の値を保存するルールを持つ文字列訪問属性です。
1. まだ存在しない場合、以下のバッジを作成します：
    * **Beginner** は、**Customer_Expertise** 訪問属性の値が `None` であるかどうかをチェックします。
    * **Basic** は、**Customer_Expertise** 訪問属性の値が `Basic` であるかどうかをチェックします。
    * **Advanced** は、**Customer_Expertise** 訪問属性の値が `Advanced` であるかどうかをチェックします。
    * **Professional** は、**Customer_Expertise** 訪問属性の値が `Professional` であるかどうかをチェックします。

複数のMoments iQ体験が時間をかけて作成される可能性があるため、異なる体験からの `tealium_event` 値が意図した属性のみをエンリッチするようにする必要があります。

この例で作成された特定の体験のUIDと一致するかどうかを確認するために、`Customer_Expertise` 訪問属性のルールを更新します。これにより、正しい体験のみが `Customer_Expertise` 属性を更新します。

この例では、タグUIDは `123` です：

![](https://docs.tealium.com/images/early-access/moments-iq/moments-iq-expertise-conditions.png)

## 結果

訪問がホームページをロードすると、体験は `div.col-main` 要素の始まりに埋め込まれます。

![](https://docs.tealium.com/images/moments-iq/momentsiq-example-home-theater.png)

顧客が質問に答えると、その回答は訪問プロファイルに保存され、専門知識レベルに基づいてバッジが割り当てられます。