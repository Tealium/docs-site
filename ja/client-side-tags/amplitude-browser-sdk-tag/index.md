---
title: AmplitudeブラウザSDKタグ構成ガイド
description: この記事では、TealiumアカウントでAmplitudeブラウザSDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amplitude-browser-sdk-tag/
---
Amplitudeは、企業が製品の力を解放するのを助ける先導的なデジタルアナリティクスプラットフォームです。ブラウザSDKを使用すると、Amplitudeにイベントを送信できます。

## ベンダー情報

このタグは、次のベンダーAPIを実装しています：

* [AmplitudeブラウザSDK 2](https://amplitude.com/docs/sdks/analytics/browser/browser-sdk-2)
* [Amplitude: Javascript SDKからブラウザSDK 1.0への移行](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-javascript-sdk-to-browser-sdk-1-0)
* [Amplitude: Javascript SDK 1.0からブラウザSDK 2.0への移行](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-browser-sdk-1-0-to-2-0)

## タグのヒント

* 注文IDが構成されると変換が発生します。
* `userId`として顧客IDが`amplitude.init()`呼び出しで送信されます（入力されている場合）。
* 以下のEコマース拡張パラメータをサポートしています：
    * 注文ID（`_corder`）
    * カートまたは注文タイプ（`_ctype`）
    * 顧客ID（`_ccustid`）
    * 製品IDリスト（`_cprod`）
    * 数量リスト（`_cquan`）
    * 価格リスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際に、以下の構成を構成します：

* **APIキー**：AmplitudeプロジェクトのAPIキー。
* **SDKバージョン**：ロードするライブラリのバージョン。デフォルトはバージョン2.6.0です。
* **セッションリプレイ**：セッションリプレイを有効または無効にします。
* **セッションリプレイバージョン**：ロードするライブラリのバージョン。デフォルト値は1.13.9です。
* **ガイドと調査の有効化**：ガイドと調査を有効または無効にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `api_key`  | 文字列 | APIキー |
| `sdk_version`  | 文字列 | SDKバージョン |
| `defaultTracking`  | ブール値 | デフォルトトラッキング|
| `deviceId`  | 文字列 | デバイスID |
| `flushIntervalMillis`  | 数値 | フラッシュ間隔（ミリ秒） |
| `flushQueueSize`  | 数値 | フラッシュキューサイズ |
| `flushMaxRetries`  | 数値 | フラッシュ最大リトライ回数 |
| `identityStorage`  | 文字列 | ID保存 |
| `logLevel`  | 文字列 | ログレベル |
| `optOut`  | ブール値 | オプトアウト |
| `serverUrl`  | 文字列 | サーバーURL |
| `serverZone`  | 文字列 | サーバーゾーン |
| `transport`  | 文字列 | トランスポート |
| `useBatch`  | ブール値 | バッチ使用 |
| `userId`  | 数値 | ユーザーID |
| `session_replay` | ブール値 | セッションリプレイを有効にする |
| `session_replay_version` | 文字列 | セッションリプレイバージョン |
| `guides_and_surveys` | ブール値 | ガイドと調査を有効にする |

### ユーザープロパティ

| 変数 | 説明 |
|:---------|:------------|
| `add.custom` | 指定された数値で数値を増やす |
| `append.custom` | 値をプロパティ配列に追加する |
| `prepend.custom` | 値をプロパティ配列の先頭に追加する |
| `set.custom` | プロパティ値を構成または上書きする |
| `setOnce.custom` | 値を構成し、一度構成するとこれらの値は上書きできない |
| `unset.custom` | 値をnullに構成する |

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
| `group.custom`  |  |

### デフォルトトラッキング

| 変数 | タイプ |
|:---------|:-----|
| `attribution`  | ブール値 |
| `pageViews`  | ブール値 |
| `sessions`  | ブール値 |
| `formInteractions`  | ブール値 |
| `fileDownloads`  | ブール値 |

### トラッキングオプション

| 変数 | タイプ |
|:---------|:-----|
| `ipAddress`  | ブール値 |
| `language`  | ブール値 |
| `platform`  | ブール値 |

### クッキーオプション

| 変数 | タイプ |
|:---------|:-----|
| `domain`  | 文字列 |
| `expiration`  | 数値 |
| `sameSite`  | 文字列 |
| `secure`  | ブール値 |
| `upgrade`  | ブール値 |

