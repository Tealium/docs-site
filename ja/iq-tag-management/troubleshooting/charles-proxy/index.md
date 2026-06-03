---
title: Charles Proxyを使用したエンリッチメントされたブラウザコンソールデバッグ
description: この記事では、Charles Proxyを使用してutag.DBからより高度な出力を取得する方法を示します。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/charles-proxy/
---
Charles Proxyに書き換え構成を追加することで、`utag.DB`からの通常のエラーがブラウザレベルのコンソール警告として表示されます。これにより、エラー、警告、情報出力をフィルタリングする際にコンソールの**警告**フィルタを使用できます。

## 前提条件

* お使いのコンピュータに[Charles Proxy Web Debugging Application](https://www.charlesproxy.com/download/)がインストールされていること。
* ブラウザで[utag.DB output](/ja/platforms/javascript/debugging/)が有効になっていること。

## XMLファイルから書き換えルールを作成する

1. 以下のXMLをコンピュータのファイルとして保存します。  
    
    ```xml
    &lt;?xml version=&#39;1.0&#39; encoding=&#39;UTF-8&#39; ?&gt;
    &lt;?charles serialisation-version=&#39;2.0&#39; ?&gt;
    &lt;rewriteSet-array&gt;
      &lt;rewriteSet&gt;
        &lt;active&gt;true&lt;/active&gt;
        &lt;name&gt;uTag DB Upgrade&lt;/name&gt;
        &lt;hosts&gt;
          &lt;locationPatterns&gt;
            &lt;locationMatch&gt;
              &lt;location&gt;
                &lt;path&gt;/*/utag.js&lt;/path&gt;
              &lt;/location&gt;
              &lt;enabled&gt;true&lt;/enabled&gt;
            &lt;/locationMatch&gt;
          &lt;/locationPatterns&gt;
        &lt;/hosts&gt;
        &lt;rules&gt;
          &lt;rewriteRule&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;ruleType&gt;7&lt;/ruleType&gt;
            &lt;matchValue&gt;;utag.o[&amp;apos;&lt;/matchValue&gt;
            &lt;matchHeaderRegex&gt;false&lt;/matchHeaderRegex&gt;
            &lt;matchValueRegex&gt;false&lt;/matchValueRegex&gt;
            &lt;matchRequest&gt;false&lt;/matchRequest&gt;
            &lt;matchResponse&gt;true&lt;/matchResponse&gt;
            &lt;newValue&gt;; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(/\s([a-zA-Z]&#43;)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == &amp;quot;undefined&amp;quot;) {     utag.db_log = [];     b = document.cookie &#43; &amp;apos;&amp;apos;;     utag.cfg.utagdb = ((b.indexOf(&amp;apos;utagdb=true&amp;apos;) &amp;gt;= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === &amp;quot;error&amp;quot;) {       utag.db_log.push(a);       t = &amp;quot;&amp;quot;;       if (a.stack &amp;amp;&amp;amp; a.stack.split) {         t = a.stack.split(&amp;quot;\n&amp;quot;)[1].replace(/^[\s\uFEFF\xA0]&#43;|[\s\uFEFF\xA0]&#43;$/g, &amp;apos;&amp;apos;).replace(/^at\s/, &amp;quot;&amp;quot;);       }       if (con) {         t = &amp;quot;utag - Error : &amp;quot; &#43; t &#43; &amp;quot; &amp;quot;&#43; a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == &amp;quot;object&amp;quot;) ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con &amp;amp;&amp;amp; con.log) con.log(&amp;quot;utag - &amp;quot;, t);     }   } };utag.o[&amp;apos;  &lt;/newValue&gt;
            &lt;newHeaderRegex&gt;false&lt;/newHeaderRegex&gt;
            &lt;newValueRegex&gt;false&lt;/newValueRegex&gt;
            &lt;matchWholeValue&gt;false&lt;/matchWholeValue&gt;
            &lt;caseSensitive&gt;false&lt;/caseSensitive&gt;
            &lt;replaceType&gt;1&lt;/replaceType&gt;
          &lt;/rewriteRule&gt;
          &lt;rewriteRule&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;ruleType&gt;7&lt;/ruleType&gt;
            &lt;matchValue&gt;\}catch\((.*?)\)\{&lt;/matchValue&gt;
            &lt;matchHeaderRegex&gt;false&lt;/matchHeaderRegex&gt;
            &lt;matchValueRegex&gt;false&lt;/matchValueRegex&gt;
            &lt;matchRequest&gt;true&lt;/matchRequest&gt;
            &lt;matchResponse&gt;false&lt;/matchResponse&gt;
            &lt;newValue&gt;}catch($1){utag.DB($1);&lt;/newValue&gt;
            &lt;newHeaderRegex&gt;false&lt;/newHeaderRegex&gt;
            &lt;newValueRegex&gt;false&lt;/newValueRegex&gt;
            &lt;matchWholeValue&gt;false&lt;/matchWholeValue&gt;
            &lt;caseSensitive&gt;false&lt;/caseSensitive&gt;
            &lt;replaceType&gt;1&lt;/replaceType&gt;
          &lt;/rewriteRule&gt;
        &lt;/rules&gt;
      &lt;/rewriteSet&gt;
    &lt;/rewriteSet-array&gt;
    ```
    
1. **Charles Rewrite Settings** (**ツール &gt; 書き換え**)を開きます。
1. **インポート**をクリックします（下の画像を参照）。
1. ファイルを選択し、**開く**をクリックします。
1. **適用**と**OK**をクリックしてインポートを完了します。
    ![](/images/iq-tag-management/charles-utag-db-upgrade.png)

1. Tealiumをロードしているブラウザウィンドウを更新します。これで、コンソールに警告の出力が表示されるようになります。[下のサンプル]()を参照してください。

## 手動で書き換えルールを作成する

1. Charles Proxyを開きます。
1. メニューから**ツール &gt; 書き換え**に移動します。
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
        ;utag.o[&#39;
        ```
        **置換**セクションの**値**フィールドに以下を配置します：
        ```js
        ; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(/\s([a-zA-Z]&#43;)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == &#34;undefined&#34;) {     utag.db_log = [];     b = document.cookie &#43; &#39;&#39;;     utag.cfg.utagdb = ((b.indexOf(&#39;utagdb=true&#39;) &gt;= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === &#34;error&#34;) {       utag.db_log.push(a);       t = &#34;&#34;;       if (a.stack &amp;&amp; a.stack.split) {         t = a.stack.split(&#34;\n&#34;)[1].replace(/^[\s\uFEFF\xA0]&#43;|[\s\uFEFF\xA0]&#43;$/g, &#39;&#39;).replace(/^at\s/, &#34;&#34;);       }       if (con) {         t = &#34;utag - Error : &#34; &#43; t &#43; &#34; &#34;&#43; a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == &#34;object&#34;) ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con &amp;&amp; con.log) con.log(&#34;utag - &#34;, t);     }   } };utag.o[&#39;
        ```
    1. **置換**セクションで、**最初に置換**オプションが選択されていることを確認します。
    1. あなたの**書き換えルール**は次のようになるはずです：  
        ![](/images/iq-tag-management/screen-shot-2020-11-09-at-9.22.49-am.png)
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
        ![](/images/iq-tag-management/screen-shot-2020-11-09-at-9.03.19-am.png)

1. 完成したときに、2つの書き換えが含まれる`uTag DB Upgrade`セットは次のようになります：
    ![](/images/iq-tag-management/charlesproxy-utagdbrewrite-full.jpg)

1. 書き換えを適用するために**適用**をクリックし、ダイアログを閉じるために**OK**をクリックします。
1. Tealiumをロードしているブラウザウィンドウを更新します。これで、コンソールに警告の出力が表示されるようになります。下のサンプルを参照してください。

## 出力サンプル

以下は、Google Chrome DevToolsで表示されるエンリッチメントされた出力のサンプルです。**情報**出力として表示されるだけでなく、エラーが展開可能な警告として表示され、**フィルタ**入力ボックスの隣のドロップダウンで**警告**オプションを選択することでフィルタリングできます。

![](/images/iq-tag-management/screen-shot-2020-11-09-at-9.07.27-am.png)
