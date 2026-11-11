---
title: KAYAKタグコネクタ構成ガイド
description: この記事では、タグ管理アカウントでKAYAKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kayak-tag-connector/
---
## タグに関するヒント

* イベントマッピングを使用して、確認ピクセルとキャンセルピクセルが送信されるタイミングを構成します。
* 「Commission Currency」の値が指定されていない場合、デフォルトでEコマースの「Currency」の値が使用されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **Partner Code**
  * KAYAKから提供される、KAYAK内部で使用されるコードです。
* **Click ID Query Parameter Name**
  * トラッキングURLでクリックIDを渡すために使用するクエリパラメータの名前です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグ構成

|変数|説明|
|---|---|
|パートナーコード| (partner\_code)|
|予約日| (bookedon)|
|KAYAKコミッション金額| (kayakcommission)|
|コミッション通貨| (commissioncurrency)|
|予約タイプ| (bookingtype)|
|KAYAKコミッション率| (commissionpercentage)|
|カスタムフィールド1| (tag1)|
|カスタムフィールド2| (tag2)|

### Eコマース

|変数|説明|
|---|---|
|注文ID／予約ID| (order\_id)（\_corderを上書き）|
|注文合計| (order\_total)（\_ctotalを上書き）|
|通貨| (order\_currency)（\_ccurrencyを上書き）|

### ホテル

|変数|説明|
|---|---|
|予約チェックイン日| (checkin)|
|予約チェックアウト日| (checkout)|
|予約施設ID| (hid)|
|旅行者数| (travelers)|
|客室数| (rooms)|

### フライト

|変数|説明|
|---|---|
|旅程の説明| (itin)|
|出発空港コード| (origin)|
|到着空港コード| (destination)|
|運賃クラス| (fareClass)|
|客室クラス| (cabinType)|

### レンタカー

|変数|説明|
|---|---|
|貸出日| (pickup)|
|返却日| (dropoff)|
|貸出場所ID| (pickupid)|
|返却場所ID| (dropoffid)|
|レンタカー会社ID| (agency)|

### イベント

|変数|説明|
|---|---|
|確認|確認|
|キャンセル|キャンセル|