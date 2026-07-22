---
title: Adition (Track) タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdition (Track)タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-track-tag/
---
## タグのヒント

* これはAditionのトラックバージョンです。
* Aditionとの契約に従ってドメインを構成します。

  * デフォルト値: `adfarm1.adition.com`
  * AdfarmID: `ad<id>.adfarm1.adition.com`
  * カスタム: `<subdomain>.<domain>.<tld>`

* デフォルトの戻りタイプは `img` です。
* 次のE-コマース変数を使用します

  * `_cprod`
  * `_cquan`
  * `_cprice`
  * `_corder`

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Adition (Track)タグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、次の構成を行います：

* **ドメイン**
  * Aditionから提供されるドメイン。
  * デフォルトのドメインは `adfarm1.adition.com` です。

* **TID**
  * 必須。
  * Aditionの広告配信システム内のランディングページを表します。

* **SID**
  * 必須。
  * Aditionの広告配信システム内のトラッキングスポットを表します。

* **タグタイプ**:

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|タグタイプ|  <ul><li>タグタイプ</li></ul> |
|ドメイン|  <ul><li>ドメイン</li></ul> |
| `tid` |  <ul><li>ランディングページID</li></ul> |
| `sid` |  <ul><li>トラッキングスポットID</li></ul> |
|`orderid`|  <ul><li>注文ID</li><li>`_corder` を上書きします。</li></ul> |
|`descr`|  <ul><li>配列</li><li>アイテムの説明。</li><li>`_cprod` を上書きします。</li></ul> |
| `quantity` |  <ul><li>配列</li><li>アイテムの数量。</li><li>`_cquan` を上書きします。</li></ul> |
|`price`|  <ul><li>配列</li><li>アイテムの価格。</li><li>`_cprice` を上書きします。</li></ul> |
|`total`|  <ul><li>配列</li><li>合計価格。</li></ul> |
|`param`|  <ul><li>パラメータ</li><li>値は1 - 20です。</li></ul> |

