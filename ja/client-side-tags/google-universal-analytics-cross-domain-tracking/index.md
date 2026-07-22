---
title: Google Universal Analytics クロスドメイン トラッキングの構成
description: クロスドメイン トラッキングは、ユーザーのセッションを別々のドメインで追跡し、ユーザーの行動の完全なビューを作成する能力です。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-cross-domain-tracking/
---

<blockquote>
2023年7月1日より、Google Universal Analytics プロパティはヒットの処理を停止しました。このタグは非推奨となり、タグマーケットプレイスではもはや利用できません。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)をご覧ください。
</blockquote>


たとえば、`www.example.com` と `www.another-domain.com` のように相互にリンクしている2つのドメインがある場合、Google Universal Analytics はデフォルトで、両方のプロパティを訪れた1人のユーザーを2人の別々のユーザーとして、2つの別々のセッションとしてカウントします。クロスドメイン トラッキングを有効にすることで、ユーザーは両ドメイン間で1人のユーザーとして表されます。

----

### タグ構成

Google Universal Analytics は、複数のサブドメインを跨いで追跡するように既に有効になっています。例えば：`test.example.com`、`example.com`、`store.example.com`。特定のサブドメインを追跡する場合は、**ドメイン** フィールドにそれらを入力してください。

![](https://docs.tealium.com/images/client-side-tags/domain.png)

### クロスドメイン構成

1. Google Universal Analytics タグ構成で、**クロスドメイン トラッキング** ドロップダウンを **オン** に切り替えます。
1. **クロストラッキング ドメイン** フィールドに、クロスドメイン トラッキングを有効にしたいドメインのカンマ区切りリストを追加します。
    
<blockquote>
カンマの後にスペースを入れないでください。
</blockquote>

    ![](https://docs.tealium.com/images/client-side-tags/no-title-998i432684d23a47f981.png)

1. 変更を保存して公開します。

### 検証

ドメインが正しくユーザーを追跡していることを確認するために、あなたのドメインの1つにアクセスし、2番目のドメインに移動するリンクをクリックします。URLに `_ga=` と長い数字の文字列が追加されているのが見えるはずです。

以下のスクリーンショットでは、`www.example.com` にナビゲートし、`www.another-domain.com` に移動するリンクをクリックしました。URLに `_ga` トラッキングコードが追加されていることに注意してください：

![](https://docs.tealium.com/images/client-side-tags/no-title-1001ia419155f039f6c22.png)

これにより、ブラウザから期待通りにクロスドメイン トラッキングが機能していることが確認されます。