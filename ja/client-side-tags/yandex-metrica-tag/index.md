---
title: Yandex.Metricaタグ構成ガイド
description: この記事では、タグ管理アカウントでYandex.Metricaタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yandex-metrica-tag/
---
Yandex.Metricaは、サイトのコンバージョン率向上に役立つ無料のツールです。Metricaを使用すると、Webサイトの主要な効果指標を監視し、ユーザー行動を分析して、広告キャンペーンの効果を評価できます。

## タグに関するヒント

マッピングを使用すると、標準の構成値を動的に上書きできます。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **タグID**：YandexタグID
* **クリックマップ**：マウスの移動、スクロール、クリックなど、サイト上でのユーザーアクティビティを詳細に記録します
* **リンクのトラッキング**：外部リンクおよびダウンロードリンクのトラッキングを構成します
* **正確な直帰トラッキング**：正確な直帰率を有効にし、15000ミリ秒（15秒）後に非直帰イベントを登録します
* **Webvisor**：Webvisorはユーザーの操作を動画形式で再現し、ページ内をどのように移動したか、マウスカーソルをどのように動かしたか、どのリンクをクリックしたかなど、サイト上でのユーザー行動を確認できるようにします。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールについて詳しくは、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
| --- | --- |
| ベースURL (base\_url) | \[文字列\] |
| ヒットイベントURL (url) | \[文字列\] |
| タグID (tagId) | \[文字列\] |
| クリックマップ (clickmap) | \[ブール値\] |
| リンクのトラッキング (trackLinks) | \[ブール値\] |
| 正確な直帰トラッキング (accurateTrackBounce) | \[ブール値\] |
| Webvisor (webvisor) | \[ブール値\] |
| Eコマースデータレイヤー (ecommerce) | \[文字列/ブール値\] |

### Eコマース

| 変数 | 説明 |
| --- | --- |
| 注文ID (order\_id)（\_corderを上書き） | \[文字列/数値\] |
| 注文クーポンコード (order\_coupon\_code)（\_cpromoを上書き） | \[文字列\] |
| 注文合計 (order\_total)（\_ctotalを上書き） | \[数値/文字列\] |
| 注文通貨 (order\_currency)（\_ccurrencyを上書き） | \[文字列\] |
| ゴールID (goal\_id) | \[数値/文字列\] |
| 商品IDのリスト (id)（\_cskuを上書き） | \[配列\] |
| 商品名のリスト (name)（\_cprodnameを上書き） | \[配列\] |
| 商品ブランドのリスト (brand)（\_cbrandを上書き） | \[配列\] |
| 商品カテゴリーのリスト (category)（\_ccatを上書き） | \[配列\] |
| 商品クーポンのリスト (coupon) | \[配列\] |
| 商品価格のリスト (price)（\_cpriceを上書き） | \[配列\] |
| 商品数量のリスト (quantity)（\_cquanを上書き） | \[配列\] |
| 商品掲載位置のリスト (position) | \[配列\] |
| 商品バリエーションのリスト (variant) | \[配列\] |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

| 変数 | 説明 |
| --- | --- |
| ヒット（ページビューイベントを送信）(hit) | hit |
| 商品を表示 (detail) | detail |
| 商品を追加 (add) | add |
| 商品を削除 (remove) | remove |
| 購入 (purchase) | purchase |

### イベント固有のパラメーター

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

| 変数 | 説明 |
| --- | --- |
| ヒット (hit) | hit |
| 商品を表示 (detail) | detail |
| 商品を追加 (add) | add |
| 商品を削除 (remove) | remove |
| 購入 (purchase) | purchase |