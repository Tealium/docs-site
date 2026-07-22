---
title: イベント要素セレクター
description: この記事では、イベントリスナーで使用される要素セレクターについて説明します。
url: https://docs.tealium.com/ja/iq-tag-management/events/selectors/
---
ほとんどのイベントリスナーでは、ページ上のどの要素がイベントリスナーをトリガーするかを指定する必要があります。たとえば、特定の広告バナーやボタンをクリックしたとき、または特定の埋め込みビデオを再生したときにクリックイベントを構成する場合などです。

要素ID、クラス、または複雑なセレクターで追跡する要素を指定します。

| セレクターの種類 | 例 | 説明 |
| ------------- | ------- | ----------- |
| 要素 ID    | `#email-address` | メールアドレスを収集するフォームフィールド |
| クラス         | `.form-field`| 任意のフォームフィールド |
| 複雑なセレクター | `div#feedback-form:not(.main) input[name='email']` | IDが`feedback-form`の`div`内のメールという名前のフォームフィールドで、クラスが`main`の`div`内にはない。 |
| 複数の要素 | `.btn-cart, .btn-cart span` | メイン要素とその中のクリック可能なネストされた要素のクリックを追跡します。 |


<blockquote>
イベントシステムはセレクターに`Element.matches()`メソッドを使用します。このメソッドの詳細については、[Mozilla Developer NetworkのElement.matches()](https://developer.mozilla.org/en-US/docs/Web/API/Element/matches)を参照してください。
</blockquote>


## 複数要素セレクターを使用するタイミング

時には、セレクターが有効であってもイベントがトリガーされないことがあります。これは、クリックされた要素が意図したターゲット要素の内部にネストされている場合によく発生します。

Tealiumのイベントは、ページの`<body>`にカーソルベースのイベントリスナー（`click`、`mousedown`、`mouseup`など）をアタッチします。ユーザーがページと対話すると、イベントハンドラーはクリックされた要素（`event.target`）が提供したセレクターと一致するかどうかを確認します。この動作は、セレクターに一致する要素に直接イベントをバインドするjQueryの`onHandler`拡張とは異なります。

Tealiumでクリックイベントリスナーがどのように機能するかの例を以下に示します：

```js
document.body.addEventListener("click", function(event) {
  if (event.target.matches("SELECTOR")) {
    console.log("Element clicked:", event.target.textContent);
    // Track event
  }
});
```

セレクターが外側の要素（ボタンなど）のみをターゲットにしていて、ユーザーがネストされた要素（ボタン内の`<span>`など）をクリックした場合、イベントリスナーはトリガーされません。この場合、メイン要素とそのクリック可能なネストされたコンテンツの両方を含む複数要素セレクターを使用します。

### 例 - カートに追加ボタン

「カートに追加」ボタンのクリックを追跡したいとします。そのHTMLは次のようになります：

```html
<button class="btn-cart">
  <span>Add to Cart</span>
</button>
```

セレクター`.btn-cart`だけを使用すると常に機能するわけではありません。ユーザーが`<span>`をクリックした場合、`event.target`は`<span>`であり、`<button>`ではありません。ボタンとそのネストされた要素の両方のクリックを確実に追跡するには、複数要素セレクターを使用します：

```css
.btn-cart, .btn-cart span
```

これにより、`<button>`またはその内部の`<span>`のいずれかがクリックされた場合にキャプチャされます。

### 正しいセレクターを見つけるためのヒント

動作するセレクターを見つけるには：

1. ページを開いて、追跡したい要素を右クリックします。
1. **Inspect**を選択してブラウザの開発者ツールを開きます。
1. イベントをトリガーするべき最も外側の要素を特定します。
1. ユーザーがクリックする可能性のある`<span>`、`<svg>`、`<img>`などのネストされた要素を確認します。
1. すべての可能なクリック可能なターゲットを含むセレクターを構築します。

セレクターを構築するのに役立つツールとして、[SelectorGadget](https://selectorgadget.com/)のブックマークレットやブラウザ拡張機能を使用することもできます。その方法は次のとおりです：

1. ページを読み込み、SelectorGadgetのブックマークレットまたはブラウザ拡張機能を開きます。
1. 要素のテキスト（例えば、「Add to Cart」）をクリックします。
1. 最初のセレクターが一般的すぎる場合（`<span>`など）、ボタンの他の部分をクリックしてそれを洗練させます。
1. 意図したクリック可能な部分が正しくハイライトされるまで続けます。
1. 最終的なセレクターをコピーして、イベント構成で使用します。

要素のセレクターを決定する方法についての詳細は、[How to Determine the CSS Selector of an Element](https://support.tealiumiq.com/en/support/solutions/articles/36000363465-how-to-determine-the-css-selector-of-an-element)を参照してください。