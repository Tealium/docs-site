---
title: Tealium通貨コンバータータグ
description: この記事では、タグ管理アカウントでTealium通貨コンバータータグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tealium-currency-converter-tag/
---
## 仕組み

通貨換算の実装には、次の2つのコンポーネントが関係します。

* Tealium通貨コンバータータグ
* 通貨コンバーター拡張機能（[詳細はこちら](https://docs.tealium.com/currency-converter-extension/)）

## Tealium通貨コンバータータグ

[Open Exchange Rates](https://openexchangerates.org)の為替レートは、1日1回Tealiumに同期されます。サイト上で通貨コンバータータグが実行されると、Tealiumから為替レート情報を取得し、拡張機能で利用できるようにします。また、コード内で手動で換算できるように、ユーティリティJavaScript関数も定義します。

為替レートは次のファイルに保存されています。

`https://tags.tiqcdn.com/utag/tiqapp/utag.currency.js`


<blockquote>
これはブロッキングタグです。非同期で読み込まれますが、読み込みが完了するまで他のTealiumタグの読み込みを停止します。
</blockquote>


## 通貨コンバーター拡張機能

この拡張機能を使用すると、換算後の値をデータレイヤー変数に保存する通貨換算を簡単に構成できます。詳しくは、[通貨コンバーター拡張機能](https://docs.tealium.com/currency-converter-extension/)を参照してください。

## タグの追加

次の手順でTealium通貨コンバータータグを追加します。

1. タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。
1. タグウィザードを使用してタグに具体的なタイトルを付け、必要に応じてメモを入力してから、ロードルールタブに進みます。
1. 適用するロードルールを選択し、**完了**をクリックします。![](https://docs.tealium.com/images/client-side-tags/no-title-1602i561ebcf8f19811c5.png)

## 通貨換算関数

通貨コンバータータグがページに読み込まれると、次のユーティリティ関数を使用できます。

`tealiumiq_currency.convert(amount, source_currency, converted_currency)`

|パラメータ|説明|
|---|---|
|`amount`|換算する通貨金額。文字列、数値、または値の配列として指定します。例：`100`または`[100, 200, 300]`|
|`source_currency`|amountの値の通貨を表す3文字の通貨コード。例：`USD`|
|`converted_currency`|amountの換算先を表す3文字の通貨コード。例：`GBP`|

例：

```
var order_total_uk = tealiumiq_currency.convert(100, "USD", "GBP");
```