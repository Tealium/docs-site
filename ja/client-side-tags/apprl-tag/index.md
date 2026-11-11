---
title: APPRLタグ構成ガイド
description: この記事では、タグ管理アカウントでAPPRLタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/apprl-tag/
---## タグに関するヒント

* 注文IDが構成されている場合、注文のトラッキングは自動的に行われます。
* 以下のEコマース拡張機能の値をサポートしています。
  * 注文ID
  * 注文合計
  * 注文通貨
  * SKUのリスト
  * 数量のリスト
  * 価格のリスト

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグ構成

|変数| 説明|
|---| ---|
|`base_url`|  <ul><li>文字列</li><li>ベースURL</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>文字列</li><li>注文ID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_value`|  <ul><li>文字列</li><li>注文金額。</li><li>`_ctotal`を上書きします。</li></ul> |
|`currency`|  <ul><li>文字列</li><li>通貨。</li><li>`_ccurrency`を上書きします。</li></ul> |
|`sku`|  <ul><li>配列</li><li>SKUのリスト。</li><li>`_csku`を上書きします。</li></ul> |
|`quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |