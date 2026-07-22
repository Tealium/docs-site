---
title: Quoraタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでQuoraタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quora-tag/
---
## タグのヒント

* マッピングを使用して：
  * 標準構成値を上書きする
  * イベントトリガーを構成する

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Quoraタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* `pixel_id`
ピクセルを一意に識別するQuoraが提供する英数字の文字列

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数   | 説明                      |
|:-----------|:---------------------------------|
| `pixel_id` | <ul><li>Quora Pixel ID</li></ul> |

### イベント

| 変数               | 説明                                      |
|:-----------------------|:-------------------------------------------------|
| `ViewContent`          | <ul><li>ページビュー</li><li>コンテンツ表示</li></ul> |
| `Generic`              | <ul><li>一般</li></ul>                        |
| `Purchase`             | <ul><li>購入</li></ul>                       |
| `GenerateLead`         | <ul><li>リード生成</li></ul>                  |
| `CompleteRegistration` | <ul><li>登録完了</li></ul>          |
| `AddPaymentInfo`       | <ul><li>支払い情報追加</li></ul>        |
| `AddToCart`            | <ul><li>カートに追加</li></ul>                    |
| `AddToWishlist`        | <ul><li>ウィッシュリストに追加</li></ul>               |
| `InitiateCheckout`     | <ul><li>チェックアウト開始</li></ul>              |
| `Search`               | <ul><li>検索</li></ul>                         |
| `Custom`               | <ul><li>カスタム</li></ul>                         |
