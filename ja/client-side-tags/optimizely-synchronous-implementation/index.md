---
title: Optimizely 同期実装
description: この記事では、utag.sync.js コンテナを使用して Optimizely を同期的に読み込む手順について説明します。utag.sync.js をページの HTML の &lt;head&gt;&lt;/head&gt; セクションに含めると、ページ読み込みの早い段階で実行されます。[Optimizely Sync タグ](/ja/client-side-tags/optimizely-sync-tag/)を現在使用している場合、このタグは非推奨になっているため、この実装方式に切り替えることを強く推奨します。既存のタグインスタンスのみがサポートされます。
url: https://docs.tealium.com/ja/client-side-tags/optimizely-synchronous-implementation/
---

<blockquote>
Tealium では、すべてのタグを非同期で読み込むことをベストプラクティスとしています。
</blockquote>


**重要**：**Optimizely ツールは `utag.sync.js` を検出できません**

執筆時点では、Optimizely のツールは、タグ管理システムを介して配信された同期スクリプトを検出できません。タグ管理システムがスクリプトを配信しているページでこのツールを実行すると、エラーメッセージが表示されます。Optimizely はこの問題の早期解決に取り組んでいます。それまでは、このエラーメッセージを無視しても問題ありません。Optimizely Synchronous がページ上で想定どおりに読み込まれているかどうかを確認するには、Ghostery ツールを使用することを推奨します。

## utag.sync.js コンテナを使用した Optimizely Sync の読み込み（推奨）

この方法では、`utag.js` ファイルがページ上で非同期に読み込まれるよう実装されていることを前提としています。

### ステップ1：utag.sync.js ファイルの生成を有効にする

1. 管理メニューで、**Configure Publish Settings**をクリックします。**Publish Configuration**ダイアログが表示されます。
1. **Implementation**項目まで下にスクロールし、**Generate utag.sync.js**トグルを有効にします。
1. **Save**をクリックして構成を適用します。  

### ステップ2：テストを実施するすべてのページに utag.sync.js スクリプトを追加する

スクリプトにアクセスする手順は次のとおりです。

1. 管理メニューで、**Code Center**をクリックします。**Code Center**ダイアログが表示されます。
1. **Code Center**ダイアログの左側のパネルで、使用する環境を選択します。対応するコードが右側のパネルに表示されます。
1. **Sample HTML**タブを選択し、`utag.sync.js` スクリプトをコピーします。
1. スクリプトをコピーし、ページの HTML の &lt;head&gt;&lt;/head&gt; セクションに追加します。  

### ステップ3：Optimizely のプロジェクト番号を構成する

1. 管理メニューで、**Manage Templates**をクリックします。  
1. テンプレートの一覧を展開し、**uTag Sync (Profile)**を選択します。
1. 以下のコードブロックをテキストエディターに貼り付けます。  

```
document.write('&lt;script type="text/javascript" src="//[cdn.optimizely.com/js/12345678.js](http://cdn.optimizely.com/js/12345678.js)"&gt;&lt;/scr'+'ipt&gt;');
```

1. `12345678` を、Optimizely から提供されたプロジェクト番号に置き換えます。
1. **Save Profile Template**をクリックし、テンプレートウィンドウを閉じます。

### ステップ4：プロファイルを保存して公開する

これで、`utag.sync.js` ファイルは HTML の &lt;head&gt;&lt;/head&gt; 内に挿入されているため、ページの最上部で読み込まれます。これにより、ページ読み込みの非常に早い段階で Optimizely の JavaScript ファイルが同期的に読み込まれ、A/B テストも早期に開始されます。その後、ページ読み込みプロセスの後半で `utag.js` ファイルが読み込まれ、残りのタグが非同期で読み込まれます。