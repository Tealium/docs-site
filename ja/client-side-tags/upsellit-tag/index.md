---
title: Upsellitタグ
description: この記事では、Upsellitタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/upsellit-tag/
---
## タグに関するヒント

* Launch JavaScriptコードは、デフォルトですべてのページで実行されます。
* 注文IDが構成されると、Confirmation Pixelが発火します。
* E-Commerce拡張機能では、以下がサポートされています。  
  * 注文ID  
  * 小計
* マッピングを使用すると、以下を実行できます。  
  * Launch Fileの標準構成値を上書きする。
  * E-Commerce拡張機能の値を上書きする。  
  * Site IDとProduct IDの値を構成する。  
  * Positionの値を上書きする（デフォルトは`1`）。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下を構成します。

* **Launch File**：  
Upsellitから提供されるLaunch JavaScriptコード。`.jsp`の前に表示される値です。
* **Site ID**：  
Confirmation PixelのSite ID。例：`1234`。
* **Product ID**：  
Confirmation PixelのProduct ID。例：`12`。


<blockquote>
UpsellitタグのLaunch Fileは、Upsellitアカウントのダッシュボードから直接取得できます。Upsellitアカウントにログインし、**Integration**または**Implementation**セクションに移動してください。提供されているJavaScriptライブラリのURLと、Account IDやSite IDなどの関連するアカウント情報をダウンロードまたはコピーします。さらにサポートが必要な場合は、Upsellitのアカウント担当者にお問い合わせください。
</blockquote>


## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `launchfile` | Launch File |
| `position` | Position |
| `USI_orderID` | 注文ID（`_corder`を上書き） |
| `USI_orderAmt` | 注文金額（`_csubtotal`を上書き） |
| `USI_currency` | 注文通貨（`_ccurrency`を上書き） |