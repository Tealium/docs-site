---
title: Medallia Digitalタグ構成ガイド
description: この記事では、タグ管理アカウントでMedallia Digitalタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/medallia-digital-tag/
---
Medalliaは、Web、モバイルWeb、アプリ内のインタラクションにおいて、25種類を超える方法でユーザーと関わることができる、美しくブランド化され、高度にターゲットを絞った対話を作成するためのカスタマーエクスペリエンス管理ツールを提供します。

## タグに関するヒント

* マッピングを使用して、標準の構成値を上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の項目を構成します。

* **WebサイトID**：サイトIDの数値。例：`https://resources.digital-cloud-west.medallia.com/{Path}/{WebSiteID}/onsite/embed.js`
* **パス**：Medallia DigitalのURLに含まれる文字列。例：`https://resources.digital-cloud-west.medallia.com/{Path}/{WebSiteID}/onsite/embed.js`

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------| ---| :------------|
| WebサイトID | 数値 | サイトIDの数値。 |
| パス | 文字列 | Medallia DigitalのURLに含まれる文字列。 |