---
title: Pulse by Analytics Intelligenceタグ構成ガイド
description: この記事では、Pulse by Analytics Intelligenceタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pulse-tag/
---
Pulse by Analytics Intelligenceは、完全にクライアント側で動作するファーストパーティの行動分析プラットフォームです。ユーザーの操作を自動的に取得し、仮名化された識別子、キャンペーンアトリビューション、および概算位置情報に関連付けます。データはバッチ処理され、第三者と共有されることなく、Analytics IntelligenceがEU内でホストするバックエンドに送信されます。

## タグに関するヒント

* Analytics Intelligenceの**Company/Profile ID**をタグ構成パネルに入力します。タグを読み込むには、このIDが必要です。
* タグは、ページごとにPulseコアライブラリを1回読み込みます。その後、Pulseはユーザー操作（ページビュー、クリック、スクロール、フォーム入力、フォーカス／フォーカス解除、マウス移動、クリップボード操作、キャンペーンアトリビューション、セッション終了）を自動的に取得し、バッチ処理してAnalytics IntelligenceがEU内でホストするバックエンドに送信します。
* **General**タブを使用して、初回ページビューにデータレイヤーの値（`page_name`、`page_type`、`site_section`、`user_id`、`environment`、`language`）をエンリッチメントします。マッピングされていない場合、それぞれ適切なデフォルト値（`document.title`、`navigator.language`など）が使用されます。
* **Configuration**タブを使用して、配信ごとに**Company/Profile ID**を上書きできます（複数ブランドのプロファイルを使用する場合など）。
* Pulseは分析Cookie（`ai_pulse_uid`、`ai_pulse_did`、`ai_pulse_cpid`）を構成します。このタグを**Analytics**同意カテゴリに割り当ててください。タグは`utag.gdpr.getConsentState()`を通じてTealiumの同意状態を尊重し、分析への同意が付与されていない場合は読み込まれません。
* Analytics Intelligenceは、すべてのデータをAWSの`eu-west-1`に保存します。すべての識別子は仮名化されており、EU域外へのデータ転送は行われません。ベンダーは、機密性の高いフォーム入力（パスワード、カード情報、カード確認値（CVV）、社会保障番号（SSN）、PIN）を取得対象から除外します。
* 推奨スコープ：**DOM Ready**で**All Pages**に配信します。
* より保守的なプライバシープログラムでは、**Enable Geolocation**をオフにします。イベントを60秒ごとのバッチではなく個別に送信するには、**Enable Batching**をオフにします。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を構成します。

* **Company / Profile ID**：必須。Analytics IntelligenceのPulse企業IDまたはプロファイルIDです。
* **Environment**：任意。イベントとともに送信される環境ラベルです。デフォルトは`production`です。
* **Language**：任意。ページビューとともに送信される言語の上書き値です。デフォルトはブラウザーの言語（`navigator.language`）です。
* **Enable Batching**：イベントをバッチ処理し、60秒ごとに送信します（デフォルト）。各イベントを直ちに送信するには、`False`に構成します。
* **Enable Geolocation**：セッションごとに1回、IPベースの概算位置情報をPulseが取得できるようにします。デフォルトは`True`です。より保守的なプライバシープログラムでは、`False`に構成します。
* **Debug Mode**：ブラウザーコンソールへのPulseのデバッグログ出力を有効にします。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 構成

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `company_id` | 文字列 | 企業IDまたはプロファイルID |

### 一般

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `page_name` | 文字列 | ページ名 |
| `page_type` | 文字列 | ページタイプ |
| `site_section` | 文字列 | サイトセクション |
| `user_id` | 文字列 | ユーザーID |
| `environment` | 文字列 | 環境 |
| `language` | 文字列 | 言語 |