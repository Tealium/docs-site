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

まず、Tealiumのタグマーケットプレイスに移動し、Amazon Ads Serverタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、次の構成を行います：

* **AASタグマネージャーID**
  * 例：`123`

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
| `id` |  &lt;ul&gt;&lt;li&gt;VersaTag ID&lt;/li&gt;&lt;/ul&gt; |
|`url`|  &lt;ul&gt;&lt;li&gt;URL&lt;/li&gt;&lt;/ul&gt; |
|`mobile`|  &lt;ul&gt;&lt;li&gt;モバイル&lt;/li&gt;&lt;li&gt;デフォルト値は`0`。&lt;/li&gt;&lt;/ul&gt; |
|`sync`|  &lt;ul&gt;&lt;li&gt;同期&lt;/li&gt;&lt;li&gt;デフォルト値は`0`。&lt;/li&gt;&lt;/ul&gt; |
|`dispType`|  &lt;ul&gt;&lt;li&gt;表示タイプ。&lt;/li&gt;&lt;li&gt;デフォルト値は`js`。&lt;/li&gt;&lt;/ul&gt; |
|`ActivityID`|  &lt;ul&gt;&lt;li&gt;アクティビティID&lt;/li&gt;&lt;/ul&gt; |
|`Session`|  &lt;ul&gt;&lt;li&gt;セッション&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;`_corder`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書き。&lt;/li&gt;&lt;/ul&gt; |

### 構成可能なパラメータ

|変数| 説明|
|---| ---|
|`act.###`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;アクティビティパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`rtp.###`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;リターゲティングパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`drtp.###`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ダイナミックリターゲティングパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`cp.###`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;条件付きパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`activityParams`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;アクティビティパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`retargetParams`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;リターゲティングパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`dynamicRetargetParams`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;ダイナミックリターゲティングパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|`conditionalParams`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;`meta charset=&#34;utf-8&#34;`&lt;/li&gt;&lt;li&gt;条件付きパラメータ。&lt;/li&gt;&lt;/ul&gt; |
