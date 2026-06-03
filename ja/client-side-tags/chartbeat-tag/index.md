---
title: Chartbeatタグ構成ガイド
description: この記事では、Chartbeatタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/chartbeat-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: Chartbeat
* **ベンダー**: Chartbeat
* **タイプ**: リアルタイムWeb分析

### 必要なもの

**サービス**: Chartbeatアカウント

**構成**:

* ChartbeatユーザーID

## Tealium iQでのタグ構成

### タグの追加

Tealium iQのタグマーケットプレイスでは、さまざまなタグを提供しています。詳細は、[タグマーケットプレイスについて]()を参照してください。

### タグの構成

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **ユーザーID** (必須): Chartbeatから提供された数値のユーザーIDを入力します。これはChartbeatアカウントで見つけることができます。例えば、`1234`
1. **ドメイン** (必須): Chartbeatを実装したいドメイン名を入力します。プレフィックス`www`は含めません。例えば、`yoursite.com`
1. **Use Canonical** (オプション): Chartbeatが[Canonical](https://support.google.com/webmasters/answer/139066?rd=1)パス（優先URL）を使用してページにアクセスするかどうかを選択します。デフォルトでは、Use Canonicalドロップダウンはfalseに構成されており、この場合、Chartbeatはページの実際のURLを使用します。  
  * サイトのHTMLでリンク要素を使用して定義したcanonicalパスをChartbeatが使用する場合は、`true`を選択します。

例えば、あるページが2つの異なるURLでアクセスできるとします：

```
http://yoursite.com/products?category=apparel&amp;kids
http://yoursite.com/apparel/kids
```

しかし、URL #2だけがcanonicalとして構成されています。**Use Canonical**フィールドを有効にすることで、Chartbeatはあなたが好むURL#2をトラッキング目的で使用することができます。  

`path`変数にマッピングすることで、この選択を上書きするオプションがあります。

#2から#4までのタグ構成を上書きするか、動的に構成するために、データマッピングツールボックスを使用することができます。

### ロードルールの適用

[ロードルール]()は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールは、デフォルトのロードルールです。特定のページでこのタグをロードするには、関連する条件を持つ新しいロードルールを作成します。

デフォルトの**すべてのページでロード**ルールはそのままにしておいてください。Chartbeatのようなほとんどの分析タグは、正確なデータ収集を確保するために、サイトのすべてのページでロードすることが推奨されています。

### マッピングの構成

[マッピング]()は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。このタグの宛先変数は、マッピングツールキットで利用可能です。

* **ユーザーID:** この宛先にマッピングして、Chartbeatが提供した数値のユーザーIDを送信します。
* **ドメイン**: この宛先にマッピングして、Chartbeatが実装されているドメイン名を送信します。
* **Use Canonical (canonical)**: この宛先にマッピングして、ページのURLが[Canonical](https://support.google.com/webmasters/answer/139066?rd=1)であるかどうかを示します。データソースの値が`true`または`false`であることを確認してください。
* **title**: この宛先にマッピングして、現在のページのタイトルを送信します。
* **path**: この変数にマッピングして、ページのパスを送信します。
* **sections**: この変数にマッピングして、Chartbeatがトラッキングする内容を含むセクション情報を送信します。複数のセクションは、カンマで区切られた値のリストとして送信する必要があります。
* **authors**: この変数にマッピングして、コンテンツの著者に関する情報を送信します。複数の著者は、カンマで区切られた値のリストとして送信する必要があります。

## ベンダー文書

* [Chartbeat Publishing for Editorialについて](http://support.chartbeat.com/?b_id=195)
* [Chartbeat実装ドキュメント](https://chartbeat.com/docs/)
* [Chartbeat構成変数](https://chartbeat.com/docs/configuration_variables/)
* [トラブルシューティング/FAQ](https://chartbeat.com/docs/troubleshooting/)


