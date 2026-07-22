---
title: Tealium SEO (JSON-LD) タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Tealium SEO (JSON-LD) タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tealium-seo-json-ld-tag/
---
## タグの構成

まず、タグマーケットプレイスにアクセスして、プロファイルに Tealium SEO タグを追加します。詳細については、[タグの管理](https://docs.tealium.com/manage-tags/#add-a-tag)を参照してください。

タグを追加した後、以下の構成を構成します：

* **ホームページ URL**: プロトコルを含む完全なホームページ URL を入力します。
* **サイト名**: あなたのサイト/会社の名前を入力します。
* **検索 URL**: 検索 URL を入力し、クエリ文字列の値を `search_term_string` に置き換えます。
  例えば、検索 URL が `http://query.example.com/search?q=smartphones` の場合、`smartphones` の値を `search_term_string` に置き換えると、最終的な URL は `http://query.example.com/search?q=search_term_string` になります。
* **パンくずリストのパス使用**: パスパンくずリストを自動生成するかどうかを選択します。
  * **はい**（デフォルト）: パス名を使用してパンくずリストを構築します。
  * **いいえ**: データマッピングを使用してパンくずリストを構築します。

* **製品データの構築**: 製品の詳細を自動的に追加するかどうかを選択します。
  * **はい**（デフォルト）: E-コマース拡張機能を使用して製品ページの製品データを自動的に構築します（E-コマースサイトに推奨）。
  * **いいえ**: 製品データを追加しません。

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをサイトのどこに、いつロードするかを決定します。

推奨されるロードルール：**全ページ**。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Tealium SEO タグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリは以下の通りです：

### 標準

| **宛先名**                 | **説明**                                                                                                               |
|:-------------------------|:---------------------------------------------------------------------------------------------------------------------|
| サイト名                  | あなたの会社またはサイト名                                                                                             |
| ホームページ URL           | 完全なホームページ URL                                                                                                |
| パンくずリストの名前のリスト   | パンくずリストの名前の配列                                                                                             |
| パンくずリストの URL のリスト  | パンくずリストの URL の配列                                                                                            |
| カスタム JSON-LD データ      | JSON-LD オブジェクト内の特定の値を構成します。`custom` をデータ名で置き換えてカスタムデータを追加します。ドット表記のネスティングに対応。例：`json_ld.contactPoint.@type` |

### カスタム JSON-LD データマッピングの作成方法

カスタム JSON-LD データはデータマッピングとドット表記の命名を使用して作成されます。最終的な JSON-LD がページ上でどのように見えるべきかを知る必要があります。`contactPoint` オブジェクトを作成する例を使用しましょう。

最終的な JSON-LD では、`contactPoint` オブジェクトは次のようになるかもしれません：

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

タグでは、最終オブジェクト全体がデータマッピングの `json_ld` 名で表されます。そこから、最終オブジェクト内の各アイテムはドット表記を使用して参照されます。上記の例からすべての値を構成するには、次のデータマッピングを作成します：

* `json_ld.@context`
* `json_ld.@type`
* `json_ld.url`

タグは、マッピングで指定したドット表記の構造に基づいて最終 JSON-LD 内でサブオブジェクトを作成します。上記の例で `contactPoint` オブジェクトを作成するには、`contactPoint` を第二レベルで、各プロパティを第三レベルでデータマッピングを作成します：

* `json_ld.contactPoint.@type`
* `json_ld.contactPoint.telephone`
* `json_ld.contactPoint.contactType`

この場合、`contact_phone` というデータレイヤー変数があり、その中に `contactPoint` の電話プロパティに構成する電話番号が含まれていると仮定しましょう。

1. `contact_phone` のためのデータマッピングを作成し、カスタム JSON-LD データ宛先を選択します。

2. `json_ld.custom` 名をクリックして編集し、値を `json_ld.contactPoint.telephone` に変更します。

### E-コマース

Tealium SEO タグは E-コマース対応しているため、デフォルトの E-コマース拡張マッピングを自動的に使用します。以下の場合を除き、手動でのマッピングは通常必要ありません：

* 拡張マッピングを上書きしたい場合
* 拡張機能で提供されていない E-コマース変数が必要な場合

**製品データの構築**が「はい」に構成されている場合、以下のマッピングを使用します。

| **宛先名**                    | **説明**                           |
|:------------------------------|:----------------------------------|
| 製品名のリスト                 | 製品名の配列。                     |
| 製品ブランドのリスト           | 製品ブランドの配列。               |
| 製品 SKU のリスト              | 製品 SKU の配列。                  |
| 価格のリスト                    | 価格の配列。                       |
| 製品画像 URL のリスト          | 画像 URL の配列。                  |
| 製品部品番号のリスト            | 製品部品番号の配列。               |
| 製品評価値のリスト              | 製品評価の配列。                   |
| 製品レビュー数のリスト          | 製品レビュー数の配列。             |
| 製品説明のリスト                | 製品説明の配列。                   |
| 製品価格通貨                    | 製品通貨の配列。                   |
## カスタムJSON-LDの作成とデータマッピング

カスタムJSON-LDデータは、データマッピングとドット表記の命名を使用して作成されます。最終的なJSON-LDがページでどのように見えるべきかを知る必要があります。例として、`contactPoint`オブジェクトの作成を使用しましょう。

最終的なJSON-LDでは、contactPointオブジェクトは次のようになります：

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

タグ内では、最終オブジェクト全体がデータマッピングの`json_ld`名で表されます。そこから、最終オブジェクト内の各項目はドット表記を使用して参照されます。例えば、上記の例からすべての値を構成するには、以下のデータマッピングを作成します：

* `json_ld.@context`
* `json_ld.@type`
* `json_ld.url`

タグは、マッピングで指定したドット表記構造に基づいて最終JSON-LD内でサブオブジェクトを作成します。上記の例で`contactPoint`オブジェクトを作成するには、`contactPoint`を第二レベル、各プロパティを第三レベルでデータマッピングを作成します：

* `json_ld.contactPoint.@type`
* `json_ld.contactPoint.telephone`
* `json_ld.contactPoint.contactType`

この場合、`contact_phone`という名前のデータレイヤー変数があり、contactPointのtelephoneプロパティ内に構成する電話番号を含んでいると仮定しましょう。

1. `contact_phone`のデータマッピングを作成し、**カスタムJSON-LDデータ**先を選択します。
![](https://docs.tealium.com/images/client-side-tags/json-ld-tag-data-mapping-custom.jpg)

1. `json_ld.custom`名をクリックして編集し、値を`json_ld.contactPoint.telephone`に変更します。


### JavaScriptを使用したカスタムJSON-LDの作成

[JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/)をこのタグにスコープした使用して、カスタムJSONオブジェクトを注入することができます。タグはカスタムオブジェクトを追加するためのJavaScriptユーティリティ関数`u.injectJSONLD()`を公開しています。これはオブジェクトの配列を1つのパラメータとして取ります。

[ContactPoint Schema](http://schema.org/ContactPoint)を追加する例：

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

* [構造化データ入門](https://developers.google.com/search/docs/guides/intro-structured-data)
* [schema.org - 完全な階層](http://schema.org/docs/full.html)
* [サイト名とパンくずリストデータ - Google Developers](https://developers.google.com/search/docs/guides/enhance-site#add-your-sites-name-logo-and-social-links)
* [製品データ - Google Developers](https://developers.google.com/search/docs/data-types/products)