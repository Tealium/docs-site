---
title: Reddit Pixel タグ構成ガイド
description: Tealium iQで広告後のインタラクションを追跡し、コンバージョンを測定し、リターゲティングを有効にするためのReddit Pixelタグを構成します。
url: https://docs.tealium.com/ja/client-side-tags/reddit-pixel-tag/
---
Reddit Pixelタグは広告後のインタラクションを追跡し、コンバージョン測定とリターゲティングをサポートします。

## 要件

* Reddit広告アカウント
* Reddit Pixel ID

## タグのヒント

* マッピングを使用して標準の構成値を上書きし、イベントをトリガーします。
* **Order ID**が構成されているときに購入イベントが発火します。
* Reddit PixelイベントIDをサーバーサイド属性として利用可能にするには、**Generate Event ID**を`true`に構成し、[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)の最新バージョンを使用します。
* Reddit PixelタグとReddit Conversionsコネクタの両方を実装している場合のみ、[Reddit Conversionsコネクタ](https://docs.tealium.com/reddit-conversions-connector/)のコンバージョンID構成を使用することをお勧めします。コンバージョンID構成を使用すると、同じコンバージョンイベントが両方のソースから送信された場合に二重計算されるのを防ぐことができます。この値が不適切に渡されると、帰属とキャンペーンのパフォーマンスに影響を与える可能性があります。
* 最も正確なコンバージョン追跡とレポートのために、Redditでの高度なマッチングを使用することをお勧めします。メールアドレスと電話番号をプレーン値またはSHA256で事前ハッシュされた形式で渡します。Redditライブラリは、送信前にプレーンメールアドレスにSHA256ハッシングを適用します。
* 使用する予定のパラメータのみをマッピングし、Redditのドキュメントでサポートを確認してください。
* 異なるイベントが異なるメタデータを必要とする場合に、イベント固有のパラメータを使用して細かい制御を行います。
* 収益イベントの場合、イベントレベルの`value`と`itemCount`、製品レベルの`quantity`と`itemPrice`の両方を送信します。一方のフィールドセットのみを送信すると、Reddit広告のレポートや最適化が制限される可能性があります。
* 製品配列をインデックスで揃えます。単一の値と配列を混在させるのは、単一製品のペイロードを意図している場合のみにしてください。
* イベント固有のパラメータを使用して、誤って購入専用のメタデータを他のイベントに適用するのを避けます。
* タグはRedditのイベントレベルパラメータ要件を強制します。未定義または空の値は削除され、特定のイベントに対してRedditがサポートしていないパラメータはペイロードから削除されます。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加するには、次の構成を構成します：

* **Pixel ID**: あなたのReddit Pixel ID。
* **Send Page Visit**
    * デフォルトでは、タグはサイトの各ページに対してページ訪問イベントを自動的に記録します。
    * Reddit Pixelにページ訪問イベントを送信したくない場合は、このオプションを`false`に構成します。
* **Send Default Purchase Event**: デフォルトでは、タグはサイト上の購入イベントを追跡します。購入イベントを無効にするには、このオプションを`false`に構成します。
* **Generate Event ID**: すべてのReddit追跡イベントに対してイベントIDを自動生成します。

### Conversions API


<blockquote>
この機能にはアクティブな[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Reddit Conversions APIをサポートするには、**Generate Event ID**を`true`に構成します。**Generate Event ID**が有効になっている場合、タグは追跡された各イベントに対して一意のイベントIDを生成します。タグはイベントIDをTealium EventStreamの属性として送信し、Reddit Conversionsコネクタで使用し、`event_id`パラメータとしてReddit Pixelに渡します。このイベントID属性をコネクタでマップして、ウェブベースのタグとサーバーサイドの統合を同期します。

タグは次の命名規則を使用してイベントIDを生成されたイベント属性として送信します：

```nohl
reddit_pixel_event_id_{REDDIT_EVENT}_{TAG_UID}
```

たとえば、タグ＃32からの購入イベントは次の属性と値を送信します：

```json
{
  "reddit_pixel_event_id_Purchase_32": "028b2ade7478..."
}
```

同じタグからのページビューイベントは次の属性と値を送信します：

```json
{
  "reddit_pixel_event_id_PageView_32": "084b1cda7461..."
}
```

#### 重複排除

適切なイベントの重複排除を確実に行うために、Reddit PixelタグからのイベントIDをTealium Collectタグによって送信されるペイロードに含める必要があります。これを行うには、次の手順を使用します：

* **Tag Timing**ドロップダウンから**Prioritized**を選択します。
* **Bundle Flag**トグルを`On`に構成します。
* [Load Order Manager画面](https://docs.tealium.com/load-order-manager/)を使用して、Tealium Collectタグの前にReddit Pixelタグを発火させます。Tealium Collectタグは最後に発火させることをお勧めします。

これらのイベントID属性の使用に関する情報については、[Reddit Conversionsコネクタ: ウェブイベントの重複排除](https://docs.tealium.com/reddit-conversions-connector/#deduplication-for-web-events)を参照してください。

## 検証

タグが期待通りに動作していることを確認するには、ブラウザの開発者ツールと[Reddit Pixel Helper](https://business.reddithelp.com/s/article/Reddit-Pixel-Helper-Chrome-extension)ブラウザ拡張機能を使用します：

* 各イベントに対して期待されるパラメータが表示されることを確認します。
* サポートされていないメタデータや無効なメタデータに関する警告が表示されないことを確認します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

以下のカテゴリを使用してパラメータをマップします。マップされたパラメータが特定のイベントに対してRedditによってサポートされていない場合、タグはそれをペイロードから削除します。[イベント固有のパラメータ](#event-specific-parameters)を使用して、イベントごとに送信されるパラメータを制御します。

利用可能なカテゴリは次のとおりです：

### 標準

| 変数                  | データタイプ | 説明              |
|-----------------------|-----------|----------------------|
| `pixel_id`            | 文字列    | Pixel ID.            |
| `send_page_visit`     | ブール値   | ページ訪問を送信する。     |
| `send_purchase_event` | ブール値   | 購入イベントを送信する。 |
| `generate_event_id`   | ブール値   | イベントIDを生成する。   |
| `event_id`            | 文字列    | イベントID。            |
| `conversion_id`       | 文字列    | コンバージョンID。       |
| `transaction_id`      | 文字列    | トランザクションID。      |

### Eコマース

| 変数            | データタイプ | 説明                            |
|-----------------|-----------|------------------------------------|
| `itemCount`     | 数値      | アイテム数。                        |
| `value`         | 数値      | 値。                             |
| `currency`      | 文字列    | 通貨（`_ccurrency`を上書き）。 |
| `transactionId` | 文字列    | トランザクションID。                    |

### 製品データ

| 変数       | タイプ/値      | 説明                                |
|:-----------|:------------|:---------------------------------------|
| `id`        | 配列       | 製品ID（`_cprod`を上書き）。         |
| `category`  | 配列       | 製品カテゴリ（`_ccat`を上書き）。    |
| `name`      | 配列       | 製品名（`_cprodname`を上書き）。   |
| `quantity`  | 配列       | 製品数量（`_cquan`を上書き）。   |
| `itemPrice` | 配列       | 製品単価（`_cprice`を上書き）。|

### イベント

選択したイベントをトリガーするために必要なマップされた変数の値を入力します。

| 変数            | 説明          |
|:----------------|:-----------------|
| `PageVisit`     | ページ訪問。      |
| `ViewContent`   | コンテンツ閲覧。    |
| `Search`        | 検索。          |
| `AddToCart`     | カートに追加。     |
| `AddToWishlist` | ウィッシュリストに追加。|
| `Purchase`      | 購入。          |
| `Lead`          | リード。        |
| `SignUp`        | サインアップ。    |
| `Custom`        | カスタムイベント。   |
### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数             | 説明                   |
|:----------------|:----------------------|
| `currency`      | 通貨。                 |
| `category`      | 商品カテゴリ。         |
| `name`          | 商品名。               |
| `id`            | 商品ID。               |
| `quantity`      | 商品数量。             |
| `itemPrice`     | 商品単価。             |
| `content_type`  | コンテンツタイプ。     |
| `contents`      | 内容。                 |
| `predicted_ltv` | 予測される生涯価値。   |
| `search_string` | 検索文字列。           |
| `status`        | ステータス。           |
| `itemCount`     | アイテム数。           |
| `value`         | 価値。                 |

### 高度なマッチング

| 変数           | データタイプ | 説明             | 
|:--------------|:------------|:----------------|
| `email`       | 文字列      | メールアドレス。 |
| `phoneNumber` | 文字列      | 電話番号。       |
| `idfa`        | 文字列      | IDFA。           |
| `aaid`        | 文字列      | AAID。           | 
| `externalId`  | 文字列      | 外部ID。         | 

### LDU

Reddit Pixelがデータ処理モードで初期化されると、ページから発火されるすべてのコンバージョンイベントには自動的に以下のパラメータが含まれます：

| 変数   | データタイプ | 説明 |
|:-------|:------------|:----|
|  `dpm` | 文字列      | データ処理モード。デフォルト値は `LDU`。 |
|  `dpcc`| 文字列      | データ処理国コード。ISO 3166-1 アルファ-2 国コード形式。 |
|  `dprc`| 文字列      | データ処理地域コード。ISO 3166-2 地域コード形式で、国のプレフィックスがあるかないか。 |