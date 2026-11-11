---
title: TradeDoublerコンバージョントラッキングタグ構成ガイド
description: この記事では、タグ管理アカウントでTradeDoublerコンバージョントラッキングタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tradedoubler-conversion-tracking-tag/
---
## 従来のTrackbackタグからの移行


<blockquote>
Trackbackタグは、新しいコンバージョントラッキングバージョンへの移行に伴い廃止され、タグマーケットプレイスでは提供されなくなりました。新しいコンバージョントラッキングタグを追加する前に、Trackbackタグのすべてのインスタンスを必ず無効化してください。
</blockquote>


## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **タグタイプ**：（必須）読み込むタグのタイプを選択します。
  * `Sale`：`tbs.tradedoubler.com`でホストされている売上トラッキングピクセルを読み込みます。
  * `Lead`：`tbl.tradedoubler.com`でホストされているリードトラッキングピクセルを読み込みます。
  * `Product`：商品レベルのトラッキングピクセルを読み込みます。

* **組織ID**：（必須）TradeDoublerから提供される数値の組織IDです。このフィールドは、**タグタイプ**が`Sale`または`Lead`に構成されている場合にのみ適用されます。
* **イベントID**：（必須）トラッキングする売上／リードイベントに割り当てられた数値識別子です。このフィールドは、**タグタイプ**が`Sale`または`Lead`に構成されている場合にのみ適用されます。データマッピングを使用してこの値を構成する場合は、このフィールドを空白のままにする必要があります。
* **トラッキング同意**：トラッキングへの同意を有効または無効にします。モードを含め、このフィールドを上書きするにはマッピングを使用します。

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトのルールは、**すべてのページで読み込む**ルールです。このタグを特定のページで読み込む場合は、該当する条件を指定して新しいルールを作成します。

### ベストプラクティス

* 売上タグは、売上の完了後に表示される確認ページに配置します。
* リードタグは、サイト訪問がサインアップまたは登録できるページに配置します。
* 商品タグは、訪問による商品や商品カテゴリーの操作をトラッキングするページに配置します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Tradedoublerコンバージョントラッキングタグの宛先変数は、［データマッピング］タブに組み込まれています。

### 標準

| 変数               | 型                  | 説明                                    |
|:-------------------|:--------------------|:----------------------------------------|
| `tracking_consent` | Boolean             | 訪問がトラッキングに同意しているかどうか。 |
| `organization`     | String              | 組織ID。                                |
| `programId`        | String              | プログラムID。                          |
| `tdevent`          | String              | イベントID。                            |
| `tagtype`          | String              | タグタイプ。                            |
| `tduid`            | String              | Tradedoubler固有のトラッキングID。      |
| `chksum`           | String              | チェックサム。                          |
| `extid`            | String              | SHA-256でハッシュ化されたメールアドレス。 |
| `exttype`          | Integer             | IDタイプ。指定可能な値は`0`または`1`です。 |
| `voucher`          | String              | バウチャーコード。                      |
| `validOn`          | String              | 有効日。`YYYY-MM-DD`形式を使用します。  |
| `validOn`          | String              | `YYYY-MM-DD`形式の検証日。              |
| `cdt`              | String              | `extid`および`exttype`の親。            |
| `cdt`              | String              | `extid`および`exttype`とともに使用されるTradeDoubler固有のフィールド。TradeDoublerの実装で指定されている値と形式をそのまま使用してください。 |
| `fallback_url`     | String              | フォールバックURL。                     |
| `program`          | Boolean             | コンバージョントラッキングタグが特定のアフィリエイトプログラムに関連付けられているかどうか。 |

### Eコマース

TradedoublerコンバージョントラッキングタグではEコマースが有効になっているため、デフォルトの[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)のマッピングが自動的に使用されます。通常、次の場合を除き、このカテゴリーで手動マッピングを行う必要はありません。

* 拡張機能のマッピングを上書きする場合。
* 使用するEコマース変数が拡張機能で提供されていない場合。

| 変数                 | 型      | 説明                                      |
|:---------------------|:--------|:------------------------------------------|
| `order_id`           | String  | 注文ID（`_corder`を上書き）。             |
| `order_subtotal`     | Number  | 小計（`_csubtotal`を上書き）。            |
| `order_currency`     | String  | 通貨（`_ccurrency`を上書き）。            |
| `order_promo_code`   | String  | プロモーションコード（`_cpromo`を上書き）。 |
| `product_id`         | Array   | 商品IDのリスト（`_cprod`を上書き）。      |
| `product_sku`        | Array   | SKUのリスト（`_csku`を上書き）。          |
| `product_quantity`   | Array   | 数量のリスト（`_cquan`を上書き）。        |
| `product_unit_price` | Array   | 価格のリスト（`_cprice`を上書き）。       |
| `gr`                 | Array   | 商品グループIDのリスト。                  |

## ベンダーのドキュメント

* [TradeDoubler：コンバージョントラッキング](http://dev.tradedoubler.com/tracking/advertiser/)
* [TradeDoubler：開発者向けリソース](http://dev.tradedoubler.com/)