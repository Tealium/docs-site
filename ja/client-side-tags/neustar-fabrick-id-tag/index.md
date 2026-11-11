---
title: Neustar Fabrick IDタグ構成ガイド
description: この記事では、タグ管理アカウントでNeustar Fabrick IDタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/neustar-fabrick-id-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


## タグに関するヒント

* 空欄のままにすると、Tealiumアカウントとプロファイルが自動的に入力されます
* 次の属性は、`neustar_fabrickId_sync`を通じてTealiumのサーバーサイドに送信されます。
  * `fabrickId`
  * `visitor_id`
  * `element_one`（任意）

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **APIキー**：（必須）Neustarから提供されたAPIキー。
* **FabrickIdの期間（日数）**：`fabrickId`が変更される頻度。デフォルトは7日です。
* **Tealiumアカウント**：Tealiumアカウント。
* **Tealiumプロファイル**：Tealiumプロファイル。
* **データソースキー**：（必須）Tealiumサーバーサイドのデータソースキー。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| ベースURL（`base_url`） | 文字列 |
| イベントURL（`event_url`） | 文字列 |
| APIキー（`apiKey`） | 文字列 |
| FabrickIdの期間（日数）（`daysSyncPeriod`） | 数値 |
| Tealiumアカウント（`tealium_account`） | 文字列 |
| Tealiumプロファイル（`tealium_profile`） | 文字列 |
| データソースキー（`tealium_datasource`） | 文字列 |
| ハッシュ化されたメールアドレス（`e`） | 文字列 |
| E.164規格のハッシュ化された電話番号（`p`） | 文字列 |
| IPv4アドレス（`raw` i4） | 文字列 |
| IPv6アドレス（`raw` i6） | 文字列 |
| モバイル広告ID（`m`） | 文字列 |
| 広告識別子（`ia`） | 文字列 |
| IFAのソース（`ifa_type`） | 文字列 |
| ユーザーをトラッキングできるかどうかを示す値（`lmt`） | 文字列 |
| パートナーまたは広告主のファーストパーティユーザーID（`1pd`） | 文字列 |