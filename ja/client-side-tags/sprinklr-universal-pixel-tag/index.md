---
title: Sprinklr Universal Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでSprinklr Universal Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sprinklr-universal-pixel-tag/
---
## タグに関するヒント

* マッピングを使用して、クライアントIDを動的に構成します。
* 次のEコマース拡張機能パラメータをサポートしています。
    * 注文小計（`_csubtotal`）
    * 注文通貨（`_ccurrency`）
    * 数量のリスト（`_cquan`）
* 数量は、特定のイベントに含まれるすべての商品の合計数です。マッピングで数量の値が指定されていない場合、Eコマース拡張機能の商品数量配列が利用可能であれば、そのリストから数量が計算されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を行います。

* **クライアントID**：Sprinklrから提供されたクライアントID。
* **イベントIDを生成**：Sprinklrの各トラッキングイベントに対してイベントIDを自動的に生成します。
<!--

### Leads API


<blockquote>
この機能を使用するには、有効な[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Sprinklr Leads API Connectorをサポートするには、**イベントIDを生成**を`true`に構成します。**イベントIDを生成**を有効にすると、このタグはトラッキングされるイベントごとに一意のイベントIDを生成し、Sprinklr Leads API Connectorで使用する属性としてEvent Streamingに送信するとともに、`event_id`パラメータでSprinklr Universal Pixelに渡します。このイベントID属性をコネクタでマッピングすることで、Webベースのタグとサーバーサイド統合を同期できます。

このタグは、次の命名規則に従って生成されたイベント属性を使用し、イベントIDを送信します。

```nohl
sprinklr_event_id_{SPRINKLR_EVENT}_{TAG_UID}
```

たとえば、タグ#32の購入イベントでは、次の属性と値が送信されます。

```json
{
  "sprinklr_event_id_Purchase_32": "028b2ade7478..."
}
```

同じタグのページビューイベントでは、次の属性と値が送信されます。

```json
{
  "sprinklr_event_id_PageView_32": "084b1cda7461..."
}
```

#### 重複排除

イベントが適切に重複排除されるようにするには、Sprinklr Universal PixelタグのイベントIDを、Tealium Collectタグから送信されるペイロードに含める必要があります。これを行うには、次の手順を実行します。

* **タグのタイミング**ドロップダウンから、**優先**を選択します。
* **バンドルフラグ**トグルを`On`に構成します。
* [読み込み順序マネージャー画面](https://docs.tealium.com/load-order-manager/)を使用して、Sprinklr Universal PixelタグをTealium Collectタグより先に実行します。Tealium Collectタグは最後に実行することをお勧めします。-->

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです。

### タグ構成とグローバルパラメータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `client_id` | 文字列 | クライアントID。 |
| `eventId` | 文字列 | イベントID。 |
| `leadId` | 文字列 | リードID。 |
| `custom.myvar` |  | カスタムパラメータ。 |
| `generate_event_id` | ブール値 | イベントIDを生成します。 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `value` | 値（`_csubtotal`を上書きします）。 |
| `currency` | 通貨（`_ccurrency`を上書きします）。 |
| `product_quantity` | 商品数量のリスト（`_cquan`を上書きします）。 |
| `quantity` | イベントに含まれるすべての商品の合計数。 |

### ユーザーデータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `userInfo.firstName` | 文字列 | 顧客の名。 |
| `userInfo.lastName` | 文字列 | 顧客の姓。 |
| `userInfo.fullName` | 文字列 | 顧客の氏名。 |
| `userInfo.customerId` | 文字列 | 顧客の一意の識別子。 |
| `userInfo.anonymousId` | 文字列 | Tealium訪問IDを自動的に送信します。上書きするには変数をマッピングします。ユーザーとして登録されていない顧客の一意の識別子です。 |
| `userInfo.phoneNo` | 文字列 | 顧客の電話番号。 |
| `userInfo.email` | 文字列 | 顧客のメールアドレス。 |