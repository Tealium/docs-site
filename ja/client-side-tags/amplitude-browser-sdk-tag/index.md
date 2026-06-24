---
title: AmplitudeブラウザSDKタグ構成ガイド
description: この記事では、TealiumアカウントでAmplitudeブラウザSDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amplitude-browser-sdk-tag/
---
Amplitudeは、企業が製品の力を解き放つのを助ける先進的なデジタルアナリティクスプラットフォームです。ブラウザSDKを使用すると、Amplitudeにイベントを送信できます。

## ベンダー情報

このタグは、以下のベンダーAPIを実装しています：

* [AmplitudeブラウザSDK 2](https://amplitude.com/docs/sdks/analytics/browser/browser-sdk-2)
* [Amplitude: Javascript SDKからブラウザSDK 1.0への移行](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-javascript-sdk-to-browser-sdk-1-0)
* [Amplitude: Javascript SDK 1.0からブラウザSDK 2.0への移行](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-browser-sdk-1-0-to-2-0)

## タグのヒント

* 注文IDが構成されると変換が発生します。
* 顧客IDが入力されている場合、`userId`として`amplitude.init()`呼び出しで送信されます。
* 以下のEコマース拡張パラメータをサポートしています：
    * 注文ID（`_corder`）
    * カートまたは注文タイプ（`_ctype`）
    * 顧客ID（`_ccustid`）
    * 製品IDリスト（`_cprod`）
    * 数量リスト（`_cquan`）
    * 価格リスト（`_cprice`）

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理]()を参照してください。

タグを追加する際に、以下の構成を構成します：

* **APIキー**：AmplitudeプロジェクトのAPIキー。
* **SDKバージョン**：読み込むAmplitudeブラウザSDKライブラリのバージョン。デフォルトは`2.6.0`です。この値はCDN URLの構築に使用されます。例えば、`2.41.1`を入力すると`https://cdn.amplitude.com/libs/analytics-browser-2.41.1-min.js.gz`が読み込まれます。
* **セッションリプレイ**：セッションリプレイを有効または無効にします。
* **セッションリプレイバージョン**：読み込むセッションリプレイライブラリのバージョン。デフォルト値は`1.13.9`です。
* **ガイドと調査の有効化**：ガイドと調査を有効または無効にします。

## 読み込みルール

すべてのページでタグを読み込むか、タグが読み込まれる条件を構成します。詳細については、[読み込みルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `api_key`  | 文字列 | APIキー |
| `sdk_version`  | 文字列 | SDKバージョン |
| `autocapture`  | ブール値 | クリック、入力変更、その他のブラウザの相互作用の自動キャプチャを有効または無効にします |
| `elementInteractions`  | ブール値 | autocaptureが有効な場合に要素の相互作用イベントの追跡を有効または無効にします |
| `deviceId`  | 文字列 | デバイスID |
| `flushIntervalMillis`  | 数値 | フラッシュ間隔（ミリ秒） |
| `flushQueueSize`  | 数値 | フラッシュキューサイズ |
| `flushMaxRetries`  | 数値 | フラッシュの最大リトライ回数 |
| `identityStorage`  | 文字列 | ID保存 |
| `logLevel`  | 文字列 | ログレベル |
| `optOut`  | ブール値 | オプトアウト |
| `serverUrl`  | 文字列 | サーバーURL |
| `serverZone`  | 文字列 | サーバーゾーン |
| `transport`  | 文字列 | トランスポート |
| `useBatch`  | ブール値 | バッチ使用 |
| `userId`  | 文字列 | ユーザーID、実行時に`amplitude.setUserId()`にマッピングされます |
| `sessionId`  | 数値 | セッションID（エポックからのミリ秒単位のUnixタイムスタンプ）、実行時に`amplitude.setSessionId()`にマッピングされます |
| `reset_identity`  | ブール値 | `true`の場合、**IDリセットを有効にする**が有効な場合、ID値を適用する前に`amplitude.reset()`を呼び出します |
| `session_replay` | ブール値 | セッションリプレイを有効にする |
| `session_replay_version` | 文字列 | セッションリプレイバージョン |
| `guides_and_surveys` | ブール値 | ガイドと調査を有効にする |

### ユーザープロパティ

| 変数 | 説明 |
|:---------|:------------|
| `add.custom` | 指定された数値で数値を増やします |
| `append.custom` | 値をプロパティ配列に追加します |
| `prepend.custom` | 値をプロパティ配列の先頭に追加します |
| `set.custom` | プロパティ値を構成または上書きします |
| `setOnce.custom` | 値を構成し、一度構成するとこれらの値は上書きできません |
| `unset.custom` | 値をnullに構成します |

### イベント

| 変数 | 説明 |
|:---------|:------------|
| `event_type` | イベントタイプ |
| `eventProperties.custom` | イベントプロパティ |
| `groups.custom` | グループ |

### 収益追跡/Eコマース

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `order_id`  | 文字列 | 注文ID（`_corder`を上書き） |
| `order_type`  | 文字列 | カートまたは注文タイプ（`_ctype`を上書き） |
| `customer_id`  | 文字列 | 顧客ID（`_ccustid`を上書き） |
| `product_id`  | 配列 | 製品IDリスト（`_cprod`を上書き） |
| `product_quantity`  | 配列 | 製品数量リスト（`_cquan`を上書き） |
| `product_unit_price`  | 配列 | 製品価格リスト（`_cprice`を上書き） |

### ユーザーグループ

| 変数 | 説明 |
|:---------|:------------|
| `group.custom`  | `amplitude.setGroup()`を介してユーザーをグループに割り当てます。`custom`をグループ名に変更します。 |

### デフォルトトラッキング

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `attribution`  | ブール値 | UTMパラメーターやリファラーなどの帰属データの自動トラッキングを有効または無効にします |
| `pageViews`  | ブール値 | ページビューの自動トラッキングを有効または無効にします |
| `sessions`  | ブール値 | セッションの自動トラッキングを有効または無効にします |
| `formInteractions`  | ブール値 | フォームの相互作用の自動トラッキングを有効または無効にします |
| `fileDownloads`  | ブール値 | ファイルダウンロードのクリックの自動トラッキングを有効または無効にします |

### トラッキングオプション

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `ipAddress`  | ブール値 | ユーザーのIPアドレスの収集を有効または無効にします |
| `language`  | ブール値 | ユーザーのブラウザ言語の収集を有効または無効にします |
| `platform`  | ブール値 | ユーザーのプラットフォーム情報の収集を有効または無効にします |

### Cookieオプション

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `domain`  | 文字列 | Amplitudeクッキーのドメイン |
| `expiration`  | 数値 | クッキーの有効期限（日数） |
| `sameSite`  | 文字列 | クッキーのSameSite属性（`Lax`、`Strict`、または`None`） |
| `secure`  | ブール値 | クッキーにSecureフラグを構成するかどうか |
| `upgrade`  | ブール値 | 以前のSDKバージョンからのクッキーをアップグレードするかどうか |

### UTM（Urchin Traffic Monitor）

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `utm_source`  | 文字列 | トラフィックを送信したウェブサイト |
| `utm_medium`  | 文字列 | マーケティング手段、例えば`email`や`cpc` |
| `utm_campaign`  | 文字列 | 特定のキャンペーン名、例えば`summer_sale` |
| `utm_term`  | 文字列 | 使用された有料検索用語、例えば`product&#43;analytics` |
| `utm_content`  | 文字列 | ユーザーをサイトに導いたものを特定するために一般的に使用される、A/Bテストなどに使用されます |
