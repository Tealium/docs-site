---
title: RTB Houseリターゲティングタグ構成ガイド
description: この記事では、RTB Houseリターゲティングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rtb-house-tag/
---
## タグに関するヒント

* 以下の[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)パラメータをサポートしています。
    * オファーID（`_cprod`）
    * コンバージョンID（`_corder`）
    * コンバージョン値（`_ctotal`）
    * カテゴリID（`_ccat`）
* UIDには、匿名化されたユーザーID（ユーザーのメールアドレスやログイン情報に基づくIDなど）を使用してください。指定されていない場合、タグは値`unknown`を送信します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下を構成します。

* **タグ付けハッシュ**：RTB Houseのタグ付けハッシュ。
* **リージョンサブドメイン**：RTB Houseのリージョンサブドメイン。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `eventType` | 文字列 | イベントタイプ |
| `size` | 文字列 | サイズ |
| `uid` | 文字列 | UID |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `offerId` | 文字列 | オファーID |
| `offerIds`（`_cprod`を上書き） | 文字列の配列 | オファーID |
| `conversionClass` | 文字列 | コンバージョンクラス |
| `conversionSubClass` | 文字列 | コンバージョンサブクラス |
| `conversionId`（`_corder`を上書き） | 文字列 | コンバージョンID |
| `conversionValue`（`_ctotal`を上書き） | 文字列 | コンバージョン値 |
| `categoryId` | 文字列 | カテゴリID |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `home` | ホーム |
| `category` | カテゴリ |
| `sales` | セールまたはプロモーション |
| `newoffers` | 新製品 |
| `offer` | 製品 |
| `wishlist` | ウィッシュリストまたはお気に入りに追加 |
| `size` | 製品サイズの選択 |
| `offlinecheck` | 実店舗の確認 |
| `listing` | 検索結果 |
| `basketadd` | ショッピングカート - カートに追加 |
| `basketstatus` | ショッピングカート - ステータス |
| `startorder` | 注文プロセスの開始 |
| `conversion` | 注文確認 |
| `custom` | カスタム |

### イベント固有のパラメータ

このカテゴリを使用して、選択したイベントにのみパラメータをマッピングします。

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。