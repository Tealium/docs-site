---
title: Tealium 通貨コンバータータグ
description: この記事では、Tealium iQ タグ管理アカウントで Tealium 通貨コンバータータグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tealium-currency-converter-tag/
---
## 動作原理

通貨変換を実装するには、以下の2つのコンポーネントが関連しています：

* Tealium 通貨コンバータータグ
* 通貨コンバーター拡張機能（[詳細はこちら](https://docs.tealium.com/currency-converter-extension/)）

## Tealium 通貨コンバータータグ

毎日一度、[Open Exchange Rates](https://openexchangerates.org) からの為替レートが Tealium に同期されます。通貨コンバータータグがサイト上で実行されると、Tealium から為替レート情報を取得し、拡張機能で利用できるようにします。また、コード内で手動で変換を行うためのユーティリティJavaScript関数も定義します。

為替レートは以下のファイルに保存されます：

`https://tags.tiqcdn.com/utag/tiqapp/utag.currency.js`


<blockquote>
これはブロッキングタグなので、非同期でロードされるものの、ロードされるまで他の Tealium タグのロードを阻止します。
</blockquote>


## 通貨コンバーター拡張機能

この拡張機能を使用すると、データレイヤー変数に変換された値を保存する通貨変換を簡単に構成できます。[通貨コンバーター拡張機能](https://docs.tealium.com/currency-converter-extension/)についてもっと学びましょう。

## タグの追加

1. タグマーケットプレイスに移動し、Tealium 通貨コンバータータグを追加します。
1. タグウィザードを使用して、タグに具体的なタイトルを付け、任意のメモを入力し、ロードルールタブに進みます。
1. 適用したいロードルールを選択し、**完了**をクリックします。![](https://docs.tealium.com/images/client-side-tags/no-title-1602i561ebcf8f19811c5.png)

## 通貨変換機能

通貨コンバータータグがページ上でロードされると、以下のユーティリティ関数が使用できます：

`tealiumiq_currency.convert(amount, source_currency, converted_currency)`

|パラメータ| 説明|
|---| ---|
|`amount`| 変換する通貨額。文字列/数値または値の配列として指定します。例：`100` または `[100, 200, 300]`|
|`source_currency`| 金額の通貨を表す3文字の通貨コード。例：`USD`|
|`converted_currency`| 金額を変換する3文字の通貨コード。例：`GBP`|

例：

```
var order_total_uk = tealiumiq_currency.convert(100, "USD", "GBP");
```
