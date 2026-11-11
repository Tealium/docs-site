---
title: utag.sync.js の仕組み
description: この記事では、utag.sync.js を使用して A/B テストおよび多変量タグを実装する方法について説明します。
url: https://docs.tealium.com/ja/tag-management/getting-started/install/utag-sync/
---
## 前提条件

この記事で説明する手順を実行するには、次の権限が必要です。

* **タグテンプレートの管理**  
タグテンプレートを追加および管理するために必要な権限です。
* **JavaScript ドラフトの昇格**  
JavaScript 拡張機能をパブリッシュするために必要な権限です。

## 仕組み

作業を開始する前に、同期（sync）JavaScript と非同期（async）JavaScript の違い、およびそれらとタグ管理のインストールとの関係を理解しておくことが重要です。詳しくは、[同期 JavaScript と非同期 JavaScript（sync と async）](https://support.tealiumiq.com/en/support/solutions/articles/36000363409-synchronous-vs-asynchronous-javascript-sync-vs-async-)を参照してください。

この記事で説明する `utag.sync.js` スクリプトは、Adobe Target や Optimizely などの A/B テストタグおよび多変量テストタグをサポートするためにページへ追加できるファイルです。このスクリプトはページコードの `<head>` セクションに配置され、一般的なベンダー要件を満たすために同期的に読み込まれます。ファイルの内容はタグ管理で管理されます。


<blockquote>
Tealium のちらつき防止 Adobe Target ソリューションを使用する場合、この機能が必要です。
</blockquote>


## utag.sync.js の有効化

デフォルトでは、タグ管理のアカウント／プロファイルを保存してパブリッシュしても、`utag.sync.js` ファイルはパブリッシュされません。まずこの機能を有効にして保存し、プロファイルレベルで適用する必要があります。

次の手順で `utag.sync.js` スクリプトを有効にします。

1. **保存／パブリッシュ**をクリックします。
1. **構成のパブリッシュ構成**をクリックします。
1. 「一般パブリッシュ」タブで「実装」セクションまで下にスクロールし、**utag.sync.js ファイルを生成**オプションを**オン**に切り替えます。  
    ![](https://docs.tealium.com/images/tag-management/utag-sync-toggle-on.png)
1. **保存**をクリックします。
1. 変更内容を保存し、必要な環境にパブリッシュします。  

<blockquote>
このプロファイルの最新バージョンを、すべてのパブリッシュ環境にパブリッシュする必要があります。パブリッシュしない場合、`utag.sync.js` ファイルを参照するページが読み込まれなくなります。
</blockquote>

 有効にすると、JavaScript または高度な JavaScript 拡張機能の「スコープ」ドロップダウンリストに「utag Sync」スコープが表示されます。  
![](https://docs.tealium.com/images/tag-management/utag-sync-enabled-in-dropdown.png)

## utag.sync.js ファイルの編集

次のいずれかの方法でコードを追加できます。

* 推奨：[utag **Sync** スコープを構成した拡張機能](https://docs.tealium.com/about-extensions/)を使用する
* [タグテンプレート](https://docs.tealium.com/manage-templates/)を編集する

次の手順で `utag.sync.js` ファイルの内容を追加、編集、または変更します。

1. ファイルを変更する JavaScript コードまたは高度な JavaScript コード拡張機能に移動します。
1. 拡張機能の名前をクリックして展開します。
1. **スコープ**ドロップダウンリストから **utag Sync** を選択します。
1. **構成**セクションで編集ボックスにカーソルを置き、必要に応じて内容を追加、編集、または変更します。  
    ![](https://docs.tealium.com/images/tag-management/edit-utag-sync-js-file-option.png)
1. 変更内容を保存してパブリッシュします。

## サイトへの utag.sync.js の追加

`utag.sync.js` スクリプトは、ページの `<head>` セクションに配置するように設計されています。ページのレンダリング時に最適なユーザーエクスペリエンスを提供するため、ベンダーコードがページのコンテンツよりも先に読み込まれるように、通常そのコードが読み込まれる場所と同じ位置にスクリプトを配置してください。

`utag.sync.js` ファイルへのパスには、次のパラメータが含まれます。

* **account**  
タグ管理アカウントの名前。
* **profile**  
タグ管理アカウント内のプロファイル名。デフォルト値は **main** です。
* **environment (env)**  
1 つ以上のパブリッシュ環境：**Dev**、**QA**、**Prod**、または **Custom**。

例：

```html
<script src="https://tags.tiqcdn.com/utag/[account]/[profile]/[env]/utag.sync.js"></script>
```

次の手順で、アカウントの[環境の管理](https://docs.tealium.com/manage-environments/)画面から、アカウント固有のスクリプトを取得します。

1. 管理メニューで**環境の管理**をクリックします。**環境の管理**ダイアログが表示されます。
1. **Tealium スクリプト**タブには、ファイルにコピー＆ペーストできるコードが表示されます。  
    ![](https://docs.tealium.com/images/tag-management/code-center-utag-sync.png)
1. **サンプル HTML** タブをクリックして、`utag.sync.js` の配置例となる HTML を表示します。
1. 必要に応じてサンプル HTML をコピーし、ページに貼り付けます。
1. **OK** をクリックし、続いて**キャンセル**をクリックしてウィンドウを閉じます。

## ユニバーサルデータオブジェクト（UDO）へのアクセス

`utag.sync.js` ファイルは、ユニバーサルデータオブジェクト（`utag_data`）よりも先に読み込まれる可能性が高いため、コードからそれらの変数を参照できない場合があります。使用する予定のカスタムコードは必ず十分にテストしてください。

## 本番環境へのパブリッシュ

プロファイルで `utag.sync.js` を有効にすると、それ以降の Prod 環境へのすべてのパブリッシュにこのファイルが含まれます。高度な JavaScript 拡張機能および基本 JavaScript 拡張機能は、特定の環境にパブリッシュされないよう制限できます。これにより、同期処理の変更をデプロイする環境をより細かく制御できます。