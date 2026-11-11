---
title: Naverタグ構成ガイド
description: この記事では、タグ管理アカウントでNaverタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/naver-tag/
---
## タグに関するヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* 次のEコマース変数を使用します。
  * `_ctotal`
* **ページタイプ**には、次のオプションがあります。
  * なし - 0
  * チェックアウト - 1
  * サインアップ - 2
  * ショッピングカート - 3
  * 予約／登録 - 4
  * その他 - 5

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の項目を構成します。

* **アカウントID**：NaverのアカウントID。
* **ページタイプ**：このパラメータは非推奨です。
* **サブドメイン**：Naverから指定された場合にのみ、このパラメータを構成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `account_id` | アカウントID。 |
| `page_type` | ページタイプ。 |
| `subdomain` | サブドメイン。 |

### Eコマース

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `order_total` | `Number` | 注文合計（`_ctotal`を上書きします）。 |
| `type` | `String` | コンバージョンイベントのタイプ。 |
| `id` | `String` | コンバージョンIDまたは顧客のアクションID。 |
| `value` | `String` | 注文内のすべての商品およびサービスについて、配送料を除いた合計価格。 |
| `item_id` | `Array` | 商品ID（`_cprod`を上書きします）。 |
| `name` | `Array` | 商品名（`_cprodname`を上書きします）。 |
| `category` | `Array` | 商品カテゴリー（`_ccat`を上書きします）。 |
| `quantity` | `Array` | 商品数量（`_cquan`を上書きします）。 |
| `payAmount` | `Array` | 特定の商品に対して支払われた合計金額。単価ではありません。 |
| `option` | `Array` | 色やサイズなどの商品オプション（例：`color:red, size:240`）。 |

### イベントトリガー

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `purchase` | 購入完了。 |
| `begin_checkout` | チェックアウト開始。 |
| `sign_up` | サインアップ。 |
| `add_to_cart` | カートに追加。 |
| `schedule` | 予約完了。 |
| `save_store` | 店舗を追加／保存。 |
| `add_to_wishlist` | 欲しいものリストに追加／保存。 |
| `inquiry` | 問い合わせ／連絡。 |
| `call` | 電話。 |
| `lead` | リード生成。 |
| `view_product` | 商品詳細を表示。 |
| `view_content` | コンテンツを表示。 |
| `search` | 検索。 |
| `share` | 共有。 |
| `clip_coupon` | クーポンを発行。 |
| `view_item_list` | リストを表示。 |
| `about_us` | 会社概要ページを表示。 |
| `staff` | サービススタッフを表示。 |
| `location` | 事業所の所在地を表示／道順を取得。 |
| `promotion` | イベント／プロモーションに登録。 |
| `add_contact_method` | 連絡チャネルを追加。 |
| `opt_in_marketing` | マーケティング情報の受信を許可。 |
| `subscribe` | 購読。 |
| `review` | レビューを投稿。 |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `order_total` | 注文合計（`_ctotal`を上書きします）。 |
| `type` | コンバージョンイベントのタイプ。 |
| `id` | コンバージョンIDまたは顧客のアクションID。 |
| `value` | 複数の商品またはサービスの合計金額。 |
| `item_id` | 商品ID（`_cprod`を上書きします）。 |
| `name` | 商品名（`_cprodname`を上書きします）。 |
| `category` | 商品カテゴリー（`_ccat`を上書きします）。 |
| `quantity` | 商品数量（`_cquan`を上書きします）。 |
| `payAmount` | 特定の商品に対して支払われた合計金額。単価ではありません。 |
| `option` | 色やサイズなどの商品オプション（例：`color:red, size:240`）。 |
| `purchase` | 購入完了。 |
| `begin_checkout` | チェックアウト開始。 |
| `sign_up` | サインアップ。 |
| `add_to_cart` | カートに追加。 |
| `schedule` | 予約完了。 |
| `save_store` | 店舗を追加／保存。 |
| `add_to_wishlist` | 欲しいものリストに追加／保存。 |
| `inquiry` | 問い合わせ／連絡。 |
| `call` | 電話。 |
| `lead` | リード生成。 |
| `view_product` | 商品詳細を表示。 |
| `view_content` | コンテンツを表示。 |
| `search` | 検索。 |
| `share` | 共有。 |
| `clip_coupon` | クーポンを発行。 |
| `view_item_list` | リストを表示。 |
| `about_us` | 会社概要ページを表示。 |
| `staff` | サービススタッフを表示。 |
| `location` | 事業所の所在地を表示／道順を取得。 |
| `promotion` | イベント／プロモーションに登録。 |
| `add_contact_method` | 連絡チャネルを追加。 |
| `opt_in_marketing` | マーケティング情報の受信を許可。 |
| `subscribe` | 購読。 |
| `review` | レビューを投稿。 |