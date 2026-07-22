---
title: パス名トークナイザー拡張
description: この記事では、パス名トークナイザー拡張について説明し、使用例を提供します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/pathname-tokenizer-extension/
---
## 前提条件

* [拡張機能の仕組み]()
* [URLコンポーネントの理解](https://docs.tealium.com/about-load-rules/)

## 仕組み

パス名トークナイザー拡張は、ページ変数 `location.pathname` を使用して、URLパス名の各セクションを表す最大8つの新しいデータレイヤー変数を作成します。この拡張機能は、通常データレイヤーを更新するために必要な開発作業を減らすことができ、特にパス名が記述的なウェブサイトにとって非常に役立ちます。

以下がその仕組みです：

* 拡張機能は `location.pathname` の値を見て、スラッシュ (`/`) 文字間の各テキスト値を分離します。したがって、場所が `https://example.com/section/folder/sub-folder/page.html` の場合、拡張機能は次の値を `_pathname1` から `_pathname8` という名前の変数としてデータレイヤーに追加します：
    * `_pathname1="section"`
    * `_pathname2="folder"`
    * `_pathname3="sub-folder"`
    * `_pathname4="page.html"`
    * `_pathname5`
    * `_pathname6`
    * `_pathname7`
    * `_pathname8`
* 拡張機能は、ロードルールの前に値が利用可能であることを確認するために、Pre Loaderスコープで実行されます。
* パス名の値は、URLに基づいてページごとに変わります。

### 例

任意のウェブサイトはパス名トークナイザーを使用できますが、URLパス名に反映された論理的で一貫した構造を持つサイトがこの拡張機能から最も恩恵を受けます。この例は、パス名の値がサイトセクション、カテゴリ、サブカテゴリのサイト構造を表すeコマースの衣料品サイトに基づいています。

以下は、例のサイトに存在する可能性のあるURLの選択です：

```
ページ1 - https://example.com/apparel/
ページ2 - https://example.com/apparel/women/
ページ3 - https://example.com/apparel/women/jeans/
ページ4 - https://example.com/apparel/women/jeans/skinny-jeans/
```

パス名トークナイザー拡張が実行されると、パス名は各セグメントごとに個別の変数に分割されます。生成された `_pathname#` 変数は、各URLのパス名によってページごとに異なります。

この表は、上記の各例のURLに対して拡張機能によって生成された結果の値を示しています。これらの変数を使用して、データレイヤーでサイトの構造を表現する方法がわかります。


<blockquote>
パス名変数により意味のある名前を付けるために、[Set Data Values extension]()を使用して、パス名変数を新しい変数名、例えば `site_section` や `site_category` などにコピーします。
</blockquote>


例えば、`_pathname1` を `site_section` に、`_pathname2` を `site_category` に、`_pathname3` を `site_subcategory` に、`_pathname4` を `site_subcategory2` に、というようにコピーすることができます。

|変数| ページ1の値| ページ2の値| ページ3の値| ページ4の値|
|---| ---| ---| ---| ---|
|`_pathname1`| "apparel"| "apparel"| "apparel"| "apparel"|
|`_pathname2`| "women"| "women"| "women"|
|`_pathname3`| "jeans"| "jeans"|
|`_pathname4`| "skinny-jeans"|
|`_pathname5`|
|`_pathname6`|
|`_pathname7`|
|`_pathname8`|
