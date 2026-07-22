---
title: Movable Ink Studio タグ構成ガイド
description: この記事では、iQタグ管理アカウントでMovable Ink Studioタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/movable-ink-tag/
---
トラッキングの実装には、2つの補完的なスクリプトが関与します：

* **行動追跡スクリプト**：追跡されるすべてのページでロードされます。
* **コンバージョン追跡スクリプト**：注文確認またはコンバージョンページでのみロードされます。これは、注文IDが構成されたときに自動的に行われます。

両方のスクリプトは非同期であり、サイトのパフォーマンスに影響を与えません。

### 行動追跡

Studioの行動スクリプトは、インストールされているすべてのページでページビューイベントを送信します。ページビューのイベントパラメータをマッピングする必要はありません。ビーコンにはページURLが含まれ、訪問プロファイルに活動がリンクされます。

コンバージョンは、`addProduct`、`addPromo`、およびコンバージョンイベントをトリガーするためにEコマース拡張機能を使用します。Studioはイベント固有のパラメータマッピングをサポートしていません。これは、明示的なイベントモデルを使用するMovable Ink Da Vinciタグとは異なります。

## 要件

Movable Ink Studioタグには以下が必要です：

* Movable Inkアカウント構成からのトラッキングサブドメイン。
* ユニークなユーザーIDとキャンペーンIDのためのメールサービスプロバイダー（ESP）内のマージタグ。

## 検証とテスト

[Movable Ink行動追跡Chrome拡張機能](https://chromewebstore.google.com/detail/movable-ink-behavior-trac/icfallhogjlkfkcojmplakniiofcllgi?hl=en-US)を使用して、行動追跡とサイトマップ構成を検証します。

Movable Ink Studioの分析ダッシュボードで、コンバージョンと製品パラメータが正しく受信および処理されていることを確認します。

## タグのヒント

* 注文IDが提供されると、コンバージョン追跡が自動的に行われます。
* Eコマース拡張機能をサポートしています：
    * 注文ID（`identifier`）
    * 注文合計（`revenue`）
    * 製品SKUのリスト（`sku`）
    * 製品名のリスト（`name`）
    * 製品数量のリスト（`quantity`）
    * 製品価格のリスト（`price`）
* マッピングを使用して：
    * プロモーションコードの配列を渡す（`promo_code`）
    * プロモーションの説明の配列を渡す（`promo_description`）
    * その他の製品データの配列を渡す（`other_product_data`）
    * Eコマース拡張機能とトラッキングサブドメインの値を動的にオーバーライドする

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **トラッキングサブドメイン**：Movable Inkアカウントのトラッキングサブドメイン。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `tracking_subdomain` | トラッキングサブドメイン。 |

### Eコマース

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文ID（`_corder`をオーバーライド）。 |
| `order_total` | `Number` | 注文合計（`_ctotal`をオーバーライド）。 |
| `product_name` | `Array` | 製品名のリスト（`_cprodname`をオーバーライド）。 |
| `product_sku` | `Array` | 製品SKUのリスト（`_csku`をオーバーライド）。 |
| `product_quantity` | `Array` | 製品数量のリスト（`_cquan`をオーバーライド）。 |
| `product_price` | `Array` | 製品価格のリスト（`_cprice`をオーバーライド）。 |
| `other_product_data` | `Array` | その他の製品データ。 |
| `promo_code` | `Array` | プロモーションコードのリスト。 |
| `promo_description` | `Array` | プロモーションの説明のリスト。 |