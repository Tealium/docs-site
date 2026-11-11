---
title: Quantum Metricタグ構成ガイド
description: この記事では、Quantum Metricタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quantum-metric-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に必要な訪問IDが利用可能になります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降にアップグレードする際のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* **Tealium Account**と**Tealium Profile**を空白のままにすると、現在のアカウントとプロファイルが自動的に入力されます。これは、**Send Replay URL**を使用する場合にのみ適用されます。
* **Time Stamp**のデフォルト値は`30days`です。
* このタグをCustomer Data Platform（CDP）と統合する方法については、[TealiumとQuantum Metricの統合ガイド](https://docs.tealium.com/tealium-quantum-metric-integration-guide/)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Subscription Name**：Quantum Metricの担当者から提供されます。
* **Send Replay URL**：Quantum MetricのリプレイURLをサーバーサイド属性`quantum_metric_replay_url`として使用できるようにするには、`True`を選択します。
* **Time Stamp**：リプレイURLのタイムスタンプです。**Send Replay URL**を使用する場合にのみ適用されます。デフォルト値は`30days`です。
* **Tealium Account**：（任意）サーバーサイドリクエストに使用される`tealium_account`を上書きします。
* **Tealium Profile**：（任意）サーバーサイドリクエストに使用される`tealium_profile`を上書きします。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `subscription_name` | サブスクリプション名。 |
| `tealium_account` | Tealiumアカウント。 |
| `tealium_profile` | Tealiumプロファイル。 |

### リプレイURLパラメータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `send_replay_url` | ブール値 | リプレイを送信するかどうか。値には`true`または`false`を指定できます。 |
| `autoreplay` | ブール値 | 自動リプレイフラグ。値には`true`または`false`を指定できます。|
| `replaysecond` | 文字列 | リプレイセッション内の再生位置として構成する秒数。 |
| `qmUserCookie` | 文字列 | Quantum MetricのユーザーCookieを上書きします。 |
| `qmSessionCookie` | 文字列 | Quantum MetricのセッションCookieを上書きします。 |
| `ts` | 文字列 | リプレイURLのタイムスタンプ。 |