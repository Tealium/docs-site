---
title: ユニバーサルタグデバッガー
description: ユニバーサルタグ（UTAG）デバッガーは、ユニバーサルデータオブジェクトの検証とトラッキングコールの追跡に使用されるツールです。
url: https://docs.tealium.com/ja/iq-tag-management/tealium-tools/utag-debugger/
---
## 動作原理

ユニバーサルタグ（UTAG）デバッガーツールは、サイト上の `utag.js` によってトリガーされる[ユニバーサルデータオブジェクト]()とイベントトラッキングコールを表示します。

![](/images/iq-tag-management/utag-debugger.png)

## インストール

### Tealium Tools

UTAGデバッガーをTealium Toolとしてインストールするには、まず[Tealium Toolsブラウザ拡張機能]()をインストールします。

拡張機能をインストールした後、カスタムツールを追加するには以下の手順に従います：

1. ブラウザの右上にあるTealiumアイコンをクリックしてTealium Toolsを開きます。
1. **カスタムツール**タブに移動し、**&#43; カスタムツール**の四角をクリックしてから**カスタムツールを追加**をクリックします。
1. 次に、以下のJSONコードを**JSON定義による追加**のフィールドにコピーして貼り付け、**カスタムツールを追加**をクリックします：  
    ```json
    {
        &#34;id&#34; : &#34;teal.sol.debug&#34;,
        &#34;title&#34; : &#34;UTAG Debugger&#34;,
        &#34;description&#34; : &#34;Universal Tag Debugger&#34;,
        &#34;no_ui&#34; : true,
        &#34;scripts&#34; : {
            &#34;utag_monitor&#34; : {
                &#34;js&#34; : &#34;void(window.open(\&#34;\&#34;,\&#34;utagmon\&#34;,\&#34;width=700,height=600,location=0,menubar=0,status=1,toolbar=0,resizable=1,scrollbars=1\&#34;).document.write(\&#34;&lt;script language=&#39;JavaScript&#39; id=&#39;utagmon&#39; src=&#39;//tags.tiqcdn.com/utag/tealium-solutions/main/prod/utag.4.js?opt_show_enrich=0&amp;opt_show_meta=0&amp;opt_show_query=0&amp;opt_show_jspage=0&amp;opt_show_tiq=1&amp;opt_show_cookie=0&amp;_cb=\&#34;&#43;Math.random()&#43;\&#34;&#39;&gt;&lt;/\&#34;&#43;\&#34;script&gt;\&#34;));&#34;,
                &#34;auto_inject&#34; : true
            }
        }
    }
    ```
1. 完了すると、**カスタムツール**タブにツール名の新しいボタンが表示されます。

### ブックマークレット

UTAGデバッガーをブックマークとしてインストールするには、次のコードを新しいブックマークのURLにコピーします：
```js
javascript:void(window.open(&#34;&#34;,&#34;utagmon&#34;,&#34;width=700,height=600,location=0,menubar=0,status=1,toolbar=0,
resizable=1,scrollbars=1&#34;).document.write(&#34;&lt;script language=&#39;JavaScript&#39; id=&#39;utagmon&#39;
src=&#39;//tags.tiqcdn.com/utag/tealium-solutions/main/prod/utag.4.js?
opt_show_enrich=0&amp;opt_show_meta=0&amp;opt_show_tiq=1&amp;opt_show_dom=0&amp;opt_show_jspage=0&amp;opt_show_cookie=0&amp;_cb=&#34;
&#43;Math.random() &#43;&#34;&#39;&gt;&lt;/&#34;&#43;&#34;script&gt;&#34;))
```

## UTAGデバッガーの使用

UTAGデバッガーを起動するには、次の手順に従います：

1. サイトに移動します。
1. Tealium Toolsの場合、Tealium Toolsを開いて**UTag Debugger**をクリックします。
1. ブックマークレットの場合、ブラウザツールバーのブックマークをクリックします。
    ![](/images/iq-tag-management/utag-debugger-bookmarklet.png) 

### バージョンと表示オプション

UTAGデバッガーが開かれると、ページ上に検出された `utag.js` ファイルの情報が上部に表示されます：

* ページ上の `utag.js` ファイルの `account/profile/environment`。
* ページ上の `utag.js` ファイルのバージョン。

![](/images/iq-tag-management/utag-debugger-options.png)

次の機能を使用します：

* **ブックマークレット** – ブラウザのツールバーにリンクをドラッグして、好みの表示オプションを保存します。
* **イベント** – ページ上で検出されたトラッキングイベントは、`view` イベントまたは `link` イベントです。これらのチェックボックスを切り替えて表示をフィルタリングします。
* **スコープ** - UDOデータの表示スコープを選択します。デフォルトは **ロードルール前**です。
    ツールに表示されるUDO変数は、**すべてのタグ - ロードルール前** にスコープされた拡張機能と **すべてのタグ - ロードルール後** にスコープされた拡張機能の後にキャプチャされます。[操作の順序]()についてもっと学びましょう。
* **データ表示** – 表示する変数タイプを選択します。UDO変数は常に表示されます。