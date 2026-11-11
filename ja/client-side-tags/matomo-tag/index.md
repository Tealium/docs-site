---
title: Matomoタグ構成ガイド
description: この記事では、Matomoタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/matomo-tag/
---
Matomo（旧称Piwik）は、ダウンロード可能な無料（GPLライセンス）のウェブ解析ソフトウェアプラットフォームで、ウェブサイトとその訪問に関する詳細なレポートを提供します。

## タグに関するヒント

マッピングを使用すると、次のことができます。

* イベントトリガーを構成する
* イベント固有のパラメーターをイベント名にマッピングする
* 標準構成値を動的に上書きする
* Eコマース拡張機能の値を動的に上書きする

`eventCategory`と`eventAction`に値が構成されている場合、`trackEvent`が自動的に呼び出されます。

**イベント固有のパラメーター**タブで、`Goal Index`と`Custom Dimension`の値を構成します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **トラッカーURL**：Matomoアカウントで確認できます。通常はドメイン名です。
* **サイトID**：Matomoで確認できるサイトIDです。
* **サブドメインのトラッキング**：メインドメインとそのサブドメイン全体でユーザーを記録するために、Matomoはすべてのサブドメイン間でCookieを共有します。1人のユーザーが`x.mydomain.com`と`y.mydomain.com`にアクセスした場合、そのユーザーは1人のユニーク訪問としてカウントされます。
* **ページビューの送信**：デフォルトでは、サイトの各ページでページビューイベントが自動的に記録されます。スニペットからMatomoにページビューイベントを送信しない場合は、このオプションを`false`に構成します。
* **サイトドメインの先頭追加**：`True`に構成すると、サブドメイン別のトラフィック概要を把握できるように、ページ名の先頭にサイトドメインが追加されます。たとえば、`blog.mydomain.com`の`About`ページは`blog / About`として記録されます。
* **エイリアスURLの構成**：Matomoアカウントで確認できます。通常はドメイン名です。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用できるカテゴリーは次のとおりです。

### 標準パラメーター

| 変数 | 説明 |
|:---------|:------------|
| トラッカーURL（`tracker_url`） | 文字列 |
| サイトID（`site_id`） | 文字列 |
| サブドメインのトラッキング（`track_subdomains`） | ブール値 |
| ページビューの送信（`send_page_view`） | ブール値 |
| サイトドメインの先頭追加（`prepend_site_domain`） | ブール値 |
| エイリアスURLの構成（`set_alias_urls`） | ブール値 |
| エイリアスURL（`alias_urls`） | 文字列 |
| ユーザーID（`user_id`） | 文字列 |
| ユーザーが入力した検索語句（`searchKeyword`） | 文字列 |
| 返された検索ページのカテゴリー名（`searchCategory`） | 文字列 |
| 返された検索結果の件数（`searchResultsCount`） | 文字列 |
| ユーザーがクリックしたリンクのURL（`linkURL`） | 文字列 |
| クリックされたリンクの説明（`linkType`） | 文字列 |

### 目標インデックス

| 変数 | 説明 |
|:---------|:------------|
| 目標インデックス（`goal_index`） | 数値 |

### 標準イベントパラメーター

| 変数 | 説明 |
|:---------|:------------|
| イベントカテゴリー（`eventCategory`） | 文字列 |
| イベントアクション（`eventAction`） | 文字列 |
| イベント名（`eventName`） | 文字列 |
| イベント値（`eventValue`） | 数値 |

### Eコマースパラメーター

| 変数 | 説明 |
|:---------|:------------|
| SKUのリスト（`product_sku`）<br>（`_csku`を上書き） | 文字列の配列 |
| 名前のリスト（`product_name`）<br>（`_cprodname`を上書き） | 文字列の配列 |
| カテゴリーのリスト（`item_category`）<br>（`_ccat`を上書き） | 文字列または配列の配列 |
| 価格のリスト（`product_unit_price`）<br>（`_cprice`を上書き） | 数値の配列 |
| 数量のリスト（`product_quantity`）<br>（`_cquan`を上書き） | 数値の配列 |
| 注文の割引（`product_discount`） | 数値またはブール値 |
| 注文ID（`order_id`）<br>（`_corder`を上書き） | 文字列 |
| 注文小計（`grand_total`）<br>（`_csubtotal`を上書き） | 数値 |
| 注文合計（`order_total`）<br>（`_ctotal`を上書き） | 数値 |
| 税額（`order_tax`）<br>（`_ctax`を上書き） | 数値 |
| 配送料（`order_shipping`）<br>（`_cship`を上書き） | 数値 |

### アクションディメンション

| 変数 | 説明 |
|:---------|:------------|
| カスタムディメンションインデックス（`custom_dimension_index`） | 数値 |
| カスタムディメンション値（`custom_dimension_value`） | 文字列 |

### イベント

イベントのマッピングについては、[イベントマッピングの追加](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| 商品の表示 | `productView` |
| カテゴリーの表示 | `ctegoryViews` |
| カートへの追加 | `addToCart` |
| カートからの削除 | `removeFromCart` |
| 購入 | `purchase` |
| ユーザーのログアウト | `resetUserId` |"
| 目標のトラッキング | `trackGoal` |
| サイト内検索 | `trackSiteSearch` |
| リンクのトラッキング | `trackLink` |
| カスタムディメンションの構成 | `setCustomDimension` |
| カスタムディメンションの削除 | `deleteCustomDimension` |

### イベント固有のパラメーター

イベントのマッピングについては、[イベントマッピングの追加](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| 商品の表示 | `productView` |
| カテゴリーの表示 | `ctegoryViews` |
| カートへの追加 | `addToCart` |
| カートからの削除 | `removeFromCart` |
| 購入 | `purchase` |
| ユーザーのログアウト | `resetUserId` |
| 目標のトラッキング | `trackGoal` |
| サイト内検索 | `trackSiteSearch` |
| リンクのトラッキング | `trackLink` |
| カスタムディメンションの構成 | `setCustomDimension` |
| カスタムディメンションの削除 | `deleteCustomDimension` |
| イベントのトラッキング | `trackEvent` |