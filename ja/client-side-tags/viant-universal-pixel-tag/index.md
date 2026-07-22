---
title: Viantユニバーサルピクセルタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでViantユニバーサルピクセルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/viant-universal-pixel-tag/
---
## 概要

Viant Universal Pixelタグは、サイトからAdelphic DSP by Viantにクライアントサイドのコンバージョンおよびエンゲージメントイベントを送信し、測定、最適化、および帰属を行います。

このタグを使用して、標準的なファネルイベント（ページビュー、カートに追加、チェックアウトの開始、購入、リードなど）を追跡し、豊富なトランザクションの詳細、顧客識別子、および製品データをViantに渡します。

Universal Pixel ID（UPID）、顧客ID、収益、通貨、およびカスタムパラメーターのサポートが組み込まれており、Viantの広告プラットフォーム全体でキャンペーンのパフォーマンス、報告の正確性、およびトラブルシューティングを改善します。

## タグのヒント
*   マッピングを使用して：
    *   標準の構成値を動的に上書き
    *   E-Commerce拡張の値を動的に上書き
*   E-Commerce拡張に対応：
    * 通貨（`_ccur`）
    * 商品カテゴリ（`_ccat`）
    * 収益/小計（`_csubtotal`）
    * トランザクションID（`_corder`）

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Universal Pixel ID**：トラッキング用のピクセルのユニークID。Adelphic DSP by Viantによって提供されます。
* **User ID**：広告主の内部顧客IDをBase64エンコードしたもの。帰属アルゴリズムと監査のトラブルシューティングに使用されます。
* **Disable Automapping**：E-Commerce拡張の変数をイベントデータに自動マッピングする機能を無効にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `upid` | `String` | Universal Pixel ID |
| `cuid` | `String` | ユーザーID |
| `disable_automapping` | `String` | 自動マッピング無効 |

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `upid` | `String` | Universal Pixel ID |
| `cuid` | `String` | ユーザーID |
| `cur` | `String` | 通貨 |
| `cust` | `String` | 顧客タイプ |
| `itms` | `String` | 商品カテゴリ |
| `url` | `String` | ページURL |
| `ref` | `String` | リファラーURL |
| `val` | `String` | 収益 |
| `tn` | `String` | トランザクションID |
| `p1` | `String` | カスタムパラメータ1 |
| `p2` | `String` | カスタムパラメータ2 |
| `p3` | `String` | カスタムパラメータ3 |
| `p4` | `String` | カスタムパラメータ4 |
| `p5` | `String` | カスタムパラメータ5 |
| `p6` | `String` | カスタムパラメータ6 |
| `p7` | `String` | カスタムパラメータ7 |
| `p8` | `String` | カスタムパラメータ8 |
| `p9` | `String` | カスタムパラメータ9 |
| `p10` | `String` | カスタムパラメータ10 |

### E-Commerce

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `cur` | `String` | 通貨（`_ccur`を上書き） |
| `itms` | `0` | 商品カテゴリ |
| `val` | `String` | 収益（`_csubtotal`を上書き） |
| `tn` | `String` | トランザクションID（`_corder`を上書き） |

### イベント固有のパラメータ
イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `cuid` | ユーザーID |
| `url` | ページURL |
| `cur` | 通貨 |
| `cust` | 顧客タイプ |
| `itms` | 商品カテゴリ |
| `ref` | リファラーURL |
| `val` | 収益 |
| `tn` | トランザクションID |
| `p1` | カスタムパラメータ1 |
| `p2` | カスタムパラメータ2 |
| `p3` | カスタムパラメータ3 |
| `p4` | カスタムパラメータ4 |
| `p5` | カスタムパラメータ5 |
| `p6` | カスタムパラメータ6 |
| `p7` | カスタムパラメータ7 |
| `p8` | カスタムパラメータ8 |
| `p9` | カスタムパラメータ9 |
| `p10` | カスタムパラメータ10 |