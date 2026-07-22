---
title: Quantum Metric タグ構成ガイド
description: この記事では、Quantum Metric タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quantum-metric-tag/
---

<blockquote>
`utag` バージョン4.50以降を使用する場合、`utag.js` の [`always_set_v_id` 構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) を `true` に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50 リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) および [utag 4.50+ へのアップグレード時の tealium_visitor_id に関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-) を参照してください。
</blockquote>


## タグのヒント

* Tealium アカウントと Tealium プロファイルが空白の場合、現在のアカウントとプロファイルが自動的に入力されます。**Send Replay URL** を使用する場合のみ適用されます。
* **Time Stamp** のデフォルト値は `30days` です。
* このタグを AudienceStream と統合する方法については、[Tealium + Quantum Metric 統合ガイド](https://docs.tealium.com/tealium-quantum-metric-integration-guide/) を参照してください。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/) を参照してください。

タグを追加する際に、以下の構成を構成します：

* **Subscription Name**: Quantum Metric 担当者から提供されます。
* **Send Replay URL**: Quantum Metric リプレイ URL をサーバーサイド属性 `quantum_metric_replay_url` として利用可能にするために `True` を選択します。
* **Time Stamp**: リプレイ URL のタイムスタンプ。**Send Replay URL** を使用する場合のみ適用されます。デフォルト値は `30days` です。
* **Tealium Account**: オプション。サーバーサイドリクエスト用に `tealium_account` を上書きします。
* **Tealium Profile**: オプション。サーバーサイドリクエスト用に `tealium_profile` を上書きします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/) を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/) を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `subscription_name` | サブスクリプション名。 |
| `tealium_account` | Tealium アカウント。 |
| `tealium_profile` | Tealium プロファイル。 |

### リプレイ URL パラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `send_replay_url` | Boolean | リプレイを送信するかどうか。値は `true` または `false` です。 |
| `autoreplay` | Boolean | 自動リプレイフラグ。値は `true` または `false` です。|
| `replaysecond` | String | リプレイセッションの再生ヘッドを構成する秒数。 |
| `qmUserCookie` |  String| Quantum metric ユーザークッキーの上書き。 |
| `qmSessionCookie` | String | Quantum metric セッションクッキーの上書き。 |
| `ts` |  String | リプレイ URL のタイムスタンプ。 |

