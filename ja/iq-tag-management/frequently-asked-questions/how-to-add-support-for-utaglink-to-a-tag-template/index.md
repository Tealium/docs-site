---
title: タグテンプレートにutag.linkのサポートを追加する方法
description: この記事では、タグテンプレートにutag.linkのサポートを追加する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/frequently-asked-questions/how-to-add-support-for-utaglink-to-a-tag-template/
---## 症状

タグはutag.view（ページビュー）イベントで発火していますが、utag.link（ユーザーインタラクション/クリック）イベントには反応していません。

## 診断

各タグテンプレートはデフォルトで以下のいずれかに対応するように構成されています：

* utag.view
* utag.view と utag.link

通常、これはタグベンダーが提供した実装ガイドに基づいていますので、ベンダーがページビュー用のコードのみを指定している場合、テンプレートにはutag.viewのサポートのみが存在します。

## 解決策

デフォルトでutag.viewのみをサポートしているタグにutag.linkサポートを追加したい場合があります。始めるには、タグテンプレートを編集する方法についてのこのドキュメントに従ってください：[タグテンプレートを編集する]()。

テンプレートを編集している間、次のように始まる行を探します：

```js
u.ev= {&#39;view&#39;: 1};
```

![](/images/iq-tag-management/viewonly.png)

この行を次のように編集します：

```js
u.ev = {&#39;view&#39; : 1, &#39;link&#39;: 1};
```

![](/images/iq-tag-management/view-link.png)

タグテンプレートを保存し、プロファイルを再公開します。これで、あなたのタグはutag.viewとutag.linkの両方のイベントに対応するようになります。