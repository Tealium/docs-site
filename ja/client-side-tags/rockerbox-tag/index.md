---
title: Rockerboxタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでRockerboxタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rockerbox-tag/
---

Rockerboxは、デジタル企業向けの主要なアトリビューションプロバイダーです。Rockerboxは、すべてのマーケティングに対する真実の一元源を提供し、企業がすべてのマーケティングの効果を迅速に把握することを可能にします。

## タグのヒント

* マッピングを使用して：
  * 標準の構成値を上書きし、カスタムパラメーターを構成する
  * 標準とカスタムのイベントをトリガーする
  * 次のE-Commerce拡張値をサポートします：
    * 注文ID (`_corder`)
    * 収益 (`_ctotal`)
    * クーポン (`_cpromo`)
    * 製品 (`_cprod`)

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **クライアント認証**: クライアント認証ID
* **自動ページビューの許可**:

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|基本URL (`base_url`)| [文字列]|
|クライアント認証 (`client_auth`)| [文字列]|
|自動ページビュー (`automatic_pageview`)| [ブール値]|
|プッシュステートの無効化 (`disablePushState`)| [ブール値]|

### E-commerce

|変数| 説明|
|---| ---|
|外部ID (`external_id`)| [文字列/数値]|
|注文ID (`order_id`) ( `_corder`を上書き)| [文字列/数値]|
|収益 (`revenue`) ( `_ctotal`を上書き)| [文字列/数値]|
|クーポン (`coupon`) ( `_cpromo`を上書き)| [文字列]|
|製品 (`products`) ( `_cprod`を上書き)| [配列]|
|メール (`email`)| [文字列]|

### 住所

|変数| 説明|
|---| ---|
|国 (`rb_country`)| [文字列]|
|州 (`rb_state`)| [文字列]|
|市 (`rb_city`)| [文字列]|
|住所1 (`rb_address_1`)| [文字列]|
|住所2 (`rb_address_2`)| [文字列]|
|郵便番号 (`rb_zip_code`)| [文字列]|

### イベント

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|ページビュー (view)| `view`|
|購入 (`conv.purchase`)| `conv.purchase`|
|カートに追加 (`conv.add_to_cart`)| `conv.add_to_cart`|
|チェックアウトの開始 (`conv.initiate_checkout`)| `conv.initiate_checkout`|
|アカウント作成 (`conv.create_account`)| `conv.create_account`|
|メール登録 (`conv.email_signup`)| `conv.email_signup`|
|登録 (`conv.enrollment`)| `conv.enrollment`|
|サブスクリプション購入 (`conv.purchase.subscription`)| `conv.purchase.subscription`|
|一回限りの購入 (`conv.purchase.one_time`)| `conv.purchase.one_time`|
|カスタム| `custom`|

### イベント固有のパラメータ

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|ページビュー (`view`)| `view`|
|購入 (`conv.purchase`)| `conv.purchase`|
|カートに追加 (`conv.add_to_cart`)| `conv.add_to_cart`|
|チェックアウトの開始 (`conv.initiate_checkout`)| `conv.initiate_checkout`|
|アカウント作成 (`conv.create_account`)| `conv.create_account`|
|メール登録 (`conv.email_signup`)| `conv.email_signup`|
|登録 (`conv.enrollment`)| `conv.enrollment`|
|サブスクリプション購入 (`conv.purchase.subscription`)| `conv.purchase.subscription`|
|一回限りの購入 (`conv.purchase.one_time`)| `conv.purchase.one_time`|
|カスタム| `custom`|

