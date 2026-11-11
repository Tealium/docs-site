---
title: Utiqタグ構成ガイド
description: この記事では、Utiqタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/utiq-tag/
---
## タグに関するヒント

* マッピングを使用して、タグ構成を上書きまたは動的に構成します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **HOST**：クライアントのドメイン。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `host` | 文字列 | Utiqタグがデプロイされているドメイン名。 |
| `customUtiqHost` | 文字列 | カスタムホスト。 |
| `consentManagerOrigin` | 文字列 | 同意マネージャーのオリジン。 |
| `consentManagerDataLayer` | 文字列 | 同意マネージャーのデータレイヤー。 |

### リスナー

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `listener_ids_available` | ブール値 | `Martechpass`と`Adtechpass`が利用可能になったときに`utiq_ids_available`イベントをトリガーする場合は、これを`true`に構成します。このイベントは、データレイヤー変数`utiq_mtid`、`utiq_category`に値を渡します。 |
| `listener_consent_update_finished` | ブール値 | 同意の更新が完了したときに`utiq_consent_update_finished`イベントをトリガーする場合は、これを`true`に構成します。このイベントは、データレイヤー変数`utiq_consent_granted`に値を渡します。 |
| `listener_consent_changing` | ブール値 | 同意ステータスをパラメーターに保持されているステータスへ変更するためのシグナルをUtiqがブラウザー（またはクライアント）から受信したときに、`utiq_consent_changing`イベントをトリガーする場合は、これを`true`に構成します。このイベントは、データレイヤー変数`utiq_consent_granted`に値を渡します。 |
| `listener_initialised` | ブール値 | ページの読み込みまたはナビゲーションのたびにUtiqが完全に初期化されたとき、`utiq_initialised`イベントをトリガーする場合は、これを`true`に構成します。 |
| `listener_eligibility_checked` | ブール値 | 現在のクライアントに対してユーザーの適格性チェックが実行されたときに`utiq_eligibility_checked`イベントをトリガーする場合は、これを`true`に構成します。このイベントは、データレイヤー変数`utiq_is_eligible`に値を渡します。 |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `handleConsentChange` | 同意を変更します。 |
| `showConsentManager` | 同意マネージャーを表示します。 |
| `setVerboseLoggingLevel` | 詳細ログを有効にします。 |
| `resetLoggingLevel` | 詳細ログを無効にします。 |
| カスタム | カスタムイベント。 |

### イベント固有のパラメーター

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `handleConsentChange` | 同意を変更します。 |
| `showConsentManager` | 同意マネージャーを表示します。 |
| `setVerboseLoggingLevel` | 詳細ログを有効にします。 |
| `resetLoggingLevel` | 詳細ログを無効にします。 |
| カスタム | カスタムイベント。 |