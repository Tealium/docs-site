---
title: Flashtalking OneTagタグ構成ガイド
description: この記事では、タグ管理アカウントでFlashtalking OneTagタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/flashtalking-onetag-tag/
---
Flashtalking OneTagは、データを使用して広告をリアルタイムでパーソナライズし、その効果を分析するとともに、エンゲージメントとROIの向上につながる最適化を可能にします。

## タグに関するヒント

マッピングを使用して、以下を行います。

* `ftXName`（トランザクション名）の値を構成する。
* カスタム変数（U1～U20）を送信する。
* 標準構成値を上書きする。
* Eコマース拡張機能の値を上書きする。
* Eコマース拡張機能を使用している場合、データレイヤーに値が構成されると、以下の値が自動的に渡されます。
    * `ftXRef`（Eコマース注文ID）
    * `ftXValue`（Eコマース注文小計）
    * `ftXType`（Eコマース注文タイプ）
    * `ftXCurrency`（Eコマース注文通貨）
    * `ftXNumItems`（Eコマースの数量リスト）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下を構成します。

* **広告主ID**：コードスニペット内の`/container/`の直後にある数字。
* **Spotlight ID**：コードスニペット内の広告主IDの直後にある数字。
* **SpotlightグループID**：コードスニペット内のSpotlight IDの直後にある数字。

例：`https://servedby.flashtalking.com/container/AdvertiserID;SpotlightID;SpotlightGroupID;iframe/?`

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| **変数** | **説明** |
|:---------|:------------|
| `aid` | 広告主ID |
| `sid` | Spotlight ID |
| `sgid` | SpotlightグループID |

### Eコマース

| **変数** | **説明** | **データ型** |
|:---------|:------------|:------------|
| `order_id` | 注文ID（ftXRef）（`_corder`を上書き） | 文字列 |
| `order_subtotal` | 小計（ftXValue）（`_csubtotal`を上書き） | 整数 |
| `order_currency` | 通貨（ftXCurrency）（`_ccurrency`を上書き） | 文字列 |
| `order_type` | カートまたは注文のタイプ（`_ctype`を上書き） | 文字列 |
| `product_quantity` | 数量のリスト（`_cquan`を上書き） | 配列 |
| `ft_vars.ftXName` | トランザクション名 | 文字列 |

### カスタム

| **変数** | **説明** |
|:---------|:------------|
| `ft_vars.U1` | カスタム変数1 |
| `ft_vars.U2` | カスタム変数2 |
| `ft_vars.U3` | カスタム変数3 |
| `ft_vars.U4` | カスタム変数4 |
| `ft_vars.U5` | カスタム変数5 |
| `ft_vars.U6` | カスタム変数6 |
| `ft_vars.U7` | カスタム変数7 |
| `ft_vars.U8` | カスタム変数8 |
| `ft_vars.U9` | カスタム変数9 |
| `ft_vars.U10` | カスタム変数10 |
| `ft_vars.U11` | カスタム変数11 |
| `ft_vars.U12` | カスタム変数12 |
| `ft_vars.U13` | カスタム変数13 |
| `ft_vars.U14` | カスタム変数14 |
| `ft_vars.U15` | カスタム変数15 |
| `ft_vars.U16` | カスタム変数16 |
| `ft_vars.U17` | カスタム変数17 |
| `ft_vars.U18` | カスタム変数18 |
| `ft_vars.U19` | カスタム変数19 |
| `ft_vars.U20` | カスタム変数20 |