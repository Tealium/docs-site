---
title: RichRelevanceタグ構成ガイド
description: この記事では、タグ管理アカウントでRichRelevanceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/richrelevance-tag/
---
RichRelevanceは、Wal-Mart、Sears、Overstock.comなど、世界最大級かつ最も革新的な小売ブランド向けに、パーソナライズされたショッピング体験を提供しています。

## タグに関するヒント

* 次のEコマース拡張機能の値をサポートしています。
  * 注文ID
  * 商品IDのリスト
  * 商品名のリスト
  * ブランドのリスト
  * カテゴリのリスト（カテゴリID）
  * カテゴリ2のリスト（カテゴリ名）
  * 数量のリスト
  * 価格のリスト

* マッピングを使用して、次の項目を上書きできます。
  * 標準構成値の上書き
  * Eコマース拡張機能の値の上書き
  * 配置リストの定義
  * IDによる項目のブロック

* **ページタイプ**は、**注文ID**（`order_id`）が構成されている場合、自動的に**購入完了ページ**（`purchase`）に構成されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **APIキー**：RichRelevanceのAPIキー。
* **ページタイプ**：通常、**ホームページ**（`home`）は、特定の商品または商品カテゴリに関連付けられていない汎用ページです。データマッピングを使用して、この選択を上書きします。**注文ID**が構成されている場合、**ページタイプ**は自動的に**購入完了ページ**（`purchase`）に構成されます。
* **テストドメイン**：本番稼働前サイトのドメイン名をカンマ区切りで指定したリスト（例：`dev.mydomain.com`または`qa.mydomain.com`）。これらのドメインからRichRelevanceへの呼び出しは、`recs.richrelevance.com`ではなく`integration.richrelevance.com`に送信されます。
* **開発モードを強制**：レコメンデーションエンジンに現在のユーザーの行動を無視させます。開発環境およびQA環境でのみ使用してください。
* **表示を強制**：**サイト上にレコメンデーションを表示**構成を上書きします。顧客向けサイトでレコメンデーションを表示する準備ができていない場合に、開発環境でレコメンデーションを確認するには、**表示を強制**を使用します。開発環境およびQA環境でのみ使用してください。
* **ダミーデータを使用**：商品キャッシュからランダムな商品を使用して、マーチャント向けのレコメンデーションを提供する方法です。商品キャッシュが空の場合は、マーチャントのカタログに由来しない静的なレコメンデーションセットが使用されます。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込むタイミングの条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数                                     | 説明                 |
|:-----------------------------------------|:---------------------|
| APIキー（`api_key`）                     | [文字列]             |
| ページタイプ（`page_type`）              | [文字列]             |
| テストドメイン（`test_domains`）         | （カンマ区切りのリスト） |
| 配置のリスト（`placements`）             | [配列]               |
| セッションID（`user_session_id`）        | [文字列]             |
| ユーザーID（`user_id`）                  | [文字列]             |
| チャネルAPIキー（`channel`）             | [文字列]             |
| 検索語句（`search_terms`）               | [文字列]             |
| 注文ID（`order_id`）                     | [文字列]             |
| 商品IDのリスト（`product_id`）           | [配列]               |
| 商品名のリスト（`product_name`）         | [配列]               |
| 価格のリスト（`price`）                  | [配列]               |
| 数量のリスト（`qty`）                    | [配列]               |
| SKUのリスト（`product_sku`）             | [配列]               |
| カテゴリID（`category_id`）              | [文字列]             |
| カテゴリ名（`category_name`）            | [文字列]             |
| ブランド（`brand`）                      | [文字列]             |
| 開発モードを強制（`forceDevMode`）       | [ブール値]           |
| 表示モードを強制（`forceDisplayMode`）   | [ブール値]           |
| ダミーデータを使用（`useDummyData`）     | [ブール値]           |
| ブロックする項目ID（`blockItemId`）      | [配列]               |
| レジストリID（`registry_id`）            | [文字列]             |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

| 変数                                   | 説明            |
|:---------------------------------------|:----------------|
| ホームページ（`home`）                | `home`          |
| 検索ページ（`search`）                | `search`        |
| 商品ページ（`item`）                  | `item`          |
| カテゴリページ（`category`）          | `category`      |
| パーソナルページ（`personal`）        | `personal`      |
| ブランドページ（`brand`）             | `brand`         |
| カート追加ページ（`addtocart`）       | `addtocart`     |
| カートページ（`cart`）                | `cart`          |
| 購入完了ページ（`purchase`）          | `purchase`      |
| エラーページ（`error`）               | `error`         |
| レジストリ追加ページ（`addtoregistry`） | `addtoregistry` |
| 汎用ページ（`generic`）               | `generic`       |
| ウィッシュリストページ（`wishlist`）  | `wishlist`      |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

| 変数                                   | 説明            |
|:---------------------------------------|:----------------|
| ホームページ（`home`）                | `home`          |
| 検索ページ（`search`）                | `search`        |
| 商品ページ（`item`）                  | `item`          |
| カテゴリページ（`category`）          | `category`      |
| パーソナルページ（`personal`）        | `personal`      |
| ブランドページ（`brand`）             | `brand`         |
| カート追加ページ（`addtocart`）       | `addtocart`     |
| カートページ（`cart`）                | `cart`          |
| 購入完了ページ（`purchase`）          | `purchase`      |
| エラーページ（`error`）               | `error`         |
| レジストリ追加ページ（`addtoregistry`） | `addtoregistry` |
| 汎用ページ（`generic`）               | `generic`       |
| ウィッシュリストページ（`wishlist`）  | `wishlist`      |