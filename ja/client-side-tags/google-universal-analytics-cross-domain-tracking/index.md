---
title: Google Universal Analyticsのクロスドメイントラッキングの構成
description: クロスドメイントラッキングとは、複数の異なるドメインにまたがってユーザーのセッションを追跡し、ユーザーの行動を完全に把握できる機能です。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-cross-domain-tracking/
---

<blockquote>
2023年7月1日をもって、Google Universal Analyticsプロパティではヒットの処理が停止されました。このタグは非推奨となり、タグマーケットプレイスでは利用できなくなりました。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)を参照してください。
</blockquote>


たとえば、`www.example.com`と`www.another-domain.com`という相互にリンクされた2つのドメインがある場合、Google Universal Analyticsはデフォルトでは、両方のプロパティにアクセスした1人のユーザーを、それぞれ個別のセッションを持つ2人のユーザーとしてカウントします。クロスドメイントラッキングを有効にすると、両方のドメイン間で同一のユーザーとして扱われます。

----

### タグの構成

Google Universal Analyticsでは、複数のサブドメインにまたがるトラッキングがすでに有効になっています。例：`test.example.com`、`example.com`、`store.example.com`。トラッキングする特定のサブドメインがある場合は、**Domain**フィールドに入力します。

![](https://docs.tealium.com/images/client-side-tags/domain.png)

### クロスドメイン構成

1. Google Universal Analyticsタグの構成で、**Cross-Domain Tracking**ドロップダウンを**On**に切り替えます。
1. **Cross-Tracking Domains**フィールドに、クロスドメイントラッキングを有効にするドメインをカンマ区切りのリストで追加します。   
    
<blockquote>
カンマの後にスペースを挿入しないでください。
</blockquote>

    ![](https://docs.tealium.com/images/client-side-tags/no-title-998i432684d23a47f981.png)

1. 変更を保存して公開します。

### 検証

ドメイン間でユーザーが正しく追跡されていることを確認するには、いずれかのドメインに移動し、2つ目のドメインに移動するリンクをクリックします。URLにGoogle Universal AnalyticsのCookie値が追加され、`_ga=`の後に長い数字列が表示されます。

以下のスクリーンショットでは、`www.example.com`に移動し、`www.another-domain.com`へのリンクをクリックしています。`_ga`トラッキングコードがURLに含まれていることに注目してください。

![](https://docs.tealium.com/images/client-side-tags/no-title-1001ia419155f039f6c22.png)

これにより、ブラウザー上でクロスドメイントラッキングが期待どおりに機能していることを確認できます。