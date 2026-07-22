---
title: Skai（旧称Kenshoo）タグ
description: この記事では、Skai（旧称Kenshoo）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/skai-tag/
---
## タグのヒント

* マッピングを通じてタグの構成を動的に上書きまたは構成することができます。
* コンバージョントラッキングをトリガーするには、`cid`、`conversion_code`、および`conversionType`を構成する必要があります。`conversionType`パラメータは、構成されていない場合デフォルトで'conv'になります。
* カスタムパラメータを追跡するには、カスタムデスティネーションにマッピングする必要があります。
* 以下のEコマース拡張パラメータをサポートします：
    * 注文ID（`_corder`）
    * 注文小計（`_csubtotal`）
    * 注文通貨（`_ccurrency`）
    * 注文クーポンコード（`_cpromo`）

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **顧客ID**：あなたのSkai顧客ID。
* **コンバージョンコード**：Skaiが提供するコンバージョンコード。
* **コンバージョンタイプ**：コンバージョンタイプ。構成されていない場合はデフォルトで'conv'になります。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応するデスティネーション変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `cid` | 顧客ID |
| `conversion_code` | コンバージョンコード |
| `conversionType` | コンバージョンタイプ |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | 注文ID（`_corder`を上書き） |
| `order_subtotal` | 小計（`_csubtotal`を上書き） |
| `order_currency` | 通貨（`_ccurrency`を上書き） |
| `order_coupon_code` | プロモコード（`_cpromo`を上書き） |

