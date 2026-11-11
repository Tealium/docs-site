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

### 必須要件

**サービス**: ChannelAdvisor Platform

**構成**:

* ChannelAdvisorアカウントID

## タグの構成

### タグの追加

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

### タグの構成

1. **タイトル**: （必須）タグインスタンスを識別するためのわかりやすいタイトルを入力します。
1. **アカウントID**: （任意）ChannelAdvisorアカウントに関連付けられている数値IDを入力します。例: `10055350`


<blockquote>
`pid`パラメータにマッピングすることで、アカウントID（プロファイルIDとも呼ばれます）フィールドに動的に値を構成できます。
</blockquote>



### ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトのロードルールは、**すべてのページで読み込む**ルールです。このタグを特定のページで読み込むには、該当する条件を指定して新しいロードルールを作成します。

**ベストプラクティス**: サイトの注文確認ページでこのタグを読み込むように、ロードルールの条件を構成します。これにより、タグはコンバージョン後の注文情報を取得できます。

### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。このタグの宛先変数は、マッピングツールボックスで使用できます。

* **pid**: ChannelAdvisorアカウントの数値IDを動的に構成するには、この変数にマッピングします。

**注**: 注文変数と製品変数が自動的にマッピングされるように、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)が構成されていることを確認してください。ただし、ツールキットに記載されている対応する宛先変数を使用して、Eコマース拡張機能のマッピングを上書きできます。

* **orderId**: 拡張機能の`_corder`変数が、この宛先にマッピングされます。このデータポイントは注文IDを示します。
* **revenue**: 拡張機能の`_csubtotal`変数が、この宛先にマッピングされます。このデータポイントは注文の小計を示します。
* **currency**: 拡張機能の`_ccurrency`変数が、この宛先にマッピングされます。このデータポイントは通貨コードを示します。
* **sku**: 拡張機能の`_cprod`変数（製品IDのリスト）が、この宛先にマッピングされます。このデータポイントは製品SKUのリストを示します。各SKUは、注文内の各明細項目に固有です。
* **price**: 拡張機能の`_cprice`変数が、この宛先にマッピングされます。このデータポイントは、注文内の各商品に関連付けられた単価のリストを示します。
* **quan**: 拡張機能の`_cquan`変数が、この宛先にマッピングされます。このデータポイントは、注文内の各商品の数量のリストを示します。

## ベンダーのドキュメント

* [注文トラッキングピクセルの実装方法](http://ssc.channeladvisor.com/howto/my-account/account-settings/tracking-pixel#Order)
* [Tealiumを使用したトラッキングピクセルの実装方法](http://ssc.channeladvisor.com/howto/implementing-tracking-pixels-tealium)
* [ChannelAdvisor Platformについて](http://ssc.channeladvisor.com/howto)
* [ChannelAdvisor戦略およびサポートセンター](http://ssc.channeladvisor.com/)