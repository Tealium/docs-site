---
title: iAdvizeタグ構成ガイド
description: この記事では、タグ管理アカウントでiAdvizeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/iadvize-tag/
---## タグに関するヒント

* 注文IDとカート金額が入力されると、トランザクションのトラッキングが自動的に行われます。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 注文小計（`_csubtotal`）
* CustomDataタグで追加のパラメータを渡す場合は、マッピングツールボックスにカスタム送信先を追加します。

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の項目を構成します。

* **サイトID**
  * iAdvizeのサイトID。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`sid`|  <ul><li>サイトID</li></ul> |
|`lang`|  <ul><li>言語</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文／トランザクションID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計／カート金額。</li><li>`_csubtotal`を上書きします。</li></ul> |