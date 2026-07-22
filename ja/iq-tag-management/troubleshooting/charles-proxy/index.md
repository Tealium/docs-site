---
title: Charles Proxyを使用したエンリッチメントされたブラウザコンソールデバッグ
description: この記事では、Charles Proxyを使用してutag.DBからより高度な出力を取得する方法を示します。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/charles-proxy/
---
Charles Proxyに書き換え構成を追加することで、`utag.DB`からの通常のエラーがブラウザレベルのコンソール警告として表示されます。これにより、エラー、警告、情報出力をフィルタリングする際にコンソールの**警告**フィルタを使用できます。

## 前提条件

* お使いのコンピュータに[Charles Proxy Web Debugging Application](https://www.charlesproxy.com/download/)がインストールされていること。
* ブラウザで[utag.DB output](https://docs.tealium.com/ja/platforms/javascript/debugging/)が有効になっていること。

## XMLファイルから書き換えルールを作成する

1. 以下のXMLをコンピュータのファイルとして保存します。  
    
    ```xml
    <?xml version='1.0' encoding='UTF-8' ?>
    <?charles serialisation-version='2.0' ?>
    <rewriteSet-array>
      <rewriteSet>
        <active>true</active>
        <name>uTag DB Upgrade</name>
        <hosts>
          <locationPatterns>
            <locationMatch>
              <location>
                <path>/*/utag.js</path>
              </location>
              <enabled>true</enabled>
            </locationMatch>
          </locationPatterns>
        </hosts>
        <rules>
          <rewriteRule>
            <active>true</active>
            <ruleType>7</ruleType>
            <matchValue>;utag.o[&apos;</matchValue>
            <matchHeaderRegex>false</matchHeaderRegex>
            <matchValueRegex>false</matchValueRegex>
            <matchRequest>false</matchRequest>
            <matchResponse>true</matchResponse>
            <newValue>; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(https://docs.tealium.com/\s([a-zA-Z]+)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == &quot;undefined&quot;) {     utag.db_log = [];     b = document.cookie + &apos;&apos;;     utag.cfg.utagdb = ((b.indexOf(&apos;utagdb=true&apos;) &gt;= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === &quot;error&quot;) {       utag.db_log.push(a);       t = &quot;&quot;;       if (a.stack &amp;&amp; a.stack.split) {         t = a.stack.split(&quot;\n&quot;)[1].replace(https://docs.tealium.com/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, &apos;&apos;).replace(https://docs.tealium.com/^at\s/, &quot;&quot;);       }       if (con) {         t = &quot;utag - Error : &quot; + t + &quot; &quot;+ a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == &quot;object&quot;) ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con &amp;&amp; con.log) con.log(&quot;utag - &quot;, t);     }   } };utag.o[&apos;  </newValue>
            <newHeaderRegex>false</newHeaderRegex>
            <newValueRegex>false</newValueRegex>
            <matchWholeValue>false</matchWholeValue>
            <caseSensitive>false</caseSensitive>
            <replaceType>1</replaceType>
          </rewriteRule>
          <rewriteRule>
            <active>true</active>
            <ruleType>7</ruleType>
            <matchValue>\}catch\((.*?)\)\{</matchValue>
            <matchHeaderRegex>false</matchHeaderRegex>
            <matchValueRegex>false</matchValueRegex>
            <matchRequest>true</matchRequest>
            <matchResponse>false</matchResponse>
            <newValue>}catch($1){utag.DB($1);</newValue>
            <newHeaderRegex>false</newHeaderRegex>
            <newValueRegex>false</newValueRegex>
            <matchWholeValue>false</matchWholeValue>
            <caseSensitive>false</caseSensitive>
            <replaceType>1</replaceType>
          </rewriteRule>
        </rules>
      </rewriteSet>
    </rewriteSet-array>
    ```
    
1. **Charles Rewrite Settings** (**ツール > 書き換え**)を開きます。
1. **インポート**をクリックします（下の画像を参照）。
1. ファイルを選択し、**開く**をクリックします。
1. **適用**と**OK**をクリックしてインポートを完了します。
    ![](https://docs.tealium.com/images/iq-tag-management/charles-utag-db-upgrade.png)

1. Tealiumをロードしているブラウザウィンドウを更新します。これで、コンソールに警告の出力が表示されるようになります。[下のサンプル](https://docs.tealium.com/enhanced-browser-console-debugging-with-charles-proxy/)を参照してください。

## 手動で書き換えルールを作成する

1. Charles Proxyを開きます。
1. メニューから**ツール > 書き換え**に移動します。
1. ダイアログで、左側の**追加**ボタンをクリックして新しいセットを追加します。タイトルは`uTag DB Upgrade`とします。
1. **ロケーション**セクションで、**追加**ボタンをクリックしてロケーションを追加します。
1. 下記のコードを**パス**テキストフィールドにコピー＆ペーストします：
    ```
    /*/utag.js
    ```
1. 他のフィールドは空白のままにし、**OK**をクリックします。
1. **タイプ/アクション**セクションで、**追加**ボタンをクリックして最初の書き換えルールを追加します。
    1. **タイプ**ドロップダウンで**ボディ**を選択します。
    1. **場所**セクションで、**レスポンス**がチェックされていることを確認します。
    1. **マッチ**と**置換**セクションで、下記のコードを対応するテキストフィールドにコピー＆ペーストします。  
      **マッチ**セクションの**値**フィールドに以下を配置します
        ```
        ;utag.o['
        ```
        **置換**セクションの**値**フィールドに以下を配置します：
        ```js
        ; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(https://docs.tealium.com/\s([a-zA-Z]+)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == "undefined") {     utag.db_log = [];     b = document.cookie + '';     utag.cfg.utagdb = ((b.indexOf('utagdb=true') >= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === "error") {       utag.db_log.push(a);       t = "";       if (a.stack && a.stack.split) {         t = a.stack.split("\n")[1].replace(https://docs.tealium.com/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '').replace(https://docs.tealium.com/^at\s/, "");       }       if (con) {         t = "utag - Error : " + t + " "+ a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == "object") ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con && con.log) con.log("utag - ", t);     }   } };utag.o['
        ```
    1. **置換**セクションで、**最初に置換**オプションが選択されていることを確認します。
    1. あなたの**書き換えルール**は次のようになるはずです：  
        ![](https://docs.tealium.com/images/iq-tag-management/screen-shot-2020-11-09-at-9.22.49-am.png)
    1. ルールを保存するために**OK**ボタンをクリックします。

1. **タイプ/アクション**セクションで、**追加**ボタンをクリックして2つ目の書き換えルールを追加します。  
    1. **タイプ**ドロップダウンで**ボディ**を選択します。
    1. **場所**セクションで、**リクエスト**がチェックされていることを確認します。
    1. **マッチ**と**置換**セクションで、下記のコードを対応するテキストフィールドにコピー＆ペーストします。  
        **マッチ**セクションの**値**フィールドに以下を配置します
        ```
        \}catch\((.*?)\)\{
        ```
        **置換**セクションの**値**フィールドに以下を配置します
        ```
        }catch($1){utag.DB($1);
        ```
    1. **マッチ**セクションで、**正規表現**ボックスがチェックされていることを確認します。
    1. **置換**セクションで、**最初に置換**オプションが選択されていることを確認します。
    1. ルールを保存するために**OK**ボタンをクリックします。
    1. あなたの**書き換えルール**は次のようになるはずです：  
        ![](https://docs.tealium.com/images/iq-tag-management/screen-shot-2020-11-09-at-9.03.19-am.png)

1. 完成したときに、2つの書き換えが含まれる`uTag DB Upgrade`セットは次のようになります：
    ![](https://docs.tealium.com/images/iq-tag-management/charlesproxy-utagdbrewrite-full.jpg)

1. 書き換えを適用するために**適用**をクリックし、ダイアログを閉じるために**OK**をクリックします。
1. Tealiumをロードしているブラウザウィンドウを更新します。これで、コンソールに警告の出力が表示されるようになります。下のサンプルを参照してください。

## 出力サンプル

以下は、Google Chrome DevToolsで表示されるエンリッチメントされた出力のサンプルです。**情報**出力として表示されるだけでなく、エラーが展開可能な警告として表示され、**フィルタ**入力ボックスの隣のドロップダウンで**警告**オプションを選択することでフィルタリングできます。

![](https://docs.tealium.com/images/iq-tag-management/screen-shot-2020-11-09-at-9.07.27-am.png)
