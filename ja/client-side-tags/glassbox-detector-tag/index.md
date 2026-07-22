---
title: Glassbox Detectorタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでGlassbox Detectorタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/glassbox-detector-tag/
---## タグのヒント

* マッピングを使用してタグの構成を上書きするか、動的に構成します。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。


## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`src_link`|  <ul><li>ソースリンク</li><li>Glassbox JavaScriptへのリンク</li></ul> |
|`data-clsconfig`|  <ul><li>`data-clsconfig`は`reportURI`を含む必要があります。</li><li>追加のオプションパラメータも含めることができます。</li></ul> |

