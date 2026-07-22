---
title: ChannelAdvisorタグ構成ガイド
description: この記事では、ChannelAdvisorタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/channeladvisor-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: ChannelAdvisor
* **ベンダー**: ChannelAdvisor
* **タイプ**: コンバージョントラッキング

### 必要条件

**サービス**: ChannelAdvisorプラットフォーム

**構成**:

* ChannelAdvisorアカウントID

## Tealium iQでのタグ構成

### タグの追加

Tealium iQのタグマーケットプレイスは、さまざまなタグを提供しています。プロファイルにタグを追加する方法については、[こちら](https://docs.tealium.com/manage-tags/)をクリックしてください。

### タグの構成

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **アカウントID** (オプション): ChannelAdvisorアカウントに関連付けられた数値IDを入力します。例: `10055350`   


<blockquote>
`pid`パラメータにマッピングすることで、アカウントID（プロファイルIDとも呼ばれます）フィールドを動的に構成することを選択できます。
</blockquote>



### ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールは、デフォルトのロードルールです。このタグを特定のページでロードするには、関連する条件を持つ新しいロードルールを作成します。

**ベストプラクティス**: このタグをサイトの注文確認ページでロードするようにロードルールの条件を構成します。これにより、タグはコンバージョン後の注文情報をキャプチャできます。

### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。このタグの宛先変数は、マッピングツールボックスで利用可能です。

* **pid**: この変数にマッピングして、ChannelAdvisorアカウントの数値IDを動的に構成します。

**注意**: [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)が注文と製品変数を自動的にマップするように構成されていることを確認してください。ただし、ツールキットに記載されている対応する宛先変数でE-Commerce Extensionのマッピングを上書きすることができます。

* **orderId**: Extensionの`_corder`変数がこの宛先にマップします。このデータポイントは注文識別子を示します。
* **revenue**: Extensionの`_csubtotal`変数がこの宛先にマップします。このデータポイントは注文の小計を識別します。
* **currency**: Extensionの`_ccurrency`変数がこの宛先にマップします。このデータポイントは通貨コードを識別します。
* **sku**: Extensionの`_cprod`変数（製品IDのリスト）がこの宛先にマップします。このデータポイントは製品SKUのリストを識別し、各SKUは注文内の行項目に固有です。
* **price**: Extensionの`_cprice`変数がこの宛先にマップします。このデータポイントは注文内のアイテムに関連する単価のリストを識別します。
* **quan**: Extensionの`_cquan`変数がこの宛先にマップします。このデータポイントは注文内の各アイテムの数量のリストを識別します。

## ベンダー文書

* [注文トラッキングピクセルの実装方法](http://ssc.channeladvisor.com/howto/my-account/account-settings/tracking-pixel#Order)
* [Tealiumを使用したトラッキングピクセルの実装方法](http://ssc.channeladvisor.com/howto/implementing-tracking-pixels-tealium)
* [Channel Advisorプラットフォームについて](http://ssc.channeladvisor.com/howto)
* [ChannelAdvisor戦略とサポートセンター](http://ssc.channeladvisor.com/)

