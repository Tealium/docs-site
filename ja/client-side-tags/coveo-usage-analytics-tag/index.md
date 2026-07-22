---
title: Coveo使用分析タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでCoveo使用分析（Coveo UA）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/coveo-usage-analytics-tag/
---
Coveo for Commerceは、推奨事項、検索、関連性の管理を提供するデータ駆動型のプラットフォームです。Coveo使用分析JavaScriptは、Coveoで動作するページ内外で発生するイベントを送信するために使用されます。

Coveo UA Javascriptについての詳細は、Coveo [Collect Commerce Events](https://docs.coveo.com/en/3188/coveo-for-commerce/collect-commerce-events)のドキュメンテーションを参照してください。

## タグのヒント

マッピングを使用して：

* 動的に構成データを上書きする
* E-Commerce拡張値を動的に上書きする
* 追加のデータ値を送信する
* イベントトリガー

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[Manage Tags](https://docs.tealium.com/manage-tags/#add-a-tag)を参照してください。

タグを追加する際には、以下の構成を行います：

* **Coveo API Key**：カタログ用に作成されたCoveo API Key for Analytics。
* **Alternate Endpoints**：あなたの地域のCoveoエンドポイントを指定します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、[data layer variable](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[data mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### グローバルフィールド

| 変数                                      | 説明 |
|:------------------------------------------|:------------|
| Coveo API Key (`coveoApiKey`)             | [文字列]    |
| エンドポイント (`customEndpoint`)               | [文字列]    |
| 通貨コード (`currencyCode`)            | [文字列]    |
| IP匿名化 (`anonymizeIp`)              | [ブール値]   |
| ロイヤリティカードID (`loyaltyCardId`)         | [文字列]    |
| ロイヤリティティア (`loyaltyTier`)              | [文字列]    |
| サードパーティペルソナ (`thirdPartyPersona`) | [文字列]    |
| 会社名 (`companyName`)              | [文字列]    |
| お気に入りの店舗 (`favoriteStore`)          | [文字列]    |
| 店舗名 (`storeName`)                  | [文字列]    |
| ユーザー業界 (`userIndustry`)            | [文字列]    |
| ユーザーロール (`userRole`)                    | [文字列]    |
| ユーザー部門 (`userDepartment`)        | [文字列]    |
| ビジネスユニット (`businessUnit`)            | [文字列]    |

### ページフィールド

| 変数              | 説明 |
|:----------------------|:------------|
| ページ (`page`)         | [文字列]    |
| タイトル (`title`)       | [文字列]    |
| ロケーション (`location`) | [文字列]    |

### 商品データフィールド

| 変数                                   | 説明 |
|:-------------------------------------------|:------------|
| ID (`id`) (Overrides `_csku`)              | [配列]     |
| 名前 (`name`) (Overrides `_cprodname`)     | [配列]     |
| ブランド (`brand`) (Overrides `_cbrand`)      | [配列]     |
| カテゴリ (`category`) (Overrides `_ccat`)  | [配列]     |
| グループ (`group)                             | [配列]     |
| バリアント (`variant`)                        | [配列]     |
| リスト (`list`)                              | [配列]     |
| 価格 (`price`) (Overrides `_cprice`)      | [配列]     |
| 数量 (`quantity`) (Overrides `_cquan`) | [配列]     |
| クーポン (`coupon`) (Overrides `_cpdisc`)    | [配列]     |
| ポジション (`position`)                      | [配列]     |

### トランザクションフィールド

| 変数                    | 説明     |
|:----------------------------|:----------------|
| ID (`id`)                   | [数値]        |
| 所属 (`affiliation`) | [文字列]        |
| 収益 (`revenue`)         | [文字列/数値] |
| 税金 (`tax`)                 | [文字列/数値] |
| 配送 (`shipping`)       | [文字列/数値] |
| クーポン (`coupon`)           | [文字列]        |

### 引用フィールド

| 変数                    | 説明 |
|:----------------------------|:------------|
| ID (`id`)                   | [数値]    |
| 所属 (`affiliation`) | [文字列]    |

### レビューフィールド

| 変数            | 説明 |
|:--------------------|:------------|
| ID (`id`)           | [数値]    |
| レーティング (`rating`)   | [数値]    |
| コメント (`comment`) | [文字列]    |

### イベント

| 変数                            | 説明     |
|:------------------------------------|:----------------|
| クリック (`click`)                     | `click`           |
| 詳細 (`detail`)                   | `detail`          |
| クイックビュー (`quickview`)            | `quickview`       |
| インプレッション (`impression`)           | `impression`      |
| 追加 (`add`)                         | `add`             |
| 削除 (`remove`)                   | `remove`          |
| 購入 (`purchase`)               | `purchase`        |
| 払い戻し (`refund`)                   | `refund`          |
| ブックマーク追加 (`bookmark_add`)       | `bookmark_add`    |
| ブックマーク削除 (`bookmark_remove`) | `bookmark_remove` |
| 比較追加 (`compare_add`)         | `compare_add`     |
| 比較削除 (`compare_remove`)   | `compare_remove`  |
| レビュー追加 (`review_add`)           | `review_add`      |
| レビュー削除 (`review_remove`)     | `review_remove`   |
| 引用 (`quote`)                     | `quote`           |
| チェックアウト (`checkout`)               | `checkout`        |
| チェックアウトオプション (`checkout_option`) | `checkout_option` |
| カスタム                              | `custom`          |

