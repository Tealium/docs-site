---
title: Amazon Ads Serverタグ構成ガイド
description: この記事では、タグ管理アカウントでAmazon Ads Serverタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-ads-server-tag/
---
## 仕組み

Amazon Ads Serverは、ウェブサイトのコードを継続的に更新することなく、サイト上のデジタルマーケティングタグをデプロイ、管理、更新できる、セキュアで一元化されたツールです。

## タグ構成のヒント

* 次のEコマース拡張機能の値をサポートしています。
  * 注文ID
  * 商品IDのリスト
  * 商品名のリスト
  * 数量のリスト
  * 商品価格のリスト

* マッピングは、次の目的で使用します。
  * Eコマース拡張機能の値を動的に上書きする
  * Activity Paramsオブジェクトの内容を定義する
    * `act`を使用
  * Retargeting Paramsオブジェクトの内容を定義する
    * `rtp`を使用
  * Dynamic Retargeting Paramsオブジェクトの内容を定義する
    * `drtp`を使用
  * Conditional Paramsオブジェクトの内容を定義する
    * `cp`を使用
  * 動的なページとイベント
    * urlの値を構成する（`url`を上書き）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **AASタグマネージャーID**
  * 例：`123`

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
| `id` |  <ul><li>VersaTag ID</li></ul> |
|`url`|  <ul><li>URL</li></ul> |
|`mobile`|  <ul><li>モバイル</li><li>デフォルト値は`0`です。</li></ul> |
|`sync`|  <ul><li>同期</li><li>デフォルト値は`0`です。</li></ul> |
|`dispType`|  <ul><li>表示タイプ。</li><li>デフォルト値は`js`です。</li></ul> |
|`ActivityID`|  <ul><li>アクティビティID</li></ul> |
|`Session`|  <ul><li>セッション</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>`_corder`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |

### 構成可能なパラメータ

|変数| 説明|
|---| ---|
|`act.###`|  <ul><li>文字列</li><li>アクティビティパラメータ。</li></ul> |
|`rtp.###`|  <ul><li>文字列</li><li>リターゲティングパラメータ。</li></ul> |
|`drtp.###`|  <ul><li>文字列</li><li>動的リターゲティングパラメータ。</li></ul> |
|`cp.###`|  <ul><li>文字列</li><li>条件パラメータ。</li></ul> |
|`activityParams`|  <ul><li>オブジェクト</li><li>アクティビティパラメータ。</li></ul> |
|`retargetParams`|  <ul><li>オブジェクト</li><li>リターゲティングパラメータ。</li></ul> |
|`dynamicRetargetParams`|  <ul><li>オブジェクト</li><li>動的リターゲティングパラメータ。</li></ul> |
|`conditionalParams`|  <ul><li>オブジェクト</li><li>`meta charset="utf-8"`</li><li>条件パラメータ。</li></ul> |