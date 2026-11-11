---
title: Adition（Track）タグ構成ガイド
description: この記事では、タグ管理アカウントで Adition（Track）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-track-tag/
---
## タグに関するヒント

* これは Adition の Track バージョンです。
* Adition との契約に従ってドメインを構成します。

  * デフォルト値：`adfarm1.adition.com`
  * AdfarmID：`ad<id>.adfarm1.adition.com`
  * カスタム：`<subdomain>.<domain>.<tld>`

* デフォルトの戻り値の型は `img` です。
* 次の E コマース変数を使用します。

  * `_cprod`
  * `_cquan`
  * `_cprice`
  * `_corder`

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **ドメイン**
  * Adition から提供されたドメイン。
  * デフォルトのドメインは `adfarm1.adition.com` です。

* **TID**
  * （必須）Adition 広告配信システム内のランディングページを表します。

* **SID**
  * （必須）Adition 広告配信システム内のトラッキングスポットを表します。

* **タグタイプ**：

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|タグタイプ|<ul><li>タグタイプ</li></ul>|
|ドメイン|<ul><li>ドメイン</li></ul>|
| `tid` |<ul><li>ランディングページ ID</li></ul>|
| `sid` |<ul><li>トラッキングスポット ID</li></ul>|
|`orderid`|<ul><li>注文 ID</li><li> `_corder` を上書きします。</li></ul>|
|`descr`|<ul><li>配列</li><li>商品の説明。</li><li> `_cprod` を上書きします。</li></ul>|
| `quantity` |<ul><li>配列</li><li>商品の数量。</li><li> `_cquan` を上書きします。</li></ul>|
|`price`|<ul><li>配列</li><li>商品の価格。</li><li> `_cprice` を上書きします。</li></ul>|
|`total`|<ul><li>配列</li><li>合計価格。</li></ul>|
|`param`|<ul><li>パラメーター</li><li>値の範囲は 1～20 です。</li></ul>|