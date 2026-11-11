---
title: Tealium SEO（JSON-LD）タグ構成ガイド
description: この記事では、タグ管理アカウントで Tealium SEO（JSON-LD）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tealium-seo-json-ld-tag/
---
## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **ホームページ URL**：プロトコルを含む完全なホームページ URL を入力します。
* **サイト名**：サイトまたは会社の名前を入力します。
* **検索 URL**：検索 URL を入力し、クエリ文字列の値を `search_term_string` に置き換えます。  
たとえば、検索 URL が `http://query.example.com/search?q=smartphones` の場合、`smartphones` の値を `search_term_string` に置き換えると、最終的な URL は `http://query.example.com/search?q=search_term_string` になります。
* **パンくずリストにパスを使用**：パスのパンくずリストを自動生成するかどうかを選択します。
  * **はい**（デフォルト）：パス名を使用してパンくずリストを作成します。
  * **いいえ**：データマッピングを使用してパンくずリストを作成します。

* **商品データを作成**：商品の詳細を自動的に追加するかどうかを選択します。
  * **はい**（デフォルト）：E-Commerce 拡張機能を使用して、商品ページの商品データを自動的に作成します（E-Commerce サイトに推奨）。
  * **いいえ**：商品データを追加しません。

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、サイト上でこのタグのインスタンスをいつ、どこで読み込むかを決定します。

推奨される読み込みルール：**すべてのページ**。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Tealium SEO タグの宛先変数は、データマッピングタブに組み込まれています。使用可能なカテゴリは次のとおりです。

### 標準

| **宛先名**                 | **説明**                                                                                                                                                                                        |
|:-------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| サイト名                    | 会社またはサイトの名前                                                                                                                                                                                  |
| ホームページ URL              | 完全なホームページ URL                                                                                                                                                                                |
| パンくずリスト名のリスト           | パンくずリスト名の配列                                                                                                                                                                                 |
| パンくずリスト URL のリスト        | パンくずリスト URL の配列                                                                                                                                                                              |
| カスタム JSON-LD データ         | JSON-LD オブジェクトに特定の値を構成します。`custom` をデータ名に置き換えて、カスタムデータを追加します。ドット表記によるネストをサポートします。例：`json_ld.contactPoint.@type` |

### カスタム JSON-LD データマッピングの作成方法

カスタム JSON-LD データは、データマッピングとドット表記の命名を使用して作成します。マッピングを決定するには、ページ内の最終的な JSON-LD がどのような構造になるかを把握しておく必要があります。ここでは、`contactPoint` オブジェクトを作成する例を使用します。

最終的な JSON-LD では、`contactPoint` オブジェクトは次のようになります。

```
<script type="application/ld+json">
{
  "@context" : "http://schema.org",
  "@type" : "Organization",
  "url" : "http://www.example.com",
  "contactPoint":
   {
      "@type": "ContactPoint",
      "telephone": "+1-888-555-1212",
      "contactType": "sales"
   }
}
</script>
```

タグでは、オブジェクト全体がデータマッピング内の `json_ld` という名前で表されます。そこから、最終的なオブジェクト内の各項目をドット表記で参照します。たとえば、上記の例にあるすべての値を構成するには、次のデータマッピングを作成します。

* `json_ld.@context`
* `json_ld.@type`
* `json_ld.url`

タグは、マッピングで指定したドット表記の構造に基づいて、最終的な JSON-LD 内にサブオブジェクトを作成します。上記の例にある `contactPoint` オブジェクトを作成するには、第 2 レベルに `contactPoint`、第 3 レベルに各プロパティを指定したデータマッピングを作成します。

* `json_ld.contactPoint.@type`
* `json_ld.contactPoint.telephone`
* `json_ld.contactPoint.contactType`

この例では、contactPoint の telephone プロパティに構成する電話番号が、`contact_phone` という名前のデータレイヤー変数に格納されているものとします。

1. `contact_phone` のデータマッピングを作成し、カスタム JSON-LD データの宛先を選択します。

2. `json_ld.custom` という名前をクリックして編集し、値を `json_ld.contactPoint.telephone` に変更します。

### E-Commerce

Tealium SEO タグは E-Commerce に対応しているため、デフォルトの E-Commerce 拡張機能のマッピングを自動的に使用します。通常、次の場合を除き、このカテゴリで手動マッピングを行う必要はありません。

* 拡張機能のマッピングを上書きする場合
* 必要な E-Commerce 変数が拡張機能で提供されていない場合

**商品データを作成**が `Yes` に構成されている場合は、次のマッピングを使用します。

| **宛先名**             | **説明**           |
|:---------------------|:-----------------|
| 商品名のリスト             | 商品名の配列。          |
| 商品ブランドのリスト          | 商品ブランドの配列。       |
| 商品 SKU のリスト          | 商品 SKU の配列。       |
| 価格のリスト              | 価格の配列。           |
| 商品画像 URL のリスト       | 画像 URL の配列。       |
| 商品部品番号のリスト          | 商品部品番号の配列。       |
| 商品評価値のリスト           | 商品評価の配列。         |
| 商品レビュー数のリスト         | 商品レビュー数の配列。      |
| 商品説明のリスト            | 商品説明の配列。         |
| 商品価格の通貨             | 商品通貨の配列。         |
## データマッピングを使用したカスタム JSON-LD の作成

カスタム JSON-LD データは、データマッピングとドット表記の名前を使用して作成します。マッピングを決定するには、ページ内で最終的な JSON-LD がどのような形式になるかを把握しておく必要があります。ここでは、`contactPoint` オブジェクトを作成する例を使用します。

最終的な JSON-LD では、contactPoint オブジェクトは次のようになります。

```
<script type="application/ld+json">
{
  "@context" : "http://schema.org",
  "@type" : "Organization",
  "url" : "http://www.example.com",
  "contactPoint":
   {
      "@type": "ContactPoint",
      "telephone": "+1-888-555-1212",
      "contactType": "sales"
   }
}
</script>
```

タグでは、オブジェクト全体がデータマッピング内の `json_ld` という名前で表されます。そこから、最終的なオブジェクト内の各項目をドット表記で参照します。たとえば、上記の例にあるすべての値を構成するには、次のデータマッピングを作成します。

* `json_ld.@context`
* `json_ld.@type`
* `json_ld.url`

タグは、マッピングで指定したドット表記の構造に基づいて、最終的な JSON-LD 内にサブオブジェクトを作成します。上記の例の `contactPoint` オブジェクトを作成するには、第 2 階層に `contactPoint`、第 3 階層に各プロパティを指定したデータマッピングを作成します。

* `json_ld.contactPoint.@type`
* `json_ld.contactPoint.telephone`
* `json_ld.contactPoint.contactType`

ここでは、contactPoint の telephone プロパティに構成する電話番号を保持する、`contact_phone` という名前のデータレイヤー変数があるものとします。

1. `contact_phone` のデータマッピングを作成し、送信先として **Custom JSON-LD Data** を選択します。
![](https://docs.tealium.com/images/client-side-tags/json-ld-tag-data-mapping-custom.jpg)

1. `json_ld.custom` という名前をクリックして編集し、値を `json_ld.contactPoint.telephone` に変更します。


### JavaScript を使用したカスタム JSON-LD の作成

このタグをスコープとする [JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/) を使用して、カスタム JSON オブジェクトを挿入できます。このタグでは、カスタムオブジェクトを追加するための JavaScript ユーティリティ関数 `u.injectJSONLD()` が公開されています。この関数は、オブジェクトの配列を 1 つのパラメーターとして受け取ります。

[ContactPoint スキーマ](http://schema.org/ContactPoint)を追加する例：

```
u.injectJSONLD([{
    "@context": "http://schema.org",
    "@type": "Organization",
    "url": "https://www.example.com",
    "contactPoint": [{
        "@type": "ContactPoint",
        "telephone": "+1-877-555-1212",
        "contactType": "Lead",
        "contactOption": "TollFree",
        "areaServed": "US"
    }]
}]);
```

## ベンダーのドキュメント

* [構造化データの概要](https://developers.google.com/search/docs/guides/intro-structured-data)
* [schema.org - 完全な階層](http://schema.org/docs/full.html)
* [サイト名とパンくずリストのデータ - Google Developers](https://developers.google.com/search/docs/guides/enhance-site#add-your-sites-name-logo-and-social-links)
* [商品データ - Google Developers](https://developers.google.com/search/docs/data-types/products)