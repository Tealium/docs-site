---
title: ActOnタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでActOnタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/acton-tag/
---
## ウェブサイト

[www.act-on.com](https://www.act-on.com)

## サンプルコードスニペット

```javascript
<script type="text/javascript">
    /* <![CDATA[ */
    document.write (
        '<img src="http://www.tealium.com/acton/bn/1234/visitor.gif?ts='+new Date().getTime()+'&ref='+escape(document.referrer) + '">'
    );
    /* ]]> */
 </script> 
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
