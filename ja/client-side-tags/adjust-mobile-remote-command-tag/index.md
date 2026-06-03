---
title: Adjustモバイルリモートコマンドタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdjustモバイルリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adjust-mobile-remote-command-tag/
---
Adjustは、モバイル測定と詐欺防止の業界リーダーです。マーケティングをよりシンプルでスマート、そして安全にすることで、データ駆動型のマーケターが成功を収めることを支援します。

## タグのヒント

* 標準の構成値を上書きするためにマッピングを使用します。
* これはネイティブモバイルアプリSDKのリモートコマンドコンパニオンタグです。

## タグの構成

まず、タグマーケットプレイスにアクセスしてAdjustモバイルリモートコマンドタグを追加します（[タグの追加方法についてはこちら]()を参照してください）。

タグを追加した後、以下の構成を行います：

* **Adjust APIトークン**
  * Adjust APIトークンはユーザーごとに割り当てられ、任意のAdjustダッシュボードアカウントおよびAdjust統合アプリで使用できます。
  * [Adjust APIトークンの検索方法](https://help.adjust.com/en/article/developer-guides#how-to-find-your-adjust-api-token)。

* **自動初期化**
  * 初期化コマンドを自動的に送信します。

* **サンドボックス**
  * アプリをテストしているあなたまたは他の誰かがtrueに構成します。

* **ログレベル**
  * テスト中に表示されるログの量を増減します。

* **遅延開始**
  * Adjust SDKの開始を遅らせることで、アプリがインストール時に送信するためのセッションパラメーター（ユニークIDなど）を取得する時間を確保できます。
  * Adjust SDKの最大遅延開始時間は10秒です。

* **iAd iOSフレームワークを許可**
  * このフレームワークは、SDKがASAキャンペーンの帰属を自動的に処理するために必要です。

* **Ad Servicesフレームワークを許可**
  * iOS 14.3以降を実行しているデバイスの場合、このフレームワークはSDKがASAキャンペーンの帰属を自動的に処理することを可能にします。
  * Apple Ads Attribution APIを活用する際に必要です。

* **iOS広告識別子を許可**
  * 重複報告を防ぐために、デバイスIDとクライアントIDを調整する必要があるサービス（例：Google Analytics）があります。

* **アプリシークレットID**
  * SDK署名機能に使用されます。

* **アプリシークレット情報1**
  * SDK署名機能に使用されます。

* **アプリシークレット情報2**
  * SDK署名機能に使用されます。

* **アプリシークレット情報3**
  * SDK署名機能に使用されます。

* **アプリシークレット情報4**
  * SDK署名機能に使用されます。

* **イベントバッファリング**
  * アプリがイベントトラッキングを頻繁に使用する場合、HTTPリクエストの一部を遅延させて、1分ごとに一括で送信することが望ましい場合があります。

* **バックグラウンドトラッキング**
  * Adjust SDKのデフォルトの動作は、アプリがバックグラウンドにある間はHTTPリクエストの送信を一時停止することです。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

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

| 変数                                                     | タイプ      |
|:-------------------------------------------------------------|:----------|
| APIトークン (`api_token`)                                      | [String]  |
| 自動初期化 (`auto_initialize`)                          | [Boolean] |
| サンドボックス (`sandbox`)                                          | [Boolean] |
| ログレベル (`settings.log_level`)                             | [String]  |
| 遅延開始 (`settings.delay_start`)                         | [Float]   |
| IADを許可 (`settings.allow_iad)                              | [Boolean] |
| Adサービスを許可 (`settings.allow_ad_services`)             | [Boolean] |
| IDFAを許可 (`settings.allow_idfa`)                           | [Boolean] |
| アプリシークレット (`settings.app_secret`)                           | [String]  |
| アプリシークレット情報1 (`settings.app_secret_info_1`)             | [String]  |
| アプリシークレット情報2 (`settings.app_secret_info_2`)             | [String]  |
| アプリシークレット情報3 (`settings.app_secret_info_3`)             | [String]  |
| アプリシークレット情報4 (`settings.app_secret_info_4`)             | [String]  |
| イベントバッファリング有効 (`settings.event_buffering_enabled`) | [Boolean] |
| バックグラウンドで送信 (`settings.send_in_background`)           | [Boolean] |

### イベントトラッキング

| 変数                                          | タイプ                                        |
|:--------------------------------------------------|:--------------------------------------------|
| イベントトークン                                       | (`event_token`)                             |
| 注文ID                                          | (`order_id`) (Overrides `_corder`)          |
| 注文合計 (`order_total`) (Overrides `_ctotal`) | [Float]                                     |
| 通貨                                          | (`order_currency`) (Overrides `_ccurrency`) |
| 変換値                                          | (`conversion_value`)                        |
| 販売地域                                      | (`sales_region`)                            |
| SKU (`sku`)                                       | [String]                                    |
| 購入トークン (`purchase_token`)                 | [String]                                    |
| 署名 (`signature`)                           | [String]                                    |

### 広告収益トラッキング

| 名前              | パラメータ             |
|:------------------|:----------------------|
| 広告収益ソース | (`ad_revenue_source`) |

### サブスクリプション

| 変数                           | タイプ              |
|:-----------------------------------|:------------------|
| アプリストアレシートデータ (`receipt`) | [JSON]            |
| 購入タイムスタンプ                 | (`purchase_time`) |

### コールバック/パートナーパラメータ

| 変数                       | パラメータ                          |
|:-------------------------------|:-----------------------------------|
| コールバックID                    | (`callback_id`)                    |
| セッションコールバックパラメータを削除 | (`remove_session_callback_params`) |
| セッションコールバックパラメータをリセット  | (`reset_session_callback_params`)  |
| セッションパートナーパラメータを削除  | (`remove_session_partner_params`)  |
| セッションパートナーパラメータをリセット   | (`reset_session_partner_params`)   |

### ディープリンキング

| 変数      | 説明           |
|:--------------|:----------------------|
| ディープリンクURL | (`deeplink_open_url`) |

### メッセージング

| 変数   | 説明    |
|:-----------|:---------------|
| プッシュトークン | (`push_token`) |

### 同意測定

| 変数            | 説明             |
|:--------------------|:------------------------|
| 同意が与えられた     | (`measurement_consent`) |
| 有効 (`enabled`) | [Boolean]               |
