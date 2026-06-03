---
title: Matomoタグ構成ガイド
description: この記事では、Matomoタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/matomo-tag/
---
Matomo（旧称Piwik）は、ダウンロード可能な無料（GPLライセンス）のウェブ分析ソフトウェアプラットフォームで、ウェブサイトとその訪問に関する詳細なレポートを提供します。

## タグのヒント

マッピングを使用して以下のことを行います：

* イベントトリガーの構成
* イベント固有のパラメータをイベント名にマッピング
* 標準構成値を動的に上書き
* eコマース拡張値を動的に上書き

`eventCategory`と`eventAction`が入力されている場合、`trackEvent`は自動的に呼び出されます。

**イベント固有のパラメータ**タブで`Goal Index`と`Custom Dimension`の値を構成します。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **トラッカーURL**：Matomoアカウントで見つけることができ、通常はドメイン名です。
* **サイトID**：Matomoで見つけることができるサイトIDです。
* **サブドメインの追跡**：メインドメインとそのすべてのサブドメインでユーザーを記録するために、Matomoはすべてのサブドメインでクッキーを共有します。ユーザーが`x.mydomain.com`と`y.mydomain.com`を訪れると、それらは1つのユニークな訪問としてカウントされます。
* **ページビューの送信**：デフォルトでは、ページビューイベントはサイトの各ページで自動的に記録されます。スニペットがMatomoにページビューイベントを送信しないようにするには、このオプションを`false`に構成します。
* **サイトドメインの前置**：`True`に構成すると、サイトドメインがページ名の前に追加され、サブドメイン別のトラフィックの概要を提供します。例えば、`blog.mydomain.com`の`About`ページは`blog / About`として記録されます。
* **エイリアスURLの構成**：Matomoアカウントで見つけることができ、通常はドメイン名です。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準パラメータ

| 変数 | 説明 |
|:---------|:------------|
| トラッカーURL (`tracker_url`) | 文字列 |
| サイトID (`site_id`)  | 文字列 |
| サブドメインの追跡 (`track_subdomains`)  | ブール値 |
| ページビューの送信 (`send_page_view`)  | ブール値 |
| サイトドメインの前置 (`prepend_site_domain`)  | ブール値 |
| エイリアスURLの構成 (`set_alias_urls`)  | ブール値 |
| エイリアスURL (`alias_urls`)  | 文字列 |
| ユーザーID (`user_id`)  | 文字列 |
| ユーザーが入力した検索ワード (`searchKeyword`)  | 文字列 |
| 戻り検索ページのカテゴリ名 (`searchCategory`)  | 文字列 |
| 戻り検索結果の数 (`searchResultsCount`)  | 文字列 |
| ユーザーがクリックしたリンクURL (`linkURL`)  | 文字列 |
| クリックしたリンクの説明 (`linkType`)  | 文字列 |

### ゴールインデックス

| 変数 | 説明 |
|:---------|:------------|
| ゴールインデックス (`goal_index`)  | 数値 |

### 標準イベントパラメータ

| 変数 | 説明 |
|:---------|:------------|
| イベントカテゴリ (`eventCategory`)  | 文字列 |
| イベントアクション (`eventAction`)  | 文字列 |
| イベント名 (`eventName`)  | 文字列 |
| イベント値 (`eventValue`)  | 数値 |

### E-コマースパラメータ

| 変数 | 説明 |
|:---------|:------------|
| SKUのリスト (`product_sku`)&lt;br&gt;(`_csku`を上書き) | 文字列の配列 |
| 名前のリスト (`product_name`)&lt;br&gt;(`_cprodname`を上書き)  | 文字列の配列 |
| カテゴリのリスト (`item_category`)&lt;br&gt;(`_ccat`を上書き)  | 文字列/配列の配列 |
| 価格のリスト (`product_unit_price`)&lt;br&gt;(`_cprice`を上書き)  | 数値の配列 |
| 数量のリスト (`product_quantity`)&lt;br&gt;(`_cquan`を上書き)  | 数値の配列 |
| 注文割引 (`product_discount`)  | 数値またはブール値 |
| 注文ID (`order_id`)&lt;br&gt;(`_corder`を上書き)  | 文字列 |
| 注文小計 (`grand_total`)&lt;br&gt;(`_csubtotal`を上書き)  | 数値 |
| 注文合計 (`order_total`)&lt;br&gt;(`_ctotal`を上書き)  | 数値 |
| 税額 (`order_tax`)&lt;br&gt;(`_ctax`を上書き)  | 数値 |
| 送料 (`order_shipping`)&lt;br&gt;(`_cship`を上書き)  | 数値 |

### アクションディメンション

| 変数 | 説明 |
|:---------|:------------|
| カスタムディメンションインデックス (`custom_dimension_index`)  | 数値 |
| カスタムディメンション値 (`custom_dimension_value`)  | 文字列 |

### イベント
イベントマッピングについての情報は、[イベントマッピングの追加]()を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| 商品ビュー | `productView` |
| カテゴリビュー | `ctegoryViews` |
| カートに追加 | `addToCart` |
| カートから削除 | `removeFromCart` |
| 購入 | `purchase` |
| ユーザーログアウト | `resetUserId` |
| ゴール追跡 | `trackGoal` |
| サイト検索 | `trackSiteSearch` |
| リンク追跡 | `trackLink` |
| カスタムディメンション構成 | `setCustomDimension` |
| カスタムディメンション削除 | `deleteCustomDimension` |

### イベント固有のパラメータ
イベントマッピングについての情報は、[イベントマッピングの追加]()を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| 商品ビュー | `productView` |
| カテゴリビュー | `ctegoryViews` |
| カートに追加 | `addToCart` |
| カートから削除 | `removeFromCart` |
| 購入 | `purchase` |
| ユーザーログアウト | `resetUserId` |
| ゴール追跡 | `trackGoal` |
| サイト検索 | `trackSiteSearch` |
| リンク追跡 | `trackLink` |
| カスタムディメンション構成 | `setCustomDimension` |
| カスタムディメンション削除 | `deleteCustomDimension` |
| イベント追跡 | `trackEvent` |

