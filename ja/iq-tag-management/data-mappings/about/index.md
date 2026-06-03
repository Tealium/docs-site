---
title: データマッピングについて
description: この記事では、データレイヤーからベンダーへデータを送信するためのタグデータマッピングの構成方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/data-mappings/about/
---
データマッピングとは、データレイヤー変数とベンダータグの間の接続です。データマッピングは、タグが受け取るデータと、行うイベントトラッキングのタイプを決定します。

例えば、タグは `pName` というパラメータにページ名を収集するかもしれませんが、データレイヤーはこの値を `page_name` という変数に保存するかもしれません。 `page_name` の値を `pName` に送信するためには、データマッピングを作成します。マッピングが構成されると、 `page_name` の値はそのタグがトリガーされたときに常にベンダーパラメータ `pName` に渡されます。

![](/images/iq-tag-management/whiteui-tiq-page-name-to-pname.png)

データマッピングはタグ構成から管理されます。サポートされるベンダーパラメータのリストはカテゴリ別に整理され、**Data Mappings** 画面で利用可能です。まず、マッピングするデータレイヤー変数を選択し、次にそれがマッピングするベンダーパラメータを選択します。

![](/images/iq-tag-management/data-mappings-select-destination.png)

## 変数マッピング

データマッピングには2つのタイプがあります：変数マッピングとカスタム値マッピングです。変数マッピングは最も一般的なタイプで、データレイヤーからの値をベンダーパラメータに渡すことができます。

## イベントマッピング

イベントマッピングは、イベント名をベンダーのイベント名に関連付ける変数マッピングです。例えば、eコマースタグは、商品の検索、商品詳細の表示、カートへの商品追加、チェックアウト、購入完了など、主要なショッピングアクションごとに特定のトラッキング機能を実行するかもしれません。

ベンダータグは、eコマースサイトに対して以下のようなトラッキングイベントを提供するかもしれません：

* `viewItem`
* `viewSearchResult`
* `addToCart`
* `viewCart`
* `completeTransaction`

同様に、データレイヤーは `tealium_event` を使用してこれらの同じイベントをトラッキングし、以下の値を使用するかもしれません：

* `product_view`
* `search`
* `cart_add`
* `cart_view`
* `purchase`

イベントマッピングは、イベント変数（ `tealium_event` ）の値をベンダーのイベント名に関連付け、対応するタグ機能をトリガーします。[イベントマッピングについて詳しく学ぶ]()。

#### 例：変数マッピング

タグベンダーは、トランザクションの通貨に一致する3文字のコードを構成するための通貨コードパラメータ `curr` を持っています。タグが複数の通貨をサポートするページで読み込まれる場合、現在の訪問に適した値に構成されるデータレイヤー変数 `site_currency` または `currency_code` を持つ可能性があります。期待される値は `USD` 、 `CAD` 、 `GBP` 、 `EUR` 、 `JPY` などです。変数マッピングは次のようになります：

![](/images/iq-tag-management/whiteui-tiq-datamapping-variables.png)

## カスタム値マッピング

カスタム値マッピングは、拡張機能やデータレイヤー変数を使用せずにマッピングで直接値を割り当てる便利な方法です。カスタム値はプレーンテキストまたはJavaScriptコードのスニペットの戻り値です。

### 例：プレーンテキストのカスタム値

タグベンダーは通貨コードのパラメータ `curr` を持っていますが、タグは常に同じ（ `CAD` など）通貨の単一の地理的地域にのみ展開されます。この場合、値がサイト全体で一定であるため、データレイヤー変数は必要ありません。期待される通貨コード `CAD` は、次のようにカスタム値マッピングとして直接構成できます：

![](/images/iq-tag-management/whiteui-tiq-datamapping-customvalue.png)

### 例：JavaScriptコードのカスタム値

カスタム値はJavaScriptコードからも返されます。このオプションは、JavaScriptの数値、ブール値、または配列値をベンダーパラメータに渡すために使用できます。高度なステートメントやインライン関数を使用することもできます。

例えば、次のJavaScriptの行は、 `hostname` が `co.uk` を含む場合はマッピングを `GB` に構成し、それ以外の場合は `USD` に構成します：

```
location.hostname.indexOf(&#34;co.uk&#34;) &gt; -1 ? &#34;GBP&#34; : &#34;USD&#34;
```

![](/images/iq-tag-management/iq-data-mappings-custom-value-jscode.jpg)

データレイヤー変数 `page_name` を参照するには、 `b` オブジェクトを使用します。例えば、 `b[&#39;page_name&#39;]` 。[bオブジェクトについて詳しく学ぶ](/ja/platforms/javascript/the-b-object/)。

## マッピングの優先順位

2つ以上の変数が同じ宛先にマッピングされている場合、例えば `page_name &gt; pageName` と `Document Title &gt; pageName` 、最後のマッピングが優先されます。データマッピングはこの優先順位を考慮して並べ替えることができます。

![](/images/iq-tag-management/whiteui-tiq-two-variabvles-mapped-to-same-destination.png)

この例では、 `page_name` と `Document Title` の両方が入力されている場合、宛先変数 `pageName` は `Document Title` からの値を受け取ります。変数が入力されている場合、最後のマッピングが優先されます。

[データマッピングの並べ替えについて詳しく学ぶ]()。

変数に値がない場合、マッピングは適用されません。
