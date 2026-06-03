---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/angular/track/
---
`TealiumUtagService`が初期化されたら、アプリケーションコード全体に追跡呼び出しを追加します。

## ビューの追跡

[`view()`](/ja/platforms/angular/api/#view) メソッドはページビューを追跡します。このメソッドは、以下の例に示すように、キーと値のペアのオブジェクトを単一のパラメータとして取ります：

```javascript
this.tealium.view({
    &#34;tealium_event&#34;  : &#34;SCREEN_NAME&#34;,
    &#34;page_type&#34;      : &#34;PAGE_TYPE&#34;,
    &#34;product_id&#34;     : [&#34;PRODUCT_ID&#34;]});
```
## イベントの追跡

[`link()`](/ja/platforms/angular/api/#link) メソッドはページ内イベントを追跡します。このメソッドは、以下の例に示すように、キーと値のペアのオブジェクトを単一のパラメータとして取ります：

```javascript
this.tealium.link({
    &#34;tealium_event&#34; : &#34;EVENT_NAME&#34;,
    &#34;customer_id&#34;   : &#34;CUSTOMER_ID&#34;});
```
