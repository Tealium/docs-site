---
title: Amazon Ads Serverタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAmazon Ads Serverタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-ads-server-tag/
---
## 仕組み

Amazon Ads Serverは、サイト上のデジタルマーケティングタグをデプロイ、管理、更新するための一元化された安全なツールで、ウェブサイトのコードを継続的に更新する必要がありません。

## タグのヒント

* 次のE-Commerce拡張値をサポートしています：
  * 注文ID
  * 製品IDのリスト
  * 製品名のリスト
  * 数量のリスト
  * 製品価格のリスト

* マッピングを使用して：
  * E-Commerce拡張値を動的に上書きします
  * Activity Paramsオブジェクトの内容を定義します
    * `act`を使用
  * Retargeting Paramsオブジェクトの内容を定義します
    * `rtp`を使用
  * Dynamic Retargeting Paramsオブジェクトの内容を定義します
    * `drtp`を使用
  * Conditional Paramsオブジェクトの内容を定義します
    * `cp`を使用
  * ダイナミックページとイベント
    * urlの値を構成します（`url`を上書き）

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Amazon Ads Serverタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、次の構成を行います：

* **AASタグマネージャーID**
  * 例：`123`

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
| `id` |  <ul><li>VersaTag ID</li></ul> |
|`url`|  <ul><li>URL</li></ul> |
|`mobile`|  <ul><li>モバイル</li><li>デフォルト値は`0`。</li></ul> |
|`sync`|  <ul><li>同期</li><li>デフォルト値は`0`。</li></ul> |
|`dispType`|  <ul><li>表示タイプ。</li><li>デフォルト値は`js`。</li></ul> |
|`ActivityID`|  <ul><li>アクティビティID</li></ul> |
|`Session`|  <ul><li>セッション</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>`_corder`を上書き。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>製品IDのリスト。</li><li>`_cprod`を上書き。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname`を上書き。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書き。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書き。</li></ul> |

### 構成可能なパラメータ

|変数| 説明|
|---| ---|
|`act.###`|  <ul><li>文字列</li><li>アクティビティパラメータ。</li></ul> |
|`rtp.###`|  <ul><li>文字列</li><li>リターゲティングパラメータ。</li></ul> |
|`drtp.###`|  <ul><li>文字列</li><li>ダイナミックリターゲティングパラメータ。</li></ul> |
|`cp.###`|  <ul><li>文字列</li><li>条件付きパラメータ。</li></ul> |
|`activityParams`|  <ul><li>オブジェクト</li><li>アクティビティパラメータ。</li></ul> |
|`retargetParams`|  <ul><li>オブジェクト</li><li>リターゲティングパラメータ。</li></ul> |
|`dynamicRetargetParams`|  <ul><li>オブジェクト</li><li>ダイナミックリターゲティングパラメータ。</li></ul> |
|`conditionalParams`|  <ul><li>オブジェクト</li><li>`meta charset="utf-8"`</li><li>条件付きパラメータ。</li></ul> |
