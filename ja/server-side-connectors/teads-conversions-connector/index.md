---
title: Teads Conversionsコネクタ構成ガイド
description: この記事では、Teads Conversionsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/teads-conversions-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Teads Conversions API
* APIバージョン：v1
* APIエンドポイント：`https://ca.teads.tv/`

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。
* **Conversion API Token**  
  * Conversion API Tokenを生成するには、構成パネルに移動し、**Conversion API Tokens > Generate Conversion API Token**をクリックします。

コネクタを構成したら、**Done**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| コンバージョンイベントを送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### コンバージョンイベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベントID（`auctid`） | イベントの一意の識別子。`URL`（`auctid`パラメータ）またはCookie（`tfpai`）から取得できます。 |
| Buyer Pixel ID | Webサイトにインストールされているピクセルの`ID`。 |
| イベントソースURL | ユーザーが訪問したページの`URL`。 |
| コンバージョンタイプ | コンバージョンイベントのタイプ：`pageView`、`AddToCart`、`AddToWishlist`、`CompleteRegistration`、`InitiateCheckout`、`Lead`、`Purchase`、`Search`、`ViewContent`。デフォルトは`pageView`イベントです。 |
| イベント時刻 | エポック秒単位のイベントのタイムスタンプ。 |

#### コンバージョンパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 名前 | （文字列）名前。最大`100`文字。 |
| 価格 | （小数）指定された通貨パラメータを単位とする金額。 |
| 通貨 | （文字列）通貨を表す3文字の`ISO 4217`通貨コード。 |

#### ファーストパーティCookie

| **パラメータ** | **説明** |
| --- | --- |
| `tfpai` | `auctid`値が格納されます。 |
| `tfpvi` | ユーザー識別子が格納されます。 |
| `tfpsi` | ユーザーセッションの算出に使用されるユーザーセッション`ID`が格納されます。 |