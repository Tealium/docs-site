---
title: Adition PostTracking構成ガイド
description: この記事では、Adition PostTrackingコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adition-posttracking-connector/
---
この記事では、Adition PostTrackingコネクタの構成方法について説明します。

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Adition API
* APIエンドポイント：`http://adfarm1.adition.com/trackdata`

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **TrackingSpot ID (SID)**  
  * TrackingSpotの内部ID。
* **LandingPage ID (TID)**  
  * LandingPageの内部ID。
* **Aditionインスタンス**  
  * （オプション）。使用しているAditionサーバーファームを指定します。これはベースURLにプレフィックスとして追加されます：`https://{adition_instance}.adfarm1.adition.com.`

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベントを追跡 | ✗ | ✓ |

アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### イベントを追跡

#### トラッキングパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| kid | キャンペーンID。 |
| bid | バナーID。 |
| wp_id | コンテンツユニットID。 |

#### 収益追跡パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| orderid | 注文の一意の識別子。 |
| itemno | アイテムの一意の識別子。 |
| quantity | 注文されたアイテムの数。 |
| descr | アイテムの説明。 |
| price | アイテムごとの価格。 |
| total | 注文された数量の合計価格。 |
