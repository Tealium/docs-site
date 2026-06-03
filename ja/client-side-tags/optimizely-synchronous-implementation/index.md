---
title: Optimizely 同期実装
description: この投稿では、utag.sync.jsコンテナを介してOptimizely Synchronousをロードする手順を説明します。utag.sync.jsは、ページのHTMLの&lt;head&gt;&lt;/head&gt;セクションに含まれている場合、ページのロード時に早期に実行されます。[Optimizely Sync Tag](/ja/client-side-tags/optimizely-sync-tag/)の現在のユーザーには、このタグが廃止されたため、この形式の実装に切り替えることを強くお勧めします。既存のタグインスタンスのみがサポートされています。
url: https://docs.tealium.com/ja/client-side-tags/optimizely-synchronous-implementation/
---
 Tealiumのベストプラクティスは、すべてのタグを非同期でロードすることです。

**重要**：**Optimizelyツールは `utag.sync.js`を検出できません**

執筆時点では、Optimizelyのツールは、タグ管理システムを介して提供される同期スクリプトを検出することができません。Tealium iQがスクリプトを提供しているページでツールを実行すると、エラーメッセージが表示されます。Optimizelyはこの問題を迅速に解決するために作業していますが、それまではエラーメッセージを無視しても安全です。私たちの推奨は、Optimizely Synchronousが期待通りにページ上でロードされているかどうかを確認するためにGhosteryツールを使用することです。

## utag.sync.jsコンテナを使用してOptimizely Syncをロードする（推奨）

この方法は、`utag.js`ファイルがページ上で非同期にコード化されていることを前提としています。

### ステップ1：utag.sync.jsファイルの作成を有効にする

1. 管理メニューで、**公開構成の構成**をクリックします。**公開構成**ダイアログが表示されます。
1. **実装**リストまでスクロールし、**utag.sync.jsを生成**トグルを有効にします。
1. **保存**をクリックして構成を適用します。  

### ステップ2：テストが実行されるすべてのページにutag.sync.jsスクリプトを追加します。スクリプトにアクセスする方法は次のとおりです：

1. 管理メニューで、**コードセンター**をクリックします。**コードセンター**ダイアログが表示されます。
1. **コードセンター**ダイアログの左パネルで、選択した環境を選択します。対応するコードが右パネルに表示されます。
1. **サンプルHTML**タブを選択し、`utag.sync.js`スクリプトをコピーします。
1. スクリプトをコピーし、ページのHTMLの&amp;lt;head&amp;gt;&amp;lt;/head&amp;gt;セクションに追加します。  

### ステップ3：Optimizelyプロジェクト番号の構成

1. 管理メニューで、**テンプレートの管理**をクリックします。  
1. テンプレートリストを展開し、**uTag Sync（プロファイル）**を選択します。
1. テキストエディタに以下のコードブロックを貼り付けます。  
```
document.write(&#39;&amp;lt;script type=&#34;text/javascript&#34; src=&#34;//[cdn.optimizely.com/js/12345678.js](http://cdn.optimizely.com/js/12345678.js)&#34;&amp;gt;&amp;lt;/scr&#39;&#43;&#39;ipt&amp;gt;&#39;);
```

1. `12345678`をOptimizelyから提供されたプロジェクト番号に置き換えます。
1. **プロファイルテンプレートを保存**をクリックし、テンプレートウィンドウを閉じます。

### ステップ4：プロファイルを保存/公開します。

これで、ページ上で`utag.sync.js`ファイルは非常に上部でロードされます。なぜなら、それはHTMLの&amp;lt;head&amp;gt;&amp;lt;/head&amp;gt;に挿入されるからです。これにより、OptimizelyのJavaScriptファイルはページのロードが非常に早い段階で同期的にロードされ、A/Bテストも非常に早い段階で開始されます。その後、ページのロードプロセスが進むと、`utag.js`ファイルがロードされ、残りのタグが非同期でロードされます。

