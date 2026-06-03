---
title: Flashtalking OneTagタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFlashtalking OneTagタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/flashtalking-onetag-tag/
---
Flashtalking OneTagは、データを使用して広告をリアルタイムでパーソナライズし、その効果を分析し、より良いエンゲージメントとROIを実現する最適化を可能にします。

## タグのヒント

マッピングを使用して：

* `ftXName`（トランザクション名）の値を構成します。
* カスタム変数（U1 - U20）を送信します。
* 標準の構成値を上書きします。
* E-Commerce拡張の値を上書きします。
* E-Commerce拡張を使用している場合、これらの値はデータレイヤーに記入されていると自動的に渡されます：
    * `ftXRef`（E-Commerceの注文ID）
    * `ftXValue`（E-Commerceの注文小計）
    * `ftXType`（E-Commerceの注文タイプ）
    * `ftXCurrency`（E-Commerceの注文通貨）
    * `ftXNumItems`（E-Commerceの数量リスト）

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **広告主ID**：コードスニペット中の`/container/`の直後の番号。
* **スポットライトID**：コードスニペット中の広告主IDの直後の番号。
* **スポットライトグループID**：コードスニペット中のスポットライトIDの直後の番号。

例：`https://servedby.flashtalking.com/container/AdvertiserID;SpotlightID;SpotlightGroupID;iframe/?`

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| **変数** | **説明** |
|:---------|:------------|
| `aid` | 広告主ID |
| `sid` | スポットライトID |
| `sgid` | スポットライトグループID |

### E-Commerce

| **変数** | **説明** | **データタイプ** |
|:---------|:------------|:------------|
| `order_id` | 注文ID (ftXRef) (`_corder`を上書き) | 文字列 |
| `order_subtotal` | 小計 (ftXValue) (`_csubtotal`を上書き) | 整数 |
| `order_currency` | 通貨 (ftXCurrency) (`_ccurrency`を上書き) | 文字列 |
| `order_type` | カートまたは注文タイプ (`_ctype`を上書き) | 文字列 |
| `product_quantity` | 数量リスト (`_cquan`を上書き) | 配列 |
| `ft_vars.ftXName` | トランザクション名 | 文字列 |

### カスタム

| **変数** | **説明** |
|:---------|:------------|
| `ft_vars.U1` | カスタム変数 1  |
| `ft_vars.U2` | カスタム変数 2  |
| `ft_vars.U3` | カスタム変数 3  |
| `ft_vars.U4` | カスタム変数 4  |
| `ft_vars.U5` | カスタム変数 5  |
| `ft_vars.U6` | カスタム変数 6  |
| `ft_vars.U7` | カスタム変数 7  |
| `ft_vars.U8` | カスタム変数 8  |
| `ft_vars.U9` | カスタム変数 9  |
| `ft_vars.U10` | カスタム変数 10  |
| `ft_vars.U11` | カスタム変数 11  |
| `ft_vars.U12` | カスタム変数 12  |
| `ft_vars.U13` | カスタム変数 13  |
| `ft_vars.U14` | カスタム変数 14  |
| `ft_vars.U15` | カスタム変数 15  |
| `ft_vars.U16` | カスタム変数 16  |
| `ft_vars.U17` | カスタム変数 17  |
| `ft_vars.U18` | カスタム変数 18  |
| `ft_vars.U19` | カスタム変数 19  |
| `ft_vars.U20` | カスタム変数 20  |

