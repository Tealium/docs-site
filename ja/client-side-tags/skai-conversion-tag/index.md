---
title: Skai変換タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSkai変換タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/skai-conversion-tag/
---
## タグのヒント

* E-commerce拡張機能 (`_corder`, `_csubtotal`, `_cpromo`, `_ccurrency`)を使用します。
* 注文ID、金額、プロモーションコード、通貨は自動的に構成されます。これらの値はマッピングを作成することで上書きすることができます。
* `type`に値をマップすると、動的な変換タイプを構成できます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに行きます。タグを追加する一般的な手順については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Skai ID**
  * URLのサブドメインを指します。
  * 以下の例では値は`00`です：`//00.xg4ken.com/`
* **プロファイルトークン**
  * URLの`cid`クエリストリングパラメータに適用される長い英数字の値を指します。
* **変換タイプ**
  * この値は変換タイプを詳細に説明しており、デフォルトでは`conv`に構成されているべきです。
  * あなたのサイトで他の関連する変換タイプにこれを変更することができます。例えば、登録を追跡したい場合は、`reg`に変更し、リードの場合は`lead`に変更します。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| (`type`)|変換タイプ|
| (`val`)|注文金額|
| (`orderId`)|注文ID|
| (`promoCode`)|注文プロモーションコード|
| (`valueCurrency`)|注文通貨|

### ベンダー文書

* [Skaiガイドシリーズ](https://skai.io/reports-and-whitepapers/)
