---
title: ユニバーサルデータオブジェクト (utag_data)
description: ユニバーサルデータオブジェクト (`utag_data`) と、それが提供するウェブページデータの種類について学びましょう。
url: https://docs.tealium.com/ja/platforms/javascript/universal-data-object/
---
## ユニバーサルデータオブジェクト (UDO)

[データレイヤー](https://docs.tealium.com/an-introduction-to-the-data-layer/)は、Tealiumソリューションの基盤であり、すべてのデジタル資産と顧客インタラクションにわたるデータの真の定義となります。データレイヤーは、サイト全体で収集されるさまざまな[変数](https://docs.tealium.com/data-layer-variables/)と、追跡される訪問のインタラクションとイベントを含みます。

データレイヤーは、ページからデータを公開するJavaScriptオブジェクト `utag_data` としてウェブサイトに実装され、Tealiumタグに使用されます。このオブジェクトのプロパティは、ビジネスに合わせてカスタマイズされたプレーンでベンダーニュートラルな名前を使用します。

以下は `utag_data` の宣言例です：

```html
<script type="text/javascript">
  var utag_data={
      "tealium_event"  : "search",
      "page_name"      : "Search Results",
      "search_results" : "42",
      "search_keyword" : "Tealium shirt"};
</script>
```



<blockquote>
ユニバーサルタグ (`utag.js`) をロードする前に `utag_data` オブジェクト変数を定義し、値を構成します。
</blockquote>


`utag.js` がページでロードされると、`utag_data` 変数を探し、そのデータを使用して `utag.view()` で自動的にページビュートラッキングコールをトリガーします。シングルページアプリケーションを持っている場合や、手動で `utag.view()` を呼び出している場合、`utag_data` は必要ないかもしれません。

ページトラッキングオプションについて[詳しく学ぶ](https://docs.tealium.com/ja/platforms/javascript/page-tracking/)。

### 構文ガイドライン

UDOを実装する際には、エラーや実装の不一致を避けるだけでなく、JavaScriptとTealiumの標準に準拠するために、特定のガイドラインに従う必要があります。

*   **文字列値**  
すべての変数に文字列値を使用します。これには、ブール値と数値データも含まれます。
*   **引用符のエスケープ**    
すべての値を二重引用符または単一引用符で囲み、値自体に引用符が含まれている場合はエスケープします。例えば、`utag_data.page_name = 'It\'s All About the Data!';`。
*   **ブール値**   
ブール値には、`true` と `false` を表すために `"1"` と `"0"` を使用します。これは、文字列を使用してブール値を表現する最も簡単な方法です。
*   **金額値**  
すべてのドル額には文字列を使用し、すべての通貨記号とカンマを除外します。例えば、`utag_data.order_total = "1234.00";` ではなく `"$1,234.00"`。  
*   **配列値**  
すべての製品関連変数には配列値を使用します。Tealiumライブラリ、および各ベンダータグ統合は、すべての製品関連データに配列を使用するように設計されています。例えば、ID、価格、または数量。   
    `utag_data.product_id = ["P1234", "P4567", "P7890"];`
*   **余分なコードを避ける**  
UDOスクリプトブロックに余分なコードを追加しないでください。同じスクリプトブロック内の任意のコードが失敗すると、UDOが正しく定義されず、予期しないデータがベンダータグに渡される可能性があります。


## 例

### 標準ページ

以下は、ページ上に表示されるUDOの_サンプル_です。この具体的な例では、カートに2つの製品が入っている「ショッピングカート」ページに表示される可能性があるプロパティを示しています。

```html
<script type="text/javascript">
  var utag_data = {
    "tealium_event"      : "cart_add",
    "country_code"       : "US",    
    "currency_code"      : "USD",    
    "page_name"          : "Cart: View Shopping Bag",   
    "page_type"          : "cart",    
    "product_id"         : ["PROD123", "PROD456"],    
    "product_name"       : ["Red Shoes", "Black Socks"],
    "product_category"   : ["Footwear", "Apparel"],    
    "product_quantity"   : ["1", "2"],    
    "product_unit_price" : ["65.00", "4.75"],    
    "cart_total_items"   : "3",    
    "cart_subtotal"      : "74.00"};
</script>
```

必要に応じて、`utag.js` をロードする前にデータが構成される限り、宣言ブロックの外部でUDOに追加の値を更新します。`utag.js` のロード後に構成されたUDO変数は無視されます。  

```html
<script type="text/javascript">
  utag_data["page_name"] = "View Cart";
</script>
```

### ページ固有のデータ

UDOを入力する際には、現在のページタイプに関連する変数のみを含めます。これにより、ページコードの混乱が減少し、どのデータが期待されるかについての混乱がなくなります。以下は、製品や注文データなどの不要な項目を省略した検索ページUDOの例です。

```html
<script type="text/javascript">
  var utag_data={
      "page_name"      : "Search Results",
      "page_type"      : "search",
      "search_results" : "42",
      "search_keyword" : "tennis shoes"};
</script>
```


### 製品配列
製品変数は、単一の製品が構成されている場合でも配列として入力されるべきです。以下は、製品ID変数を1つの製品ID（製品詳細ページで）と3つの製品ID（ショッピングカートページなど）で構成する例です。

```javascript
// 単一の製品。例えば、製品詳細ページ
utag_data["product_id"] = ["PROD123"];

// 複数の製品。例えば、カートページ
utag_data["product_id"] = ["PROD123", "PROD456", "PROD789"];
```

### 配列の整列

すべての製品配列変数は、データの整列を確保するために同じ数の要素を持つ必要があります。この例では、各配列の最初の要素が最初の製品に対応していることに注意してください。この製品に関連するプロパティ（ID、価格、数量など）はすべて各配列の最初の要素に表示され、2番目の製品のプロパティは各配列の2番目の要素に表示され、以下同様です。

```javascript
// 製品1：
//   ID    = PROD123
//   価格 = 3.00
//   数量   = 1
//
// 製品2：
//   ID    = PROD456
//   価格 = 5.00
//   数量   = 1
//
utag_data["product_id"]       = ["PROD123", "PROD456"];
utag_data["product_price"]    = ["3.00", "5.00"];
utag_data["product_quantity"] = ["1", "1"];
```
