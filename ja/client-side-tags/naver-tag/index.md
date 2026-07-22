---
title: ネイバータグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでネイバータグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/naver-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* 次のEコマース変数を使用します
  * `_ctotal`
* **ページタイプ**には次のオプションがあります
  * なし - 0
  * チェックアウト - 1
  * サインアップ - 2
  * ショッピングカート - 3
  * 予約/登録 - 4
  * その他 - 5

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **アカウントID**：ネイバーのアカウントID。
* **ページタイプ**：このパラメータは非推奨です。
* **サブドメイン**：ネイバーが指定する場合のみ、このパラメータを構成します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `account_id` | アカウントID。 |
| `page_type` | ページタイプ。 |
| `subdomain` | サブドメイン。 |

### Eコマース

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `order_total` | `Number` | 注文合計（`_ctotal`を上書き）。 |
| `type` | `String` | 変換イベントのタイプ。 |
| `id` | `String` | 変換IDまたは顧客のアクションID。 |
| `value` | `String` | 注文内のすべての製品およびサービスの送料を除く合計価格。 |
| `item_id` | `Array` | アイテムID（`_cprod`を上書き）。 |
| `name` | `Array` | アイテム名（`_cprodname`を上書き）。 |
| `category` | `Array` | アイテムカテゴリ（`_ccat`を上書き）。 |
| `quantity` | `Array` | アイテム数量（`_cquan`を上書き）。 |
| `payAmount` | `Array` | 特定のアイテムに対して支払われた合計金額。これは単価ではありません。 |
| `option` | `Array` | アイテムの製品オプション（例：`color:red, size:240`）。 |

### イベントトリガー

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `purchase` | 購入完了。 |
| `begin_checkout` | チェックアウト開始。 |
| `sign_up` | サインアップ。 |
| `add_to_cart` | カートに追加。 |
| `schedule` | 予約完了。 |
| `save_store` | 店舗を追加/保存。 |
| `add_to_wishlist` | お気に入りリストに追加/保存。 |
| `inquiry` | 問い合わせ/お問い合わせ。 |
| `call` | 電話通話。 |
| `lead` | リード生成。 |
| `view_product` | 製品詳細の表示。 |
| `view_content` | コンテンツの表示。 |
| `search` | 検索。 |
| `share` | 共有。 |
| `clip_coupon` | クーポンの発行。 |
| `view_item_list` | リストの表示。 |
| `about_us` | 会社情報ページの表示。 |
| `staff` | サービススタッフの表示。 |
| `location` | 事業所の場所の表示/道順の取得。 |
| `promotion` | イベント/プロモーションへの登録。 |
| `add_contact_method` | 通信チャンネルの追加。 |
| `opt_in_marketing` | マーケティングコミュニケーションの受信。 |
| `subscribe` | 登録。 |
| `review` | レビューの作成。 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `order_total` | 注文合計（`_ctotal`を上書き）。 |
| `type` | 変換イベントのタイプ。 |
| `id` | 変換IDまたは顧客のアクションID。 |
| `value` | 複数の製品またはサービスの合計金額。 |
| `item_id` | アイテムID（`_cprod`を上書き）。 |
| `name` | アイテム名（`_cprodname`を上書き）。 |
| `category` | アイテムカテゴリ（`_ccat`を上書き）。 |
| `quantity` | アイテム数量（`_cquan`を上書き）。 |
| `payAmount` | 特定のアイテムに対して支払われた合計金額。これは単価ではありません。 |
| `option` | アイテムの製品オプション（例：`color:red, size:240`）。 |
| `purchase` | 購入完了。 |
| `begin_checkout` | チェックアウト開始。 |
| `sign_up` | サインアップ。 |
| `add_to_cart` | カートに追加。 |
| `schedule` | 予約完了。 |
| `save_store` | 店舗を追加/保存。 |
| `add_to_wishlist` | お気に入りリストに追加/保存。 |
| `inquiry` | 問い合わせ/お問い合わせ。 |
| `call` | 電話通話。 |
| `lead` | リード生成。 |
| `view_product` | 製品詳細の表示。 |
| `view_content` | コンテンツの表示。 |
| `search` | 検索。 |
| `share` | 共有。 |
| `clip_coupon` | クーポンの発行。 |
| `view_item_list` | リストの表示。 |
| `about_us` | 会社情報ページの表示。 |
| `staff` | サービススタッフの表示。 |
| `location` | 事業所の場所の表示/道順の取得。 |
| `promotion` | イベント/プロモーションへの登録。 |
| `add_contact_method` | 通信チャンネルの追加。 |
| `opt_in_marketing` | マーケティングコミュニケーションの受信。 |
| `subscribe` | 登録。 |
| `review` | レビューの作成。 |
