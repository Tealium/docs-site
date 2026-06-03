---
title: PriceGrabberタグ構成ガイド
description: この記事では、PriceGrabberタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pricegrabber-tag/
---
## 仕様

* **名前**: PriceGrabber
* **ベンダー**: PriceGrabber
* **タイプ**: コンバージョントラッキング

## 必要条件

**サービス**: PriceGrabber Merchant Account

**構成**:

* リテーラーID
* コンバージョントラッキングコード (CTS)
* マーチャントサーベイコード
* ポップアップ位置値 (XとY)

## タグを追加する

Tealium iQのタグマーケットプレイスは、さまざまなタグを提供しています。プロファイルにタグを追加する方法については、[こちら]()をクリックしてください。

## タグを構成する

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **リテーラーID** (必須): PriceGrabberコードの`retid`パラメータの値である数値のリテーラーIDを入力します。例えば、`12345`
1. **タグ** (必須): ドロップダウンリストから、ロードしたいタグタイプを選択します。
  * `conversion.php`: これにより、PriceGrabberのコンバージョントラッキングコードがロードされます。
  * `rating_merchrevpopjs.php`: これにより、PriceGrabberのマーチャントサーベイコードがロードされます。

1. **位置X** (オプション): `popup_pos_xパラメータ`の値を入力して、マーチャントサーベイがページの位置Xに対してどこに入れるかを指定します。この値はPriceGrabberのマーチャントサーベイコードで指定され、`rating_merchrevpopjs.php`タグタイプにのみ適用されます。例えば、`popup_pos_x=200`;
1. **位置Y** (オプション): `popup_pos_yパラメータ`の値を入力して、マーチャントサーベイがページの位置Yに対してどこに入れるかを指定します。この値はPriceGrabberのマーチャントサーベイコードで指定され、`rating_merchrevpopjs.php`タグタイプにのみ適用されます。例えば、`popup_pos_x=20`;

**注**: マーチャントサーベイをページの中央にポップアップさせるには、位置Xと位置Yのフィールドを空白にしてください。

## ロードルールを適用する

[ロードルール]()は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページにロード**ルールは、デフォルトのロードルールです。このタグを特定のページでロードするには、関連する条件で新しいロードルールを作成します。

### ベストプラクティス

* `conversion.php`は、タグが注文に特有のデータを取得できるように、チェックアウトページに配置する必要があります。
* `rating_merchrevpopjs.php`タグは、注文完了後に表示される確認ページに配置する必要があります。

### マッピングを構成する

[マッピング]()は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。このタグの宛先変数は、マッピングツールボックスで利用可能です。

 [E-Commerce Extension]()を追加し、コンバージョンに適用可能なOrderとProduct変数を構成することをお勧めします：`_cbrand`、`_cprod`、`_cprice`、`_csku`、そして`_cquan`。これにより、Extensionはこれらの値をこのタグがサポートする対応する宛先にマップすることができます。

`conversion.php`タグタイプの場合、これらの宛先にマップします：

* **retid**: PriceGrabberコンバージョンコードで指定されたリテーラーID
* **Manufacturer [Array]**: 製品メーカーのリスト  
 この宛先へのマッピングは、Extensionの`_cbrand`変数を上書きします。
* **Manufacturer Part Number [Array]**: 製品識別子のリスト  
 この宛先へのマッピングは、Extensionの`_cprod`変数を上書きします。
* **Retailer Price [Array]**: 製品価格のリスト  
 この宛先へのマッピングは、Extensionの`_cprice`変数を上書きします。
* **Internal Merchant SKU [Array]**: 製品SKUのリスト  
 この宛先へのマッピングは、Extensionの`_csku`変数を上書きします。
* **UPC [Array]**: 製品のユニバーサル製品コードのリスト
* **Quantity [Array]**: 注文内の製品の数量のリスト  
 この宛先へのマッピングは、Extensionの`_cquan`変数を上書きします。

`rating_merchrevpopjs.php`タグタイプの場合、この宛先にマップします：

* `popup_email`: 顧客が提供したメールアドレス

## ベンダー文書

* [PriceGrabber Merchant Resources](https://partner.pricegrabber.com/mss_main.php?ccode=us) (ログインが必要です)
* [PriceGrabber Data Feed Requirements](https://partner.pricegrabber.com/mss_main.php?sec=2&amp;ccode=us)

