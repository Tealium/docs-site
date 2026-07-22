---
title: NextDoor コンバージョンピクセル（レガシー）
description: この記事では、Nextdoor コンバージョンピクセルタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/nextdoor-conversion-pixel-tag/
---

<blockquote>
これはタグのレガシーバージョンです。近々非推奨となり、[Nextdoor ユニバーサルピクセルタグ](https://docs.tealium.com/nextdoor-universal-pixel-tag/)に置き換えられます。
</blockquote>


Nextdoor の広告に起因するコンバージョンを正確に測定するために、Nextdoor コンバージョンピクセルを使用します。Nextdoor ピクセルは、キャンペーンのコストパフォーマンス（CPA）を理解するための鍵です。さらに、ターゲティングとクリエイティブ戦略を最適化することで、投資収益率（ROI）を向上させることができます。

## タグのヒント

* 標準パラメータを上書きするためにマッピングを使用します。
* サポートされている E-コマース拡張パラメータ。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Pixel ID**: あなたのNextDoorピクセルID。
* **Auto Page View**: ページビューのトリガーを自動的に作成します。
* **Auto Purchase Event**: 購入イベントのトリガーを自動的に作成します。
* **Generate Event ID**: Nextdoor トラッキングイベントごとにイベントIDを自動生成します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 構成

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `pixelId`  | 文字列 | NextDoor ピクセルID |
|  `autoPageView`  | ブール値 | 自動ページビュー |
| `autoPurchaseEvent`  | ブール値 | 自動購入イベント |
| `generate_event_id` | ブール値 | イベントIDの生成 |
| `event_id` | 文字列 | イベントID |

### ユーザー

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `userEmail`  | 文字列 | ユーザーのメールアドレス |
|  `UserEmailHashed`  | 文字列 | ハッシュ化されたユーザーのメールアドレス |

### E-コマース

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `order_id` (Overrides `_corder`)  | 文字列 | 注文ID |

### イベント
イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `PAGE_VIEW`| ページビュー |
| `LEAD`| リード |
| `PURCHASE`| 購入 |
| `SIGN_UP`| サインアップ |
| `ADD_TO_CART` | カートに追加 |
| `INITIATE_CHECKOUT` | チェックアウトの開始 |
| `SEARCH` | 検索 |
| `ADD_TO_WISHLIST` | ほしい物リストに追加 |
| `SUBSCRIBE` | 登録 |
| `VIEW_CONTENT` | コンテンツの閲覧 |
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
