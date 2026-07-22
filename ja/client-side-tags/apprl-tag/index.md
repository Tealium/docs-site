---
title: APPRLタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAPPRLタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/apprl-tag/
---## タグのヒント

* 注文IDが入力されている場合、注文の追跡は自動的に行われます。
* 次のE-Commerce拡張値をサポートしています：
  * 注文ID
  * 注文合計
  * 注文通貨
  * SKUのリスト
  * 数量のリスト
  * 価格のリスト

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。


## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### タグ構成

|変数| 説明|
|---| ---|
|`base_url`|  <ul><li>文字列</li><li>ベースURL</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>文字列</li><li>注文ID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_value`|  <ul><li>文字列</li><li>注文価値。</li><li>`_ctotal`を上書きします。</li></ul> |
|`currency`|  <ul><li>文字列</li><li>通貨。</li><li>`_ccurrency`を上書きします。</li></ul> |
|`sku`|  <ul><li>配列</li><li>SKUのリスト。</li><li>`_csku`を上書きします。</li></ul> |
|`quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |

