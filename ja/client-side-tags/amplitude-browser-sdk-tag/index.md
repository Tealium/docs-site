---
title: Amplitude Browser SDKタグ構成ガイド
description: この記事では、TealiumアカウントでAmplitude Browser SDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amplitude-browser-sdk-tag/
---
Amplitudeは、企業が自社製品の力を最大限に引き出せるよう支援する、業界をリードするデジタル分析プラットフォームです。Browser SDKを使用すると、Amplitudeにイベントを送信できます。

## ベンダー情報

このタグは、次のベンダーAPIを実装します。

* [Amplitude Browser SDK 2](https://amplitude.com/docs/sdks/analytics/browser/browser-sdk-2)
* [Amplitude：Javascript SDKからBrowser SDK 1.0への移行](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-javascript-sdk-to-browser-sdk-1-0)
* [Amplitude：Javascript SDK 1.0からBrowser SDK 2.0への移行](https://amplitude.com/docs/sdks/analytics/browser/migrate-from-browser-sdk-1-0-to-2-0)

## タグに関するヒント

* 注文IDが構成されると、コンバージョンが送信されます。
* 顧客IDが入力されている場合、`amplitude.init()`の呼び出しで`userId`として送信されます。
* 次のEコマース拡張機能パラメータをサポートしています。
    * 注文ID（`_corder`）
    * カートまたは注文タイプ（`_ctype`）
    * 顧客ID（`_ccustid`）
    * 製品IDのリスト（`_cprod`）
    * 数量のリスト（`_cquan`）
    * 価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **APIキー**：AmplitudeプロジェクトのAPIキー。
* **SDKバージョン**：読み込むAmplitude Browser SDKライブラリのバージョン。デフォルトは`2.6.0`です。この値はCDN URLの構築に使用されます。たとえば、`2.41.1`と入力すると、`https://cdn.amplitude.com/libs/analytics-browser-2.41.1-min.js.gz`が読み込まれます。
* **セッションリプレイ**：セッションリプレイを有効または無効にします。
* **セッションリプレイのバージョン**：読み込むセッションリプレイライブラリのバージョン。デフォルト値は`1.13.9`です。
* **ガイドとアンケートを有効化**：ガイドとアンケートを有効または無効にします。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `api_key`  | 文字列 | APIキー |
| `sdk_version`  | 文字列 | SDKバージョン |
| `autocapture`  | ブール値 | クリック、入力変更、その他のブラウザインタラクションの自動キャプチャを有効または無効にします |
| `elementInteractions`  | ブール値 | 自動キャプチャが有効な場合に、要素インタラクションイベントのトラッキングを有効または無効にします |
| `deviceId`  | 文字列 | デバイスID |
| `flushIntervalMillis`  | 数値 | ミリ秒単位のフラッシュ間隔 |
| `flushQueueSize`  | 数値 | フラッシュキューのサイズ |
| `flushMaxRetries`  | 数値 | フラッシュの最大再試行回数 |
| `identityStorage`  | 文字列 | ID保存 |
| `logLevel`  | 文字列 | ログレベル |
| `optOut`  | ブール値 | オプトアウト |
| `serverUrl`  | 文字列 | サーバーURL |
| `serverZone`  | 文字列 | サーバーゾーン |
| `transport`  | 文字列 | トランスポート |
| `useBatch`  | ブール値 | バッチを使用 |
| `userId`  | 文字列 | ユーザーID。実行時に`amplitude.setUserId()`にマッピングされます |
| `sessionId`  | 数値 | エポックからの経過ミリ秒（Unixタイムスタンプ）で表されるセッションID。実行時に`amplitude.setSessionId()`にマッピングされます |
| `reset_identity`  | ブール値 | `true`で、かつ**IDのリセットを有効化**が有効な場合、ID値を適用する前に`amplitude.reset()`を呼び出します |
| `session_replay` | ブール値 | セッションリプレイを有効にします |
| `session_replay_version` | 文字列 | セッションリプレイのバージョン |
| `guides_and_surveys` | ブール値 | ガイドとアンケートを有効にします |

### ユーザープロパティ

| 変数 | 説明 |
|:---------|:------------|
| `add.custom` | 数値を指定した数だけ増加させます |
| `append.custom` | プロパティ配列の末尾に値を追加します |
| `prepend.custom` | プロパティ配列の先頭に値を追加します |
| `set.custom` | プロパティ値を構成または上書きします |
| `setOnce.custom` | 値を構成します。一度構成すると、これらの値は上書きできません |
| `unset.custom` | 値をnullに構成解除します |

### イベント

| 変数 | 説明 |
|:---------|:------------|
| `event_type` | イベントタイプ |
| `eventProperties.custom` | イベントプロパティ |
| `groups.custom` | グループ |

### 収益トラッキング／Eコマース

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `order_id`  | 文字列 | 注文ID（`_corder`を上書き） |
| `order_type`  | 文字列 | カートまたは注文タイプ（`_ctype`を上書き） |
| `customer_id`  | 文字列 | 顧客ID（`_ccustid`を上書き） |
| `product_id`  | 配列 | 製品IDのリスト（`_cprod`を上書き） |
| `product_quantity`  | 配列 | 製品数量のリスト（`_cquan`を上書き） |
| `product_unit_price`  | 配列 | 製品価格のリスト（`_cprice`を上書き） |

### ユーザーグループ

| 変数 | 説明 |
|:---------|:------------|
| `group.custom`  | `amplitude.setGroup()`を使用してユーザーをグループに割り当てます。`custom`をグループ名に変更してください。 |

### デフォルトトラッキング

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `attribution`  | ブール値 | UTMパラメータやリファラーなどのアトリビューションデータの自動トラッキングを有効または無効にします |
| `pageViews`  | ブール値 | ページビューの自動トラッキングを有効または無効にします |
| `sessions`  | ブール値 | セッションの自動トラッキングを有効または無効にします |
| `formInteractions`  | ブール値 | フォームインタラクションの自動トラッキングを有効または無効にします |
| `fileDownloads`  | ブール値 | ファイルダウンロードのクリックの自動トラッキングを有効または無効にします |

### トラッキングオプション

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `ipAddress`  | ブール値 | ユーザーのIPアドレスの収集を有効または無効にします |
| `language`  | ブール値 | ユーザーのブラウザ言語の収集を有効または無効にします |
| `platform`  | ブール値 | ユーザーのプラットフォーム情報の収集を有効または無効にします |

### Cookieオプション

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `domain`  | 文字列 | Amplitude Cookieのドメイン |
| `expiration`  | 数値 | Cookieの有効期限が切れるまでの日数 |
| `sameSite`  | 文字列 | CookieのSameSite属性（`Lax`、`Strict`、または`None`） |
| `secure`  | ブール値 | CookieにSecureフラグを構成するかどうか |
| `upgrade`  | ブール値 | 以前のSDKバージョンから既存のCookieをアップグレードするかどうか |

### UTM（Urchin Traffic Monitor）

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `utm_source`  | 文字列 | トラフィックの送信元Webサイト |
| `utm_medium`  | 文字列 | マーケティングメディア（例：`email`または`cpc`） |
| `utm_campaign`  | 文字列 | 特定のキャンペーン名（例：`summer_sale`） |
| `utm_term`  | 文字列 | 使用された有料検索語句（例：`product+analytics`） |
| `utm_content`  | 文字列 | ユーザーをサイトに誘導した要素を識別します。一般的にA/Bテストに使用されます |