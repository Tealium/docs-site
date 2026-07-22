---
title: Adlucentタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdlucentタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adlucent-tag/
---
## タグのヒント

* E-Commerce拡張機能を使用して以下のパラメーターを構成します：
  * 注文ID
  * 顧客ID
  * SKUのリスト
  * 数量のリスト
  * 価格のリスト
  * カテゴリのリスト

* マッピングを使用して：
  * 標準の構成値を動的に上書きします
  * E-Commerce拡張機能の値を動的に上書きします
  * 顧客タイプの値を構成します

## タグの構成

まず、タグマーケットプレイスに移動し、Adlucentタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **リテーラーID**：あなたのAdlucentリテーラーID。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数                            | 説明             |
|:--------------------------------|:-----------------|
| リテーラーID                     | (`retailer`)     |
| 顧客ID                          | (`customerID`)   |
| 顧客タイプ                      | (`customerType`) |
| 注文ID                          | (`orderKey`)     |
| SKUのリスト (`sku`)             | [配列]           |
| 数量のリスト (`qty`)            | [配列]           |
| 価格のリスト (`price`)          | [配列]           |
| カテゴリのリスト (`category`)   | [配列]           |
