---
title: LinkShareタグ構成ガイド
description: この記事では、LinkShareタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/linkshare-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: LinkShare
* **ベンダー**: 楽天
* **タイプ**: アフィリエイトマーケティング

### 必要なもの

**サービス**: LinkShare Network Account

**構成**:

* マーチャントID

## Tealium iQでのタグ構成

### タグの追加

Tealium iQのタグマーケットプレイスは、さまざまなタグを提供しています。詳細については、[タグの管理](https://docs.tealium.com/manage-tags/#add-a-tag)を参照してください。

### タグの構成

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **マーチャントID** (必須): LinkShareによって割り当てられた広告主のユニークIDを入力します。

#### ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールは、デフォルトのロードルールです。サイトの特定のページでこのタグをロードするには、関連する条件を持つ新しいロードルールを作成します。

**ベストプラクティス**: 以下のベストプラクティスは、このタグに強く推奨されています。

* このタグをコンバージョンページ（注文確認/チェックアウト）およびコンバージョン後のページ（レシート/サンキュー）でロードします。
* 最適なパフォーマンスのため、コンバージョンページごとにタグを一度だけロードします。

#### マッピングの構成

[マッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。このタグの宛先変数は、マッピングツールキットで利用できます。使いやすさのために、変数は異なるカテゴリにグループ化されています。


<blockquote>
このタグのために[E-commerce Extension](https://docs.tealium.com/e-commerce-extension/)を構成することを忘れないでください。
</blockquote>


[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)を適切に追加および構成していれば、タグ構成で何もマップする必要はありません。E-Commerce Extensionがそれを処理します。ただし、特定のE-commerce変数を上書きしたい場合や、E-Commerce Extensionを使用していない場合は、以下の宛先変数にマップします。

* **ord**: 注文/トランザクションのユニークIDを送信するためにこの変数にマップします。
* **cur**: アルファベット3文字の通貨値を送信するためにこの変数にマップします。   
 `"cur"=USD`
* **skulist**: アイテムSKUのリストを送信するためにこの変数にマップします。リスト内の各SKUはアイテムに固有でなければなりません。   
 `"skulist"=sku1|sku2|sku3`
* **qlist**: アイテムの数量のリストをこの変数にマップします。数量は、対応するSKUと同じ順序でリストされていなければなりません。   
 `"qlist"=2|4|8`
* **amtlist**: アイテムの小計のリストをこの変数にマップします。小計は、対応するSKUと同じ順序でリストされ、`price*quantity*100`としてフォーマットされていなければなりません。   
 `"amtlist"=1000|2000|4000`
* **namelist**: アイテム名のリストをこの変数にマップします。アイテム名は、対応するSKUと同じ順序でリストされていなければなりません。  
 `"namelist"=XXX|YYY|ZZZ`

### ベンダーのドキュメンテーション

* [楽天LinkShareについて](http://www.linkshare.com/about/)
* [用語集](http://helpcenter.linkshare.com/publisher/glossary.php)
* [アフィリエイトマーケティング追跡技術：ビデオチュートリアル](https://rakutenlinkshare.zendesk.com/hc/en-us/articles/200694358-Understanding-Affiliate-Marketing-Tracking-Technology-VIDEO-)
* [アフィリエイトマーケティングリソース](http://www.linkshare.com/campus/performance_marketing_resources/) (記事とビデオの閲覧にはログインが必要です)


