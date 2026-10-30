---
title: AppLovin Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでAppLovin Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/applovin-pixel-tag/
---
AppLovin Pixelは、サイトにAppLovin Webピクセルを読み込み、ページビュー、Eコマース、リードの各イベントをAppLovinに送信して、Webキャンペーンを測定および最適化します。

## タグに関するヒント

* タグは最初の発火時に`https://s.axon.ai/pixel.js`を読み込み、2回目以降の発火時にのみイベントを送信します。ページで使用できるEvent Keyは1つだけで、正確に36文字である必要があります。そうでない場合、タグは発火しません。
* **Events**タブで、変数をAppLovinの13種類のカタログイベントにマッピングします。カスタムイベントはサポートされていません。**Auto Page View**は、ビューごとに`page_view`を送信し、同じビューで2回発火することはありません。
* タグはイベントごとにフィールドをフィルタリングし、空の値を送信しません。単一のイベントでフィールドを上書きするには、**Event-specific Parameters**を使用します。デバッグモードでは、必須フィールドが欠落している場合にログへ記録しますが、イベントはそのまま発火します。
* `user_data`フィールドには、メールアドレス、電話番号、ユーザーIDが格納されます。`add_to_cart`、`remove_from_cart`、`purchase`の各項目には数量が必要です。イベントごとのフィールド（必須／*任意*）は次のとおりです。
   * `page_view`、`login`：*user_data*
   * `view_item`、`view_cart`、`add_to_cart`、`remove_from_cart`：items／*currency、value、user_data*
   * `begin_checkout`：currency、value、items／*user_data*
   * `add_payment_info`：*currency、value、items、payment_type、user_data*
   * `purchase`：transaction_id、currency、value、shipping、tax、items、user_data／*is_new_customer*
   * `search`：search_term／*results、user_data*
   * `generate_lead`：currency、value／*user_data*
   * `sign_up`：user_data／*method*
   * `subscribe`：*currency、value、user_data*
* タグは、E-Commerce Extension変数`_ccurrency`、`_csubtotal`、`_corder`、`_cship`、`_ctax`、`_cprod`、`_cprodname`、`_cprice`、`_cquan`、`_ccat`、`_csku`、`_cbrand`、`_cpdisc`をサポートしています。
* タグは、メールアドレスと電話番号の値を、プレーンテキストまたは事前にSHA256でハッシュ化された形式で受け付けます。ピクセルはプレーンテキストの値を自動的にハッシュ化します。
* **Generate Event ID**は、イベントごとに一意の`dedupe_id`を送信し、`utag.globals`に`applovin_event_id_<event>`として保存します。マッピングされた`dedupe_id`が優先されます。
* `utag.gdpr`によって同意が拒否されている場合、タグはイベントを抑制します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Event Key**：36文字のAppLovin Event Key。AppLovinダッシュボードの**Account > General > Keys**で確認できます。
* **Auto Page View**：タグのビューイベントごとに`page_view`を送信します。代わりにEventsタブからページビューの発火を制御するには、**False**に構成します。デフォルト：**True**。
* **Generate Event ID**：イベントごとに一意のIDを生成し、ブラウザーとサーバー間での重複排除のために`dedupe_id`として渡します。このIDは、`utag.globals`にも`applovin_event_id_<event>`として保存されます。デフォルト：**False**。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングとは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### Configuration

Configurationカテゴリを使用すると、特定のタグ発火について、タグレベルのEvent Keyを上書きできます。

| 変数 | 型／値 | 説明 |
|:---------|:------------|:------------|
| `event_key` | 文字列 | この発火で使用するAppLovin Event Key。正確に36文字である必要があります。タグ構成で指定された値を上書きします。 |

### General

Generalカテゴリにマッピングされた値は、すべてのイベントに適用されます。特定のイベントの値を上書きするには、[Event-specific Parameters](#event-specific-parameters)カテゴリを使用します。

| 変数 | 型／値 | 説明 |
|:---------|:------------|:------------|
| `dedupe_id` | 文字列 | （任意）イベントとともに渡される重複排除ID。 |
| `event_data` | オブジェクト | （任意）GA4形式のEコマースオブジェクト。GeneralおよびE-Commerceのマッピングは、一致するキーを上書きします。イベントが受け付けないキーは破棄されます。 |
| `user_data.email` | 文字列 | （任意）ユーザーのメールアドレス（プレーンテキストまたは事前にSHA256でハッシュ化された値）。 |
| `user_data.phone` | 文字列 | （任意）ユーザーの電話番号（プレーンテキストまたは事前にSHA256でハッシュ化された値）。 |
| `user_data.user_id` | 文字列 | （任意）顧客識別子。 |
| `payment_type` | 文字列 | （任意）支払い方法。`add_payment_info`イベントで使用されます。 |
| `search_term` | 文字列 | （`search`では必須）ユーザーが検索したテキスト。 |
| `method` | 文字列 | （任意）登録方法（例：`email`または`google`）。`sign_up`イベントで使用されます。 |
| `is_new_customer` | 真偽値 | （任意）購入者が新規顧客かどうか。`purchase`イベントで使用されます。 |

### E-Commerce

E-Commerceカテゴリにマッピングされた値は、対応するE-Commerce Extension変数を上書きします。

| 変数 | 型／値 | 説明 |
|:---------|:------------|:------------|
| `currency` | 文字列 | ISO 4217通貨コード（例：`USD`）。`begin_checkout`、`purchase`、`generate_lead`では必須です。`_ccurrency`を上書きします。 |
| `value` | 数値 | イベントの金額。`begin_checkout`、`purchase`、`generate_lead`では必須です。`_csubtotal`を上書きします。 |
| `transaction_id` | 文字列 | 一意の注文識別子。`purchase`では必須です。`_corder`を上書きします。 |
| `shipping` | 数値 | 送料。`purchase`では必須です。マッピングされていない場合は`0`として送信されます。`_cship`を上書きします。 |
| `tax` | 数値 | 税額。`purchase`では必須です。マッピングされていない場合は`0`として送信されます。`_ctax`を上書きします。 |
| `product_id` | 配列 | 商品ごとに1つの製品ID。`view_item`、`view_cart`、`add_to_cart`、`remove_from_cart`、`begin_checkout`、`purchase`では必須です。`_cprod`を上書きします。 |
| `product_name` | 配列 | 商品ごとに1つの商品名。`_cprodname`を上書きします。 |
| `product_price` | 配列 | 商品ごとに1つの単価。`_cprice`を上書きします。 |
| `product_quantity` | 配列 | 商品ごとに1つの数量。`add_to_cart`、`remove_from_cart`、`purchase`では、商品ごとに必須です。`_cquan`を上書きします。 |
| `product_category_id` | 配列 | 商品ごとに1つの整数カテゴリID。整数以外の値は破棄されます。`_ccat`を上書きします。 |
| `product_variant_id` | 配列 | 商品ごとに1つのバリアントID。`_csku`を上書きします。 |
| `product_brand` | 配列 | 商品ごとに1つのブランド名。`_cbrand`を上書きします。 |
| `product_discount` | 配列 | 商品ごとの割引額。`_cpdisc`を上書きします。 |
| `product_image_url` | 配列 | 商品ごとに1つの商品画像URL。 |
| `product_affiliation` | 配列 | 商品ごとに1つのアフィリエーション値。 |

### Events

イベントをマッピングする方法については、[イベントマッピングを作成する](#add-an-event-mapping)を参照してください。

次の13種類のカタログイベントのみがサポートされています。カスタムイベント名は通知なしでスキップされます。

| イベント | 必須 | 任意 |
|:------|:---------|:---------|
| `page_view` | なし | `user_data` |
| `view_item` | `items` | `currency`、`value`、`user_data` |
| `view_cart` | `items` | `currency`、`value`、`user_data` |
| `add_to_cart` | `items`（各商品に`quantity`が必須） | `currency`、`value`、`user_data` |
| `remove_from_cart` | `items`（各商品に`quantity`が必須） | `currency`、`value`、`user_data` |
| `begin_checkout` | `currency`、`value`、`items` | `user_data` |
| `add_payment_info` | なし | `currency`、`value`、`items`、`payment_type`、`user_data` |
| `purchase` | `transaction_id`、`currency`、`value`、`shipping`、`tax`、`items`（各商品に`quantity`が必須）、`user_data` | `is_new_customer` |
| `search` | `search_term` | `results`、`user_data` |
| `generate_lead` | `currency`、`value` | `user_data` |
| `sign_up` | `user_data` | `method` |
| `login` | なし | `user_data` |
| `subscribe` | なし | `currency`、`value`、`user_data` |
### イベント固有のパラメータ

イベント固有のパラメータカテゴリを使用すると、単一のイベントについて、一般またはEコマースのマッピングを上書きできます。ここで構成した値は、選択したイベントに対して、一般およびEコマースカテゴリの値より優先されます。