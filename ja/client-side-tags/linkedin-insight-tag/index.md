---
title: LinkedIn Insightタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでLinkedIn Insightタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/linkedin-insight-tag/
---
## タグのヒント

* マッピングを通じて標準構成を上書きします。
* 複数のパートナーIDの場合、**パートナーID**フィールドにカンマ区切りのリストを入力します。
* 次のEコマース変数を使用します：
    * 注文ID（`_corder`）
    * 注文合計（`_ctotal`）
    * 注文通貨（`_ccurrency`）
    * 顧客ID（`_ccustid`）

## タグの構成
 
タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、を参照してください。

タグを追加した後、以下の構成を構成します：

* **パートナーID**：LinkedInアカウントのパートナーID。
* **イベントIDの生成**：LinkedInの追跡イベントごとに自動的にイベントIDを生成します。デフォルト値は`true`です。

### Web用コンバージョンAPI

Web用LinkedInコンバージョンAPIをサポートするために、タグは各イベントに対してユニークなイベントIDを生成し、それをTealium EventStreamに送信してLinkedInコンバージョンコネクタで使用します。このイベントIDはコネクタでマッピング可能で、Webベースのサーバーベースの統合を同期させることができます。この機能にはアクティブな[Tealium Collectタグ]()が必要です。

タグは次の命名規則を使用して新しいイベント属性を発行します：

```nohl
linkedin_event_id_{CONVERSION_EVENT}_{TAG_UID}
```

例：`window.lintrk(&#39;track&#39;, { conversion_id: 11563522 });`

[LinkedInコンバージョンコネクタ構成ガイド]()を参照してください。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明|
|---| ---|
| `partner_id`| パートナーID|
| `event_id` | イベントID |
| `linkedin.custom_channel_id` | カスタムチャネル |
| `linkedin.custom_group_id` | カスタムグループID |
| `linkedin.custom_user_id` | カスタムユーザーID |
| `linkedin.zoom_info_id` | Zoom情報ID |
| `linkedin.title` | タイトル |
| `linkedin.domain` | ドメイン |
| `linkedin.company` | 会社 |
| `linkedin.gender` | 性別 |
| `linkedin.location` | 場所 |
| `linkedin.education` | 教育 |
| `linkedin.email_sha256` | Email SHA256 |
| `linkedin.email_sha512` | Email SHA512 |
| `linkedin.raw_data` | 生データ |
| `linkedin.raw_data_overwrite` | 生データ上書き |
| `linkedin.encrypted_data` | 暗号化データ |
| `linkedin.partner_data` | パートナーデータ |
| `linkedin.sic_codes` | Sicコード |
| `linkedin.employee_range` | 従業員範囲 |
| `linkedin.default_keywords` | デフォルトキーワード |
| `linkedin.async_target` | 非同期ターゲット |
| `linkedin.use_iframe` | Iframe使用 |
| `linkedin.use_callback` | コールバック使用 |
| `linkedin.test_url` | テストURL |
| `conversionId` | コンバージョンID |

