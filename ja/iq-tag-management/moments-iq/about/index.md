---
title: Moments iQについて
description: このドキュメントでは、Tealiumプラットフォーム上のMoments iQについて説明します。
url: https://docs.tealium.com/ja/iq-tag-management/moments-iq/about/
---
## 要件

Moments iQには以下の製品が必要です：

* Tealium iQタグ管理

サーバーサイド製品とMoments iQを統合するには、以下が必要です：

* Tealium AudienceStreamまたはTealium EventStream
* 最新バージョンの[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)

Moments iQのルールやダイナミックテキストでAudienceStreamの変数を使用するには、以下のいずれかが必要です：

* [データレイヤーエンリッチメント](https://docs.tealium.com/data-layer-enrichment/)が有効
* Moments API

## Moments iQについて

Moments iQは、訪問からリアルタイムで好み（ゼロパーティデータ）を直接収集する埋め込みまたはモーダル体験をウェブサイト上で作成できます。ゼロパーティデータは顧客から直接収集した情報であり、ファーストパーティデータは訪問の活動（例えば、サイトでの閲覧活動や購入）から推測される情報です。このデータを使用することで、訪問が何を望んでいるか、現在の意図、およびブランドに対してどのように見られたいかをよりよく理解できます。追加のツールを必要とせずに、訪問のプロファイルにこのデータをエンリッチメントすると、より堅牢で正確なオーディエンスを作成し、ブランドとのオープンで信頼された関係を育むより意味のある方法で顧客と関わることができます。

以下の例は、訪問の職務機能に関する情報を収集します：

![](https://docs.tealium.com/images/moments-iq/moments-iq-example.png)

## 機能

Moments iQは以下の機能を提供します：

* **簡単なインストール**  
タグマーケットプレイスからMoments iQ Experiencesタグを追加し、質問、回答、スタイルを構成します。Moments iQの構成は、既存のJavaScriptライブラリ（`utag.js`）のインストールと一緒にバンドルされます。サイトに追加のコードは必要ありません。
* **リアルタイムデータ収集**  
組み込みのトラッキングにより、ユーザーの回答はデータレイヤーで即座に利用可能です。このデータは、ユーザー体験をパーソナライズし、訪問プロファイルをエンリッチメントし、任意のベンダーシステムに送信するために使用できます。
* **精密なターゲティング**  
ロードルール、訪問データ、イベントリスナーを活用して、体験が表示されるタイミング、場所、対象を決定します。
* **カスタムスタイルと外観**  
シンプルな構成またはCSSを使用して、サイトのルックアンドフィールに合わせて訪問にシームレスなモーダルまたは埋め込み体験を提供します。また、ページの任意の場所に体験を配置することも、スタイルのあるモーダルウィンドウで体験をポップアップさせることもできます。
* **複数の質問形式**  
ラジオボタン、チェックボックス、テキストボックスの回答をサポートします。
* **プライバシーバイデザイン**  
訪問の同意構成に基づいて、データは適切に収集、変換、送信されます。
* **シームレスな統合**  
イベントデータをAudienceStreamに送信して訪問プロファイルをエンリッチメントし、バッジを割り当て、オーディエンスメンバーシップを更新してコネクタをトリガーします。

## ステップ

Moments iQは、[Moments iQタグ](https://docs.tealium.com/manage-moments-iq/)の以下の画面を通じて構成されます：

* **タグ構成**：ページ上の体験の位置と外観を構成します。
* **ロードルールとイベントリスナー**：体験が表示されるタイミング、場所、対象を決定する条件を構成します。
* **データマッピング**：プロンプトのスタイルや構成を構成し、上書きするための高度な構成。

## イベント

訪問が体験を送信または閉じたとき、Moments iQは`utag.track`コールを送信します。**Track Load**が有効になっている場合、体験がロードされたときにもコールを送信します。

Moments iQイベントは以下の変数を使用します：

| 変数 | タイプ | 説明 | 例 |
| -------- | ---- | ----------- | ------- |
| `tealium_event` | 文字列 | イベントタイプ。可能な値：<ul><li>`momentsiq_close`: 訪問が体験を送信せずに閉じました。</li><li>`momentsiq_submit`: 訪問が体験を送信しました。質問に回答したかどうかにかかわらず。</li><li>`momentsiq_view`: **Track Load**が有効な間に体験がロードされました。</li></ul> | `momentsiq_close` |
| `momentsiq_question1` | 文字列 | 体験の最初の質問のテキスト。複数質問の調査の場合、タグは質問ごとに追加の変数を追加します：`momentsiq_question2`, `momentsiq_question3`など。 | `あなたの好きな色は何ですか？` |
| `momentsiq_questions_answered` | 文字列 | `momentsiq_close`イベントでのみ存在します。訪問が体験を閉じる前に回答した質問のIDのカンマ区切りリストを含みます（例：`question1,question2`）。訪問が質問に回答せずに閉じた場合は空です。この変数を使用して、訪問が体験を閉じる前に回答した質問を特定します。 | `question1,question2` |
| `momentsiq_question1_type` | 文字列 | 最初の質問の回答タイプ（`checkbox`, `text`, `radio`）。複数質問の調査の場合、タグは質問ごとに追加の変数を追加します：`momentsiq_question2_type`, `momentsiq_question3_type`など。 | `radio` |
| `momentsiq_id` | 文字列 | タグUID。 | `34` |
| `momentsiq_answer1` | 文字列 | 訪問が最初の質問に入力または選択した回答または回答。複数の回答はパイプ（&#124;）文字で区切られます。複数質問の調査の場合、タグは質問ごとに追加の変数を追加します：`momentsiq_answer2`, `momentsiq_answer3`など。 | `赤` |

### 例

以下の例は、送信された回答を持つラジオボタン体験のイベントです：

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "54",
  "momentsiq_question1_type": "radio",
  "momentsiq_question1": "あなたの好きな色は何ですか？",
  "momentsiq_answer1": "青"
}
```

以下の例は、複数の回答が送信されたチェックボックス体験のイベントです：

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "55",
  "momentsiq_question1_type": "checkbox",
  "momentsiq_question1": "あなたの好きな色は何ですか？",
  "momentsiq_answer1": "青|紫"
}
```

以下の例は、訪問が回答または送信する前に体験を閉じた場合のイベントです：

```json
{
  "tealium_event" : "momentsiq_close",
  "momentsiq_questions_answered": "",
  "momentsiq_id"  : "56"
}
```

以下の例は、訪問が3つの質問のうち最初の2つに回答してから体験を閉じた場合の`momentsiq_close`イベントを示しています：

```json
{
  "tealium_event": "momentsiq_close",
  "momentsiq_id": "72",
  "momentsiq_questions_answered": "question1,question2"
}
```

`momentsiq_questions_answered`を使用して調査の放棄を追跡します。この変数は、訪問が閉じる前に回答した質問をリストします。質問ごとの完了率を計算し、複数質問の調査で訪問がどこでドロップオフするかを特定し、部分的な回答者のオーディエンスを構築するために使用します。全体的な完了率を測定するには、オーディエンスルールまたは分析タグを使用して`momentsiq_submit`と`momentsiq_close`イベントを比較します。

以下の例は、体験がロードされ、**Track Load**構成の値が`True`である場合のイベントです：

```json
{
  "tealium_event" : "momentsiq_view",
  "momentsiq_id"  : "56"
}
```

Moments iQ体験の基本的な例については、[Moments iQの例](https://docs.tealium.com/moments-iq-expertise-example/)を参照してください。