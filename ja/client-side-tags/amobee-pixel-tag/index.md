---
title: Amobee Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでAmobee Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amobee-pixel-tag/
---
## タグに関するヒント

マッピングツールボックスを使用すると、マッピング用のサンプル値を確認できます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **ID**
  * 画像ピクセルの場合、URL内の`b2= value`です。
  * スクリプトピクセルの場合、`/id/`の後にある英数字の長い文字列です。ここで、`id`はAmobeeから提供されるIDです。
* **タグタイプ**
  * **r.turn.com（画像ピクセル）**または**d.turn.com（スクリプトピクセル）**を選択します。
* **キャンペーンID**
  * 画像ピクセルでのみ使用します。
  * URL内の`cid= value`です。
  * マッピングを使用して、この値を上書きします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|アカウントID／b2パラメーター|（acct）|
|検索先|（SearchDest）|
|検索結果数|（SearchNum）|
|検索日|（SearchDate）|
|物件の日付|（PropDate）|
|物件の目的地|（PropDest）|
|物件数|（PropNum）|
|物件の評価|（PropRating）|
|画像タグのキャンペーンID|（cid）|