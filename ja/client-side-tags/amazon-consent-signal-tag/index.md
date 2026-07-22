---
title: Amazon Consent Signal タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Amazon Consent Signal タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-consent-signal-tag/
---
## タグのヒント

* [Amazon: コンセント管理プラットフォーム向け Amazon Consent Signal (ACS) 統合ガイド](https://advertising.amazon.co.uk/help/GKJQ7E8SE9BRG73Q/)

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します：

* **Tealium Consent Cookieから自動的に読み取り**: 有効にすると、タグはTealium Consent Managerと統合し、Tealium Consent Cookieから同意状態を読み取り、以下の変数をそれに応じて構成します：
    * **Ad Storage**: Amazon Adsが広告目的でブラウザの広告関連保存（クッキー、localStorage、類似のID）を使用することが許可されているかどうか。**Tealium Consent Cookieから自動的に読み取り**が有効で、訪問が部分的に同意した場合、Tealiumは選択した同意カテゴリをチェックします。訪問がこのカテゴリに同意している場合、`amzn_ad_storage`は`granted`に構成されます。訪問が完全に同意した場合、`amzn_ad_storage`は常に`granted`に構成されます。デフォルト値は`denied`です。
    * **Ad User Data**: Amazon Adsがユーザーの広告関連データ（識別子、行動）をターゲティング、測定、マッチングのために使用することが許可されているかどうか。**Tealium Consent Cookieから自動的に読み取り**が有効で、訪問が部分的に同意した場合、Tealiumは選択した同意カテゴリをチェックします。訪問がこのカテゴリに同意している場合、`amzn_user_data`は`granted`に構成されます。訪問が完全に同意した場合、`amzn_user_data`は常に`granted`に構成されます。デフォルト値は`denied`です。

**Ad Storage**および**Ad User Data**構成のために利用可能な同意カテゴリは以下の通りです：

* `Denied`: 同意が拒否されました。
* `Granted`: 同意が与えられました。
* `Analytics`: 分析のために同意が与えられました。
* `Affiliates`: アフィリエイトのために同意が与えられました。
* `Display Ads`: ディスプレイ広告のために同意が与えられました。
* `Search`: 検索のために同意が与えられました。
* `Email`: メールのために同意が与えられました。
* `Personalization`: パーソナライゼーションのために同意が与えられました。
* `Social`: ソーシャルのために同意が与えられました。
* `Big Data`: ビッグデータのために同意が与えられました。
* `Misc`: 雑多な目的のために同意が与えられました。
* `Cookie Match`: クッキーマッチングのために同意が与えられました。
* `CDP`: 顧客データプラットフォームのために同意が与えられました。
* `Mobile`: モバイルのために同意が与えられました。
* `Engagement`: エンゲージメントのために同意が与えられました。
* `Monitoring`: モニタリングのために同意が与えられました。
* `CRM`: 顧客関係管理のために同意が与えられました。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `tealium_consent` | Boolean | Tealium Consent Cookieから同意情報を読み取るかどうか。 |
| `countryCode` | String | 国コード。 |
| `amzn_ad_storage` | String | 広告保存の同意。 |
| `amzn_user_data` | String | ユーザー広告データの同意。 |
