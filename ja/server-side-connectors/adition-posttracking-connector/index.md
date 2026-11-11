---
title: Adition PostTracking セットアップガイド
description: この記事では、Adition PostTrackingコネクターのセットアップ方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adition-posttracking-connector/
---
この記事では、Adition PostTrackingコネクターのセットアップ方法について説明します。

## API情報

このコネクターでは、以下のベンダーAPIを使用します。

* API名：Adition API
* APIエンドポイント：`http://adfarm1.adition.com/trackdata`

## 構成

コネクターマーケットプレイスに移動し、新しいコネクターを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクターを追加したら、以下の項目を構成します。

* **TrackingSpot ID（SID）**  
  * TrackingSpotの内部ID。
* **LandingPage ID（TID）**  
  * LandingPageの内部ID。
* **Aditionインスタンス**  
  * （任意）使用しているAditionサーバーファームを指定します。これは、ベースURLのプレフィックスとして追加されます：`https://{adition_instance}.adfarm1.adition.com.`

コネクターの構成が完了したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントをトラッキング | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### イベントをトラッキング

#### トラッキングパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| kid | キャンペーンID。 |
| bid | バナーID。 |
| wp_id | コンテンツユニットID。 |

#### 収益トラッキングパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| orderid | 注文の一意の識別子。 |
| itemno | 商品の一意の識別子。 |
| quantity | 注文された商品の数量。 |
| descr | 商品の説明。 |
| price | 商品1点あたりの価格。 |
| total | 注文数量分の合計価格。 |