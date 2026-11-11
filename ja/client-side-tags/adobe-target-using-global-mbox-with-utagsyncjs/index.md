---
title: グローバル mbox と utag.sync.js を使用した Adobe Target
description: この記事では、タグ管理アカウントでグローバル mbox と utag.sync.js を使用して Adobe Target を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-target-using-global-mbox-with-utagsyncjs/
---
## 始める前に

この記事では、以下のトピックに関する知識があることを前提としています。

* [Adobe Target タグ構成ガイド](https://docs.tealium.com/adobe-test-target-tag/)
* [非同期のフリッカーフリー Target 実装](https://docs.tealium.com/flicker-free-test-and-target/)

## 概要

Adobe Target には、コンテンツの変更に使用できる方法が 2 つあります。

* コンテンツを変更するページ上の正確な位置に、リージョナル mbox を配置します。
* グローバル mbox の作成ステートメントをページに配置し、変更するコンテンツに関するすべてのロジックを Adobe TnT インターフェイス内で定義します。

この記事では、グローバル mbox を使用する方法の実装について説明します。グローバル mbox を使用する方法は同期実装です。リスクを軽減するため、ベストプラクティスとして、すべてを非同期に保つことをお勧めします。要素を同期的に読み込むことのリスクを十分に理解してください。

この記事で説明する方法では、Tealium の実装を非同期に保ちながら、グローバル mbox を同期的に読み込むことができます。また、このソリューションでは、Adobe Target の比較的新しいバージョンの `mbox.js` ファイルを使用していることを前提としています。新しいバージョンでは、`mboxDefault` クラスを持つコンテナが自動的に作成されますが、古いバージョンの `mbox.js` では作成されません。

古いバージョンの `mbox.js` を使用している場合も対応できますが、追加の手順が必要です。詳細については、「従来の `mbox.js`」セクションを参照してください。

## パブリッシュ構成で utag.sync.js を有効にする

最初に、適切なパブリッシュ構成を有効にする必要があります。

1. 管理メニューで **Configure Publish Settings** をクリックします。**Publish Configuration** ダイアログが表示されます。
1. **Flicker-Free Support for Adobe Target** 機能を有効にします。  
これにより、「Manage Templates」セクションにテンプレートが追加され、`utag.sync.js` ファイル内で読み込むコードを貼り付けられるようになります。

## utag.sync.js をページに組み込む

次に、`utag.sync.js` ファイルをページに組み込む必要があります。前述のとおり、このファイルはページの head に配置し、同期的に読み込む必要があります。Adobe Target を使用するすべてのページに `utag.sync.js` ファイルが含まれていることを確認してください。

`utag.sync.js` ファイルには、ロードルールを割り当てることができません。`utag.sync.js` 内のコードが実行されないようにするには、ファイル内で「if」ステートメントまたはその他の条件を使用する必要があります。

## mbox.js をダウンロードする

Adobe インターフェイス内でキャンペーンとオファーを構成したら、`mbox.js` ファイルをダウンロードする必要があります。

![](https://docs.tealium.com/images/client-side-tags/no-title-704ibe6eea6542f7b685.png)

## mbox.js ファイルをローカルでホストする

mbox を提供するすべてのホスト（ドメイン）に、`mbox.js` ファイルを保存する必要があります。このファイルはサイトから読み込めるように、一般公開されている必要があります。

## utag.sync.js を構成する

`mbox.js` ファイルをダウンロードしたら、ファイルを開いて内容をコピーします。

Tealium ユーザーインターフェイス内で、`utag.sync.js` ファイル（uTag sync）のテンプレートを開きます。画面右上にある自分の名前をクリックし、**Manage Templates** を選択します。表示されたドロップダウンから **uTag sync** を選択します。

![](https://docs.tealium.com/images/client-side-tags/no-title-705i000275e236003fa2.png)

テンプレートに以下をコピーして貼り付けます。

```
var mboxjs_location = "//path/to/mbox.js";
var global_mbox_name = "Global mbox name";
document.write('<script src="' + mboxjs_location + '"></script>');
document.write('<script type="text/javascript">mboxCreate("'+global_mbox_name+'")</script>');

```

最初の行には、`mbox.js` ファイルへのパスを追加します。`//path/to/mbox.js` を実際のパスに置き換えます。

2 行目には、グローバル mbox の名前を追加します。`Global mbox name` をグローバル mbox の名前に置き換えます。

すべてを追加した後の `utag.sync.js` テンプレートの例を示すテキストファイルが添付されています。

## 従来の mbox.js

古いバージョンの `mbox.js` ファイルを使用している場合は、mboxDefault 要素を手動で作成する必要があります。そのためには、上記と同様のコードを使用します。

```
//Create mboxDefault
document.write('<div class="mboxDefault"></div>')

```

このコードは、`mboxCreate` 関数よりも前に、以下のような div 要素を head 内に作成するだけなので、通常は変更する必要はありません。

```
<div class="mboxDefault"></div>

```

このブロックは、document.write で始まる既存の 2 行の間に配置する必要があります。

この方法を使用すると、`utag.sync.js` ファイルには、最初に `mbox.js` コード、次に要素を作成するこのコードブロック、最後に `mboxCreate` 関数を呼び出すコードが含まれます。添付されている Sample `utag.sync.js` Legacy Template ファイルで、この例を確認できます。

## まとめ

この構成が完了すると、`utag.sync.js` ファイルが Web サイトの head に組み込まれ、同期的に読み込まれます。ページの body では、メインの Tealium ライブラリ（`utag.js`）ファイルが非同期に読み込まれます。

`utag.sync.js` 内には、`mbox.js` ファイルの内容を貼り付け、`mboxCreate()` を呼び出すための 1 つまたは 2 つの短いコードスニペットを追加します。


<blockquote>
`utag.footer.js` は非推奨となり、現在は使用できません。`utag.footer.js` を使用している古い実装は、これまでどおり引き続き機能します。古い Content Modification 拡張機能のスコープを変更する必要はありません。当初「Footer」をスコープとしていた古い Content Modification 拡張機能は、「DOM Ready」をスコープとしているように表示されますが、引き続き `utag.footer.js` ファイルにパブリッシュされます。
</blockquote>
