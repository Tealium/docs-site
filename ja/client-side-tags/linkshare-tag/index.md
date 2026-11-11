---
title: LinkShareタグ構成ガイド
description: この記事では、LinkShareタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/linkshare-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: LinkShare
* **ベンダー**: Rakuten
* **タイプ**: アフィリエイトマーケティング

### 必要条件

**サービス**: LinkShareネットワークアカウント

**構成**:

* マーチャントID

## タグの構成

### タグの追加

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

### タグの構成

1. **タイトル**:（必須）タグインスタンスを識別するための分かりやすいタイトルを入力します。
1. **マーチャントID**:（必須）LinkShareによって広告主に割り当てられた一意のIDを入力します。

#### 読み込みルールの適用

[読み込みルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトの読み込みルールは、**すべてのページで読み込む**ルールです。サイト内の特定のページでこのタグを読み込むには、該当する条件を指定した新しい読み込みルールを作成します。

**ベストプラクティス**: このタグには、以下のベストプラクティスを強く推奨します。

* このタグをコンバージョンページ（注文確認／チェックアウト）と、コンバージョン後のページ（領収書／サンキューページ）で読み込みます。
* パフォーマンスを最適化するため、コンバージョンページごとにタグを1回だけ読み込みます。

#### マッピングの構成

[マッピング](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信する簡単なプロセスです。このタグの宛先変数は、マッピングツールキットで使用できます。使いやすいように、変数は複数のカテゴリにグループ化されています。


<blockquote>
このタグ用に[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を必ず構成してください。
</blockquote>


[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を正しく追加して構成していれば、タグ構成でマッピングを行う必要はありません。Eコマース拡張機能が自動的に処理します。ただし、特定のEコマース変数を上書きする場合や、Eコマース拡張機能を使用していない場合は、以下の宛先変数にマッピングしてください。

* **ord**: 注文／トランザクションの一意のIDを送信するには、この変数にマッピングします。
* **cur**: 3文字の英数字通貨コードを送信するには、この変数にマッピングします。   
 `"cur"=USD`
* **skulist**: 商品SKUのリストを送信するには、この変数にマッピングします。リスト内の各SKUは、商品ごとに一意である必要があります。   
 `"skulist"=sku1|sku2|sku3`
* **qlist**: 商品数量のリストをこの変数にマッピングします。数量は、対応するSKUと同じ順序で指定する必要があります。   
 `"qlist"=2|4|8`
* **amtlist**: 商品小計のリストをこの変数にマッピングします。小計は、対応するSKUと同じ順序で指定し、`price*quantity*100`の形式にする必要があります。   
 `"amtlist"=1000|2000|4000`
* **namelist**: 商品名のリストをこの変数にマッピングします。商品名は、対応するSKUと同じ順序で指定する必要があります。  
 `"namelist"=XXX|YYY|ZZZ`

### ベンダーのドキュメント

* [Rakuten LinkShareについて](http://www.linkshare.com/about/)
* [用語集](http://helpcenter.linkshare.com/publisher/glossary.php)
* [アフィリエイトマーケティングのトラッキング技術：動画チュートリアル](https://rakutenlinkshare.zendesk.com/hc/en-us/articles/200694358-Understanding-Affiliate-Marketing-Tracking-Technology-VIDEO-)
* [アフィリエイトマーケティングのリソース](http://www.linkshare.com/campus/performance_marketing_resources/)（記事や動画の閲覧にはログインが必要です）