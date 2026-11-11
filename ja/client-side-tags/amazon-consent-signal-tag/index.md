---
title: Amazon Consent Signalタグ構成ガイド
description: この記事では、タグ管理アカウントでAmazon Consent Signalタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-consent-signal-tag/
---
## タグに関するヒント

* [Amazon：同意管理プラットフォーム向けAmazon Consent Signal（ACS）統合ガイド](https://advertising.amazon.co.uk/help/GKJQ7E8SE9BRG73Q/)

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Tealium同意Cookieから自動的に読み取る**：有効にすると、タグがTealium Consent Managerと統合され、Tealium同意Cookieから同意ステータスを読み取り、それに応じて次の変数を構成します。
    * **広告保存**：Amazon Adsが広告目的でブラウザー内の広告関連保存（Cookie、localStorage、類似のID）を使用できるかどうかを指定します。**Tealium同意Cookieから自動的に読み取る**が有効で、訪問が部分的に同意した場合、Tealiumは選択した同意カテゴリを確認します。訪問がこのカテゴリに同意している場合、`amzn_ad_storage`は`granted`に構成されます。訪問が完全に同意した場合、`amzn_ad_storage`は常に`granted`に構成されます。デフォルト値は`denied`です。
    * **広告ユーザーデータ**：Amazon Adsが、ターゲティング、測定、照合のためにユーザーの広告関連データ（識別子、行動）を使用できるかどうかを指定します。**Tealium同意Cookieから自動的に読み取る**が有効で、訪問が部分的に同意した場合、Tealiumは選択した同意カテゴリを確認します。訪問がこのカテゴリに同意している場合、`amzn_user_data`は`granted`に構成されます。訪問が完全に同意した場合、`amzn_user_data`は常に`granted`に構成されます。デフォルト値は`denied`です。

**広告保存**および**広告ユーザーデータ**の構成では、次の同意カテゴリを使用できます。

* `Denied`：同意が拒否されています。
* `Granted`：同意が付与されています。
* `Analytics`：分析に対する同意が付与されています。
* `Affiliates`：アフィリエイトに対する同意が付与されています。
* `Display Ads`：ディスプレイ広告に対する同意が付与されています。
* `Search`：検索に対する同意が付与されています。
* `Email`：メールに対する同意が付与されています。
* `Personalization`：パーソナライゼーションに対する同意が付与されています。
* `Social`：ソーシャルに対する同意が付与されています。
* `Big Data`：ビッグデータに対する同意が付与されています。
* `Misc`：その他の目的に対する同意が付与されています。
* `Cookie Match`：Cookieマッチングに対する同意が付与されています。
* `CDP`：カスタマーデータプラットフォームに対する同意が付与されています。
* `Mobile`：モバイルに対する同意が付与されています。
* `Engagement`：エンゲージメントに対する同意が付与されています。
* `Monitoring`：モニタリングに対する同意が付与されています。
* `CRM`：顧客関係管理に対する同意が付与されています。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `tealium_consent` | ブール値 | Tealium同意Cookieから同意情報を読み取るかどうか。 |
| `countryCode` | 文字列 | 国コード。 |
| `amzn_ad_storage` | 文字列 | 広告保存への同意。 |
| `amzn_user_data` | 文字列 | 広告ユーザーデータ。 |