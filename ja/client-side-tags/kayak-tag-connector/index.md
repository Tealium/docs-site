---
title: Kayak タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでKAYAKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kayak-tag-connector/
---
## タグのヒント

* 確認とキャンセルのピクセルが発火するタイミングを構成するためにイベントマッピングを使用します。
* Commission Currencyの値は、提供されていない場合はe-commerce Currencyの値がデフォルトになります。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグの概要]()の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **パートナーコード**
  * KAYAKから提供される、KAYAKの内部コードです。
* **クリックIDクエリパラメータ名**
  * トラッキングURLでクリックIDを渡すために使用されるクエリパラメータの名前。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

|変数| 説明|
|---| ---|
|パートナーコード| (partner\_code)|
|予約日| (bookedon)|
|カヤックコミッション額| (kayakcommission)|
|コミッション通貨| (commissioncurrency)|
|予約タイプ| (bookingtype)|
|カヤックコミッションパーセンテージ| (commissionpercentage)|
|カスタムフィールド1| (tag1)|
|カスタムフィールド2| (tag2)|

### E-コマース

|変数| 説明|
|---| ---|
|注文ID/予約ID| (order\_id) (\_corderを上書き)|
|注文合計| (order\_total) (\_ctotalを上書き)|
|通貨| (order\_currency) (\_ccurrencyを上書き)|

### ホテル

|変数| 説明|
|---| ---|
|予約チェックイン日| (checkin)|
|予約チェックアウト日| (checkout)|
|予約物件ID| (hid)|
|旅行者数| (travelers)|
|部屋数| (rooms)|

### フライト

|変数| 説明|
|---| ---|
|旅程説明| (itin)|
|出発空港コード| (origin)|
|目的地空港コード| (destination)|
|運賃クラス| (fareClass)|
|キャビンタイプ| (cabinType)|

### 車

|変数| 説明|
|---| ---|
|ピックアップ日| (pickup)|
|ドロップオフ日| (dropoff)|
|ピックアップロケーションID| (pickupid)|
|ドロップオフロケーションID| (dropoffid)|
|カーエージェンシーID| (agency)|

### イベント

|変数| 説明|
|---| ---|
|確認| Confirmation|
|キャンセル| Cancellation|

