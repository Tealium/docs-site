---
title: ActOnタグ構成ガイド
description: この記事では、タグ管理アカウントでActOnタグを構成する方法について説明します。
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

## タグ管理の構成

ActOnタグでは、ほとんど構成は必要ありません。

1. 「Tags」タブに移動し、**Add Tag**をクリックします。
1. **Act On**を検索します。
1. **Add**ボタンをクリックして、ActOnタグを追加します。
1. **Tag Configuration Wizard**で、新しいAct Onタグに分かりやすいタイトルを付けます。
1. アカウントIDを入力します。
1. パス（アカウントIDにつながるURLパス。例：`http:www/tealium.com/acton/bn/1234/visitor.gif?`）を入力します。
1. **Next**をクリックしてタグに特定のロードルールを割り当てるか、**Finish**をクリックしてこのタグにデフォルトのロードルールを適用します。