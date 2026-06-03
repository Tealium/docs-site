---
title: ActOnタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでActOnタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/acton-tag/
---
## ウェブサイト

[www.act-on.com](https://www.act-on.com)

## サンプルコードスニペット

```javascript
&lt;script type=&#34;text/javascript&#34;&gt;
    /* &lt;![CDATA[ */
    document.write (
        &#39;&lt;img src=&#34;http://www.tealium.com/acton/bn/1234/visitor.gif?ts=&#39;&#43;new Date().getTime()&#43;&#39;&amp;ref=&#39;&#43;escape(document.referrer) &#43; &#39;&#34;&gt;&#39;
    );
    /* ]]&gt; */
 &lt;/script&gt; 
```

## Tealium iQ構成

ActOnタグの構成はほとんど必要ありません。

1. タグタブに移動し、**タグを追加**をクリックします。
1. **Act On**を検索します。
1. **追加**ボタンをクリックしてActOnタグを追加します。
1. **タグ構成ウィザード**で、新しいAct Onタグに意味のあるタイトルを付けます。
1. アカウントIDを入力します。
1. パスを入力します（例えば、`http:www/tealium.com/acton/bn/1234/visitor.gif?`のように、アカウントIDに至るURLパス）。
1. **次へ**をクリックしてタグに特定のロードルールを割り当てるか、**完了**をクリックしてこのタグにデフォルトのロードルールを適用します。
