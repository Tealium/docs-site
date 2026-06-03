---
title: コンテンツ変更拡張
description: この記事では、コンテンツ変更拡張とその構成方法について説明します。コンテンツ変更拡張を使用してHTML要素の内容を変更します。これは、条件に基づいてA/Bコンテンツを表示するために使用されます。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/content-modification-extension/
---
## 前提条件

* 開始する前に、[拡張について]()を参照してください。

## 仕組み

コンテンツ変更拡張は、新しいコンテンツを追加したり、HTML要素の既存のコンテンツを変更します。例えば、ウェブサイトに広告バナーを追加して更新する必要がある場合、コンテンツ変更拡張を使用して、新しいバナーをサイトの指定された位置に追加します。

この拡張は、ページ内のターゲット要素を特定し、新しい要素の位置、挿入する新しいHTML要素を選択し、構成された条件（ある場合）に基づいてコンテンツが変更されます。

ターゲット要素は、[DOM ID]()または[XPath]()のいずれかで選択できます。[Tealium Web Companion]()を使用して、**On-Page Selecter Element**ツールを使用して、ターゲット要素の識別子値を見つけます。

新しいコンテンツは、ターゲット要素に対する相対位置に基づいて挿入されます。いくつかのオプションがあります：

* **Before Node**：新しいコンテンツは、指定された要素の前に適用されます。
* **After Node**：新しいコンテンツは、指定された要素の後に適用されます。
* **Beginning of Node**：新しいコンテンツは、指定された要素の始まりに挿入されます。
* **End of Node**：新しいコンテンツは、指定された要素の終わりに挿入されます。
* **Replace Node Content**：新しいコンテンツは、指定された要素のコンテンツを置き換えます。
* **Replace Node**：新しいコンテンツは、指定された要素を完全に置き換えます。

**Content**テキストエリアに、新しいコンテンツの標準HTMLコードをコピーして貼り付けます。シングルクォートは使用しないでください。IDを提供することをお勧めします。そうしないと、新しいコンテンツはIDなしで挿入されます。例：`&lt;div id=&#34;myNewId&#34;&gt;My New Content&lt;/div&gt;`

**Condition**を構成して、拡張が実行されるタイミングを制御します。例えば、訪問がショッピングカートページにいて、特定のテストグループにも属している場合に、広告バナーの表示を制御します。

このアプローチを使用して、A/Bテストのパフォーマンスを比較します。各テストグループに対して、コンテンツと条件がわずかに異なる拡張を複製します。次に、Google Analyticsを使用して、A/Bテストが各テストグループに与える影響を分析します。

[コンテンツ変更拡張を使用したA/Bテスト](https://education.tealium.com/learner/courseinfo/id:375)について詳しく学びましょう（Tealium Educationアカウントが必要です）。

## 拡張の使用

拡張が追加されると、次の構成オプションが利用可能になります：

* **Element Type**：変更する要素のタイプ
    * **DOM ID**：（デフォルト）HTMLドキュメント内の選択された要素の一意のID値。
    * **XPath**：ルート要素またはルートノードに対する選択された要素の位置パス名。
* **Identifier**：変更する対象のコンテンツのDOM IDまたはXPath値。  
  例 ID：`myDomId`  
  例 xpath：`/html/body/div/examplecontent`
* **Position**：新しいコンテンツの位置を、ターゲットノードに対する相対位置で選択します。  
以下の位置が利用可能です：
    * Before Node
    * After Node
    * Beginning of Node
    * End of Node
    * Replace Node Content
    * Replace Node
* **Content**：新しいコンテンツを標準HTML形式で入力します。シングルクォートは使用しないでください。
* 条件を追加するには、**Add Condition**ボタンをクリックします。条件を使用すると、コンテンツの変更をいつ行うかを決定できます。
    * 条件ボックス内の**&#43;**ボタンをクリックして、別のAND条件を追加します。
    * OR条件を追加するには、条件ボックスの外側の**&#43;**ボタンをクリックします。

### フッターへのスコープ指定（非推奨）

フッタースコープ機能は非推奨となりました。フッターにスコープ指定された古い拡張は正常に機能しますが、フッタースコープはもはや選択肢として利用できません。コンテンツ変更拡張をフッターにスコープ指定するには、フッタータグ内またはページのbodyタグの下部に別のスクリプトを挿入する必要がありました。以下は、ページのコード内のスクリプトの例です：

```html
     &lt;script type=&#34;text/javascript&#34; src=&#34;//tags.tiqcdn.com/utag/account/profile/environment/utag.footer.js&#34;&gt;&lt;/script&gt;
     &lt;/body&gt;
&lt;/html&gt;

```

### ノード位置

以下は、ノード位置についての詳細な説明です。例は、ソースに次のターゲット要素を含むウェブページに基づいています：

```html
&lt;div id=&#34;myDomId&#34;&gt;Target Node&lt;/div&gt;
```

ターゲット要素に`id`属性があるため、この例では**Element Type**のオプションとして**DOM ID**を使用します。

![](/images/iq-tag-management/iq-extension-content-modification.png)

この拡張により実行されるJavaScriptについての追加の技術詳細を提供するために、以下のステートメントが仮定されます：

* `d = document.getElementById(&#39;myDomId&#39;);`
* `n = document.createElement(&#39;div&#39;);`
* `n.innerHTML = &#39;My New Content&#39;;`

この表は、ターゲット要素に対する各ノード位置オプションの効果を示しています：

| **Node Postion**     | **Result After Insertion** | **Code Applied**  |
| -------------------- | -------------------------- | ----------------- |
| Before Node          | ``` &lt;div&gt;My New Content&lt;/div&gt; &lt;div id=&#34;myDomId&#34;&gt;Target Node&lt;/div&gt; ```       | `d.parentElement.insertBefore(n, d)`              |
| After Node           | ``` &lt;div id=&#34;myDomId&#34;&gt;Target Node&lt;/div&gt; &lt;div&gt;My New Content&lt;/div&gt; ```       | `d.parentElement.insertBefore(n, d.nextSibling);` |
| Beginning of Node    | ``` &lt;div id=&#34;myDomId&#34;&gt;   &lt;div&gt;My New Content&lt;/div&gt;   Target Node &lt;/div&gt; ``` | `d.insertBefore(n, d.firstChild);`                |
| End of Node          | ``` &lt;div id=&#34;myDomId&#34;&gt;   Target Node   &lt;div&gt;My New Content&lt;/div&gt; &lt;/div&gt; ``` | `d.appendChild(n);`                               |
| Replace Node Content | ``` &lt;div id=&#34;myDomId&#34;&gt;My New Content&lt;/div&gt; ```                       | `d.innerHTML=&#39;My New Content&#39;;` |


コンテンツ変更拡張で使用されるJavaScriptメソッドについて詳しく学びましょう：

* [insertBefore](http://www.w3schools.com/jsref/met_node_insertbefore.asp)
* [appendChild](http://www.w3schools.com/jsref/met_node_appendchild.asp) 
* [nextSibling](http://www.w3schools.com/jsref/prop_node_nextsibling.asp) 
* [firstChild](http://www.w3schools.com/jsref/prop_node_firstchild.asp) 
* [innerHTML](http://www.w3schools.com/jsref/prop_html_innerhtml.asp) 

## FAQ

#### jQueryセレクタを使用できますか、それとも要素のIDでなければなりませんか？

コンテンツ変更拡張はjQueryを使用せず、DOM IDまたはXpathを使用してターゲットノードを取得するネイティブJavaScript関数を使用します。ただし、サイトにjQueryがあり、その高度なセレクタ機能を活用したい場合は、ターゲット要素にDOM IDを追加するために使用できます。これを行うには、Pre Loaderにスコープ指定されたJavaScript Code拡張を使用して、ターゲット要素に`id`属性を追加します。これにより、そのDOM IDをコンテンツ変更拡張で使用できます。

JavaScript Code拡張の例：

```js
jQuery(&#34;.my-custom-selector&#34;).get(0).setAttribute(&#34;id&#34;, &#34;myDomId&#34;);
```

