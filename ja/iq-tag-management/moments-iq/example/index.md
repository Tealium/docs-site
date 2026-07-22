---
title: Moments iQ 専門知識の例
description: この記事では、訪問を専門知識評価を通じて導くMoments iQの体験の例を提供します。
url: https://docs.tealium.com/ja/iq-tag-management/moments-iq/example/
---
以下の例では、訪問の専門知識レベルを尋ねるために、電子機器のサイトに体験を組み込みます。これにより、訪問が製品ラインにどれだけ慣れているかを判断し、ホーム庭用インストールサービスや追加のアクセサリー（スピーカーケーブルや延長保証など）の提案に役立てることができます。

## 要件

この例には以下が必要です：

* Moments iQ.

## ステップ 1 タグの作成

以下の体験はホームページに表示されます。

[Create a Moments iQ experience](https://docs.tealium.com/manage-moments-iq/#create-a-moments-iq-tag) を使用して、訪問との最初のエンゲージメントにTealium Moments iQタグを追加します。以下のプロパティを構成します：

* **タイトル**: `Visitor expertise`
* **体験の配置**: `Center`
* **体験のタイプ**: `Embedded`
* **体験の位置**: `After Begin`
* **リダイレクトがタブを開く**: `False`
* **ヘッダーテキスト**: `Expertise`
* **メインテキスト**: `Help us to get to know you`
* **質問テキスト**: `What is your experience level with home theater equipment?`
* **回答タイプ**: `Radio button`
* **回答**: `Professional|Advanced|Basic|None`

**配置セレクター**には、体験をロードしたいCSSプロパティを入力します（例：`div.col-main`）。

### ロードルールの作成

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


この例では、タグUIDが `123` であると仮定します。

## ステップ 2: 回答の保存

訪問の回答を使用して訪問の体験をパーソナライズするには、訪問の回答を保存する必要があります。この例ではクライアントサイドの機能のみを使用し、訪問のWebブラウザで、Persist data values拡張機能を使用してクッキーに値を保存します：

![](https://docs.tealium.com/images/early-access/moments-iq/manage-moments-persist-data-value.png)

拡張機能が `momentsiq_submit` イベントが発生したときのみ実行されるように条件を追加してください。この場合、`momentsiq_id` が `123` と等しいかを確認します。

データはJavaScript拡張機能を通じて `b["MomentsiQExp123","momentsiq_answer1"]` または `MomentsiQExp123` クッキー変数を通じてアクセスできます。

詳細については、[Persist data value extension](https://docs.tealium.com/persist-data-value-extension/)を参照してください。

## 結果

訪問がホームページをロードすると、ホームページは `div.col-main` 要素の始まりの後に体験を埋め込みます。

![](https://docs.tealium.com/images/moments-iq/momentsiq-example-home-theater.png)