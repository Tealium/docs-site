---
title: NextDoorコンバージョンピクセル（レガシー）
description: この記事では、Nextdoorコンバージョンピクセルタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/nextdoor-conversion-pixel-tag/
---

<blockquote>
これはタグのレガシーバージョンです。近日中に非推奨となり、[Nextdoorユニバーサルピクセルタグ](https://docs.tealium.com/nextdoor-universal-pixel-tag/)に置き換えられる予定です。
</blockquote>


Nextdoorコンバージョンピクセルを使用すると、Nextdoor上の広告に起因するコンバージョンを正確に測定できます。Nextdoorピクセルは、キャンペーンのアクション単価（CPA）を把握するうえで重要です。また、ターゲティングとクリエイティブ戦略を最適化できるため、最終的に投資収益率（ROI）の向上につながります。

## タグに関するヒント

* マッピングを使用してStandardパラメータを上書きします。
* Eコマース拡張機能のパラメータがサポートされています。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **ピクセルID**：NextDoorピクセルID。
* **自動ページビュー**：ページビュー用のトリガーを自動的に作成します。
* **自動購入イベント**：購入イベント用のトリガーを自動的に作成します。
* **イベントIDを生成**：Nextdoorの各トラッキングイベントに対してイベントIDを自動的に生成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `pixelId` | 文字列 | NextDoorピクセルID |
| `autoPageView` | ブール値 | 自動ページビュー |
| `autoPurchaseEvent` | ブール値 | 自動購入イベント |
| `generate_event_id` | ブール値 | イベントIDを生成 |
| `event_id` | 文字列 | イベントID |

### ユーザー

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `userEmail` | 文字列 | ユーザーのメールアドレス |
| `UserEmailHashed` | 文字列 | ユーザーのメールアドレス（ハッシュ化済み） |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `order_id`（`_corder`を上書き） | 文字列 | 注文ID |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `PAGE_VIEW` | ページビュー |
| `LEAD` | リード |
| `PURCHASE` | 購入 |
| `SIGN_UP` | サインアップ |
| `ADD_TO_CART` | カートに追加 |
| `INITIATE_CHECKOUT` | チェックアウトを開始 |
| `SEARCH` | 検索 |
| `ADD_TO_WISHLIST` | ウィッシュリストに追加 |
| `SUBSCRIBE` | 購読 |
| `VIEW_CONTENT` | コンテンツを表示 |
| `CUSTOM_CONVERSION_1` | カスタムコンバージョン1 |
| `CUSTOM_CONVERSION_2` | カスタムコンバージョン2 |
| `CUSTOM_CONVERSION_3` | カスタムコンバージョン3 |
| `CUSTOM_CONVERSION_4` | カスタムコンバージョン4 |
| `CUSTOM_CONVERSION_5` | カスタムコンバージョン5 |
| `CUSTOM_CONVERSION_6` | カスタムコンバージョン6 |
| `CUSTOM_CONVERSION_7` | カスタムコンバージョン7 |
| `CUSTOM_CONVERSION_8` | カスタムコンバージョン8 |
| `CUSTOM_CONVERSION_9` | カスタムコンバージョン9 |
| `CUSTOM_CONVERSION_10` | カスタムコンバージョン10 |