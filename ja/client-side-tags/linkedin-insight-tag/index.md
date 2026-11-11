---
title: LinkedIn Insightタグ構成ガイド
description: この記事では、Tag ManagementアカウントでLinkedIn Insightタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/linkedin-insight-tag/
---
## タグに関するヒント

* マッピングを使用して標準構成を上書きします。
* 複数のパートナーIDを指定する場合は、**Partner ID**フィールドにカンマ区切りのリストを入力します。
* 次のEコマース変数を使用します。
    * 注文ID（`_corder`）
    * 注文合計（`_ctotal`）
    * 注文通貨（`_ccurrency`）
    * 顧客ID（`_ccustid`）

## タグの構成
 
新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **Partner ID**：LinkedInアカウントのパートナーID。
* **Generate Event ID**：LinkedInの各トラッキングイベントに対してイベントIDを自動的に生成します。デフォルト値は`true`です。

### Web向けConversions API

LinkedIn Conversions API for Webをサポートするために、タグはトラッキング対象のイベントごとに一意のイベントIDを生成し、LinkedIn Conversionsコネクタで使用できるようにEvent Streamingへ送信します。Webベースとサーバーベースの統合を同期するために、コネクタでイベントIDをマッピングできます。この機能を使用するには、[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が有効になっている必要があります。

タグは、次の命名規則を使用して新しいイベント属性を送信します。

```nohl
linkedin_event_id_{CONVERSION_EVENT}_{TAG_UID}
```

例：`window.lintrk('track', { conversion_id: 11563522 });`

[LinkedIn Conversionsコネクタ構成ガイド](https://docs.tealium.com/linkedin-conversions-connector/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明|
|---| ---|
| `partner_id`| パートナーID|
| `event_id` | イベントID |
| `linkedin.custom_channel_id` | カスタムチャネル |
| `linkedin.custom_group_id` | カスタムグループID |
| `linkedin.custom_user_id` | カスタムユーザーID |
| `linkedin.zoom_info_id` | Zoom Info ID |
| `linkedin.title` | タイトル |
| `linkedin.domain` | ドメイン |
| `linkedin.company` | 会社 |
| `linkedin.gender` | 性別 |
| `linkedin.location` | 所在地 |
| `linkedin.education` | 学歴 |
| `linkedin.email_sha256` | メールアドレスのSHA256 |
| `linkedin.email_sha512` | メールアドレスのSHA512 |
| `linkedin.raw_data` | 生データ |
| `linkedin.raw_data_overwrite` | 生データの上書き |
| `linkedin.encrypted_data` | 暗号化データ |
| `linkedin.partner_data` | パートナーデータ |
| `linkedin.sic_codes` | SICコード |
| `linkedin.employee_range` | 従業員数の範囲 |
| `linkedin.default_keywords` | デフォルトキーワード |
| `linkedin.async_target` | 非同期ターゲット |
| `linkedin.use_iframe` | iframeを使用 |
| `linkedin.use_callback` | コールバックを使用 |
| `linkedin.test_url` | テストURL |
| `conversionId` | コンバージョンID |