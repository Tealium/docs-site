---
title: Coveo Usage Analyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでCoveo Usage Analytics（Coveo UA）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/coveo-usage-analytics-tag/
---
Coveo for Commerceは、レコメンデーション、検索、関連性の管理機能を提供するデータ駆動型プラットフォームです。Coveo Usage Analytics JavaScriptは、Coveoを利用したページの内外で発生するイベントを送信するために使用されます。

Coveo UA JavaScriptの詳細については、Coveoの[コマースイベントの収集](https://docs.coveo.com/en/3188/coveo-for-commerce/collect-commerce-events)ドキュメントを参照してください。

## タグに関するヒント

マッピングを使用すると、次のことができます。

* 構成データを動的に上書きする
* E-Commerce拡張機能の値を動的に上書きする
* 追加のデータ値を送信する
* イベントをトリガーする

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Coveo APIキー**：カタログ用に作成されたAnalytics向けCoveo APIキー。
* **代替エンドポイント**：地域に対応するCoveoエンドポイントを指定します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)ドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### グローバルフィールド

| 変数                                      | 説明       |
|:------------------------------------------|:-----------|
| Coveo APIキー（`coveoApiKey`）            | [文字列]   |
| エンドポイント（`customEndpoint`）        | [文字列]   |
| 通貨コード（`currencyCode`）              | [文字列]   |
| IPの匿名化（`anonymizeIp`）               | [真偽値]   |
| ロイヤルティカードID（`loyaltyCardId`）   | [文字列]   |
| ロイヤルティ階層（`loyaltyTier`）         | [文字列]   |
| サードパーティペルソナ（`thirdPartyPersona`） | [文字列] |
| 会社名（`companyName`）                   | [文字列]   |
| お気に入り店舗（`favoriteStore`）         | [文字列]   |
| 店舗名（`storeName`）                     | [文字列]   |
| ユーザーの業種（`userIndustry`）          | [文字列]   |
| ユーザーの役割（`userRole`）              | [文字列]   |
| ユーザーの部署（`userDepartment`）        | [文字列]   |
| ビジネスユニット（`businessUnit`）        | [文字列]   |

### ページフィールド

| 変数                  | 説明     |
|:----------------------|:---------|
| ページ（`page`）      | [文字列] |
| タイトル（`title`）   | [文字列] |
| 場所（`location`）    | [文字列] |

### 商品データフィールド

| 変数                                       | 説明   |
|:-------------------------------------------|:-------|
| ID（`id`）（`_csku`を上書き）              | [配列] |
| 名前（`name`）（`_cprodname`を上書き）     | [配列] |
| ブランド（`brand`）（`_cbrand`を上書き）   | [配列] |
| カテゴリ（`category`）（`_ccat`を上書き）  | [配列] |
| グループ（`group)                          | [配列] |
| バリアント（`variant`）                    | [配列] |
| リスト（`list`）                           | [配列] |
| 価格（`price`）（`_cprice`を上書き）       | [配列] |
| 数量（`quantity`）（`_cquan`を上書き）     | [配列] |
| クーポン（`coupon`）（`_cpdisc`を上書き）  | [配列] |
| 位置（`position`）                         | [配列] |

### トランザクションフィールド

| 変数                          | 説明          |
|:------------------------------|:--------------|
| ID（`id`）                    | [数値]        |
| アフィリエーション（`affiliation`） | [文字列] |
| 収益（`revenue`）             | [文字列/数値] |
| 税（`tax`）                   | [文字列/数値] |
| 送料（`shipping`）            | [文字列/数値] |
| クーポン（`coupon`）          | [文字列]      |

### 見積もりフィールド

| 変数                                | 説明     |
|:------------------------------------|:---------|
| ID（`id`）                          | [数値]   |
| アフィリエーション（`affiliation`） | [文字列] |

### レビューフィールド

| 変数                    | 説明     |
|:------------------------|:---------|
| ID（`id`）              | [数値]   |
| 評価（`rating`）        | [数値]   |
| コメント（`comment`）   | [文字列] |

### イベント

| 変数                                      | 説明              |
|:------------------------------------------|:------------------|
| クリック（`click`）                       | `click`           |
| 詳細（`detail`）                          | `detail`          |
| クイックビュー（`quickview`）             | `quickview`       |
| インプレッション（`impression`）          | `impression`      |
| 追加（`add`）                             | `add`             |
| 削除（`remove`）                          | `remove`          |
| 購入（`purchase`）                        | `purchase`        |
| 返金（`refund`）                          | `refund`          |
| ブックマーク追加（`bookmark_add`）        | `bookmark_add`    |
| ブックマーク削除（`bookmark_remove`）     | `bookmark_remove` |
| 比較対象に追加（`compare_add`）            | `compare_add`     |
| 比較対象から削除（`compare_remove`）       | `compare_remove`  |
| レビュー追加（`review_add`）              | `review_add`      |
| レビュー削除（`review_remove`）           | `review_remove`   |
| 見積もり（`quote`）                       | `quote`           |
| チェックアウト（`checkout`）              | `checkout`        |
| チェックアウトオプション（`checkout_option`） | `checkout_option` |
| カスタム                                  | `custom`          |