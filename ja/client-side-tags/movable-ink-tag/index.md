---
title: Movable Ink Studioタグ構成ガイド
description: この記事では、タグ管理アカウントでMovable Ink Studioタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/movable-ink-tag/
---
トラッキングの実装には、相互に補完する2つのスクリプトが含まれます。

* **行動トラッキングスクリプト**：トラッキング対象のすべてのページで読み込まれます。
* **コンバージョントラッキングスクリプト**：注文確認ページまたはコンバージョンページでのみ読み込まれます。注文IDが構成されると、自動的に読み込まれます。

どちらのスクリプトも非同期であり、サイトのパフォーマンスには影響しません。

### 行動トラッキング

Studioの行動スクリプトは、インストールされているすべてのページでページビューイベントを送信します。ページビューにイベントパラメータをマッピングする必要はありません。ビーコンにはページURLが含まれ、アクティビティが訪問プロファイルに関連付けられます。

コンバージョンでは、E-Commerce拡張機能を使用して`addProduct`、`addPromo`、およびコンバージョンイベントをトリガーします。Studioでは、イベント固有のパラメーターマッピングはサポートされていません。これは、明示的なイベントモデルを使用するMovable Ink Da Vinciタグとは異なります。

## 要件

Movable Ink Studioタグには、以下が必要です。

* Movable Inkアカウント構成のトラッキングサブドメイン。
* 一意のユーザーIDとキャンペーンIDを取得するための、メールサービスプロバイダー（ESP）のマージタグ。

## 検証とテスト

[Movable Ink Behavior Tracking Chrome拡張機能](https://chromewebstore.google.com/detail/movable-ink-behavior-trac/icfallhogjlkfkcojmplakniiofcllgi?hl=en-US)を使用して、行動トラッキングとサイトマップの構成を検証します。

Movable Ink Studioの分析ダッシュボードで、コンバージョンと製品パラメーターが正しく受信および処理されていることを確認します。

## タグに関するヒント

* 注文IDが指定されると、コンバージョントラッキングが自動的に実行されます。
* 以下の項目についてE-Commerce拡張機能をサポートしています。  
    * 注文ID（`identifier`）  
    * 注文合計（`revenue`）  
    * 製品SKUのリスト（`sku`）  
    * 製品名のリスト（`name`）  
    * 製品数量のリスト（`quantity`）  
    * 製品価格のリスト（`price`）
* マッピングは、以下の目的で使用します。  
    * プロモーションコードの配列（`promo_code`）を渡す  
    * プロモーションの説明の配列（`promo_description`）を渡す  
    * その他の製品データの配列（`other_product_data`）を渡す  
    * E-Commerce拡張機能とトラッキングサブドメインの値を動的に上書きする

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を行います。

* **トラッキングサブドメイン**：Movable Inkアカウントのトラッキングサブドメイン。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `tracking_subdomain` | トラッキングサブドメイン。 |

### E-Commerce

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文ID（`_corder`を上書き）。 |
| `order_total` | `Number` | 注文合計（`_ctotal`を上書き）。 |
| `product_name` | `Array` | 製品名のリスト（`_cprodname`を上書き）。 |
| `product_sku` | `Array` | 製品SKUのリスト（`_csku`を上書き）。 |
| `product_quantity` | `Array` | 製品数量のリスト（`_cquan`を上書き）。 |
| `product_price` | `Array` | 製品価格のリスト（`_cprice`を上書き）。 |
| `other_product_data` | `Array` | その他の製品データ。 |
| `promo_code` | `Array` | プロモーションコードのリスト。 |
| `promo_description` | `Array` | プロモーションの説明のリスト。 |