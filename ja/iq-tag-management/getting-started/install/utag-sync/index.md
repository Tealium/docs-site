---
title: utag.sync.jsの仕組み
description: この記事では、A/Bテストと多変量タグを実装するためにutag.sync.jsを使用する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/getting-started/install/utag-sync/
---
## 前提条件

この記事で説明されている手順を完了するには、以下の権限が必要です：

* **タグテンプレートの管理**  
この権限は、タグテンプレートを追加および管理するために必要です。
* **JavaScriptドラフトの昇格**  
この権限は、JavaScript拡張機能を公開するために必要です。

## 仕組み

始める前に、同期（sync）と非同期（async）のJavaScriptの違いと、それがiQタグ管理インストールにどのように関連しているかを学ぶことが重要です。([詳細を学ぶ](https://support.tealiumiq.com/en/support/solutions/articles/36000363409-synchronous-vs-asynchronous-javascript-sync-vs-async-))。

この記事で説明されている`utag.sync.js`スクリプトは、Adobe TargetやOptimizelyなどのA/Bおよび多変量テストタグをサポートするためにページに追加できる追加ファイルです。このスクリプトはページコードの`<head>`セクションに配置され、最も一般的なベンダー要件に準拠して同期的にロードされます。ファイルの内容はiQタグ管理で管理されます。


<blockquote>
この機能は、TealiumのフリッカーフリーAdobe Targetソリューションを使用する際に必要です。
</blockquote>


## utag.sync.jsの有効化

デフォルトでは、iQタグ管理アカウント/プロファイルを保存して公開しても`utag.sync.js`ファイルは公開されません。まず、プロファイルレベルで有効にして保存し、適用する必要があります。

`utag.sync.js`スクリプトを有効にするには、次の手順に従います：

1. **保存/公開**をクリックします。
1. **構成公開構成**をクリックします。
1. 一般公開タブから、実装セクションまでスクロールダウンし、**utag.sync.jsファイルを生成**オプションを**オン**に切り替えます。  
    ![](https://docs.tealium.com/images/iq-tag-management/utag-sync-toggle-on.png)
1. **保存**をクリックします。
1. 変更を希望する環境に保存して公開します。  

<blockquote>
このプロファイルの最新バージョンをすべての公開環境に公開する必要があります。そうしないと、`utag.sync.js`ファイルを参照するページがロードされなくなります。
</blockquote>

 有効にすると、utag Syncの範囲がJavaScriptまたはAdvanced JavaScript拡張機能の範囲ドロップダウンリストに表示されます。  
![](https://docs.tealium.com/images/iq-tag-management/utag-sync-enabled-in-dropdown.png)

## utag.sync.jsファイルの編集

次のいずれかの方法でコードを追加できます：

* 推奨：[utag **Sync**範囲の拡張セット](https://docs.tealium.com/about-extensions/)を使用する
* [タグテンプレート](https://docs.tealium.com/manage-templates/)を編集する。

`utag.sync.js`ファイルの内容を次のように追加、編集、または変更します：

1. 変更したいJavaScriptコードまたはAdvanced JavaScriptコード拡張機能に移動します。
1. 拡張機能の名前をクリックして展開します。
1. **範囲**ドロップダウンリストから**utag Sync**を選択します。
1. **構成**セクションで、編集ボックスにカーソルを置き、必要に応じて内容を追加、編集、または変更します。  
    ![](https://docs.tealium.com/images/iq-tag-management/edit-utag-sync-js-file-option.png)
1. 変更を保存して公開します。

## サイトにutag.sync.jsを追加する

`utag.sync.js`スクリプトは、ページがレンダリングされる際に最適なユーザーエクスペリエンスを提供するために、ページの`<head>`セクションに配置するよう設計されています。ベンダーコードがページの内容より先にロードされるように、通常ベンダーコードがロードされる場所と同じ場所にスクリプトを配置する必要があります。

`utag.sync.js`ファイルへのパスには次のパラメータが含まれます：

* **account**  
iQタグ管理アカウントの名前。
* **profile**  
iQタグ管理アカウント内のプロファイルの名前。デフォルト値は**main**です。
* **environment (env)**  
一つ以上の公開環境：**Dev**、**QA**、**Prod**、または**Custom**。

例：

```html
<script src="https://tags.tiqcdn.com/utag/[account]/[profile]/[env]/utag.sync.js"></script>
```

アカウントの[環境管理](https://docs.tealium.com/manage-environments/)画面から特定のスクリプトを取得するには、次の手順に従います：

1. 管理メニューで**環境管理**をクリックします。**環境管理**ダイアログが表示されます。
1. **Tealiumスクリプト**タブには、ファイルにコピーして貼り付けるためのコードが表示されます。  
    ![](https://docs.tealium.com/images/iq-tag-management/code-center-utag-sync.png)
1. **サンプルHTML**タブをクリックして、`utag.sync.js`の配置のサンプルHTMLを表示します。
1. 必要に応じてサンプルHTMLをコピーしてページに使用します。
1. **OK**をクリックし、次に**キャンセル**をクリックしてウィンドウを閉じます。

## ユニバーサルデータオブジェクト（UDO）へのアクセス

`utag.sync.js`ファイルは、ユニバーサルデータオブジェクト（`utag_data`）よりも先にロードされる可能性があるため、コードがそれらの変数を参照できない場合があります。カスタムコードを使用する前に、十分にテストすることを確認してください。

## 本番環境への公開

プロファイルで`utag.sync.js`が有効になると、その後のProd環境へのすべての公開にこのファイルが含まれます。AdvancedおよびBasic JavaScript拡張機能は、特定の環境への公開から制限される場合があり、これにより、同期変更をデプロイする環境をより詳細に制御できます。