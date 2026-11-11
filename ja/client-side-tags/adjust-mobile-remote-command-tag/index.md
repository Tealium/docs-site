---
title: Adjust Mobileリモートコマンドタグ構成ガイド
description: この記事では、タグ管理アカウントでAdjust Mobileリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adjust-mobile-remote-command-tag/
---
Adjustは、モバイル計測と不正防止の業界リーダーです。マーケティングをよりシンプル、スマート、かつ安全にすることで、データドリブンなマーケターの成功を支援します。

## タグに関するヒント

* マッピングを使用して、標準の構成値を上書きします。
* これは、ネイティブモバイルアプリSDK用のリモートコマンドコンパニオンタグです。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **Adjust APIトークン**
  * Adjust APIトークンはユーザーごとに割り当てられ、Adjustダッシュボードの任意のアカウントおよびAdjustと連携する任意のアプリで使用できます。
  * [Adjust APIトークンを確認する](https://help.adjust.com/en/article/developer-guides#how-to-find-your-adjust-api-token)。

* **自動初期化**
  * Initializeコマンドを自動的に送信します。

* **サンドボックス**
  * 自分または他のユーザーがアプリをテストしている場合は、trueに構成します。

* **ログレベル**
  * テスト中に表示されるログの量を増減します。

* **開始の遅延**
  * Adjust SDKの開始を遅らせることで、インストール時に送信する一意の識別子などのセッションパラメータを取得する時間をアプリに確保できます。
  * Adjust SDKの開始を遅らせることができる時間は、最大10秒です。

* **iAd iOSフレームワークを許可**
  * このフレームワークは、実施している可能性のあるASAキャンペーンのアトリビューションをSDKが自動的に処理するために必要です。

* **Ad Servicesフレームワークを許可**
  * iOS 14.3以降を実行しているデバイスでは、このフレームワークにより、SDKがASAキャンペーンのアトリビューションを自動的に処理できます。
  * Apple Ads Attribution APIを利用する場合に必要です。

* **iOS広告識別子を許可**
  * 一部のサービス（Google Analyticsなど）では、重複レポートを防ぐために、デバイスIDとクライアントIDを連携させる必要があります。

* **アプリシークレットID**
  * SDK署名機能に使用します。

* **アプリシークレット情報1**
  * SDK署名機能に使用します。

* **アプリシークレット情報2**
  * SDK署名機能に使用します。

* **アプリシークレット情報3**
  * SDK署名機能に使用します。

* **アプリシークレット情報4**
  * SDK署名機能に使用します。

* **イベントバッファリング**
  * アプリでイベントトラッキングを頻繁に使用する場合は、一部のHTTPリクエストを遅延させ、1分ごとに1つのバッチとして送信できます。

* **バックグラウンドトラッキング**
  * Adjust SDKのデフォルトの動作では、アプリがバックグラウンドにある間、HTTPリクエストの送信を一時停止します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### コマンド

| リモートコマンド              |
|:----------------------------|
| `launch`                    |
| `track_deeplink`            |
| `purchase`                  |
| `event`                     |
| `contact`                   |
| `ad_revenue`                |
| `subscribe`                 |
| `received_push_token`       |
| `add_session_parameters`    |
| `remove_session_parameters` |
| `reset_session_parameters`  |
| `consent_revoked`           |
| `consent_granted`           |
| `set_enabled`               |
| `offline`                   |

### 標準

| 変数                                                          | 型        |
|:-------------------------------------------------------------|:----------|
| APIトークン（`api_token`）                                      | [String]  |
| 自動初期化（`auto_initialize`）                                  | [Boolean] |
| サンドボックス（`sandbox`）                                      | [Boolean] |
| ログレベル（`settings.log_level`）                               | [String]  |
| 開始の遅延（`settings.delay_start`）                             | [Float]   |
| IADを許可（`settings.allow_iad`）                                | [Boolean] |
| Ad Servicesを許可（`settings.allow_ad_services`）                | [Boolean] |
| IDFAを許可（`settings.allow_idfa`）                              | [Boolean] |
| アプリシークレット（`settings.app_secret`）                        | [String]  |
| アプリシークレット情報1（`settings.app_secret_info_1`）             | [String]  |
| アプリシークレット情報2（`settings.app_secret_info_2`）             | [String]  |
| アプリシークレット情報3（`settings.app_secret_info_3`）             | [String]  |
| アプリシークレット情報4（`settings.app_secret_info_4`）             | [String]  |
| イベントバッファリングを有効化（`settings.event_buffering_enabled`） | [Boolean] |
| バックグラウンドで送信（`settings.send_in_background`）              | [Boolean] |

### イベントトラッキング

| 変数                                                    | 型                                          |
|:-------------------------------------------------------|:--------------------------------------------|
| イベントトークン                                           | （`event_token`）                             |
| 注文ID                                                  | （`order_id`）（`_corder`を上書き）              |
| 注文合計（`order_total`）（`_ctotal`を上書き）               | [Float]                                     |
| 通貨                                                    | （`order_currency`）（`_ccurrency`を上書き）      |
| コンバージョン値                                           | （`conversion_value`）                        |
| 販売地域                                                 | （`sales_region`）                            |
| SKU（`sku`）                                            | [String]                                    |
| 購入トークン（`purchase_token`）                            | [String]                                    |
| 署名（`signature`）                                      | [String]                                    |

### 広告収益トラッキング

| 名前       | パラメータ                 |
|:-----------|:--------------------------|
| 広告収益ソース | （`ad_revenue_source`）     |

### サブスクリプション

| 変数                                  | 型                  |
|:-------------------------------------|:--------------------|
| App Storeレシートデータ（`receipt`）     | [JSON]              |
| 購入タイムスタンプ                        | （`purchase_time`）   |

### コールバック／パートナーパラメータ

| 変数                                 | パラメータ                                  |
|:------------------------------------|:-------------------------------------------|
| コールバックID                         | （`callback_id`）                            |
| セッションコールバックパラメータを削除      | （`remove_session_callback_params`）         |
| セッションコールバックパラメータをリセット    | （`reset_session_callback_params`）          |
| セッションパートナーパラメータを削除         | （`remove_session_partner_params`）          |
| セッションパートナーパラメータをリセット       | （`reset_session_partner_params`）           |

### ディープリンク

| 変数          | 説明                    |
|:--------------|:------------------------|
| ディープリンクURL | （`deeplink_open_url`）   |

### メッセージング

| 変数          | 説明               |
|:--------------|:-------------------|
| プッシュトークン | （`push_token`）     |

### 同意の計測

| 変数                 | 説明                        |
|:--------------------|:----------------------------|
| 同意済み              | （`measurement_consent`）     |
| 有効（`enabled`）     | [Boolean]                   |