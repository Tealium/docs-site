---
title: Upsellitタグ
description: この記事では、Upsellitタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/upsellit-tag/
---
## タグのヒント

* Launch JavaScriptコードはデフォルトで全てのページで実行されます。
* 注文IDが構成されたときにConfirmation Pixelが発火します。
* 次のE-Commerce拡張機能をサポートしています：  
  * 注文ID  
  * 小計
* マッピングを使用して：  
  * Launch Fileの標準構成値を上書きします。
  * E-Commerce拡張機能の値を上書きします。  
  * サイトIDと製品IDの値を構成します。  
  * 位置の値を上書きします（デフォルトは`1`です）。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理]()を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Launch File**:  
Upsellitによって提供されるLaunch JavaScriptコード。この値は`.jsp`の前に表示されます。
* **Site ID**:  
Confirmation PixelのためのサイトID。例：`1234`。
* **Product ID**:  
Confirmation Pixelのための製品ID。例：`12`。

 UpsellitタグのLaunch Fileは、Upsellitアカウントダッシュボードから直接取得できます。Upsellitアカウントにログインし、**インテグレーション**または**実装**セクションに移動します。提供されたJavaScriptライブラリURLおよび関連するアカウント詳細（アカウントIDおよびサイトIDなど）をダウンロードまたはコピーします。さらなる支援が必要な場合は、Upsellitアカウント担当者に連絡してください。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `launchfile` | Launch File |
| `position` | 位置 |
| `USI_orderID` |注文ID（`_corder`を上書き） |
| `USI_orderAmt` |注文金額（`_csubtotal`を上書き） |
| `USI_currency` | 注文通貨（`_ccurrency`を上書き） |
