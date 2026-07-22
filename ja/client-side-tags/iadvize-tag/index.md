---
title: iAdvizeタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでiAdvizeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/iadvize-tag/
---## タグのヒント

* 注文IDとカートの金額が入力されると、トランザクションの追跡が自動的に行われます。
* 次のeコマース拡張パラメーターをサポートしています：
  * 注文ID (`_corder`)
  * 注文の小計 (`_csubtotal`)
* CustomDataタグに追加のパラメーターを渡したい場合は、マッピングツールボックスにカスタムデスティネーションを追加します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[Tag Overview](https://docs.tealium.com/about-tags/)記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **サイトID**
  * あなたのiAdvizeサイトID。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応するデスティネーション変数にデータを送信するプロセスです。変数をタグのデスティネーションにマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### スタンダード

|変数| 説明|
|---| ---|
|`sid`|  <ul><li>サイトID</li></ul> |
|`lang`|  <ul><li>言語</li></ul> |

### E-コマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文/トランザクションID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計/カートの金額。</li><li>`_csubtotal`を上書きします。</li></ul> |

