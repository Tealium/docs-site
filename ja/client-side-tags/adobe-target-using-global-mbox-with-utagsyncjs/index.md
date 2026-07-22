---
title: Adobe TargetをGlobal mboxとutag.sync.jsを使用して構成する
description: この記事では、Tealium iQタグ管理アカウントでAdobe TargetをGlobal mboxとutag.sync.jsを使用して構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-target-using-global-mbox-with-utagsyncjs/
---
## 開始する前に

この記事では、以下のトピックについての知識があることを前提としています：

* [Adobe Targetタグ構成ガイド](https://docs.tealium.com/adobe-test-target-tag/)
* [非同期フリッカーフリーターゲット実装](https://docs.tealium.com/flicker-free-test-and-target/)

## 概要

Adobe Targetには、コンテンツを変更するために使用できる2つの方法があります。

* コンテンツが変更される正確な場所に地域のmboxesを配置します。
* ページにGlobal mbox作成ステートメントを配置し、Adobe TnTインターフェース内で全てのロジックを定義し、どのコンテンツが変更されるかを決定します。

この投稿では、Global mboxアプローチの実装をレビューします。Global mboxアプローチは同期的な実装です。ベストプラクティスとして、リスクを軽減するためにすべてを非同期に保つことをお勧めします。要素を同期的にロードするリスクを理解してください。

この投稿で概説する方法を使用すると、Tealiumの実装を非同期に保ちつつ、Global mboxを同期的にロードすることができます。このソリューションは、Adobe Targetからの`mbox.js`ファイルの後期バージョンのいずれかを使用していることを前提としています。後期バージョンは、`mboxDefault`クラスを自動的に作成しますが、`mbox.js`の古いバージョンでは作成されません。

古いバージョンの`mbox.js`を使用している場合でも、サポートは可能ですが、追加のステップが必要になります。詳細については、Legacy `mbox.js`セクションを参照してください。

## Publish Settingsでutag.sync.jsを有効にする

まず、適切な公開構成を有効にする必要があります：

1. 管理メニューで、**公開構成の構成**をクリックします。**公開構成**ダイアログが表示されます。
1. **Adobe Targetのフリッカーフリーサポート**機能を有効にします。  
これで、`utag.sync.js`ファイル内にロードしたいコードを貼り付けることができる追加のテンプレートがManage Templatesセクションに表示されます。

## ページにutag.sync.jsをコードする

次に、`utag.sync.js`ファイルをページにコードする必要があります。このファイルは、ページの中に含めるべきであり、同期的に含める必要があります。Adobe Targetを使用するすべてのページに`utag.sync.js`ファイルが含まれていることを確認してください。

`utag.sync.js`ファイルを使用すると、このファイルにロードルールを割り当てることはできません。`utag.sync.js`内のコードの実行を停止する唯一の方法は、ファイル自体内の"if"ステートメントや他の条件を使用することです。

## mbox.jsをダウンロードする

Adobeインターフェース内でキャンペーンとオファーを構成した後、`mbox.js`ファイルをダウンロードする必要があります。

![](https://docs.tealium.com/images/client-side-tags/no-title-704ibe6eea6542f7b685.png)

## mbox.jsファイルをローカルにホストする

mboxesを提供するすべてのホスト（ドメイン）で`mbox.js`ファイルを保存する必要があります。これは公開アクセス可能なファイルである必要があり、あなたのサイトからロードできるようにする必要があります。

## utag.sync.jsを構成する

`mbox.js`ファイルをダウンロードしたら、ファイルを開き、その内容をコピーします。

Tealiumユーザーインターフェース内の`utag.sync.js`ファイル（uTag sync）のテンプレートを開きます。これは、画面の右上隅にあるあなたの名前をクリックし、**テンプレートの管理**を選択することで行います。表示されるドロップダウンから、**uTag sync**を選択します。

![](https://docs.tealium.com/images/client-side-tags/no-title-705i000275e236003fa2.png)

テンプレートに以下の内容をコピーして貼り付けます：

```
var mboxjs_location = "//path/to/mbox.js";
var global_mbox_name = "Global mbox name";
document.write('<script src="' + mboxjs_location + '"></script>');
document.write('<script type="text/javascript">mboxCreate("'+global_mbox_name+'")</script>');

```

最初の行は、`mbox.js`ファイルへのパスを追加する場所です。`//path/to/mbox.js`を実際のパスに置き換えてください。

2行目は、Global mboxの名前を追加する場所です。`Global mbox name`をGlobal mboxの名前に置き換えてください。

添付されているテキストファイルは、すべてを追加した後のサンプル`utag.sync.js`テンプレートの見た目を示しています。

## Legacy mbox.js

古いバージョンの`mbox.js`ファイルを使用している場合、mboxDefault要素を手動で作成する必要があります。これを行うためには、上記と同様のコードを使用します：

```
//Create mboxDefault
document.write('<div class="mboxDefault"></div>')

```

これは変更する必要はありません。なぜなら、これは単に以下のような見た目の`mboxCreate`関数よりも上にあるhead内のdiv要素を作成するだけだからです：

```
<div class="mboxDefault"></div>

```

このブロックは、document.writeで始まる2つの既存の行の間に配置する必要があります。

この方法を使用すると、`utag.sync.js`ファイルには`mbox.js`コードが含まれ、その後にこの他のコードブロックが続き、要素を作成し、その後に`mboxCreate`関数を呼び出すコードが続きます。これのサンプルは、添付されているSample `utag.sync.js` Legacy Templateファイルで見ることができます。

## 結論

これが構成されると、`utag.sync.js`ファイルがあなたのウェブサイトのheadに同期的にコード化されます。ページの本文には、主要なTealiumライブラリ（`utag.js`）ファイルが非同期でロードされます。

`utag.sync.js`内には、`mbox.js`ファイルが貼り付けられ、`mboxCreate()`を呼び出す小さなスニペット、または2つの小さなスニペットが追加されます。


<blockquote>
`utag.footer.js`は廃止され、もう選択肢ではありません。`utag.footer.js`を使用している古い実装は以前と同様に機能し続けます。古いコンテンツ変更拡張のスコープを変更する必要はありません。元々'Footer'にスコープされていた古いコンテンツ変更拡張は、'DOM Ready'にスコープされているように見え、`utag.footer.js`ファイルに引き続き公開されます。
</blockquote>

