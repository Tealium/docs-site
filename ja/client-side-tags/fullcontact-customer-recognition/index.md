---
title: FullContact 顧客認識タグ構成ガイド
description: この記事では、FullContact 顧客認識タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fullcontact-customer-recognition/
---
FullContact は、人々とブランドの間に信頼を築く、プライバシーに配慮した ID 解決企業です。データを統合し、重要なタイミングでインサイトを適用することで、顧客一人ひとりに合わせた体験の創出に必要な機能を提供します。

## タグに関するヒント

* マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **FullContact キー**：FullContact タグ認識キー。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `fullContactKey`  | 文字列 | FullContact キー |
|  `base_url`  | 文字列 | ベース URL |
|  `forceCallback`  | ブール値 | コールバックを強制 |
|  `fc_cb`  | 関数 | FullContact コールバック |