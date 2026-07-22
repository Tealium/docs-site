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

Moments iQのルールやダイナミックテキストの体験でAudienceStreamの変数を使用するには、以下のいずれかが必要です：

* [Data Layer Enrichment](https://docs.tealium.com/data-layer-enrichment/)が有効
* Moments API

## Moments iQについて

Moments iQは、訪問からリアルタイムで直接好み（ゼロパーティデータ）を収集する埋め込みまたはモーダル体験をウェブサイト上で作成できます。ゼロパーティデータは顧客から直接収集した情報であり、ファーストパーティデータは訪問の活動（例えば、サイトでの閲覧活動や購入）から推測される情報です。このデータを使用することで、訪問が何を望んでいるか、現在の意図、およびブランドに対してどのように見られたいかをよりよく理解できます。さらに、このデータで訪問プロファイルをエンリッチすることで、顧客とのより意味のある関係を築くために、より堅牢で正確なオーディエンスを作成できます。

以下の例は、訪問の職務機能に関する情報を収集します：

![](https://docs.tealium.com/images/moments-iq/moments-iq-example.png)

## 機能

Moments iQは以下の機能を提供します：

* **簡単なインストール**  
タグマーケットプレイスからMoments iQ Experiencesタグを追加し、質問、回答、スタイルを構成します。Moments iQの構成は、既存のJavaScriptライブラリ（`utag.js`）のインストールと一緒にバンドルされます。サイトに追加のコードは必要ありません。
* **リアルタイムデータ収集**  
組み込みのトラッキングにより、ユーザーの回答はデータレイヤーで即座に利用可能です。このデータは、ユーザー体験をパーソナライズし、訪問プロファイルを豊かにし、任意のベンダーシステムに送信するために使用できます。
* **精密なターゲティング**  
ロードルール、訪問データ、イベントリスナーを活用して、体験が表示されるタイミング、場所、対象を決定します。
* **カスタムスタイルと外観**  
シンプルな構成またはCSSを使用して、サイトのルックアンドフィールに合わせて訪問にシームレスなモーダルまたは埋め込み体験を提供します。また、体験をページの任意の場所に配置するか、スタイルのあるモーダルウィンドウでポップアップさせることができます。
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

訪問が体験を送信または閉じると、ブラウザは関連するデータを含む`utag.track`コールを送信し、タグと拡張機能が処理します。

Moments iQイベントは以下の変数を使用します：

| 変数 | タイプ | 説明 | 例 |
| -------- | ---- | ----------- | ------- |
| `tealium_event` | 文字列 | イベントには以下の値のいずれかが含まれます：<ul><li>`momentsiq_close`：訪問が通常閉じるボタンでウィンドウを閉じた場合。</li><li>`momentsiq_submit`：訪問が送信ボタンをクリックした場合、質問に回答したかどうかにかかわらず。</li></ul> | `momentsiq_close` |
| `momentsiq_question1` | 文字列 | 体験で尋ねられた質問。 | `あなたの好きな色は何ですか？` |
| `momentsiq_questions_answered` | 文字列 | この変数は訪問が体験を送信せずに閉じた場合にのみ表示されます。値は空白または訪問が閉じる前に入力または選択した選択肢またはテキストを含む場合があります。この変数を使用して不完全な値をフィルタリングし、データの汚染を避けることができます。 | `"test1"` |
| `momentsiq_question1_type` | 文字列 | 訪問がプライマリボタンをクリックした場合の質問のタイプ（`checkbox`, `text`, `radio`） | `radio` |
| `momentsiq_id` |  数値 | タグUID。 | `34` | 
| `momentsiq_answer1` | 文字列 | 訪問がプライマリボタンをクリックした場合、訪問が入力または選択した回答または回答。複数の回答はパイプ（&#124;）文字で区切られます。 | `Red` |

### 例

以下の例は、送信された回答を持つラジオボタン体験のイベントです：

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "54",
  "momentsiq_question1_type": "radio",
  "momentsiq_question1": "あなたの好きな色は何ですか？",
  "momentsiq_answer1": "Blue"
}
```

以下の例は、複数の回答が送信されたチェックボックス体験のイベントです：

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "55",
  "momentsiq_question1_type": "checkbox",
  "momentsiq_question1": "あなたの好きな色は何ですか？",
  "momentsiq_answer1": "Blue|Purple"
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

以下の例は、体験がロードされ、**Track On Load**構成の値が`True`である場合のイベントです：

```json
{
  "tealium_event" : "momentsiq_view",
  "momentsiq_id"  : "56"
}
```

Moments iQ体験の基本的な例については、[Moments iQ example](https://docs.tealium.com/moments-iq-expertise-example/)を参照してください。