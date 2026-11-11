---
title: Rockerboxタグ構成ガイド
description: この記事では、タグ管理アカウントでRockerboxタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rockerbox-tag/
---

Rockerboxは、デジタル企業向けの主要なアトリビューションプロバイダーです。Rockerboxは、すべてのマーケティング活動に関する信頼できる唯一の情報源を提供し、企業があらゆるマーケティング施策の効果を迅速に把握できるようにします。

## タグに関するヒント

* マッピングを使用して、以下を実行できます。
  * 標準の構成値を上書きし、カスタムパラメータを構成する
  * 標準イベントおよびカスタムイベントをトリガーする
  * 以下のEコマース拡張機能の値をサポートする
    * 注文ID（`_corder`）
    * 収益（`_ctotal`）
    * クーポン（`_cpromo`）
    * 商品（`_cprod`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下を構成します。

* **クライアント認証**：クライアント認証ID
* **自動ページビューを許可**：

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

|変数| 説明|
|---| ---|
|ベースURL（`base_url`）| [文字列]|
|クライアント認証（`client_auth`）| [文字列]|
|自動ページビュー（`automatic_pageview`）| [真偽値]|
|プッシュステートを無効化（`disablePushState`）| [真偽値]|

### Eコマース

|変数| 説明|
|---| ---|
|外部ID（`external_id`）| [文字列／数値]|
|注文ID（`order_id`）（`_corder`を上書き）| [文字列／数値]|
|収益（`revenue`）（`_ctotal`を上書き）| [文字列／数値]|
|クーポン（`coupon`）（`_cpromo`を上書き）| [文字列]|
|商品（`products`）（`_cprod`を上書き）| [配列]|
|メールアドレス（`email`）| [文字列]|

### 住所

|変数| 説明|
|---| ---|
|国（`rb_country`）| [文字列]|
|州（`rb_state`）| [文字列]|
|市区町村（`rb_city`）| [文字列]|
|住所1（`rb_address_1`）| [文字列]|
|住所2（`rb_address_2`）| [文字列]|
|郵便番号（`rb_zip_code`）| [文字列]|

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|ページビュー（view）| `view`|
|購入（`conv.purchase`）| `conv.purchase`|
|カートに追加（`conv.add_to_cart`）| `conv.add_to_cart`|
|チェックアウト開始（`conv.initiate_checkout`）| `conv.initiate_checkout`|
|アカウント作成（`conv.create_account`）| `conv.create_account`|
|メール登録（`conv.email_signup`）| `conv.email_signup`|
|登録（`conv.enrollment`）| `conv.enrollment`|
|サブスクリプション購入（`conv.purchase.subscription`）| `conv.purchase.subscription`|
|一回限りの購入（`conv.purchase.one_time`）| `conv.purchase.one_time`|
|カスタム| `custom`|

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|ページビュー（view）| `view`|
|購入（`conv.purchase`）| `conv.purchase`|
|カートに追加（`conv.add_to_cart`）| `conv.add_to_cart`|
|チェックアウト開始（`conv.initiate_checkout`）| `conv.initiate_checkout`|
|アカウント作成（`conv.create_account`）| `conv.create_account`|
|メール登録（`conv.email_signup`）| `conv.email_signup`|
|登録（`conv.enrollment`）| `conv.enrollment`|
|サブスクリプション購入（`conv.purchase.subscription`）| `conv.purchase.subscription`|
|一回限りの購入（`conv.purchase.one_time`）| `conv.purchase.one_time`|
|カスタム| `custom`|