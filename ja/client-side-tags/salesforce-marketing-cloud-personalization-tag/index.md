---
title: Salesforce Marketing Cloud パーソナライゼーションタグ
description: この記事では、Salesforce Marketing Cloud パーソナライゼーションタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salesforce-marketing-cloud-personalization-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* 次の E-Commerce 拡張パラメータをサポートします：
  * 顧客ID (`_ccustid`)

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **アカウント**: あなたのSalesforce MCPアカウント名。
* **データセットID**: イベントトラッキング用のデータセットID。

アカウント名とデータセットIDは、SalesforceビーコンURLで見つけることができます。例えば、`{{MY_ACCOUNT}}`はアカウント名で、`{{MY_DATASET}}`はデータセットIDです。URLは`//cdn.evgnet.com/beacon/{{MY_ACCOUNT}}/{{MY_DATASET}}/scripts/evergage.min.js`です。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `acct` | アカウントID。 |
| `dataset` | データセットID。 |
| `company_name` | 会社名。 |
| `customer_id` | 顧客ID（`_ccustid`を上書き）。 |

### カスタム

| 変数 | 説明 |
|:---------|:------------|
| `custom.request.myvar` | カスタムリクエストフィールド。 |
| `custom.page.myvar` | カスタムページフィールド。 |
| `custom.visit.myvar` | カスタム訪問フィールド。 |