---
title: Qualarooタグ
description: この記事では、Qualarooタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/qualaroo-tag/
---
## タグに関するヒント

* マッピングを使用すると、標準の構成値を動的に上書きできます。
* ログインしている顧客のメールアドレス（またはその他の識別子）を送信するには、マッピングを使用してその値を`identify`に割り当てます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **JavaScriptファイルパス**：Qualaroo JavaScriptライブラリファイルへのパス。例：`s3.amazonaws.com/ki.js/12345/example.js`

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `jspath`| 文字列 | Qualaroo JavaScriptライブラリファイルへのパス。例：`s3.amazonaws.com/ki.js/12345/example.js` |
|`identify`| 文字列 | メールアドレスまたはその他の識別子パラメータ。 |