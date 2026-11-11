---
title: Glassbox Detectorタグ構成ガイド
description: この記事では、タグ管理アカウントでGlassbox Detectorタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/glassbox-detector-tag/
---## タグに関するヒント

* マッピングを使用して、タグ構成を上書きまたは動的に構成します。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。


## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`src_link`| <ul><li>ソースリンク</li><li>Glassbox JavaScriptへのリンク</li></ul> |
|`data-clsconfig`| <ul><li>`data-clsconfig`には`reportURI`を含める必要があります。</li><li>追加のオプションパラメーターを含めることもできます。</li></ul> |