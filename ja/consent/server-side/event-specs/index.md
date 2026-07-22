---
title: 同意変更イベント仕様
description: 同意イベントは、訪問がTealium同意マネージャーとのやり取りを識別します。
url: https://docs.tealium.com/ja/consent/server-side/event-specs/
---
これらのイベントは、**プライバシー**カテゴリーの下でイベント仕様として見つけることができます。

同意イベントは監査目的で使用され、サーバーサイドで実行できるコネクタを制御するために使用されます。

詳細については、以下を参照してください：

* [オプトアウトプライバシーバナーとポップアップ](https://docs.tealium.com/about-ccpa-privacy-banner-and-popup/)
* [同意管理：イベントログ](https://docs.tealium.com/event-logging-for-consent-management/)

## 同意変更イベント

以下の同意イベントはこれらのパラメータを使用します：

|名前| 説明| 例|
|---| ---| ---|
|`policy`| 同意の文脈で、通常は訪問に同意を得る際に提示される条件に特有です。値: `gdpr`（オプトイン）、`ccpa`（オプトアウト） | `gdpr`|
|`consent_categories`| 承認されたトラッキングおよびデータ収集の種類のカテゴリ名。| `["affiliates", "social"]`|
|`do_not_sell`| 個人情報の販売をブロックするタグIDのリスト。| `[1, 42, 51]`|

### `grant_full_consent`

`grant_full_consent` イベントは、訪問がトラッキングおよびデータ収集に完全に同意したことを示します。

#### オプトイン例

```json
{
    "tealium_event"      : "grant_full_consent",
    "policy"             : "gdpr",
    "consent_categories" : [
        "analytics",
        "affiliates",
        "display_ads",
        "search",
        "email",
        "personalization",
        "social",
        "big_data",
        "misc",
        "cookiematch",
        "cdp",
        "mobile",
        "engagement",
        "monitoring",
        "crm"
    ],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

#### オプトアウト例（明示的な販売許可の決定）

```json
{
    "tealium_event"      : "grant_full_consent",
    "policy"             : "ccpa",
    "consent_categories" : [],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

### `grant_partial_consent`

`grant_partial_consent` イベントは、訪問が部分的にのみ同意を与えたことを示します。**同意構成**インターフェースから与えられた同意には、ユーザーが同意したカテゴリ名のリストが付随します。**オプトアウト同意マネージャー**インターフェースから与えられた同意には、個人情報の販売をブロックするタグのIDリストが付随します。

#### オプトイン例

```json
{
    "tealium_event"      : "grant_partial_consent",
    "policy"             : "gdpr",
    "consent_categories" : ["affiliates", "social"],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

#### オプトアウト例（販売しない決定）

```json
{
    "tealium_event"      : "decline_consent",
    "policy"             : "gdpr",
    "consent_categories" : [],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

### `decline_consent`

この `decline_consent` イベントは、訪問がトラッキングおよびデータ収集への同意を拒否したことを示します。

#### オプトイン例

```json
{
    "tealium_event"      : "decline_consent",
    "policy"             : "gdpr",
    "consent_categories" : [],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```
