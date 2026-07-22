---
title: Snap Pixel タグ構成ガイド
description: この記事では、Snap Pixel タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/snap-pixel-tag/
---
Snap Pixel は、広告主がキャンペーンのクロスデバイス影響を測定するのに役立ちます。広告主は、広告を見た後にSnapchattersが自分のウェブサイトでどのようなアクションを取ったかを確認できます。

## タグのヒント

* 注文IDが構成されている場合、購入追跡は自動的に発火します。自動購入追跡を無効にするには、マッピングで `auto_purchase_tracking` を `false` に構成します。
* 自動ページビュー追跡はデフォルトで有効になっています。自動ページビュー追跡を無効にするには、マッピングで `auto_page_tracking` を `false` に構成します。
* 次のEコマース拡張パラメータをサポートします：
  * 注文ID (`_corder`)
  * 小計 (`_csubtotal`)
  * 通貨 (`_ccurrency`)
  * 顧客ID (`_ccustid`)
  * 商品IDリスト (`_cprod`)
  * カテゴリリスト (`_ccat`)
  * 数量リスト (`_cquan`)
  * 価格リスト (`_cprice`)
* ユーザーのメールアドレスと電話番号は、Snap Pixel SDK内でSHA256に変換され、その後Snapのサーバーに渡されます。
* Snap Pixel イベントIDをサーバーサイド属性として利用可能にするには、**イベントID生成**を `true` に構成し、Tealium Collectタグの最新バージョンを使用します。
* イベントID属性名は `snap_event_id_<イベント名>_<タグUID>` の形式です（例：`snap_event_id_PageView_512`）。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法については、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際には、次の構成を構成します：

* **ピクセルID**：Snapchat広告マネージャーで見つかります。
* **イベントID生成**：すべてのSnap追跡イベントに対して自動的にイベントIDを生成します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです：

### タグ構成

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `pixel_id`  | 文字列 | ピクセルID  |
|  `auto_page_tracking`  | ブール値 | 自動ページ追跡 |
|  `auto_purchase_tracking`  | ブール値 | 自動購入追跡 |
|  `generate_event_id`  | ブール値 | イベントIDを生成 |

### 標準パラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `currency`  | 文字列 | 通貨 | 
|  `description`  | 文字列 | 説明 |
| `item_category` | 文字列 | 商品カテゴリ |
| `item_ids` | 配列 | 商品ID |
| `number_items` | 整数 | 商品数 |
| `payment_info_available` | ブール値 | 支払情報の有無 |
| `price` | 配列 | 価格 |
|  `search_string`  | 文字列 | 検索文字列 |
|  `sign_up_method`  | 文字列 | 登録方法（例：Facebook、Email、X） |
|  `success` | ブール値 | 成功 |
|  `transaction_id`  | 文字列 | トランザクションID |

### Eコマース

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `order_id` (Overrides `_corder`)  | 文字列 | 注文ID |
|  `order_subtotal` (Overrides `_csubtotal`)  | 文字列 | 小計 |
|  `order_currency` (Overrides `_ccurrency`)  | 文字列 | 通貨 |
|  `customer_id` (Overrides `_ccustid`)  | 文字列 | 顧客ID |
|  `product_id` (Overrides `_cprod`)  | 配列 | 商品IDリスト |
|  `product_category` (Overrides `_ccat`)  | 配列 | カテゴリリスト |
|  `product_unit_price` (Overrides `_cprice`)  | 配列 | 価格リスト |
|  `product_quantity` (Overrides `_cquan`)  | 配列 | 数量リスト |

### ユーザーパラメータ

訪問をSnapにマッチさせるために、メールアドレスまたは電話番号パラメータを含めることをお勧めします。

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `user_email`  | 文字列 | 現在サインインしているユーザーのメールアドレス。 |
|  `user_hashed_email`  | 文字列 | 小文字に変換され、空白が削除されたメールアドレスのSHA256ハッシュ。 |
|  `user_hashed_phone_number`  | 文字列 | 小文字に変換され、空白が削除された電話番号のSHA256ハッシュ。 |
|  `user_phone_number`  | 文字列 | 国コード、エリアコード、番号のみの数字。その他の書式文字は含まれません。例：`12125551212`。|

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `ACHIEVEMENT_UNLOCKED` | 達成解除を追跡します。 |
| `ADD_BILLING` | 支払情報の構成状況を追跡します。 |
| `ADD_CART` | カートへの追加を追跡します。ダイナミック広告には必須で、`item_ids` または `item_category` のイベント固有パラメータを含める必要があります。 |
| `ADD_TO_WISHLIST` | ほしい物リストへの追加を追跡します。|
| `AD_CLICK` | 広告クリックを追跡します。 |
| `AD_VIEW` | 広告表示を追跡します。 |
| `COMPLETE_TUTORIAL` | チュートリアルの完了を追跡します。 |
| `INVITE` | 招待を追跡します。 |
| `LIST_VIEW` | リスト表示を追跡します。 |
| `LOGIN` | ログインを追跡します。 |
| `OPEN_APP` | アプリケーションのオープンを追跡します。 |
| `PAGE_VIEW` | ページビューを追跡します。ダイナミック広告には必須で、`item_ids` または `item_category` のイベント固有パラメータを含める必要があります。 |
| `PURCHASE` | 購入を追跡します。ダイナミック広告には必須で、`item_ids` または `item_category` のイベント固有パラメータを含める必要があります。 |
| `RATE` | 評価を追跡します。 |
| `RESERVE` | 予約を追跡します。 |
| `SAVE` | 特定のアイテムのほしい物リストへの追加イベントを追跡します。 |
| `SEARCH` | 検索イベントを追跡します。 |
| `SHARE` | 共有を追跡します。 |
| `SIGN_UP` | 登録方法を追跡します（例：Facebook、Email、X）。 |
| `SPENT_CREDITS` | 使用されたクレジットを追跡します。 |
| `START_CHECKOUT` | チェックアウトイベントを追跡します。 |
| `START_TRIAL` | トライアルの開始を追跡します。 |
| `SUBSCRIBE` | サブスクリプションを追跡します。 |
| `VIEW_CONTENT` | コンテンツ表示イベントを追跡します。ダイナミック広告には必須で、`item_ids` または `item_category` のイベント固有パラメータを含める必要があります。 |
| `CUSTOM_EVENT_1` | CUSTOM_EVENT_1 |
| `CUSTOM_EVENT_2` | CUSTOM_EVENT_2 |
| `CUSTOM_EVENT_3` | CUSTOM_EVENT_3 |
| `CUSTOM_EVENT_4` | CUSTOM_EVENT_4 |
| `CUSTOM_EVENT_5` | CUSTOM_EVENT_5 |
| `Custom` | カスタム |

ダイナミック広告を実行するには、商品カタログまたはフィードをアップロードし、Snapchat Pixelに接続する必要があります。ダイナミック広告についての詳細は、[Snapchat広告：ダイナミック広告](https://businesshelp.snapchat.com/s/article/pixel-dynamic-best?language=en_US)を参照してください。

### イベント固有パラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `currency`| 文字列 | ISO 4217通貨コード  |
| `description` | 文字列 | 説明  |
| `item_category` | 文字列 | 商品カテゴリ。カテゴリIDはアップロードするカタログの `item_group_id` フィールドと一致する必要があります。例：`{'item_category':Shoes',item_ids': ['097man',16span']});`   |
| `item_ids` | 配列 | 商品ID。商品IDはアップロードするカタログの `id` フィールドと一致する必要があります。例：`{'item_category':Shoes',item_ids': ['097man',16span']});`   |
| `number_items` | 数 | 商品数   |
| `payment_info_available`| ブール値 | 支払情報の有無   |
| `price` | 数 | 購入価格 |
| `search_string` | 文字列 | 検索文字列 |
| `sign_up_method` | 文字列 | 登録方法（例：Facebook、Email、X）。  |
| `success` | ブール値 | 成功。`1`ははいを表し、`0`はいいえを表します。   |
| `transaction_id` | 文字列 | トランザクションID   |
| `custom_parameter`| 文字列 | カスタムパラメータ。   |

各パラメータについての詳紀は、[SnapChat広告：ウェブサイトにピクセルを直接実装する](https://businesshelp.snapchat.com/s/article/pixel-direct-implementation?language=en_US)を参照してください。
#### 推奨されるカスタムパラメーター

マッチング率を向上させるために、以下のカスタムユーザーパラメーターの少なくとも1つを含めることをお勧めします：

* 名（`firstname`）
* 姓（`lastname`）
* 市区町村（`geo_city`）
* 州（`geo_region`）
* 郵便番号（`geo_postal_code`）
* 国（`geo_country`）
* 年齢（`age`）

詳細については、[SnapChat広告: ウェブサイトにピクセルを直接実装する](https://businesshelp.snapchat.com/s/article/pixel-direct-implementation?language=en_US)をご覧ください。