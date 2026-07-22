---
title: TradeDoubler コンバージョン トラッキング タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで TradeDoubler コンバージョン トラッキング タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tradedoubler-conversion-tracking-tag/
---
## レガシー Trackback タグからの移行


<blockquote>
Trackback タグは現在非推奨となり、新しいコンバージョン トラッキング バージョンに置き換えられ、タグマーケットプレイスではもはや提供されていません。新しいコンバージョン トラッキング タグを追加する前に、すべての Trackback タグのインスタンスを無効にしてください。
</blockquote>


## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加した後、以下の構成を構成します：

* **タグタイプ**：（必須）ロードしたいタグのタイプを選択します。
  * `Sale`：`tbs.tradedoubler.com` にホストされている販売トラッキングピクセルをロードします。
  * `Lead`：`tbl.tradedoubler.com` にホストされているリードトラッキングピクセルをロードします。
  * `Product`：製品レベルのトラッキングピクセルをロードします。

* **組織 ID**：（必須）TradeDoubler によって提供される数値の組織 ID。このフィールドは **タグタイプ** が `Sale` または `Lead` に構成されている場合のみ適用されます。
* **イベント ID**：（必須）追跡したい販売/リードイベントに割り当てられた数値識別子。このフィールドは **タグタイプ** が `Sale` または `Lead` に構成されている場合のみ適用されます。この値をデータマッピングを通じて構成する場合は、このフィールドを空白のままにする必要があります。
* **トラッキング同意**：トラッキング同意を有効または無効にします。このフィールドを上書きするためのマッピングを使用します。

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールがデフォルトのルールです。特定のページでこのタグをロードしたい場合は、関連する条件を持つ新しいルールを作成します。

### ベストプラクティス

* 販売完了後に表示される確認ページに販売タグを配置します。
* サイト訪問がサインアップまたは登録できるページにリードタグを配置します。
* 製品と製品カテゴリの訪問のインタラクションを追跡したいページに製品タグを配置します。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Tradedoubler コンバージョン トラッキング タグの宛先変数は、そのデータマッピングタブに組み込まれています。

### 標準

| 変数                | タイプ                | 説明                                       |
|:-------------------|:--------------------|:------------------------------------------|
| `tracking_consent` | Boolean             | 訪問がトラッキング同意を与えたかどうか。       |
| `organization`     | String              | 組織 ID。                                  |
| `programId`        | String              | プログラム ID。                            |
| `tdevent`          | String              | イベント ID。                              |
| `tagtype`          | String              | タグタイプ。                               |
| `tduid`            | String              | Tradedoubler 固有のトラッキング ID。       |
| `chksum`           | String              | チェックサム。                             |
| `extid`            | String              | SHA-256 ハッシュを使用したメールアドレス。   |
| `exttype`          | Integer             | ID タイプ。可能な値は `0` または `1`。     |
| `voucher`          | String              | バウチャーコード。                         |
| `validOn`          | String              | 有効日。`YYYY-MM-DD` 形式を使用します。    |
| `validOn`          | String              | `YYYY-MM-DD` 形式の検証日。                |
| `cdt`              | String              | `extid` と `exttype` の親。                |
| `cdt`              | String              | TradeDoubler 固有のフィールドで、`extid` と `exttype` と一緒に使用します。TradeDoubler の実装で提供された正確な値と形式を使用してください。 |
| `fallback_url`     | String              | フォールバック URL。                       |
| `program`          | Boolean             | コンバージョン トラッキング タグが特定のアフィリエイトプログラムに関連しているかどうか。 |

### Eコマース

Tradedoubler コンバージョン トラッキング タグは Eコマース対応であり、デフォルトの [Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/) マッピングを自動的に使用します。拡張機能のマッピングを上書きしたい場合や、拡張機能で提供されていない Eコマース変数が必要な場合を除き、このカテゴリでの手動マッピングは通常必要ありません。

| 変数                  | タイプ    | 説明                                         |
|:---------------------|:--------|:--------------------------------------------|
| `order_id`           | String  | 注文 ID（`_corder` を上書き）。               |
| `order_subtotal`     | Number  | 小計（`_csubtotal` を上書き）。               |
| `order_currency`     | String  | 通貨（`_ccurrency` を上書き）。               |
| `order_promo_code`   | String  | プロモコード（`_cpromo` を上書き）。           |
| `product_id`         | Array   | 製品 ID のリスト（`_cprod` を上書き）。        |
| `product_sku`        | Array   | SKU のリスト（`_csku` を上書き）。            |
| `product_quantity`   | Array   | 数量のリスト（`_cquan` を上書き）。           |
| `product_unit_price` | Array   | 価格のリスト（`_cprice` を上書き）。          |
| `gr`                 | Array   | 製品グループ ID のリスト。                   |

## ベンダー文書

* [TradeDoubler: コンバージョン トラッキング](http://dev.tradedoubler.com/tracking/advertiser/)
* [TradeDoubler: 開発者リソース](http://dev.tradedoubler.com/)