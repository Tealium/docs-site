---
title: Namogooタグ構成ガイド
description: この記事では、タグ管理アカウントでNamogooタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/namogoo-tag/
---
Namogooは、ウェブセッションに侵入する不正な広告をブロックすることでオンライン顧客体験を向上させ、ユーザーがコンテンツに集中できる、気が散ることのないブラウジング環境を実現します。

## タグに関するヒント

* マッピングを使用すると、標準の構成値を動的に上書きできます。
* 次のEコマース拡張パラメータをサポートしています。
    * カート合計
    * 割引後の注文合計
    * クーポンコード
    * 商品数
    * 通貨

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **クライアントID**：Namogooのクライアント（アカウント）ID

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `client_Id`  | 文字列 | クライアントID。 |
| `cartTotal`  | 数値 | カート合計（`_csubtotal`を上書き）。 |
| `orderTotalBeforeDiscount`  | 数値 | 割引前の注文合計。 |
| `orderTotalAfterDiscount`  | 数値 | 割引後の注文合計（`_ctotal`を上書き）。 |
| `couponCode`  | 文字列 | クーポンコード（`_cpromo`を上書き）。 |
| `numOfItems`  | 数値 | 商品数（`_cquan`を上書き）。 |
| `currency`  | 文字列 | 通貨（`_ccurrency`を上書き）。 |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `addCartData` | カートデータを追加します。 |
| `addOrderData` | 注文データを追加します。 |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `addCartData` | カートデータを追加します。 |
| `addOrderData` | 注文データを追加します。 |