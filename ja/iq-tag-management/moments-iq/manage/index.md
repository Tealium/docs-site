---
title: Moments iQ エクスペリエンスの管理
description: この記事では、Moments iQ エクスペリエンスの管理方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/moments-iq/manage/
---
## 要件

* Moments iQ エクスペリエンスは、Tealium iQ プロファイルでのみ作成できます。プロファイルライブラリでは作成できません。
* アカウントで[tag marketplace policy](https://docs.tealium.com/tag-marketplace-policy/)が有効になっている場合、**Show** リストに Moments iQ Experience タグを追加する必要があります。そうしないと、タグはタグマーケットプレイスに表示されません。

## 動作方法

Moments iQ エクスペリエンスを作成するには、タグマーケットプレイスに移動し、**Tealium Moments iQ** をクリックして、**続行** をクリックします。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## 構成

### プロパティ

次の構成を構成します：

1. Moments iQ Experience タグの**タイトル**を入力します。同じタグの複数のインスタンスがある場合は、他のインスタンスと区別するために説明的なタイトルを使用します。
1. タグに関する**メモ**を入力します。

### エクスペリエンスの種類と配置

次の構成を構成します：

* **コードバージョン**: 使用する Moments iQ エクスペリエンス生成コードのバージョンを選択します。コードバージョンを変更する場合は、テンプレートも更新する必要があります。
  * **2.0**: このバージョンは、このドキュメントで説明されているすべての機能をサポートしています。
  * **1.0**: このバージョンは、エクスペリエンススタイルを構成する**スタイルシート**方法をサポートしていません。
* **エクスペリエンスタイプ**: 作成するエクスペリエンスのタイプ。
  * **モーダル**: エクスペリエンスはポップアップウィンドウとして表示されます。
  * **埋め込み**: エクスペリエンスはページに埋め込まれて表示されます。
* **エクスペリエンス配置**: モーダルウィンドウの位置。これは**モーダル**配置オプションでのみ使用されます。
* **モーダル背景の不透明度**: ページの残りの部分に適用する不透明度の強さを選択します。これにより、コンテンツがより際立ちます。
* **配置セレクタ**: エクスペリエンスを配置するページ要素を識別する CSS セレクタを選択します。要素のセレクタを決定する方法についての詳細は、[要素の CSS セレクタを決定する方法](https://support.tealiumiq.com/en/support/solutions/articles/36000363465-how-to-determine-the-css-selector-of-an-element)を参照してください。
* **エクスペリエンス位置**: **配置セレクタ**の要素に対して挿入された要素の位置。
  * **Before Begin**: ページ要素の前。
  * **After Begin**: ページ要素の内部、最初の子の前。
  * **Before End**: ページ要素の内部、最後の子の後。
  * **After End:** ページ要素の後。
  * **Replace:** ページ要素を置き換えます。
* **Z-index**: ページ上でのエクスペリエンスのzオーダー位置を上書きする値。高い値は低い値の上に積み重なります（例: "1", "2", "-1", "auto"）。

### エクスペリエンスの追跡

次の構成を構成して、エクスペリエンスの動作を制御します：

* **エクスペリエンスの抑制**: 次の条件の下で、訪問が戻ってきた場合に自動的にエクスペリエンスを抑制することができます：
  * **Never**
  * **クローズボタン選択後**
  * **回答送信後**
  * **回答送信またはクローズボタン選択後**  
  ブラウザはこの情報をローカル保存の `momentsiq_suppress` キーとして保存します。

* **トラックロード**: ページ上でエクスペリエンスが初めてロードされたときにトラッキングコールを送信するには `True` を選択します。
* **Tealium トラックタイプ**: モーダルクローズと送信アクションをトラッキングする際にトリガーされる `utag.track` コールのイベントタイプ。
  * **View**
  * **Link**

### エクスペリエンスの背景画像

エクスペリエンスに背景画像を追加するには、次の手順を完了します：

1. **画像配置**の下で、画像の背景がモーダルの左半分または右半分を埋めるかを選択します。
1. **画像位置**で、画像がエクスペリエンスウィンドウの左または右に合わせるかを選択します。
1. **画像 URL**に、httpsで保護された外部ホストされた画像へのリンクを入力します。推奨される画像サイズ：500px x 400px。ファイルは `.png`, `.jpg`, `.gif`, または `.svg` のファイル拡張子を持っている必要があります。

## フォーム

エクスペリエンスに表示されるテキストと回答を構成するために、次の手順を完了します。

次のテキストフィールドは、プレーンテキストまたは[dynamic text](#dynamic-text)に必要な演算子のみをサポートします。スタイルオプションを使用してフォーマットを調整することができます。改行、改ページ、タブ、またはHTMLは使用しないでください。

### ヘッダー

次の構成でエクスペリエンスに表示されるテキストを構成します：

* **ヘッダーテキスト**: エクスペリエンスの上部に表示されるテキスト。
* **メインテキスト**: ヘッダーテキストの下に表示されるテキスト。
* **質問テキスト**: 訪問に尋ねる質問。

### 回答

Moments iQは、訪問をサイトの適切なエクスペリエンスに導くための質問をカスタマイズするために、複数の質問形式を提供します。

次の構成で質問と回答を構成します：

* **回答タイプ**: 回答の入力タイプ。
  * **ラジオ**: 訪問は表示されたリストから1つの回答のみを選択できます。
  * **テキスト**: 訪問は1行のフィールドに回答を入力できます。
  * **チェックボックス**: 訪問は1つ以上のチェックボックスをラベル付きで選択できます。
  * **ボタン**: 訪問は表示された2つの回答のいずれかをボタンとして選択できます。
* **回答必須**: 訪問がエクスペリエンスを送信する前に回答を入力または選択することを要求するには `True` を選択します。
* **リダイレクトが新しいタブを開く**: 訪問が **リダイレクト URL** が構成された回答またはエクスペリエンスをクリックしたときに新しいタブを開くには `True` を選択します。
* **回答**: **ラジオ**、**チェックボックス**、および**ボタン**タイプの場合、各回答のラベルとオプションの**リダイレクト URL**を指定します。
  * その回答にリダイレクションが必要ない場合は、**リダイレクト URL** を空白のままにします。
  回答に**リダイレクト URL**を入力すると、一般的な**リダイレクト URL**構成は無効になります。
  * **テキスト**タイプは**回答**フィールドを無視し、**ボタン**タイプは最初の2つの回答とその**リダイレクト URL**のみを使用します。
  * **+ 追加**をクリックして、さらに回答を含めます。
* **リダイレクト URL**: 個々の回答に**リダイレクト URL**が構成されておらず、主要なボタンがクリックされたときに訪問をリダイレクトする URL。
* **プライマリボタンテキスト**: プライマリボタンのテキストラベル。デフォルト値は `Submit` です。

#### ダイナミックテキスト

**ヘッダーテキスト**、**メインテキスト**、**質問テキスト**、および**回答**パラメーターに動的テキストを作成するために変数を使用できます。変数は2つの波括弧の間に表示されます。たとえば、`{{VARIABLENAME}}`です。

変数は次のデータを使用できます：
* `utag.data` (例：`{{utag.data.customer_name}}`)
* Bオブジェクト (例：`{{b.customer_alias}}`)
* AudienceStream属性、Bオブジェクトを通じて (例：`{{b.variable_name}}`)

データが利用できない場合に表示されるフォールバック値を構成できます。フォールバック値はパイプ文字のペアの後に表示されます (例：`{{VARIABLENAME || FALLBACK}}`)。
## スタイル

Moments iQのエクスペリエンスには、カスタマイズ可能な複数のエリアがあり、それぞれに特定のスタイルプロパティがサポートされています。以下の画像は、構成可能なコンポーネントと各コンポーネントに適用可能なCSSスタイルプロパティを視覚的に参照するためのものです。このガイドを使用して、テキスト、ボタン、レイアウト、コンテナのスタイリングの外観を制御する構成フィールドを理解してください。

![](https://docs.tealium.com/images/early-access/moments-iq/moments-components.png)

このエクスペリエンスをあなたのサイトの外観に合わせて構成してください。エクスペリエンスのスタイルを構成するための以下の方法から一つを選択してください：

* **構成フィールド**：エクスペリエンスの各要素に対してスタイル構成をフォームで入力します。
* **スタイルシート**：カスケーディングスタイルシート（CSS）を使用してエクスペリエンスにスタイルを適用します。


<blockquote>
**構成フィールド** 方法を使用して行われた変更は **スタイルシート** 方法に影響を与えず、**スタイルシート** 方法を使用して行われた変更は **構成フィールド** 方法に影響を与えません。
</blockquote>


複数のMoments iQエクスペリエンスタグを持っている場合は、各エクスペリエンスタグのスタイル構成を個別に構成する必要があります。

### 手動で構成を入力する

**構成フィールド** をクリックして、フォームにスタイル構成を入力します：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **フォントファミリー** | テキストのフォントファミリー。 |  `Arial`  |
| **フォントサイズ** | テキストのフォントサイズ（`px`または`em`単位）。    |  `14px`|
| **フォントスタイル** | テキストのフォントスタイル。 | `normal`|
| **フォントウェイト** | テキストのフォントウェイト。 |  `normal`|
| **テキストカラー** | テキストの色（16進コードまたは標準色名）。  | `#1B1B1B` |

#### 外部コンテナ

エクスペリエンスの外部コンテナに対して以下の構成を行います：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **外部コンテナの背景色** | エクスペリエンスの背景色（16進コードまたは標準色名）。デフォルト値は `#FCFCFC`。 |  `#1B1B1B` |
| **外部コンテナのマージン** | 最も外側のコンテナのマージンサイズ。デフォルト値は `0`。マージン構成の詳細については、[MDN Web Docs: margin](https://developer.mozilla.org/en-US/docs/Web/CSS/margin)を参照してください。 |  `1px`|
| **外部コンテナのボーダースタイル** | エクスペリエンスの最も外側のコンテナのボーダースタイル。デフォルト値は `none`。 |   `none`|
| **外部コンテナのボーダーカラー** | エクスペリエンスの最も外側のコンテナのボーダーの色（16進コードまたは標準色名）。ボーダースタイルを `none` 以外の値に構成した場合にのみ、ボーダーカラーが表示されます。 |`Black`|
| **外部コンテナのボーダーラディウス** | エクスペリエンスの最も外側のコンテナのボーダーの半径。デフォルト値は `8px`。 |`8px`|
| **外部コンテナの幅** | 最も外側のコンテナの幅。デフォルト値は `500px`。 |`500px`|

#### 質問コンテナ

エクスペリエンスの質問コンテナに対して以下の構成を行います：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **質問コンテナのマージン** | 質問コンテナのマージンサイズ。デフォルト値は `0`。 |  `0`|
| **質問コンテナのテキストアライン** | コンテナ内の質問テキストのアラインメント方向。デフォルト値は `start`。 |  `start`|

#### 回答コンテナ

エクスペリエンスの回答コンテナに対して以下の構成を行います：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **回答コンテナのマージン** | 回答コンテナのマージンサイズ。デフォルト値は `0`。 |`0`|
| **回答コンテナのテキストアライン** | コンテナ内の回答テキストのアラインメント方向。デフォルト値は `start`。 |   `start`|
| **回答コンテナのフレックス方向** | 回答のアラインメント方向、縦（column）または横（row）。デフォルト値は `column`。 |`column`|
| **回答コンテナのアイテムアライン** | コンテナ内の回答のアラインメント方向（例：`start`, `flex-start`, `self-start`）。デフォルト値は `flex-start`。 |`flex-start`|

#### ボタンスタイル

プライマリおよびセカンダリボタンの以下の構成を行います：

| パラメータ | 説明 | 例 |
| --------  | ----------  | ------- |
| **プライマリボタンの背景色** | プライマリボタンの背景色。デフォルト値は `#1B1B1B`。 | `#1B1B1B` |
| **セカンダリボタンの背景色** | セカンダリボタンの背景色（16進コードまたは標準色名）。デフォルト値は `#1B1B1B`。**回答タイプ**が `Button`に構成されている場合にのみ、セカンダリボタンの構成が使用されます。 | `#1B1B1B` |

### CSS

**スタイルシート** をクリックして、CSS形式でスタイル構成を入力します。利用可能なすべてのパラメータとそのデフォルト値を含むサンプルCSSファイルが提供されています。

![](https://docs.tealium.com/images/early-access/moments-iq/moments_iq_css.png)

CSSの編集ガイドライン：

* `--uniqueSurveyId--` 変数は公開時に自動的にエクスペリエンスIDに置き換えられます。
* **スタイルシート** 方法から **構成フィールド** 方法に切り替えてタグを保存せずに終了した場合、**スタイルシート** の変更は破棄されます。
* CSSファイル内のクラス名を変更しないでください。

#### CSS依存のエクスペリエンス構成

スラッシュとアスタリスク（例：`/*width:800px;*/`）で囲まれたCSSプロパティはコメントアウトされています。これらは、特定の**エクスペリエンスタイプ**、**エクスペリエンス背景画像**、または**回答タイプ**の構成を使用する場合のそれらのプロパティの代替値を表します。

##### 背景画像CSS構成

コメントで始まるCSSプロパティ（`/*default for image`）は、背景画像を使用するタグに推奨される値を表します。

例えば、外部コンテナの幅のデフォルト値は500ピクセルです：

```css
.--uniqueSurveyId--_MIQ_outerContainer {
  display: flex;
  width: 500px;
  /*default for image type*/
  /*width: 800px;*/
```

しかし、**エクスペリエンス背景画像**の構成を構成する場合、幅を800ピクセルに変更することをお勧めします。800ピクセルの幅を構成する行のコメントを外し、標準の500ピクセルの幅の行をコメントアウトします：

```css
.--uniqueSurveyId--_MIQ_outerContainer {
  display: flex;
  /*width: 500px;*/
  /*default for image type*/
  width: 800px;
```

`/*default for image` コメントで先行するすべてのプロパティのインスタンスに対してCSSファイルを調整してください。

また、**画像位置**を`Right`に構成する場合、`border-radius`プロパティを代替値を使用するように更新する必要があります：

```css
.--uniqueSurveyId--_MIQ_imageNode {
  /*border-radius: 8px 0px 0px 8px;*/
  /*default for image right*/
  border-radius: 0px 8px 8px 0px;
```

##### エクスペリエンスタイプ構成

`/*default for modal*/`で始まるコメントで先行するCSSプロパティは、`Modal`タグと特定の**エクスペリエンス配置**構成のタグに推奨される値を表します。

例えば、外部コンテナの変換のデフォルト値は`translate(-50%, -50%);`です：

```css
  /*default for modal center*/
  transform: translate(-50%, -50%);
```

しかし、**エクスペリエンス配置**を`Top-center`または`Bottom-center`に構成する場合、標準値をコメントアウトして、`transform`プロパティの推奨値のコメントを外す必要があります：

```css
  /*default for modal center*/
  /*transform: translate(-50%, 0%);*/

  /*default for modal top-center, bottom-center*/
  transform: translate(-50%, 0%);
```

選択した**エクスペリエンス配置**に対して`top`, `left`, `right`, `bottom`, `transform`の値の行をコメントアウトおよびコメント解除する必要があります。
##### ボタンタイプのCSS構成

タグの**回答タイプ**を`Button`に構成する場合、`answerOptionContainer`セクションの値が記載された行のコメントを解除します：

```css
.--uniqueSurveyId--_MIQ_answerOptionContainer {
  /*ボタンタイプのデフォルト*/
  width: 100%;

  /*ボタンタイプ列のデフォルト*/
  margin-bottom: 8px;

  /*ボタンタイプ行のデフォルト*/
  margin-right: 16px;
}
```

## ルールとイベント

すべてのページでエクスペリエンスをロードするか、エクスペリエンスが表示される条件を構成します。ロードルールとイベントについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)および[イベント](https://docs.tealium.com/about-events/)を参照してください。


<blockquote>
データの衝突を避けるため、1ページに表示できるMoments iQエクスペリエンスは1つだけです。複数のエクスペリエンスがある場合は、ロードルールを構成して、一度に1つのエクスペリエンスのみがロードされるようにします。
</blockquote>


## データマッピング

拡張機能を使用して、構成で動的な値を取得するか、エクスペリエンス間でスタイリングを一貫させるための以下のマッピングを使用します：

### 基本パラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `type`  | String | エクスペリエンスのタイプ|
|  `placement`  | String | エクスペリエンスの配置|
|  `selector`  | String | 配置セレクタ|
|  `position`  | String | エクスペリエンスの位置|
|  `imagePosition` | String | 画像の位置|
|  `imageUrl` | String | 画像URL|
|  `altText` | String | 画像の代替テキスト |
|  `redirect_url`  | String | リダイレクトURL|
|  `redirect_open_tab`  | String | 新しいタブでリダイレクトを開く|
|  `zindex`  | String | Z-index|
|  `headerText`  | String | ヘッダーテキスト|
|  `mainText`  | String | メインテキスト|
|  `questionText`  | String | 質問テキスト|
|  `answerType`  | String | 回答タイプ|
|  `answers`  | Array | 回答|
|  `primaryText`  | String | プライマリボタンのテキスト|
|  `trackType` | String | Tealiumトラックタイプ |
|  `trackOnLoad` | String | ロード時のトラック |

### テキストフォーマットパラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `headerTitle.color`  | String | ヘッダーテキストの色| 
|  `headerTitle.fontFamily`  | String | ヘッダーテキストのフォントファミリー| 
|  `headerTitle.fontSize`  | String | ヘッダーテキストのフォントサイズ| 
|  `headerTitle.fontStyle`  | String | ヘッダーテキストのフォントスタイル| 
|  `headerTitle.fontWeight`  | String |  ヘッダーフォントの太さ| 
|  `mainBodyText.color`  | String | メインテキストの色| 
|  `mainBodyText.fontFamily`  | String | メインテキストのフォントファミリー| 
|  `mainBodyText.fontSize`  | String | メインテキストのフォントサイズ| 
|  `mainBodyText.fontStyle`  | String | メインテキストのフォントスタイル| 
|  `mainBodyText.fontWeight`  | String | メインテキストのフォントの太さ| 
|  `questionContainer.color`  | String | 質問テキストの色| 
|  `questionContainer.fontFamily`  | String | 質問テキストのフォントファミリー| 
|  `questionContainer.fontSize`  | String | 質問テキストのフォントサイズ| 
|  `questionContainer.fontStyle`  | String | 質問テキストのフォントスタイル| 
|  `questionContainer.fontWeight`  | String | 質問フォントの太さ| 
|  `answerContainer.color`  | String | 回答テキストの色| 
|  `answerContainer.fontFamily`  | String | 回答テキストのフォントファミリー| 
|  `answerContainer.fontSize`  | String | 回答テキストのフォントサイズ| 
|  `answerContainer.fontStyle`  | String | 回答テキストのフォントスタイル| 
|  `answerContainer.fontWeight`  | String | 回答フォントの太さ| 
|  `primaryButton.color`  | String | プライマリボタンのテキストの色| 
|  `primaryButton.fontFamily`  | String | プライマリボタンのフォントファミリー| 
|  `primaryButton.fontSize`  | String | プライマリボタンのテキストのフォントサイズ| 
|  `primaryButton.fontStyle`  | String | プライマリボタンのフォントスタイル| 
|  `primaryButton.fontWeight`  | String | プライマリボタンのフォントの太さ| 
|  `secondaryButton.color`  | String | セカンダリボタンのテキストの色| 
|  `secondaryButton.fontFamily`  | String | セカンダリボタンのフォントファミリー| 
|  `secondaryButton.fontSize`  | String | セカンダリボタンのテキストのフォントサイズ| 
|  `secondaryButton.fontStyle`  | String | セカンダリボタンのフォントスタイル| 
|  `secondaryButton.fontWeight`  | String | セカンダリボタンのフォントの太さ| 

### コンテナフォーマットパラメータ

| 変数 | 説明 |
|:---------|:------------|
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
|  `radioContainer.alignItems`  | String | ラジオ回答コンテナのアイテムの配置|
|  `radioContainer.flexDirection`  | String | ラジオ回答コンテナのフレックス方向|
|  `checkboxContainer.alignItems`  | String | チェックボックス回答コンテナのアイテムの配置|
|  `checkboxContainer.flexDirection`  | String | チェックボックス回答コンテナのフレックス方向|
|  `textFieldContainer.alignItems`  | String | テキストフィールド回答コンテナのアイテムの配置|

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
|  `textFieldContainer` |  [Object] |  テキストフィールド回答コンテナ|
|  `footerContainer` | [Object] |  フッターコンテナ|
|  `imageNode` | [Object] | 画像エレメント|

### データレイヤー変数

エクスペリエンスは自動的に以下の変数をデータレイヤータブに追加します：

```
momentsiq_id, UDO Variable
momentsiq_question1, UDO Variable
momentsiq_question1_type, UDO Variable
momentsiq_questions_answered, UDO Variable
momentsiq_answer1, UDO Variable
```

## クライアントサイドデータの永続化

訪問の回答を使用して訪問のエクスペリエンスをパーソナライズする場合、訪問の回答をPersist data values拡張クッキーで保存する必要があります。

以下の画像は、そのような拡張の例を示しています：

![](https://docs.tealium.com/images/early-access/moments-iq/manage-moments-persist-data-value.png)

詳細については、[Persist data value extension](https://docs.tealium.com/persist-data-value-extension/)を参照してください。

## サーバーサイド統合

AudienceStreamやEventStreamなどのサーバーサイド製品とMoments iQを統合する予定の場合、Tealium Collectタグを通じてデータを収集し、Tealium iQをAudienceStreamプロファイルにリンクする必要があります。

サーバーサイド属性をエンリッチするために、`momentsiq_answer1`が回答を含み、`momentsiq_id`が作成したエクスペリエンスのUIDと一致することを確認するルールを作成します。

例：

![](https://docs.tealium.com/images/early-access/moments-iq/manage-moments-audiencestream-attribute-setup.png)

また、Moments iQのルールでAudienceStream変数を活用する予定の場合、データレイヤーのエンリッチされた情報を有効にする必要があります。

詳細については、[データレイヤーのエンリッチされた情報について](https://docs.tealium.com/about-data-layer-enrichment/)および[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)を参照してください。

## 保存して公開

エクスペリエンスをテストしてリリースするには、他のタグと同じワークフローに従います。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。