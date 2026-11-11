---
title: Quantcast Easy Tag for Advertise セットアップガイド
description: この記事では、タグ管理アカウントで Quantcast Easy Tag for Advertise を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quantcast-easy-tag-for-advertise/
---
## タグに関するヒント

* マッピングを使用すると、以下のことが可能です。
  * アカウントの標準構成値を動的に上書きする。
  * E-Commerce 拡張機能の値を動的に上書きする。
  * `_qevents` の一部として任意の `_fp` ラベルを渡す。
  * 任意の自由形式ラベル（`mylabel`）を渡す。
  * 自由形式ラベルへの配列のマッピングは、Quantcast のドキュメントに従って処理されます。

* 次の E-Commerce 拡張機能パラメータをサポートしています。
  * 注文 ID（`_corder`）
  * 注文小計（`_csubtotal`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **アカウントコード**
  * アカウントコード（P-code）。
  * `p-` で始まる、大文字と小文字を区別する13文字の英数字コード。
  * ご不明な点がある場合は、Quantcast の担当者にお問い合わせください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`qacct`| <ul><li>アカウントコード（P-code）。</li><li>`p-` で始まる、大文字と小文字を区別する13文字の英数字コード。</li></ul> |
|`_fp.event`| <ul><li>イベント</li></ul> |
|`_fp.channel`| <ul><li>チャネル</li></ul> |
|`_fp.subchannel`| <ul><li>サブチャネル</li></ul> |
|`_fp.customer`| <ul><li>顧客</li></ul> |
|`_fp.pcat`| <ul><li>商品カテゴリー</li></ul> |
|`mylabel`| <ul><li>カスタムラベル</li></ul> |

### E-Commerce

|変数|説明|
|---|---|
|`orderid`| <ul><li>注文 ID。</li><li>E-Commerce の注文 ID を上書きします。</li></ul> |
|`revenue`| <ul><li>収益。</li><li>E-Commerce の注文小計を上書きします。</li></ul> |