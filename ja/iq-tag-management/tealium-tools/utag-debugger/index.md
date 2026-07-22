---
title: ユニバーサルタグデバッガー
description: ユニバーサルタグ（UTAG）デバッガーは、ユニバーサルデータオブジェクトの検証とトラッキングコールの追跡に使用されるツールです。
url: https://docs.tealium.com/ja/iq-tag-management/tealium-tools/utag-debugger/
---
## 動作原理

ユニバーサルタグ（UTAG）デバッガーツールは、サイト上の `utag.js` によってトリガーされる[ユニバーサルデータオブジェクト](https://docs.tealium.com/universal-data-object/)とイベントトラッキングコールを表示します。

![](https://docs.tealium.com/images/iq-tag-management/utag-debugger.png)

## インストール

### Tealium Tools

UTAGデバッガーをTealium Toolとしてインストールするには、まず[Tealium Toolsブラウザ拡張機能](https://docs.tealium.com/tealium-tools-browser-extension/)をインストールします。

拡張機能をインストールした後、カスタムツールを追加するには以下の手順に従います：

1. ブラウザの右上にあるTealiumアイコンをクリックしてTealium Toolsを開きます。
1. **カスタムツール**タブに移動し、**+ カスタムツール**の四角をクリックしてから**カスタムツールを追加**をクリックします。
1. 次に、以下のJSONコードを**JSON定義による追加**のフィールドにコピーして貼り付け、**カスタムツールを追加**をクリックします：  
    ```json
    {
        "id" : "teal.sol.debug",
        "title" : "UTAG Debugger",
        "description" : "Universal Tag Debugger",
        "no_ui" : true,
        "scripts" : {
            "utag_monitor" : {
                "js" : "void(window.open(\"\",\"utagmon\",\"width=700,height=600,location=0,menubar=0,status=1,toolbar=0,resizable=1,scrollbars=1\").document.write(\"<script language='JavaScript' id='utagmon' src='//tags.tiqcdn.com/utag/tealium-solutions/main/prod/utag.4.js?opt_show_enrich=0&opt_show_meta=0&opt_show_query=0&opt_show_jspage=0&opt_show_tiq=1&opt_show_cookie=0&_cb=\"+Math.random()+\"'></\"+\"script>\"));",
                "auto_inject" : true
            }
        }
    }
    ```
1. 完了すると、**カスタムツール**タブにツール名の新しいボタンが表示されます。

### ブックマークレット

UTAGデバッガーをブックマークとしてインストールするには、次のコードを新しいブックマークのURLにコピーします：
```js
javascript:void(window.open("","utagmon","width=700,height=600,location=0,menubar=0,status=1,toolbar=0,
resizable=1,scrollbars=1").document.write("<script language='JavaScript' id='utagmon'
src='//tags.tiqcdn.com/utag/tealium-solutions/main/prod/utag.4.js?
opt_show_enrich=0&opt_show_meta=0&opt_show_tiq=1&opt_show_dom=0&opt_show_jspage=0&opt_show_cookie=0&_cb="
+Math.random() +"'></"+"script>"))
```

## UTAGデバッガーの使用

UTAGデバッガーを起動するには、次の手順に従います：

1. サイトに移動します。
1. Tealium Toolsの場合、Tealium Toolsを開いて**UTag Debugger**をクリックします。
1. ブックマークレットの場合、ブラウザツールバーのブックマークをクリックします。
    ![](https://docs.tealium.com/images/iq-tag-management/utag-debugger-bookmarklet.png) 

### バージョンと表示オプション

UTAGデバッガーが開かれると、ページ上に検出された `utag.js` ファイルの情報が上部に表示されます：

* ページ上の `utag.js` ファイルの `account/profile/environment`。
* ページ上の `utag.js` ファイルのバージョン。

![](https://docs.tealium.com/images/iq-tag-management/utag-debugger-options.png)

次の機能を使用します：

* **ブックマークレット** – ブラウザのツールバーにリンクをドラッグして、好みの表示オプションを保存します。
* **イベント** – ページ上で検出されたトラッキングイベントは、`view` イベントまたは `link` イベントです。これらのチェックボックスを切り替えて表示をフィルタリングします。
* **スコープ** - UDOデータの表示スコープを選択します。デフォルトは **ロードルール前**です。
    
<blockquote>
ツールに表示されるUDO変数は、**すべてのタグ - ロードルール前** にスコープされた拡張機能と **すべてのタグ - ロードルール後** にスコープされた拡張機能の後にキャプチャされます。[操作の順序](https://docs.tealium.com/order-of-operations/)についてもっと学びましょう。
</blockquote>

* **データ表示** – 表示する変数タイプを選択します。UDO変数は常に表示されます。