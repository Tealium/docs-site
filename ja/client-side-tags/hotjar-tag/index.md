---
title: Hotjarタグ構成ガイド
description: この記事では、Hotjarタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/hotjar-tag/
---
## タグに関するヒント

マッピングを使用すると、標準構成値を動的に上書きできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **Hotjar ID**
  * HotjarサイトID。

* **Hotjar Snippet Version**
  * Hotjarのトラッキングコードのバージョン。

### コードからタグを追加する（任意）

コードからHotjarタグを追加するには、以下の手順を実行します。

1. Hotjarアカウントにログインします。
1. アカウントダッシュボードで、**Install code manually**をクリックします。
1. **Copy to clipboard**をクリックします。
1. Tag Managementにログインし、**Tag Management &gt; Tags**に移動します。
1. **Add Tag**をクリックします。
1. **Detect Tag from Code**をクリックします。
1. 手順3でコピーしたコードを貼り付けます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`hjid`| <ul><li>Hotjar ID</li></ul> |
| `hjsv` | <ul><li>Hotjarスニペットバージョン</li></ul> |