---
title: RTB House リターゲティングタグ構成ガイド
description: この記事では、RTB House リターゲティングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rtb-house-tag/
---
## タグのヒント

* 次の [E-Commerce extension]() パラメータをサポートしています:
    * オファーID (`_cprod`)
    * コンバージョンID (`_corder`)
    * コンバージョン値 (`_ctotal`)
    * カテゴリID (`_ccat`)
* UIDは匿名化されたユーザーIDであるべきです（例えば、ユーザーのメールアドレスやログインに基づいています）。提供されていない場合、タグは `unknown` の値を送信します。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際に、以下の構成を構成します:

* **タグハッシュ**: あなたのRTB House タグハッシュ。
* **リージョンサブドメイン**: あなたのRTB House リージョンサブドメイン。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです:

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `eventType`  | 文字列 | イベントタイプ |
|  `size`  | 文字列 | サイズ |
|  `uid`  | 文字列 | UID |

### E-Commerce

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `offerId`  | 文字列 | オファーID |
|  `offerIds` (Overrides `_cprod`)  | 文字列の配列 | オファーID群 |
|  `conversionClass`  | 文字列 | コンバージョンクラス |
|  `conversionSubClass`  | 文字列 | コンバージョンサブクラス |
|  `conversionId` (Overrides `_corder`)  | 文字列 | コンバージョンID |
|  `conversionValue` (Overrides `_ctotal`)  | 文字列 | コンバージョン値 |
| `categoryId`  | 文字列 | カテゴリID |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `home` | ホーム | 
| `category` | カテゴリ | 
| `sales` | セールまたはプロモーション | 
|  `newoffers` | 新商品 |
| `offer` | 商品 | 
| `wishlist` | お気に入りリストまたはお気に入りに追加 | 
| `size` | 商品サイズ選択 | 
| `offlinecheck` | オフラインストアチェック | 
|  `listing` | 検索結果 |
| `basketadd` | ショッピングカート - カートに追加 | 
| `basketstatus` | ショッピングカート - ステータス | 
| `startorder` | 注文プロセス開始 | 
|  `conversion` |注文確認 |
|  `custom` |カスタム |

### イベント固有のパラメータ

このカテゴリを使用して、選択したイベントのみのパラメータをマッピングします。

イベントをマッピングするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。
