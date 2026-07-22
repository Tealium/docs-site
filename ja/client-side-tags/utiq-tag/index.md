---
title: Utiqタグ構成ガイド
description: この記事では、Utiqタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/utiq-tag/
---
## タグのヒント

* マッピングを使用して、タグの構成をオーバーライドまたは動的に構成します。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **HOST**: クライアントのドメイン。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `host`  | 文字列 | Utiqタグがデプロイされるドメイン名。 |
| `customUtiqHost`  | 文字列 | カスタムホスト。 |
| `consentManagerOrigin`  | 文字列 | 同意管理者の起源。 |
| `consentManagerDataLayer`  | 文字列 | 同意管理者データレイヤー。 |

### リスナー

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `listener_ids_available` | 真偽値 | `Martechpass`と`Adtechpass`が利用可能になったときに`utiq_ids_available`イベントをトリガーする場合は`true`に構成します。このイベントは次のデータレイヤー変数にフィードされます：`utiq_mtid`, `utiq_category`。 |
| `listener_consent_update_finished` | 真偽値 | 同意更新が完了したときに`utiq_consent_update_finished`イベントをトリガーする場合は`true`に構成します。このイベントは次のデータレイヤー変数にフィードされます：`utiq_consent_granted`。 |
| `listener_consent_changing` | 真偽値 | Utiqがブラウザ（またはクライアント）からの信号を受け取り、パラメーターで保持されている同意状態に変更する場合に`utiq_consent_changing`イベントをトリガーする場合は`true`に構成します。このイベントは次のデータレイヤー変数にフィードされます：`utiq_consent_granted`。 |
| `listener_initialised` | 真偽値 | Utiqがすべてのページの読み込みまたはナビゲーションで完全に初期化されたときに`utiq_initialised`イベントをトリガーする場合は`true`に構成します。 |
| `listener_eligibility_checked` | 真偽値 | 現在のクライアントに対してユーザーの適格性チェック情報が実行されたときに`utiq_eligibility_checked`イベントをトリガーする場合は`true`に構成します。このイベントは次のデータレイヤー変数にフィードされます：`utiq_is_eligible`。 |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

| 変数 | 説明 |
|:---------|:------------|
| `handleConsentChange` | 同意の変更。 |
| `showConsentManager` | 同意管理者の表示。 |
| `setVerboseLoggingLevel` | 詳細なログ記録を有効にする。 |
| `resetLoggingLevel` | 詳細なログ記録を無効にする。 |
| カスタム | カスタムイベント。 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

| 変数 | 説明 |
|:---------|:------------|
| `handleConsentChange` | 同意の変更。 |
| `showConsentManager` | 同意管理者の表示。 |
| `setVerboseLoggingLevel` | 詳細なログ記録を有効にする。 |
| `resetLoggingLevel` | 詳細なログ記録を無効にする。 |
| カスタム | カスタムイベント。 |
