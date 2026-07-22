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

まず、Tealiumのタグマーケットプレイスにアクセスし、Sailthruパーソナライゼーションエンジンタグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)）。

タグを追加した後、以下の構成を構成します：

* **顧客ID**
  * あなたのSailthru顧客ID。

* **ページビュートラッキング**
  * 手動ページビュートラッキングには、追跡されるページのページビューURL（`pageview.url`）へのマッピングが必要です。
  * データマッピングを使用して追加のオプションパラメータを構成します。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`init.customerId`|  <ul><li>Sailthru顧客ID</li></ul> |
|`pageviewTracking`|  <ul><li>ページビュートラッキング</li><li>オプションは**自動**または**手動**です。</li></ul> |
|`init.isCustom`|  <ul><li>オプションは`true`または`false`です。</li></ul> |
|`init.useStoredTags`|  <ul><li>オプションは`true`または`false`です。</li></ul> |
|`init.excludeContent`|  <ul><li>オプションは`true`または`false`です。</li></ul> |
|`pageview.url`|  <ul><li>ページビューURL</li></ul> |
|`pageview.tags`|  <ul><li>ページビュータグ</li></ul> |
|`pageview.onSuccess`|  <ul><li>コールバック関数名</li><li>ページビュー成功時</li></ul> |
|`pageview.onError`|  <ul><li>コールバック関数名</li><li>ページビュー失敗時</li></ul> |
|`meta.custom`|  <ul><li>カスタムメタタグ</li></ul> |

#### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>製品IDリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>製品名リスト</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>製品数量リスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>製品価格リスト</li><li>`_cprice`を上書きします。</li></ul> |

#### イベントトリガー

|変数| 説明|
|---| ---|
|`userSignUp`|  <ul><li>ユーザー登録</li></ul> |
|`userSignUpConfirmedOptIn`|  <ul><li>ユーザー登録オプトイン確認</li></ul> |
|`addToCart`|  <ul><li>カートに追加</li></ul> |
|`purchase`|  <ul><li>購入</li></ul> |
|`customEvent`|  <ul><li>カスタムイベント</li></ul> |

#### イベントデータ: userSignUp

|変数| 説明|
|---| ---|
|`userSignUp.email`|  <ul><li>文字列</li><li>ユーザーのメール</li><li>Eコマース顧客IDを上書きします</li></ul> |
|`userSignUp.id`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`userSignUp.key`|  <ul><li>文字列</li><li>ユーザーIDタイプ</li></ul> |
|`userSignUp.lists`|  <ul><li>オブジェクト</li><li>リスト</li></ul> |
|`userSignUp.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`userSignUp.source`|  <ul><li>文字列</li><li>獲得ソース</li></ul> |
|`userSignUp.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`userSignUp.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ: userSignUpConfirmedOptIn

|変数| 説明|
|---| ---|
|`userSignUpConfirmedOptIn.email`|  <ul><li>文字列</li><li>ユーザーのメール</li><li>Eコマース顧客IDを上書きします。</li></ul> |
|`userSignUpConfirmedOptIn.id`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`userSignUpConfirmedOptIn.key`|  <ul><li>文字列</li><li>ユーザーIDタイプ</li></ul> |
|`userSignUpConfirmedOptIn.template_name`|  <ul><li>文字列</li><li>オプトインテンプレート名</li></ul> |
|`userSignUpConfirmedOptIn.template_vars`|  <ul><li>オブジェクト</li><li>オプトインテンプレート変数</li></ul> |
|`userSignUpConfirmedOptIn.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`userSignUpConfirmedOptIn.source`|  <ul><li>文字列</li><li>獲得ソース</li></ul> |
|`userSignUpConfirmedOptIn.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`userSignUpConfirmedOptIn.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ: addToCart

|変数| 説明|
|---| ---|
|`addToCart.email`|  <ul><li>文字列</li><li>ユーザーのメール</li><li>Eコマース顧客IDを上書きします</li></ul> |
|`addToCart.reminder_time`|  <ul><li>文字列</li><li>リマインダー時間</li></ul> |
|`addToCart.reminder_template`|  <ul><li>文字列</li><li>リマインダーテンプレート</li></ul> |
|`product_url`|  <ul><li>配列</li><li>製品URLリスト</li></ul> |
|`product_images`|  <ul><li>オブジェクトの配列</li><li>製品画像リスト</li></ul> |
|`product_vars`|  <ul><li>オブジェクトの配列</li><li>製品変数リスト</li></ul> |
|`addToCart.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`addToCart.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`addToCart.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ: purchase

|変数| 説明|
|---| ---|
|`purchase.email`|  <ul><li>文字列</li><li>ユーザーのメール</li><li>Eコマース顧客IDを上書きします。</li></ul> |
|`product_url`|  <ul><li>配列</li><li>製品URLリスト</li></ul> |
|`product_images`|  <ul><li>オブジェクトの配列</li><li>製品画像リスト</li></ul> |
|`product_vars`|  <ul><li>オブジェクトの配列</li><li>製品変数リスト</li></ul> |
|`purchase.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`purchase.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`purchase.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ: customEvent

|変数| 説明|
|---| ---|
|`customEvent.name`|  <ul><li>文字列</li><li>イベント名</li></ul> |
|`customEvent.email`|  <ul><li>文字列</li><li>ユーザーのメール</li><li>Eコマース顧客IDを上書きします。</li></ul> |
|`customEvent.id`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`customEvent.key`|  <ul><li>文字列</li><li>ユーザーIDタイプ</li></ul> |
|`customEvent.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`customEvent.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`customEvent.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |
