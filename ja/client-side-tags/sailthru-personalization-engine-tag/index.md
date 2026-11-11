---
title: Sailthru Personalization Engineタグ構成ガイド
description: この記事では、タグ管理アカウントでSailthru Personalization Engineタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sailthru-personalization-engine-tag/
---
## タグに関するヒント

* マッピングを使用して、以下を行います。
  * 標準構成値を動的に上書きする
  * Personalization Engineのオプション構成パラメータを構成する（[詳細はこちら](https://getstarted.sailthru.com/site/personalization-engine/pe-setup/)）
  * Sailthruメタタグをサイトに動的に追加する
  * イベントトリガー（カスタムイベントを含む）を構成する
  * 必須およびオプションのイベントパラメータを送信する

* 以下のEコマース拡張パラメータをサポートしています。
  * 注文ID
  * 顧客ID
  * 製品IDのリスト
  * 製品名のリスト
  * 製品数量のリスト
  * 製品価格のリスト

* 必須およびオプションのイベントパラメータの一覧については、SailthruのJavaScript API Libraryドキュメントを参照してください。[Sailthru JavaScript API Library](https://getstarted.sailthru.com/developers/api-client/javascript/)

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下を構成します。

* **顧客ID**
  * Sailthruの顧客ID。

* **ページビューのトラッキング**
  * 手動でページビューをトラッキングするには、トラッキング対象ページのページビューURL（`pageview.url`）へのマッピングが必要です。
  * 追加のオプションパラメータを構成するには、データマッピングを使用します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`init.customerId`|  <ul><li>Sailthruの顧客ID</li></ul> |
|`pageviewTracking`|  <ul><li>ページビューのトラッキング</li><li>オプションは**自動**または**手動**です。</li></ul> |
|`init.isCustom`|  <ul><li>オプションは`true`または`false`です。</li></ul> |
|`init.useStoredTags`|  <ul><li>オプションは`true`または`false`です。</li></ul> |
|`init.excludeContent`|  <ul><li>オプションは`true`または`false`です。</li></ul> |
|`pageview.url`|  <ul><li>ページビューURL</li></ul> |
|`pageview.tags`|  <ul><li>ページビュータグ</li></ul> |
|`pageview.onSuccess`|  <ul><li>コールバック関数名</li><li>ページビュー成功時</li></ul> |
|`pageview.onError`|  <ul><li>コールバック関数名</li><li>ページビューエラー時</li></ul> |
|`meta.custom`|  <ul><li>カスタムメタタグ</li></ul> |

#### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>製品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>製品名のリスト</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>製品数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>製品価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |

#### イベントトリガー

|変数| 説明|
|---| ---|
|`userSignUp`|  <ul><li>ユーザー登録</li></ul> |
|`userSignUpConfirmedOptIn`|  <ul><li>ユーザー登録のオプトイン確認</li></ul> |
|`addToCart`|  <ul><li>カートへの追加</li></ul> |
|`purchase`|  <ul><li>購入</li></ul> |
|`customEvent`|  <ul><li>カスタムイベント</li></ul> |

#### イベントデータ：userSignUp

|変数| 説明|
|---| ---|
|`userSignUp.email`|  <ul><li>文字列</li><li>ユーザーのメールアドレス</li><li>Eコマースの顧客IDを上書きします</li></ul> |
|`userSignUp.id`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`userSignUp.key`|  <ul><li>文字列</li><li>ユーザーIDの種類</li></ul> |
|`userSignUp.lists`|  <ul><li>オブジェクト</li><li>リスト</li></ul> |
|`userSignUp.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`userSignUp.source`|  <ul><li>文字列</li><li>獲得元</li></ul> |
|`userSignUp.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`userSignUp.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ：userSignUpConfirmedOptIn

|変数| 説明|
|---| ---|
|`userSignUpConfirmedOptIn.email`|  <ul><li>文字列</li><li>ユーザーのメールアドレス</li><li>Eコマースの顧客IDを上書きします。</li></ul> |
|`userSignUpConfirmedOptIn.id`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`userSignUpConfirmedOptIn.key`|  <ul><li>文字列</li><li>ユーザーIDの種類</li></ul> |
|`userSignUpConfirmedOptIn.template_name`|  <ul><li>文字列</li><li>オプトインテンプレート名</li></ul> |
|`userSignUpConfirmedOptIn.template_vars`|  <ul><li>オブジェクト</li><li>オプトインテンプレート変数</li></ul> |
|`userSignUpConfirmedOptIn.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`userSignUpConfirmedOptIn.source`|  <ul><li>文字列</li><li>獲得元</li></ul> |
|`userSignUpConfirmedOptIn.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`userSignUpConfirmedOptIn.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ：addToCart

|変数| 説明|
|---| ---|
|`addToCart.email`|  <ul><li>文字列</li><li>ユーザーのメールアドレス</li><li>Eコマースの顧客IDを上書きします</li></ul> |
|`addToCart.reminder_time`|  <ul><li>文字列</li><li>リマインダー時刻</li></ul> |
|`addToCart.reminder_template`|  <ul><li>文字列</li><li>リマインダーテンプレート</li></ul> |
|`product_url`|  <ul><li>配列</li><li>製品URLのリスト</li></ul> |
|`product_images`|  <ul><li>オブジェクトの配列</li><li>製品画像のリスト</li></ul> |
|`product_vars`|  <ul><li>オブジェクトの配列</li><li>製品変数のリスト</li></ul> |
|`addToCart.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`addToCart.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`addToCart.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ：purchase

|変数| 説明|
|---| ---|
|`purchase.email`|  <ul><li>文字列</li><li>ユーザーのメールアドレス</li><li>Eコマースの顧客IDを上書きします。</li></ul> |
|`product_url`|  <ul><li>配列</li><li>製品URLのリスト</li></ul> |
|`product_images`|  <ul><li>オブジェクトの配列</li><li>製品画像のリスト</li></ul> |
|`product_vars`|  <ul><li>オブジェクトの配列</li><li>製品変数のリスト</li></ul> |
|`purchase.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`purchase.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`purchase.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |

#### イベントデータ：customEvent

|変数| 説明|
|---| ---|
|`customEvent.name`|  <ul><li>文字列</li><li>イベント名</li></ul> |
|`customEvent.email`|  <ul><li>文字列</li><li>ユーザーのメールアドレス</li><li>Eコマースの顧客IDを上書きします。</li></ul> |
|`customEvent.id`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`customEvent.key`|  <ul><li>文字列</li><li>ユーザーIDの種類</li></ul> |
|`customEvent.vars`|  <ul><li>オブジェクト</li><li>変数</li></ul> |
|`customEvent.onSuccess`|  <ul><li>文字列</li><li>成功時のコールバック関数名</li></ul> |
|`customEvent.onError`|  <ul><li>文字列</li><li>エラー時のコールバック関数名</li></ul> |