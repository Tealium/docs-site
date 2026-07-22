---
title: Web Companion
description: Web Companionを使用すると、タグや拡張機能がWebページ上で正しくロードされているかを検査し、検証することができます。
url: https://docs.tealium.com/ja/iq-tag-management/tealium-tools/web-companion/
---
## Web Companionのインストール

Web Companionは、iQタグ管理アカウントまたはTealium Toolsブラウザプラグインから直接インストールできます。

### Tealium Toolsから

1. [Tealium Toolsブラウザプラグイン](https://docs.tealium.com/tealium-tools-browser-extension/)をインストールします。
1. **ホーム**タブで**Web Companion**をクリックします。

### iQタグ管理を使用する

Web Companionをインストールするには、以下の手順を使用します：

1. TiQコンソールの右上隅にあるあなたの名前をクリックします。
1. **アカウント管理**構成の下で、ドロップダウンリストから**Web Companion**を選択します。  
Web Companionのインストール手順が記載されたポップアップウィンドウが表示されます。
1. メッセージボックスから**Tealium Web Companion**リンクをブラウザのブックマークバーにドラッグします。  

![](https://docs.tealium.com/images/iq-tag-management/iq-web-companion.png)

### ブックマークレット

Web Companionをブックマークとしてインストールするには、次のコードを新しいブックマークのURLにコピーします：
```js
javascript:(function()%7Bif(typeof%20__tealium_tagcompanion=='undefined')%7B__tealium_tagcompanion=document.createElement('SCRIPT');__tealium_tagcompanion.type='text/javascript';__tealium_tagcompanion.src='//tags.tiqcdn.com/utui//utui.tagcompanion.js?v='+Math.random();document.getElementsByTagName('head')[0].appendChild(__tealium_tagcompanion);}})();
```

## Web Companionの起動

Web Companionを起動するには、Universal Tag (`utag.js`)がインストールされているサイトに移動し、ブラウザのブックマークバーにある**Web Companion**リンクをクリックするか、Tealium Toolsブラウザプラグインから開きます。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-tlc.png)

## Web Companionの使用

Web Companionは、**概要**、**データ**、**ツール**の3つの画面（またはタブ）に整理されています。以下のセクションでは、各タブで利用可能な内容について説明します。

### 概要タブ

* **アカウント情報**  
このタブには、ページが実行されている現在のアカウント、プロファイル、バージョン、環境が表示されます。
* **ターゲット環境（デフォルトでは無効）**  
ページコードで検出された環境はオレンジ色で概説され、現在表示されている環境は青色で強調表示されます。環境を変更するには、ロードしたいターゲット環境をクリックし、**ページを更新**をクリックします。他の[環境スイッチャー方法]()について学びます。  

<blockquote>
この機能を有効にするには、公開構成で[Web Companion構成]()をオンにします。
</blockquote>

* **タグ＆拡張タブ**  
このタブでは、どのタグがロードされ、正常にリクエストを送信したかが表示されます。正常に完了した拡張機能も表示されます。
* **タイマー**  
タグのロード時間と送信時間が表示されます。
    * **ロード済み** - `utag.js`ファイルをページにロードするまでの時間。
    * **送信済み** - ページ上のすべてのベンダータグをトリガーするまでの時間。
* **キュー（未保存の変更）**  
Web Companionを使用してプロファイルに適用された変更はキューに入れられ、**保存...**ボタンをクリックするまでコミットされません。変更をコミットしたくない場合は、適切な変更の横にある**X**をクリックしてその変更をキューから削除することもできます。  

![](https://docs.tealium.com/images/iq-tag-management/web-companion-unsaved-changes.png)

### データタブ

データタブでは、ページ上の利用可能なデータ変数を簡単に探索できます。これらは**追加**ボタンを使用してアカウントのデータレイヤーに追加することができます。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-data.png)

次のタイプのデータを表示できます：

* **HTMLメタデータ**  
Webページ、著者、タイトル、およびHTMLドキュメントの他のメタ要素に関する情報。
* **クエリ文字列パラメータ**  
URLのクエリ文字列内に位置するパラメータの名前と値。
* **クッキー**  
訪問とセッション情報を格納する小さなファイル。
* **JavaScript変数**  
`utag_data`以外のJavaScriptページ変数。
* **[Universal Data Object](https://docs.tealium.com/universal-data-object/)**

#### データレイヤーに変数を追加する

データレイヤーに変数を追加するには、次の手順を使用します：

1. **データタブ**をクリックし、データタイプを選択します。  
変数のリストが表示されます。
1. 追加したい変数を見つけて**+追加**をクリックします。  
![](https://docs.tealium.com/images/iq-tag-management/web-companion-js-variables.png)

#### Universal Data Object

Universal Dataオブジェクト（UDO）、または`utag_data`ビューは、ページ上で検出されたデータオブジェクトを表示します。詳細については、[ウェブサイトのデータレイヤーの仕組み](https://docs.tealium.com/how-the-data-layer-works-for-websites/)ガイドを参照してください。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-udo.png)

### ツールタブ

**ツール**タブは、アカウントに構成を追加するのを容易にする便利な機能を提供します。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-tools.png)
利用可能なツールは次のとおりです：

* **オンページ要素セレクタ**  
このシンプルなポイントアンドクリックツールを使用して、イベントトラッキングまたはコンテンツ変更に使用するページ上の要素を選択します。
* **ロードルールヘルパー**  
ターゲットにしたいページから直接ロードルール条件を作成します。現在のページに基づいてページ変数値が事前に入力されます。
* **カスタムターゲット環境**  
デフォルトのDev、QA、Prod以外の環境に切り替えるためにこのツールを使用します。
* **Adobe Test and Target**  
アカウント内のAdobe Targetタグの構成を支援するためにこのツールを使用します。


<blockquote>
Web Companionでアカウントに追加された拡張機能またはロードルールは、iQタグ管理に戻って有効にして公開するまでアクティブになりません。
</blockquote>


#### **オンページ要素セレクタ**

Webページ上の要素を選択して、それに対してContent Modification ExtensionまたはjQuery Live Handler Extensionを事前構成します。ターゲット要素を選択した後、拡張タイプを選択して**キュー**をクリックし、拡張機能をプロファイルに保存します。

関連するDOMノード情報も表示されます。

![](https://docs.tealium.com/images/iq-tag-management/jquery-web-companion.png)

#### **ロードルールヘルパ**

新しいロードルールを作成して、タグがロードされる場所と瞬間を決定します。**キューに追加**をクリックして、ロードルールをプロファイルに保存します。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-load-rule-helper.png)

#### **カスタムターゲット環境**

3つのデフォルト環境（Dev、QA、Prod）の代わりにカスタム環境に公開します。ターゲット環境の名前をテキストボックスに入力し、**環境構成**をクリックします。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-custom-target.png)

#### **Adobe Test and Target**

この拡張機能を追加して、ページ上で変更したいコンテンツを修正します。拡張機能を構成し、**キューに追加**をクリックしてプロファイルに保存します。詳細については、[Adobe Test and Target Extension](https://docs.tealium.com/adobe-target-extension/)を参照してください。

![](https://docs.tealium.com/images/iq-tag-management/web-companion-adobe-target.png)