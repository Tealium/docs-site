---
title: Salesforce Marketing Cloud (ExactTarget) タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSalesforce Marketing Cloud (ExactTarget) タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salesforce-marketing-cloud-exacttarget/
---
Salesforce Marketing Cloud（旧ExactTarget）は、企業と顧客を全く新しい方法でつなぐ1対1の顧客旅行のプラットフォームです。

## タグのヒント

* 以下のE-Commerce拡張パラメータをサポートしています：
    * 注文ID
    * 製品IDのリスト
    * 価格のリスト
* このタグをランディングページとコンバージョンページに追加します。
* 自動的に訪問情報をクッキーに保存し、確認ページで送信します。
* マッピングを使用して、標準の構成値またはE-Commerce拡張値を動的に上書きします。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います：

* **アカウント**: ExactTargetメンバーID。ランディングページのクエリ文字列の`mid = param`と一致する必要があります。
* **コンバージョンページID**: 複数のコンバージョンページを区別するための一意の番号。
* **コンバージョンページエイリアス**: このコンバージョンページに対してExactTargetで表示される名前。
* **コンバージョンページ順序**: コンバージョンページがExactTargetに表示される順序を表す番号。
* **S4を使用する**: デフォルトは**いいえ**です。ピクセル位置`click.s4.exacttarget.com`を使用するには**はい**に構成します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
|  `account` |アカウントID  |
|  `convid` |コンバージョンリンクID  |
|  `alias` |リンクエイリアス  |
|  `displayorder` |表示順序  |
|   `s4` |S4を使用する |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
|  `order_id` (`_corder`を上書き) |注文ID  |
| `product_id` (`_cprod`を上書き)  | 製品IDのリスト  |
|  `product_unit_price` (`_cprice`を上書き)  | 価格のリスト |

