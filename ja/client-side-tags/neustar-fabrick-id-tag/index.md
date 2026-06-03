---
title: Neustar Fabrick IDタグ構成ガイド
description: この記事では、iQタグ管理（TiQ）アカウントでNeustar Fabrick IDタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/neustar-fabrick-id-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## タグのヒント

* 空白の場合、Tealiumアカウントとプロファイルは自動的に入力されます
* 次の属性は`neustar_fabrickId_sync`を通じてTealiumサーバーサイドに送信されます：
  * `fabrickId`
  * `visitor_id`
  * `element_one` (オプション)

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **APIキー**：必須。Neustarが提供するAPIキー。
* **FabrickId Timespan Days**：`fabrickId`が変更される頻度。デフォルトは7日です。
* **Tealiumアカウント**：あなたのTealiumアカウント。
* **Tealiumプロファイル**：あなたのTealiumプロファイル。
* **データソースキー**：必須。Tealiumサーバーサイドからのデータソースキー。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| Base Url (`base_url`) | 文字列 |
| Event Url (`event_url`) | 文字列 |
| Api Key (`apiKey`) | 文字列 |
| FabrickId Timespan Days (`daysSyncPeriod`) | 数値 |
| Tealium Account (`tealium_account`) | 文字列 |
| Tealium Profile (`tealium_profile`) | 文字列 |
| Data Source Key (`tealium_datasource`) | 文字列 |
| ハッシュ化されたメールアドレス (`e`) | 文字列 |
| E.164標準のハッシュ化された電話番号 (`p`) | 文字列 |
| IPv4アドレス (`raw` i4) | 文字列 |
| IPv6アドレス (`raw` i6) | 文字列 |
| モバイル広告ID (`m`) | 文字列 |
| 広告用識別子 (`ia`) | 文字列 |
| IFAのソースを示す (`ifa_type`) | 文字列 |
| ユーザーが追跡可能かどうかを示す (`lmt`) | 文字列 |
| パートナーまたは広告主の第一者ユーザーID (`1pd`) | 文字列 |

