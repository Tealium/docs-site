---
title: データ値構成拡張機能
description: データ値構成拡張機能は、テキスト、別のデータレイヤー変数、またはJavaScriptコードを使用してデータレイヤー変数の値を構成します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/set-data-values-extension/
---
## 前提条件

* utag v4.38以降。`utag.js`テンプレートの更新についての詳細は、当社のナレッジベース記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。
* [拡張機能の仕組み]()について理解しておくこと。

## 動作原理

この拡張機能を使用して、テキスト、別のデータレイヤー変数、またはJavaScriptコードを使用してデータレイヤー変数の値を構成します。データレイヤー変数は**Set**構成オプションで指定され、新しい値は**To**テキストボックスで指定されます。拡張機能の一回のインスタンスで複数の変数に値を割り当てることができます。オプションで条件を追加して、値が割り当てられるタイミングを制御できます。

## 拡張機能の使用方法

拡張機能を追加すると、以下の構成オプションが利用可能になります：

* **Set**: 値を割り当てたいデータレイヤー変数。変数のドロップダウンリストから選択するか、**&#43; Add Variable**ボタンをクリックして新しい変数を作成します。
* **To**: 変数に割り当てる値。別の変数を構成するには**&#43;**ボタンをクリックし、拡張機能から変数を削除するには**-**ボタンをクリックします。
値は以下のオプションのいずれかになります：
    * **Text**: タイプしたテキスト値に構成します。
    * **Variable**: 別のデータレイヤー変数の値に構成します。
    * **JS Code**: JavaScriptコードステートメントの値に構成します。

* **Condition**: オプション。変数が割り当てられるタイミングを制御するための条件を追加します。条件が追加された場合、変数に新しい値が割り当てられるためには、条件が`true`と評価されなければなりません。

## 例

### テキスト値を構成する

この例では、変数にテキスト値を構成する方法を示します。このシナリオでは、クエリ文字列パラメーター`q`が入力されているかどうかを検出する条件を使用し、データレイヤー変数`page_type`をテキスト値`search`に構成して、これが検索結果ページであることを示します。

1. **Set Data Values**拡張機能を追加します。
1. **Title**に`Set search as the page type`を構成します。
1. ドロップダウンメニューから変数`page_type`を選択します。
1. 値のタイプを**Text**に構成します。
1. テキストボックスに`search`と入力します。
1. **Add Condition**をクリックして以下を構成します：
    * 変数`q (js)`を選択します。
    * 条件を`is defined`に構成します。

![](/images/iq-tag-management/setdatavalues-1.png)

### 変数値を構成する

この例では、変数を別の変数の値に構成する方法を示します。このシナリオでは、変数`page_name`に値がない場合、`document.title`変数の値に構成されます。

1. Set Data Values拡張機能を追加します。
1. **Title**に`Set page_name`を構成します。
1. ドロップダウンメニューから変数`page_name`を選択します。
1. 値のタイプを**Variable**に構成します。変数のドロップダウンリストが表示されます。
1. ドロップダウンメニューから`Document Title`を選択します。
1. **Add Condition**をクリックして以下を構成します：
    * 変数`page_name`を選択します。
    * 条件を`is not defined`に構成します。
    * **Condition**ボックスの外にある**&#43;**をクリックして**Or**条件を追加します。
    * 変数`page_name`を選択します。
    * 条件を`is defined`に構成します。
    * `is defined`テキストボックスの隣にある**&#43;**をクリックして**And**条件を追加します。
    * 変数`page_name`を選択します。
    * 条件を`is not populated`に構成します。

![](/images/iq-tag-management/setdatavalues-2.png)

### JavaScriptコード値を構成する

この例では、JavaScriptステートメントによって返される値に変数を構成する方法を示します。このシナリオでは、検索ページ上の検索結果リンク要素の数をjQueryを使用して選択することによって、検索結果の数が決定されます。変数`search_results`はJavaScriptコードによって返される値に構成されます。

1. Set Data Values拡張機能を追加します。
1. **Title**に`Determine number of search results`を構成します。
1. ドロップダウンメニューから変数**search_results**を選択します。
1. 値のタイプを**JS Code**に構成します。
1. テキストボックスにページ内でのJavaScriptコードをそのまま入力します（またはブラウザコンソールで）。この例では、シンプルなjQueryセレクタと`.length`プロパティを使用します：`$(&#39;.search-results a&#39;).length;`。
1. **Add Condition**をクリックして以下を構成します：
    * 変数`page_type`を選択します。
    * 条件を`equals`に構成し、テキストボックスに`search`を入力します。

![](/images/iq-tag-management/setdatavalues-3.png)

