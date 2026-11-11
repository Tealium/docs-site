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

### 必須要件

**サービス**: Chartbeatアカウント

**構成**:

* ChartbeatユーザーID

## タグの構成

### タグの追加

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

### タグの構成

1. **タイトル**: （必須）タグインスタンスを識別するための分かりやすいタイトルを入力します。
1. **ユーザーID**: （必須）Chartbeatから提供された数値のユーザーIDを入力します。このIDはChartbeatアカウントで確認できます。例: `1234`
1. **ドメイン**: （必須）Chartbeatを実装するドメイン名を入力します。プレフィックス `www` は含めないでください。例: `yoursite.com`
1. **Canonicalを使用**: （任意）Chartbeatがページへのアクセスに[Canonical](https://support.google.com/webmasters/answer/139066?rd=1)パス（優先URL）を使用するかどうかを選択します。デフォルトでは、［Canonicalを使用］ドロップダウンはfalseに構成されており、この場合、Chartbeatはページの実際のURLを使用します。  
  * サイトのHTML内のlink要素を使用して定義したcanonicalパスをChartbeatで使用する場合は、`true` を選択します。

たとえば、あるページに2つの異なるURLからアクセスできるとします。

```
http://yoursite.com/products?category=apparel&kids
http://yoursite.com/apparel/kids
```

ただし、URL #2のみがcanonicalとして構成されています。**Canonicalを使用**フィールドを有効にすると、Chartbeatはトラッキングに優先URL #2を使用できます。  


<blockquote>
`path` 変数へのマッピングにより、この選択を上書きできます。
</blockquote>


データマッピングツールボックスを使用すると、#2から#4までのタグ構成を上書きしたり、動的に構成したりできます。

### 読み込みルールの適用

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトの読み込みルールは、**すべてのページで読み込む**ルールです。特定のページでこのタグを読み込むには、該当する条件を指定した新しい読み込みルールを作成します。


<blockquote>
デフォルトの**すべてのページで読み込む**ルールは変更しないでください。正確なデータ収集を確保するため、Chartbeatは、ほとんどの分析タグと同様に、サイトのすべてのページで読み込むことを推奨します。
</blockquote>


### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数にデータを送信する簡単なプロセスです。このタグの宛先変数は、マッピングツールキットで使用できます。

* **ユーザーID:** Chartbeatから提供された数値のユーザーIDを送信するには、この宛先にマッピングします。
* **ドメイン**: Chartbeatが実装されているドメイン名を送信するには、この宛先にマッピングします。
* **Canonicalを使用（canonical）**: ページのURLが[Canonical](https://support.google.com/webmasters/answer/139066?rd=1)かどうかを示すには、この宛先にマッピングします。データソースの値が `true` または `false` のいずれかであることを確認してください。
* **title**: ページの現在のタイトルを送信するには、この宛先にマッピングします。
* **path**: ページのパスを送信するには、この変数にマッピングします。
* **sections**: Chartbeatでトラッキングするコンテンツを含むセクション情報を送信するには、この変数にマッピングします。複数のセクションは、値をカンマで区切ったリストとして送信する必要があります。
* **authors**: コンテンツの作成者に関する情報を送信するには、この変数にマッピングします。複数の作成者は、値をカンマで区切ったリストとして送信する必要があります。

## ベンダーのドキュメント

* [編集者向けChartbeat Publishingについて](http://support.chartbeat.com/?b_id=195)
* [Chartbeat実装ドキュメント](https://chartbeat.com/docs/)
* [Chartbeat構成変数](https://chartbeat.com/docs/configuration_variables/)
* [トラブルシューティング／よくある質問](https://chartbeat.com/docs/troubleshooting/)