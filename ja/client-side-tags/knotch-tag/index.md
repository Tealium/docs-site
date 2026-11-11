---
title: Knotchタグ構成ガイド
description: この記事では、Knotchタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/knotch-tag/
---
## タグに関するヒント

* `utag.js`の最小バージョン：4.36。`utag.js`テンプレートの更新について詳しくは、ナレッジベースの記事「[utag.jsを最新バージョンに更新するためのベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)」を参照してください。
* マッピングを使用すると、標準の構成値を動的に上書きできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を行います。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数              | 説明                                                                                                                                                 |
|:------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `unit_id`         | <ul><li>KnotchユニットID。</li><li>例：`knotch_12ab3cd456ef789a0bc12345`</li></ul>                                                                      |
| `tag_type`        | <ul><li>値は`js`または`iframe`です。</li></ul>                                                                                                        |
| `target_element`  | <ul><li>Knotchウィジェットを表示する場所となる、ページ上にすでに存在する要素のDOM ID。</li></ul>                                                        |
| `widget_position` | <ul><li>ターゲット要素を基準としたKnotchウィジェットの位置。</li><li>値は`append_child`、`before`、または`after`です。</li></ul>                          |