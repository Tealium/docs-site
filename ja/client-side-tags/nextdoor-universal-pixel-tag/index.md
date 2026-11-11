---
title: NextDoorユニバーサルピクセル
description: この記事では、Nextdoorユニバーサルピクセルタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/nextdoor-universal-pixel-tag/
---
Nextdoorユニバーサルトラッキングピクセルを使用すると、Webサイト全体で標準化されたイベントベースのトラッキングが可能になり、Nextdoorの最新のアトリビューションモデルと最適化モデルを利用できます。

## タグに関するヒント

* マッピングを使用して、標準パラメータを上書きします。
* Eコマース拡張機能のパラメータをサポートしています。
* 制限付きデータ使用により、広告主はNextdoorのシステムでデータがどのように使用されるかを管理でき、米国各州のプライバシー規制へのコンプライアンス対応をエンリッチメントできます。広告主が制限付きデータ使用を有効にすると、Nextdoorは州固有の規約に従い、特定の州に居住するユーザーの個人データの使用を制限します。これにより、キャンペーンのパフォーマンスが低下し、リターゲティング機能や測定機能が制限される場合があります。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下を構成します。

* **ピクセルID**：NextDoorピクセルID。
* **ページビューの自動構成**：ページビュー用のトリガーを自動的に作成します。
* **購入イベントの自動構成**：購入イベント用のトリガーを自動的に作成します。
* **イベントIDの自動生成**：Nextdoorの各トラッキングイベントに対してイベントIDを自動的に生成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `pixelId` | 文字列 | ピクセルID |
| `autoPageView` | ブール値 | ページビューの自動構成 |
| `autoPurchaseEvent` | ブール値 | 購入イベントの自動構成 |
| `generate_event_id` | ブール値 | イベントIDの自動生成 |
| `event_id` | 文字列 | イベントID |
| `click_id` | 文字列 | Next DoorクリックID |
| `nickname` | 文字列 | カスタムコンバージョンのニックネーム |

### ユーザー

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `userEmail` | 文字列 | ユーザーのメールアドレス |
| `userEmailHashed` | 文字列 | ユーザーのメールアドレス（ハッシュ化済み） |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `order_id` | 文字列 | 注文ID（`_corder`を上書き） |
| `order_value` | 文字列 | 注文金額（`_ctotal`を上書き） |
| `id` | 配列 | 商品IDのリスト（`_cprod`を上書き） |
| `quantity` | 配列 | 数量のリスト（`_cquan`を上書き） |
| `item_price` | 配列 | 価格のリスト（`_cprice`を上書き） |
| `content_name` | 配列 | コンテンツ名のリスト |

### ユーザー属性

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `city` | 文字列 | 市区町村 |
| `country` | 文字列 | 国 |
| `date_of_birth` | 文字列 | 生年月日 |
| `external_id` | 文字列 | 外部ID |
| `email` | 文字列 | メールアドレス |
| `first_name` | 文字列 | 名 |
| `gender` | 文字列 | 性別 |
| `last_name` | 文字列 | 姓 |
| `phone_number` | 文字列 | 電話番号 |
| `state` | 文字列 | 州 |
| `street_address` | 文字列 | 住所 |
| `zip_code` | 文字列 | 郵便番号 |

### 制限付きデータ使用

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `restricted_data_usage_country` | 数値 | 使用国 |
| `restricted_data_usage_state` | 数値 | 使用州 |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `city` | 市区町村 |
| `country` | 国 |
| `date_of_birth` | 生年月日 |
| `external_id` | 外部ID |
| `email` | メールアドレス |
| `first_name` | 名 |
| `gender` | 性別 |
| `last_name` | 姓 |
| `phone_number` | 電話番号 |
| `state` | 州 |
| `street_address` | 住所 |
| `zip_code` | 郵便番号 |
| `order_id` | 注文ID（`_corder`を上書き） |
| `order_value` | 注文金額（`_ctotal`を上書き） |
| `id` | 商品IDのリスト（`_cprod`を上書き） |
| `quantity` | 数量のリスト（`_cquan`を上書き） |
| `item_price` | 価格のリスト（`_cprice`を上書き） |
| `content_name` | コンテンツ名のリスト |