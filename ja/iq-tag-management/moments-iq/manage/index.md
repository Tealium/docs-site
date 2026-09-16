---
title: Moments iQ エクスペリエンスの管理
description: この記事では、Moments iQ エクスペリエンスの管理方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/moments-iq/manage/
---
## 要件

* Moments iQ エクスペリエンスは、Tealium iQ プロファイルでのみ作成できます。プロファイルライブラリでは作成できません。
* アカウントで [タグマーケットプレイスポリシー](https://docs.tealium.com/tag-marketplace-policy/) を有効にしている場合は、Moments iQ Experience タグを **表示** リストに追加する必要があります。そうしないと、タグはタグマーケットプレイスに表示されません。

## 動作方法

Moments iQ エクスペリエンスを作成するには、タグマーケットプレイスにアクセスし、**Tealium Moments iQ** をクリックして、**続行** をクリックします。詳細については、[タグについて](https://docs.tealium.com/about-tags/) を参照してください。

## 構成

### プロパティ

以下の構成を構成します：

1. Moments iQ Experience タグの **タイトル** を入力します。同じタグの複数のインスタンスを持っている場合は、他のインスタンスと区別するために説明的なタイトルを使用してください。
1. タグに関する任意の **ノート** を入力します。

### エクスペリエンスの種類と配置

以下の構成を構成します：

* **コードバージョン**: 使用する Moments iQ エクスペリエンス生成コードのバージョンを選択します。コードバージョンを変更する場合は、テンプレートも更新する必要があります。
  * **2.0**: このバージョンは、このドキュメントで説明されているすべての機能をサポートしています。
  * **1.0**: このバージョンは、エクスペリエンススタイルを構成する **スタイルシート** メソッドをサポートしていません。
* **エクスペリエンスタイプ**: 作成するエクスペリエンスのタイプ。
  * **モーダル**: エクスペリエンスはポップアップウィンドウとして表示されます。
  * **埋め込み**: エクスペリエンスはページに埋め込まれて表示されます。
* **エクスペリエンス配置**: モーダルウィンドウの位置。これは **モーダル** 配置オプションでのみ使用されます。
* **モーダル背景の不透明度**: ページの残りの部分に適用する不透明度の強さを選択します。これにより、コンテンツがより際立ちます。
* **配置セレクタ**: エクスペリエンスを配置するページ要素を識別する CSS セレクタを選択します。これは **埋め込み** 配置オプションでのみ使用されます。要素のセレクタを決定する方法についての詳細は、[要素の CSS セレクタを決定する方法](https://support.tealiumiq.com/en/support/solutions/articles/36000363465-how-to-determine-the-css-selector-of-an-element) を参照してください。
* **エクスペリエンス位置**: **配置セレクタ** の要素に対して挿入された要素の位置。
  * **開始前**: ページ要素の前。
  * **開始後**: ページ要素内、最初の子の前。
  * **終了前**: ページ要素内、最後の子の後。
  * **終了後**: ページ要素の後。
  * **置換**: ページ要素を置換します。
* **Z-index**: ページ上でのエクスペリエンスのzオーダー位置を上書きする値。高い値は低い値の上に積み重なります（例: "1", "2", "-1", "auto"）。

### エクスペリエンス追跡

エクスペリエンスの動作を制御するために、以下の構成を構成します：

* **エクスペリエンスの抑制**: 条件に応じて、エクスペリエンスはリターン訪問に対して自動的に抑制されることがあります：
  * **決してない**
  * **閉じるボタンが選択された後**
  * **回答が送信された後**
  * **回答が送信されたか閉じるボタンが選択された後**  
  ブラウザはこの情報を `momentsiq_suppress` キーとしてローカル保存に保存します。訪問に対して抑制がアクティブかどうかを確認するには、ブラウザの開発者ツールを開いて **アプリケーション > ローカル保存** に移動します。値は調査 ID によってキー付けされた JSON オブジェクトです。テスト中に抑制をリセットするには、キーを削除してページをリロードします。

* **ロード追跡**: ページ上でエクスペリエンスが初めてロードされたときに追跡コールを送信するために `True` を選択します。
* **Tealium トラックタイプ**: モーダルの閉じると送信アクションを追跡する際にトリガーされる `utag.track` コールのイベントタイプ。
  * **ビュー**
  * **リンク**

### エクスペリエンスの背景画像

エクスペリエンスに背景画像を追加するために、以下の手順を完了します：

1. **画像配置** の下で、画像の背景がモーダルの左半分か右半分を埋めるかを選択します。
1. **画像位置** の下で、画像がエクスペリエンスウィンドウの左または右に合わせるかを選択します。
1. **画像 URL** の下で、https-securedで外部ホストされた画像へのリンクを入力します。推奨される画像サイズ：500px x 400px。ファイルは `.png`, `.jpg`, `.gif`, または `.svg` のファイル拡張子を持っている必要があります。

## フォーム

エクスペリエンスに表示されるテキストと回答を構成するために、以下の手順を完了します。

以下のテキストフィールドは、プレーンテキストまたは [動的テキスト](#dynamic-text) に必要な演算子のみをサポートします。必要に応じてスタイルオプションを調整してフォーマットを整えてください。改行、改ページ、タブ、またはHTMLは使用しないでください。

### ヘッダー

以下の構成で、エクスペリエンスに表示されるテキストを構成します：

* **ヘッダーテキスト**: エクスペリエンスの上部に表示されるテキスト。
* **メインテキスト**: ヘッダーテキストの下に表示されるテキスト。
* **質問テキスト**: 訪問に尋ねる質問。

### 回答

Moments iQ は、訪問をサイト上の適切なエクスペリエンスに導くための質問をカスタマイズすることができる複数の質問形式を提供します。

以下の構成で質問と回答を構成します：

* **回答タイプ**: 回答の入力タイプ。
  * **ラジオ**: 訪問は表示されたリストから単一の回答のみを選択できます。
  * **テキスト**: 訪問は単一行フィールドに回答を入力できます。
  * **チェックボックス**: 訪問はラベル付きの1つ以上のチェックボックスを選択できます。
  * **ボタン**: 訪問は2つの回答のいずれかをボタンとして表示されるものから選択できます。
* **回答必須**: 訪問がエクスペリエンスを送信する前に回答を入力または選択することを要求するために `True` を選択します。
* **リダイレクトが新しいタブを開く**: 訪問が **リダイレクト URL** が構成された回答またはエクスペリエンスをクリックしたときに新しいタブを開くために `True` を選択します。
* **回答**: **ラジオ**、**チェックボックス**、および **ボタン** タイプの場合、各回答のラベルとオプションの **リダイレクト URL** を指定します。
  * **リダイレクト URL** が必要ない場合は、その回答の **リダイレクト URL** を空にします。個々の回答の **リダイレクト URL** は、一般的な **リダイレクト URL** が空の場合にのみ適用されます。
  * **チェックボックス** 回答の場合、個々の回答の **リダイレクト URL** は無視されます。チェックボックス送信後に訪問をリダイレクトするには、一般的な **リダイレクト URL** を使用します。
  * **テキスト** 回答の場合、最初の回答は入力フィールドのプレースホルダーテキストとして使用されます。提供されている場合、最初の回答の **リダイレクト URL** は送信後に使用されます。
  * **ボタン** タイプは最初の2つの回答とその **リダイレクト URL** のみを使用します。
  * より多くの回答を含めるには、**+ 追加** をクリックします。
* **リダイレクト URL**: 個々の回答に **リダイレクト URL** が構成されておらず、主要なボタンがクリックされたときに訪問をリダイレクトする URL。
* **プライマリボタンテキスト**: プライマリボタンのテキストラベル。デフォルト値は `送信` です。

#### 動的テキスト

変数を使用して **ヘッダーテキスト**、**メインテキスト**、**質問テキスト**、および **回答** パラメータの動的テキストを作成できます。変数は2つの波括弧の間に表示されます。たとえば、`{{VARIABLENAME}}`。

変数は次のデータを使用できます：
* `utag.data`（例：`{{utag.data.customer_name}}`）
* Bオブジェクト（例：`{{b.customer_alias}}`）
* AudienceStream属性、Bオブジェクトを通じて（例：`{{b.variable_name}}`）

データが利用できない場合に表示されるフォールバック値を構成できます。フォールバック値はパイプ文字のペアの後に表示されます（例：`{{VARIABLENAME || FALLBACK}}`）。
## スタイル

Moments iQのエクスペリエンスには、カスタマイズ可能な複数のエリアがあり、それぞれに特定のスタイルプロパティを適用できます。以下の画像は、構成可能なコンポーネントと各コンポーネントに適用可能なCSSスタイルプロパティを視覚的に示しています。このガイドを使用して、テキスト、ボタン、レイアウト、コンテナのスタイリングの外観を制御する構成フィールドを理解してください。

![](https://docs.tealium.com/images/early-access/moments-iq/moments-components.png)

このエクスペリエンスをあなたのサイトの外観に合わせて構成してください。エクスペリエンスのスタイルを構成するための以下の方法のいずれかを選択してください：

* **構成フィールド**：エクスペリエンスの各要素に対してスタイル構成をフォームで入力します。
* **スタイルシート**：カスケーディングスタイルシート（CSS）を使用してエクスペリエンスにスタイルを適用します。


<blockquote>
**構成フィールド**メソッドを使用して行われた変更は**スタイルシート**メソッドに影響を与えず、**スタイルシート**メソッドを使用して行われた変更は**構成フィールド**メソッドに影響を与えません。
</blockquote>


複数のMoments iQエクスペリエンスタグを持っている場合は、各エクスペリエンスタグのスタイル構成を個別に構成する必要があります。

### 手動で構成を入力

**構成フィールド**をクリックして、フォームにスタイル構成を入力します：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **フォントファミリー** | テキストのフォントファミリー。 |  `Arial`  |
| **フォントサイズ** | テキストのフォントサイズ（`px`または`em`単位）。    |  `14px`|
| **フォントスタイル** | テキストのフォントスタイル。 | `normal`|
| **フォントウェイト** | テキストのフォントウェイト。 |  `normal`|
| **テキストカラー** | テキストの色（16進コードまたは標準色名）。  | `#1B1B1B` |

#### 外部コンテナ

エクスペリエンスの外部コンテナに対する以下の構成を構成します：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **外部コンテナの背景色** | エクスペリエンスの背景色（16進コードまたは標準色名）。デフォルト値は `#FCFCFC`。 |  `#1B1B1B` |
| **外部コンテナのマージン** | 最外部コンテナのマージンサイズ。デフォルト値は `0`。マージン構成の詳細については、[MDN Web Docs: margin](https://developer.mozilla.org/en-US/docs/Web/CSS/margin)を参照してください。 |  `1px`|
| **外部コンテナのボーダースタイル** | エクスペリエンスの最外部コンテナのボーダースタイル。デフォルト値は `none`。 |   `none`|
| **外部コンテナのボーダーカラー** | エクスペリエンスの最外部コンテナの周りのボーダーの色（16進コードまたは標準色名）。ボーダースタイルを `none`以外の値に構成した場合にのみ、ボーダーカラーが表示されます。 |`Black`|
| **外部コンテナのボーダーラディウス** | エクスペリエンスの最外部コンテナの周りのボーダーの半径。デフォルト値は `8px`。 |`8px`|
| **外部コンテナの幅** | 最外部コンテナの幅。デフォルト値は `500px`。 |`500px`|

#### 質問コンテナ

エクスペリエンスの質問コンテナに対する以下の構成を構成します：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **質問コンテナのマージン** | 質問コンテナのマージンサイズ。デフォルト値は `0`。 |  `0`|
| **質問コンテナのテキストアライン** | コンテナ内の質問テキストのアラインメント方向。デフォルト値は `start`。 |  `start`|

#### 回答コンテナ

エクスペリエンスの回答コンテナに対する以下の構成を構成します：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **回答コンテナのマージン** | 回答コンテナのマージンサイズ。デフォルト値は `0`。 |`0`|
| **回答コンテナのテキストアライン** | コンテナ内の回答テキストのアラインメント方向。デフォルト値は `start`。 |   `start`|
| **回答コンテナのフレックス方向** | 回答のアラインメント方向、縦（column）または横（row）。デフォルト値は `column`。 |`column`|
| **回答コンテナのアイテムアライン** | コンテナ内の回答のアラインメント方向（例：`start`、`flex-start`、`self-start`）。デフォルト値は `flex-start`。 |`flex-start`|

#### ボタンスタイル

プライマリおよびセカンダリボタンの以下の構成を構成します：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **プライマリボタンの背景色** | プライマリボタンの背景色。デフォルト値は `#1B1B1B`。 | `#1B1B1B` |
| **セカンダリボタンの背景色** | セカンダリボタンの背景色（16進コードまたは標準色名）。デフォルト値は `#1B1B1B`。**回答タイプ**が`Button`に構成されている場合にのみ、セカンダリボタンの構成が使用されます。 | `#1B1B1B` |

### CSS

**スタイルシート**をクリックして、CSS形式でスタイル構成を入力します。利用可能なすべてのパラメータとそのデフォルト値を含むサンプルCSSファイルが提供されています。

![](https://docs.tealium.com/images/early-access/moments-iq/moments_iq_css.png)

CSSの編集に関するガイドライン：

* `--uniqueSurveyId--`変数は、公開時に自動的にエクスペリエンスIDに置き換えられます。
* **スタイルシート**メソッドから**構成フィールド**メソッドに切り替えてタグを保存せずに終了した場合、**スタイルシート**の変更は破棄されます。
* CSSファイル内のクラス名を変更しないでください。

#### CSS依存のエクスペリエンス構成

スラッシュとアスタリスク（例：`/*width:800px;*/`）で囲まれたCSSプロパティはコメントアウトされています。これらは特定の**エクスペリエンスタイプ**、背景画像、または**回答タイプ**の構成に対する代替値を提供します。

##### 背景画像CSS構成

`/*default for image`で始まるコメントに先行するCSSプロパティは、背景画像を使用するタグに推奨される値を表します。

例えば、外部コンテナの幅のデフォルト値は500ピクセルです：

```css
.--uniqueSurveyId--_MIQ_outerContainer {
  display: flex;
  width: 500px;
  /*default for image type*/
  /*width: 800px;*/
```

しかし、**エクスペリエンス背景画像**の構成を構成する場合、幅を800ピクセルに変更することを推奨します。800ピクセルの幅を構成する行のコメントを外し、標準の500ピクセルの幅の行をコメントアウトします：

```css
.--uniqueSurveyId--_MIQ_outerContainer {
  display: flex;
  /*width: 500px;*/
  /*default for image type*/
  width: 800px;
```

`/*default for image`コメントで先行するすべてのプロパティのCSSファイルを調整してください。

また、**画像位置**を`Right`に構成する場合、`border-radius`プロパティを代替値を使用するように更新する必要があります：

```css
.--uniqueSurveyId--_MIQ_imageNode {
  /*border-radius: 8px 0px 0px 8px;*/
  /*default for image right*/
  border-radius: 0px 8px 8px 0px;
```

##### エクスペリエンスタイプ構成

`/*default for modal*/`で始まるコメントに先行するCSSプロパティは、`Modal`タグと特定の**エクスペリエンス配置**構成に推奨される値を表します。

例えば、外部コンテナの変換のデフォルト値は`translate(-50%, -50%);`です：

```css
  /*default for modal center*/
  transform: translate(-50%, -50%);
```

しかし、**エクスペリエンス配置**を`Top-center`または`Bottom-center`に構成する場合、標準値のコメントを外し、`transform`プロパティの推奨値のコメントを外す必要があります：

```css
  /*default for modal center*/
  /*transform: translate(-50%, 0%);*/

  /*default for modal top-center, bottom-center*/
  transform: translate(-50%, 0%);
```

選択した**エクスペリエンス配置**に応じて、`top`、`left`、`right`、`bottom`、`transform`の値の行のコメントを外し、コメントを入れる必要があります。

##### ボタンタイプCSS構成

タグの**回答タイプ**を`Button`に構成する場合、`answerOptionContainer`セクションの値の行のコメントを外します：

```css
.--uniqueSurveyId--_MIQ_answerOptionContainer {
  /*default for button type*/
  width: 100%;

  /*default for button type column*/
  margin-bottom: 8px;

  /*default for button type row*/
  margin-right: 16px;
}
```
## ルールとイベント

すべてのページでエクスペリエンスをロードするか、エクスペリエンスが表示される条件を構成します。ロードルールとイベントについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/) と [イベント](https://docs.tealium.com/about-events/) を参照してください。


<blockquote>
データの衝突を避けるため、1ページに表示できるMoments iQのエクスペリエンスは1つだけです。複数のエクスペリエンスがある場合は、ロードルールを構成して、一度に1つのエクスペリエンスのみがロードされるようにしてください。
</blockquote>


## マルチクエスチョン調査

単一のMoments iQタグは、連続する複数の質問を表示できます。各質問は異なる回答タイプを使用できます：ラジオ、テキスト、チェックボックス、またはボタン。訪問がエクスペリエンスを送信すると、Moments iQは各質問の変数セットを含む1つの`momentsiq_submit`イベントを送信します：`momentsiq_question1`、`momentsiq_answer1`、`momentsiq_question2`、`momentsiq_answer2`など。

ボタン回答タイプは2つの回答のみをサポートします。2つ以上の回答オプションが必要な調査では、ラジオまたはチェックボックスの回答タイプを使用してください。

次の例は、NPSスコアとオープンテキストのフォローアップを収集する2つの質問調査を示しています：

```json
{
  "tealium_event": "momentsiq_submit",
  "momentsiq_id": "72",
  "momentsiq_question1_type": "radio",
  "momentsiq_question1": "当社をお勧めする可能性はどれくらいですか？",
  "momentsiq_answer1": "非常に高い",
  "momentsiq_question2_type": "text",
  "momentsiq_question2": "スコアの主な理由は何ですか？",
  "momentsiq_answer2": "素晴らしいサポート体験"
}
```

## データマッピング

データレイヤー変数を構成パラメータにマッピングして、現在のページロードのタグの静的構成をオーバーライドできます。たとえば、データレイヤー変数`page_survey_question`を`questionText`パラメータにマッピングすることで、各ページに異なる質問を提供するために別々のタグを作成することなく、異なる質問を提供できます。このオーバーライドは`questionText`、`answers`、`answerType`、およびすべてのスタイリングパラメータに適用されます。

次のマッピングを拡張機能とともに使用して、構成値を動的に構成するか、エクスペリエンス全体でスタイリングを再利用します：

### 基本パラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `type`  | String | エクスペリエンスタイプ|
|  `placement`  | String | エクスペリエンスの配置|
|  `selector`  | String | 配置セレクタ|
|  `position`  | String | エクスペリエンスの位置|
|  `imagePosition` | String | 画像の位置|
|  `imageUrl` | String | 画像URL|
|  `altText` | String | 画像の代替テキスト |
|  `redirect_url`  | String | リダイレクトURL|
|  `redirect_open_tab`  | String | リダイレクトが新しいタブを開く|
|  `zindex`  | String | Z-index|
|  `headerText`  | String | ヘッダーテキスト|
|  `mainText`  | String | メインテキスト|
|  `questionText`  | String | 質問テキスト|
|  `answerType`  | String | 回答タイプ|
|  `answers`  | Array | 回答|
|  `primaryText`  | String | プライマリボタンテキスト|
|  `trackType` | String | Tealiumトラックタイプ |
|  `trackOnLoad` | String | ロード時のトラック |

### テキストフォーマットパラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `headerTitle.color`  | String | ヘッダーテキストの色| 
|  `headerTitle.fontFamily`  | String | ヘッダーテキストのフォントファミリー| 
|  `headerTitle.fontSize`  | String | ヘッダーテキストのフォントサイズ| 
|  `headerTitle.fontStyle`  | String | ヘッダーテキストのフォントスタイル| 
|  `headerTitle.fontWeight`  | String |  ヘッダーフォントの重さ| 
|  `mainBodyText.color`  | String | メインテキストの色| 
|  `mainBodyText.fontFamily`  | String | メインテキストのフォントファミリー| 
|  `mainBodyText.fontSize`  | String | メインテキストのフォントサイズ| 
|  `mainBodyText.fontStyle`  | String | メインテキストのフォントスタイル| 
|  `mainBodyText.fontWeight`  | String | メインテキストのフォントの重さ| 
|  `questionContainer.color`  | String | 質問テキストの色| 
|  `questionContainer.fontFamily`  | String | 質問テキストのフォントファミリー| 
|  `questionContainer.fontSize`  | String | 質問テキストのフォントサイズ| 
|  `questionContainer.fontStyle`  | String | 質問テキストのフォントスタイル| 
|  `questionContainer.fontWeight`  | String | 質問フォントの重さ| 
|  `answerContainer.color`  | String | 回答テキストの色| 
|  `answerContainer.fontFamily`  | String | 回答テキストのフォントファミリー| 
|  `answerContainer.fontSize`  | String | 回答テキストのフォントサイズ| 
|  `answerContainer.fontStyle`  | String | 回答テキストのフォントスタイル| 
|  `answerContainer.fontWeight`  | String | 回答フォントの重さ| 
|  `primaryButton.color`  | String | プライマリボタンテキストの色| 
|  `primaryButton.fontFamily`  | String | プライマリボタンのフォントファミリー| 
|  `primaryButton.fontSize`  | String | プライマリボタンテキストのフォントサイズ| 
|  `primaryButton.fontStyle`  | String | プライマリボタンのフォントスタイル| 
|  `primaryButton.fontWeight`  | String | プライマリボタンのフォントの重さ| 
|  `secondaryButton.color`  | String | セカンダリボタンテキストの色| 
|  `secondaryButton.fontFamily`  | String | セカンダリボタンのフォントファミリー| 
|  `secondaryButton.fontSize`  | String | セカンダリボタンテキストのフォントサイズ| 
|  `secondaryButton.fontStyle`  | String | セカンダリボタンのフォントスタイル| 
|  `secondaryButton.fontWeight`  | String | セカンダリボタンのフォントの重さ| 

### コンテナフォーマットパラメータ

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
|  `outerContainer.background`  | String | 外側コンテナの背景色|
|  `outerContainer.margin`  | String | 外側コンテナのマージン|
|  `outerContainer.borderStyle`  | String | 外側コンテナのボーダースタイル|
|  `outerContainer.borderColor`  | String | 外側コンテナのボーダーカラー|
|  `outerContainer.borderRadius`  | String | 外側コンテナのボーダーラディウス|
|  `outerContainer.width`  | String | 外側コンテナの幅|
|  `questionContainer.margin`  | String | 質問コンテナのマージン|
|  `questionContainer.textAlign`  | String | 質問コンテナのテキストアライン|
|  `answerContainer.margin`  | String | 回答コンテナのマージン|
|  `answerContainer.textAlign`  | String | 回答コンテナのテキストアライン|
|  `primaryButton.background`  | String | プライマリボタンの背景色|
|  `primaryButton.borderRadius`  | String | プライマリボタンのボーダーラディウス|
|  `secondaryButton.background`  | String | セカンダリボタンの背景色|
|  `secondaryButton.borderRadius`  | String | セカンダリボタンのボーダーラディウス|
|  `radioContainer.alignItems`  | String | ラジオ回答コンテナのアイテム配置|
|  `radioContainer.flexDirection`  | String | ラジオ回答コンテナのフレックス方向|
|  `checkboxContainer.alignItems`  | String | チェックボックス回答コンテナのアイテム配置|
|  `checkboxContainer.flexDirection`  | String | チェックボックス回答コンテナのフレックス方向|
|  `textFieldContainer.alignItems`  | String | テキストフィールド回答コンテナのアイテム配置|

### コンテナとテキストオブジェクト

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `headerTitle` |  [Object] |  ヘッダーテキスト|
|  `mainBodyText` | [Object] |  メインテキスト|
|  `questionContainer` | [Object] |  質問|
|  `answerContainer` |  [Object] |  回答|
|  `primaryButton` | [Object] |  プライマリボタン|
|  `secondaryButton` | [Object] |  セカンダリボタン|
|  `outerContainer` | [Object] |  外側コンテナ|
|  `radioContainer` | [Object] |  ラジオ回答コンテナ|
|  `checkboxContainer` |  [Object] |  チェックボックス回答コンテナ|
|  `textFieldContainer` | [Object] |  テキストフィールド回答コンテナ|
|  `footerContainer` | [Object] |  フッターコンテナ|
|  `imageNode` | [Object] | 画像エレメント|

### データレイヤー変数

エクスペリエンスは自動的に以下の変数をデータレイヤータブに追加します。マルチクエスチョン調査の場合、タグは`momentsiq_question{n}`、`momentsiq_question{n}_type`、および`momentsiq_answer{n}`を各質問ごとに1回追加します。ここで`n`は質問のキー番号です（例えば、`1`は`question1`のためです）。

| 変数 | タイプ |
|:---------|:-----|
| `momentsiq_id` | UDO変数 |
| `momentsiq_question{n}` | UDO変数 |
| `momentsiq_question{n}_type` | UDO変数 |
| `momentsiq_questions_answered` | UDO変数 |
| `momentsiq_answer{n}` | UDO変数 |
## クライアント側データの永続性

訪問の反応をもとに、クライアント側のツールのみを使用して訪問の体験をパーソナライズしたい場合、訪問の反応をPersist data values拡張クッキーで保存する必要があります。

以下の画像は、そのような拡張の例を示しています：

![](https://docs.tealium.com/images/early-access/moments-iq/manage-moments-persist-data-value.png)

詳細については、[Persist data value extension](https://docs.tealium.com/persist-data-value-extension/)を参照してください。

## サーバー側の統合

AudienceStreamやEventStreamなどのサーバー側製品とMoments iQを統合する予定がある場合、Tealium Collectタグを通じてデータを収集し、Tealium iQをAudienceStreamプロファイルにリンクする必要があります。

サーバー側の属性をエンリッチするために、`momentsiq_answer1`が回答を含み、`momentsiq_id`が作成した体験のUIDと一致することを確認するルールを作成します。

例：

![](https://docs.tealium.com/images/early-access/moments-iq/manage-moments-audiencestream-attribute-setup.png)

また、Moments iQのルールでAudienceStreamの変数を活用する予定がある場合、データレイヤーのエンリッチメントを有効にする必要があります。

詳細については、[About data layer enrichment](https://docs.tealium.com/about-data-layer-enrichment/)と[Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/)を参照してください。

## 保存して公開

体験をテストしてリリースするには、他のタグと同じワークフローに従ってください。詳細については、[About tags](https://docs.tealium.com/about-tags/)を参照してください。