---
title: Quoraタグ構成ガイド
description: この記事では、タグ管理アカウントでQuoraタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quora-tag/
---
## タグに関するヒント

* マッピングを使用して、以下を行います。
  * 標準構成値を上書きする
  * イベントトリガーを構成する

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下を構成します。

* `pixel_id`
ピクセルを一意に識別する、Quoraから提供される英数字の文字列

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数       | 説明                             |
|:-----------|:---------------------------------|
| `pixel_id` | <ul><li>QuoraピクセルID</li></ul> |

### イベント

| 変数                    | 説明                                                   |
|:------------------------|:-------------------------------------------------------|
| `ViewContent`           | <ul><li>ページビュー</li><li>コンテンツ表示</li></ul> |
| `Generic`               | <ul><li>汎用</li></ul>                                 |
| `Purchase`              | <ul><li>購入</li></ul>                                 |
| `GenerateLead`          | <ul><li>リード生成</li></ul>                           |
| `CompleteRegistration`  | <ul><li>登録完了</li></ul>                             |
| `AddPaymentInfo`        | <ul><li>支払い情報を追加</li></ul>                     |
| `AddToCart`             | <ul><li>カートに追加</li></ul>                         |
| `AddToWishlist`         | <ul><li>欲しいものリストに追加</li></ul>               |
| `InitiateCheckout`      | <ul><li>チェックアウトを開始</li></ul>                 |
| `Search`                | <ul><li>検索</li></ul>                                 |
| `Custom`                | <ul><li>カスタム</li></ul>                             |