---
title: Sailthruパーソナライゼーションエンジンタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSailthruパーソナライゼーションエンジンタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sailthru-personalization-engine-tag/
---
## タグのヒント

* マッピングを使用して：
  * 標準構成値を動的に上書き
  * オプションのパーソナライゼーションエンジン構成パラメータを構成します。([詳細はこちら](https://getstarted.sailthru.com/site/personalization-engine/pe-setup/))
  * サイトにSailthruメタタグを動的に追加
  * イベントトリガーを構成（カスタムイベントを含む）
  * 必要なイベントパラメータとオプションのイベントパラメータを送信

* これらのEコマース拡張パラメータをサポート：
  * 注文ID
  * 顧客ID
  * 製品IDリスト
  * 製品名リスト
  * 製品数量リスト
  * 製品価格リスト

* 必要なイベントパラメータとオプションのイベントパラメータのリストについては、こちらのSailthruのJavaScript APIライブラリのドキュメントを参照してください：[Sailthru JavaScript APIライブラリ](https://getstarted.sailthru.com/developers/api-client/javascript/)

## タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスし、Sailthruパーソナライゼーションエンジンタグを追加します（[タグの追加方法についてはこちら]()）。

タグを追加した後、以下の構成を構成します：

* **顧客ID**
  * あなたのSailthru顧客ID。

* **ページビュートラッキング**
  * 手動ページビュートラッキングには、追跡されるページのページビューURL（`pageview.url`）へのマッピングが必要です。
  * データマッピングを使用して追加のオプションパラメータを構成します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`init.customerId`|  &lt;ul&gt;&lt;li&gt;Sailthru顧客ID&lt;/li&gt;&lt;/ul&gt; |
|`pageviewTracking`|  &lt;ul&gt;&lt;li&gt;ページビュートラッキング&lt;/li&gt;&lt;li&gt;オプションは**自動**または**手動**です。&lt;/li&gt;&lt;/ul&gt; |
|`init.isCustom`|  &lt;ul&gt;&lt;li&gt;オプションは`true`または`false`です。&lt;/li&gt;&lt;/ul&gt; |
|`init.useStoredTags`|  &lt;ul&gt;&lt;li&gt;オプションは`true`または`false`です。&lt;/li&gt;&lt;/ul&gt; |
|`init.excludeContent`|  &lt;ul&gt;&lt;li&gt;オプションは`true`または`false`です。&lt;/li&gt;&lt;/ul&gt; |
|`pageview.url`|  &lt;ul&gt;&lt;li&gt;ページビューURL&lt;/li&gt;&lt;/ul&gt; |
|`pageview.tags`|  &lt;ul&gt;&lt;li&gt;ページビュータグ&lt;/li&gt;&lt;/ul&gt; |
|`pageview.onSuccess`|  &lt;ul&gt;&lt;li&gt;コールバック関数名&lt;/li&gt;&lt;li&gt;ページビュー成功時&lt;/li&gt;&lt;/ul&gt; |
|`pageview.onError`|  &lt;ul&gt;&lt;li&gt;コールバック関数名&lt;/li&gt;&lt;li&gt;ページビュー失敗時&lt;/li&gt;&lt;/ul&gt; |
|`meta.custom`|  &lt;ul&gt;&lt;li&gt;カスタムメタタグ&lt;/li&gt;&lt;/ul&gt; |

#### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品名リスト&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品数量リスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品価格リスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |

#### イベントトリガー

|変数| 説明|
|---| ---|
|`userSignUp`|  &lt;ul&gt;&lt;li&gt;ユーザー登録&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn`|  &lt;ul&gt;&lt;li&gt;ユーザー登録オプトイン確認&lt;/li&gt;&lt;/ul&gt; |
|`addToCart`|  &lt;ul&gt;&lt;li&gt;カートに追加&lt;/li&gt;&lt;/ul&gt; |
|`purchase`|  &lt;ul&gt;&lt;li&gt;購入&lt;/li&gt;&lt;/ul&gt; |
|`customEvent`|  &lt;ul&gt;&lt;li&gt;カスタムイベント&lt;/li&gt;&lt;/ul&gt; |

#### イベントデータ: userSignUp

|変数| 説明|
|---| ---|
|`userSignUp.email`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;li&gt;Eコマース顧客IDを上書きします&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.key`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーIDタイプ&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.lists`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;リスト&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.vars`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;変数&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.source`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;獲得ソース&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.onSuccess`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;成功時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |
|`userSignUp.onError`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エラー時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |

#### イベントデータ: userSignUpConfirmedOptIn

|変数| 説明|
|---| ---|
|`userSignUpConfirmedOptIn.email`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;li&gt;Eコマース顧客IDを上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.key`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーIDタイプ&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.template_name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;オプトインテンプレート名&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.template_vars`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;オプトインテンプレート変数&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.vars`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;変数&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.source`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;獲得ソース&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.onSuccess`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;成功時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |
|`userSignUpConfirmedOptIn.onError`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エラー時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |

#### イベントデータ: addToCart

|変数| 説明|
|---| ---|
|`addToCart.email`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;li&gt;Eコマース顧客IDを上書きします&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.reminder_time`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;リマインダー時間&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.reminder_template`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;リマインダーテンプレート&lt;/li&gt;&lt;/ul&gt; |
|`product_url`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品URLリスト&lt;/li&gt;&lt;/ul&gt; |
|`product_images`|  &lt;ul&gt;&lt;li&gt;オブジェクトの配列&lt;/li&gt;&lt;li&gt;製品画像リスト&lt;/li&gt;&lt;/ul&gt; |
|`product_vars`|  &lt;ul&gt;&lt;li&gt;オブジェクトの配列&lt;/li&gt;&lt;li&gt;製品変数リスト&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.vars`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;変数&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.onSuccess`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;成功時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |
|`addToCart.onError`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エラー時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |

#### イベントデータ: purchase

|変数| 説明|
|---| ---|
|`purchase.email`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;li&gt;Eコマース顧客IDを上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_url`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品URLリスト&lt;/li&gt;&lt;/ul&gt; |
|`product_images`|  &lt;ul&gt;&lt;li&gt;オブジェクトの配列&lt;/li&gt;&lt;li&gt;製品画像リスト&lt;/li&gt;&lt;/ul&gt; |
|`product_vars`|  &lt;ul&gt;&lt;li&gt;オブジェクトの配列&lt;/li&gt;&lt;li&gt;製品変数リスト&lt;/li&gt;&lt;/ul&gt; |
|`purchase.vars`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;変数&lt;/li&gt;&lt;/ul&gt; |
|`purchase.onSuccess`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;成功時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |
|`purchase.onError`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エラー時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |

#### イベントデータ: customEvent

|変数| 説明|
|---| ---|
|`customEvent.name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベント名&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.email`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;li&gt;Eコマース顧客IDを上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.key`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーIDタイプ&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.vars`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;変数&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.onSuccess`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;成功時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |
|`customEvent.onError`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エラー時のコールバック関数名&lt;/li&gt;&lt;/ul&gt; |
