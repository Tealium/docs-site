---
title: Salesforce Marketing Cloud Personalizationタグ
description: この記事では、Salesforce Marketing Cloud Personalizationタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salesforce-marketing-cloud-personalization-tag/
---
## タグに関するヒント

* マッピングを使用して、標準構成値を動的に上書きできます。
* 次のEコマース拡張パラメータをサポートしています。
  * 顧客ID（`_ccustid`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **アカウント**：Salesforce MCPのアカウント名。
* **データセットID**：イベントトラッキングに使用するデータセットID。

アカウント名とデータセットIDは、SalesforceビーコンURLで確認できます。たとえば、`//cdn.evgnet.com/beacon/{{MY_ACCOUNT}}/{{MY_DATASET}}/scripts/evergage.min.js`では、`{{MY_ACCOUNT}}`がアカウント名、`{{MY_DATASET}}`がデータセットIDです。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `acct` | アカウントID。 |
| `dataset` | データセットID。 |
| `company_name` | 会社名。 |
| `customer_id` | 顧客ID（`_ccustid`を上書きします）。 |

### カスタム

| 変数 | 説明 |
|:---------|:------------|
| `custom.request.myvar` | カスタムリクエストフィールド。 |
| `custom.page.myvar` | カスタムページフィールド。 |
| `custom.visit.myvar` | カスタム訪問フィールド。 |