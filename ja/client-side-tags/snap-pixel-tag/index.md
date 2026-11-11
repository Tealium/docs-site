---
title: Snap Pixelタグ構成ガイド
description: この記事では、Snap Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/snap-pixel-tag/
---
Snap Pixelを使用すると、広告主はキャンペーンが複数のデバイスに与える影響を測定できます。広告主は、広告を見た後にウェブサイトでアクションを実行したSnapchatユーザーの数を確認できます。

## タグに関するヒント

* 注文IDが構成されると、購入トラッキングが自動的に実行されます。購入の自動トラッキングを無効にするには、マッピングを使用して宛先の`auto_purchase_tracking`を`false`に構成します。
* ページビューの自動トラッキングはデフォルトで有効になっています。ページビューの自動トラッキングを無効にするには、マッピングを使用して`auto_page_tracking`を`false`に構成します。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 小計（`_csubtotal`）
  * 通貨（`_ccurrency`）
  * 顧客ID（`_ccustid`）
  * 商品IDのリスト（`_cprod`）
  * カテゴリのリスト（`_ccat`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）
* ユーザーのメールアドレスと電話番号は、Snapのサーバーに渡される前に、Snap Pixel SDK内でSHA256に変換されます。
* Snap PixelイベントIDをサーバーサイド属性として使用できるようにするには、**イベントIDを生成**を`true`に構成し、最新バージョンのTealium Collectタグを使用します。
* イベントID属性名の形式は`snap_event_id_<Event Name>_<Tag UID>`です（例：`snap_event_id_PageView_512`）。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **ピクセルID**：Snapchat広告マネージャーで確認できます。
* **イベントIDを生成**：SnapトラッキングイベントごとにイベントIDを自動生成します。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグの構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `pixel_id` | 文字列 | ピクセルID |
| `auto_page_tracking` | ブール値 | ページの自動トラッキング |
| `auto_purchase_tracking` | ブール値 | 購入の自動トラッキング |
| `generate_event_id` | ブール値 | イベントIDを生成 |

### 標準パラメータ

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `currency` | 文字列 | 通貨 |
| `description` | 文字列 | 説明 |
| `item_category` | 文字列 | 商品カテゴリ |
| `item_ids` | 配列 | 商品ID |
| `number_items` | 整数 | 商品数 |
| `payment_info_available` | ブール値 | 支払い情報が利用可能かどうか。 |
| `price` | 配列 | 価格 |
| `search_string` | 文字列 | 検索 |
| `sign_up_method` | 文字列 | 登録方法（例：Facebook、メール、X）。 |
| `success` | ブール値 | 成功 |
| `transaction_id` | 文字列 | トランザクションID |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `order_id`（`_corder`を上書き） | 文字列 | 注文ID |
| `order_subtotal`（`_csubtotal`を上書き） | 文字列 | 小計 |
| `order_currency`（`_ccurrency`を上書き） | 文字列 | 通貨 |
| `customer_id`（`_ccustid`を上書き） | 文字列 | 顧客ID |
| `product_id`（`_cprod`を上書き） | 配列 | 商品IDのリスト |
| `product_category`（`_ccat`を上書き） | 配列 | カテゴリのリスト |
| `product_unit_price`（`_cprice`を上書き） | 配列 | 価格のリスト |
| `product_quantity`（`_cquan`を上書き） | 配列 | 数量のリスト |

### ユーザーパラメータ

Snapが訪問を照合できるように、メールアドレスまたは電話番号のパラメータを含めることをお勧めします。

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `user_email` | 文字列 | 現在サインインしているユーザーのメールアドレス。 |
| `user_hashed_email` | 文字列 | 小文字に変換し、空白を削除したメールアドレスのSHA256ハッシュ。 |
| `user_hashed_phone_number` | 文字列 | 小文字に変換し、空白を削除した電話番号のSHA256ハッシュ。 |
| `user_phone_number` | 文字列 | 国番号、市外局番、電話番号を数字のみで指定します。その他の書式構成文字は使用できません。例：`12125551212`。 |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `ACHIEVEMENT_UNLOCKED` | アンロックされた実績を追跡します。 |
| `ADD_BILLING` | 支払い情報の構成ステータスを追跡します。 |
| `ADD_CART` | カートへの追加を追跡します。動的広告では必須であり、イベント固有のパラメータ`item_ids`または`item_category`を含める必要があります。 |
| `ADD_TO_WISHLIST` | ウィッシュリストへの追加を追跡します。 |
| `AD_CLICK` | 広告のクリックを追跡します。 |
| `AD_VIEW` | 広告の表示を追跡します。 |
| `COMPLETE_TUTORIAL` | チュートリアルの完了を追跡します。 |
| `INVITE` | 招待を追跡します。 |
| `LIST_VIEW` | リストの表示を追跡します。 |
| `LOGIN` | ログインを追跡します。 |
| `OPEN_APP` | アプリケーションが開かれたことを追跡します。 |
| `PAGE_VIEW` | ページビューを追跡します。動的広告では必須であり、イベント固有のパラメータ`item_ids`または`item_category`を含める必要があります。 |
| `PURCHASE` | 購入を追跡します。動的広告では必須であり、イベント固有のパラメータ`item_ids`または`item_category`を含める必要があります。 |
| `RATE` | 評価を追跡します。 |
| `RESERVE` | 予約を追跡します。 |
| `SAVE` | 特定の商品をウィッシュリストに追加するイベントを追跡します。 |
| `SEARCH` | 検索イベントを追跡します。 |
| `SHARE` | 共有を追跡します。 |
| `SIGN_UP` | 登録方法（例：Facebook、メール、X）を追跡します。 |
| `SPENT_CREDITS` | 使用されたクレジットを追跡します。 |
| `START_CHECKOUT` | チェックアウトイベントを追跡します。 |
| `START_TRIAL` | 開始されたトライアルサブスクリプションを追跡します。 |
| `SUBSCRIBE` | サブスクリプションを追跡します。 |
| `VIEW_CONTENT` | コンテンツの閲覧イベントを追跡します。動的広告では必須であり、イベント固有のパラメータ`item_ids`または`item_category`を含める必要があります。 |
| `CUSTOM_EVENT_1` | CUSTOM_EVENT_1 |
| `CUSTOM_EVENT_2` | CUSTOM_EVENT_2 |
| `CUSTOM_EVENT_3` | CUSTOM_EVENT_3 |
| `CUSTOM_EVENT_4` | CUSTOM_EVENT_4 |
| `CUSTOM_EVENT_5` | CUSTOM_EVENT_5 |
| `Custom` | カスタム |

動的広告を実行するには、商品カタログまたはフィードをアップロードしてから、Snapchat Pixelに接続する必要があります。動的広告の詳細については、[Snapchat広告：動的広告](https://businesshelp.snapchat.com/s/article/pixel-dynamic-best?language=en_US)を参照してください。

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `currency` | 文字列 | ISO 4217通貨コード |
| `description` | 文字列 | 説明 |
| `item_category` | 文字列 | 商品カテゴリ。カテゴリIDは、アップロードするカタログ内の`item_group_id`フィールドと一致する必要があります。例：`{'item_category':Shoes',item_ids': ['097man',16span']});` |
| `item_ids` | 配列 | 商品ID。商品IDは、アップロードするカタログ内の`id`フィールドと一致する必要があります。例：`{'item_category':Shoes',item_ids': ['097man',16span']});` |
| `number_items` | 数値 | 商品数 |
| `payment_info_available` | ブール値 | 支払い情報が利用可能かどうか |
| `price` | 数値 | 購入価格 |
| `search_string` | 文字列 | 検索文字列 |
| `sign_up_method` | 文字列 | 登録方法（例：Facebook、メール、X）。 |
| `success` | ブール値 | 成功。`1`は「はい」、`0`は「いいえ」を表します。 |
| `transaction_id` | 文字列 | トランザクションID |
| `custom_parameter` | 文字列 | カスタムパラメータ。 |

各パラメータの詳細については、[Snapchat広告：ウェブサイトへのPixelの直接実装](https://businesshelp.snapchat.com/s/article/pixel-direct-implementation?language=en_US)を参照してください。
#### 推奨されるカスタムパラメーター

マッチ率を向上させるため、次のカスタムユーザーパラメーターのうち少なくとも1つを含めることをお勧めします。

* 名 (`firstname`)
* 姓 (`lastname`)
* 市区町村 (`geo_city`)
* 州／地域 (`geo_region`)
* 郵便番号 (`geo_postal_code`)
* 国 (`geo_country`)
* 年齢 (`age`)

詳細については、[Snapchat広告：ウェブサイトにピクセルを直接実装する](https://businesshelp.snapchat.com/s/article/pixel-direct-implementation?language=en_US)を参照してください。