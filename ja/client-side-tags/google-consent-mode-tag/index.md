---
title: Google 同意モードタグ構成ガイド
description: タグ管理アカウントで Google 同意モードタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-consent-mode-tag/
---
Google 同意モードは、ユーザーの同意ステータスを Google タグに伝達し、指定された同意構成に応じてデータの収集および測定動作を調整できるようにします。

## 同意モードについて

同意モードは、基本モードと高度なモードの 2 つの方法で実装できます。

詳細については、[Google 広告ヘルプ：同意モードについて](https://support.google.com/google-ads/answer/10000067?hl=en)を参照してください。

### 基本の同意モード

基本の同意モードを使用すると、ユーザーが同意バナーを操作するまで、タグの読み込みが完全にブロックされます。Google 同意モードタグは、他の Google タグに同意シグナルを送信できるよう常に配信される設計ですが、同意が得られるまでは Google にデータを送信しません。

### 高度な同意モード

高度な同意モードを使用すると、Google タグが読み込まれ、デフォルトでは同意が拒否されたものとして扱われます（Google で別途構成されている場合を除く）。Google 同意モードタグは同意シグナルを記録し、各 Google タグは更新された同意ステータスに応じて動作します。同意が拒否されている間、Google タグは Cookie を使用しない ping を使用して、同意ステータスと匿名のユーザーアクティビティを送信します。

詳細については、[Google アナリティクス ヘルプ：同意モードの ping](https://support.google.com/analytics/answer/10000067?sjid=16066762200831072014-NC#Pings)を参照してください。

このアプローチは、同意が得られた場合に限って個人を特定できる情報（PII）を使用しながら、分析および広告コンバージョンのために最大限のデータを収集することを目的としています。

## タグに関するヒント

このセクションでは、タグの構成とマッピングオプションに関する一般的な情報を提供します。Google 同意モードを Tealium 同意レジスター（クライアント側の[同意統合](https://docs.tealium.com/about-consent-integrations/)および[同意マネージャー](https://docs.tealium.com/about-consent-management/)の機能）と統合する方法については、[Tealium 同意レジスター](https://docs.tealium.com/consent-register/)を参照してください。これが推奨される実装方法です。

Google 同意モードタグがユーザーの同意ステータスに動的に対応できるようにするには、以下を推奨します。

* 基本の同意モード：
  * 同意統合で Google 同意モードタグを**厳密に必要**に構成するか、同意管理の対象からこのタグを除外します。
  * 同意統合または同意管理で、Google タグをそれぞれ対応する同意カテゴリーにマッピングします。
* 高度な同意モード：
  * 同意統合で Google 同意モードタグおよび Google タグを**厳密に必要**に構成するか、同意管理の対象からこれらのタグを除外します。
  * JavaScript 拡張機能を使用して、エンドユーザーの同意選択を Google 同意モードの構成にマッピングします。詳細については、[同意目的のマッピング](https://docs.tealium.com/google-consent-mode/#consent-purpose-mapping)を参照してください。

## タグ構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **Tealium 同意 Cookie から自動的に読み取る**：`true`に構成すると、Tealium 同意マネージャーに基づいて Google の同意が構成されます。正確な動作については、ほかの構成項目の説明を参照してください。
* **広告保存**：同意マネージャーとの統合が有効で、部分的な同意が得られた場合、`ad_storage_consent`の値が`granted`に構成されます。完全な同意が得られた場合も、`granted`に構成されます。
* **広告ユーザーデータ**：同意マネージャーとの統合が有効で、部分的な同意が得られた場合、この同意カテゴリーを使用して`ad_user_data`の値を`granted`に構成します。完全な同意が得られた場合も、`granted`に構成されます。
* **広告のパーソナライズ**：同意マネージャーとの統合が有効で、部分的な同意が得られた場合、この同意カテゴリーを使用して`ad_personalization`の値を`granted`に構成します。完全な同意が得られた場合も、`granted`に構成されます。
* **アナリティクス保存**：同意マネージャーとの統合が有効で、部分的な同意が得られた場合、`analytics_storage_consent`の値が`granted`に構成されます。完全な同意が得られた場合も、`granted`に構成されます。
* **広告データの編集マッピング**  
`ads_data_redaction`が`true`で、`ad_storage`が`denied`の場合、Google 広告タグおよび Floodlight タグがネットワークリクエストで送信する広告クリック識別子は編集されます。
* **URL パススルー**：測定品質を向上させるため、ページ間で URL パラメータを介して情報を渡すよう任意で構成できます。
* **更新を待機**：同意ツールが非同期で読み込まれる場合、Google タグより前に実行されるとは限りません。これに対応するには、`wait_for_update`にミリ秒単位の値を指定し、データを送信するまでの待機時間を制御します。
* **データレイヤー名**：デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーの名前は`dataLayer`です。プロジェクトで別の名前が必要な場合にのみ、データレイヤーの名前を変更してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `tealium_consent` | Boolean | Tealium 同意 Cookie から読み取ります。 |
| `ad_storage_consent` | String | 広告保存の同意。 |
| `ad_user_data` | String | 広告ユーザーデータ。 |
| `ad_personalization` | String | 広告のパーソナライズ。 |
| `analytics_storage_consent` | String | アナリティクス保存の同意。 |
| `ads_data_redaction` | Boolean | 広告データの編集マッピング。 |
| `url_passthrough` | Boolean | URL パススルー。 |
| `wait_for_update` | Number | 更新を待機。 |
| `data_layer_name` | `String` | データレイヤー名。 |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `update` | 更新 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `tealium_consent` | Boolean | Tealium 同意 Cookie から読み取ります。 |
| `ad_storage_consent` | String | 広告保存の同意。 |
| `ad_user_data` | String | 広告ユーザーデータ。 |
| `ad_personalization` | String | 広告のパーソナライズ。 |
| `analytics_storage_consent` | String | アナリティクス保存の同意。 |
| `ads_data_redaction` | Boolean | 広告データの編集マッピング。 |
| `url_passthrough` | Boolean | URL パススルー。 |
| `wait_for_update` | Number | 更新を待機。 |
| `Custom_Parameter` | | カスタムパラメータ。 |
| `update` | | 更新。 |

## ベンダーのドキュメント

* [Google 同意モードについて](https://support.google.com/analytics/answer/9976101?hl=en)
* [Google Developers：同意に基づいてタグの動作を調整する](https://developers.google.com/gtagjs/devguide/consent)