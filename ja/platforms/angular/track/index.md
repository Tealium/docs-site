---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/angular/track/
---
`TealiumUtagService`が初期化されたら、アプリケーションコード全体に追跡呼び出しを追加します。

## ビューの追跡

[`view()`](https://docs.tealium.com/ja/platforms/angular/api/#view) メソッドはページビューを追跡します。このメソッドは、以下の例に示すように、キーと値のペアのオブジェクトを単一のパラメータとして取ります：

```javascript
this.tealium.view({
    "tealium_event"  : "SCREEN_NAME",
    "page_type"      : "PAGE_TYPE",
    "product_id"     : ["PRODUCT_ID"]});
```
## イベントの追跡

[`link()`](https://docs.tealium.com/ja/platforms/angular/api/#link) メソッドはページ内イベントを追跡します。このメソッドは、以下の例に示すように、キーと値のペアのオブジェクトを単一のパラメータとして取ります：

```javascript
this.tealium.link({
    "tealium_event" : "EVENT_NAME",
    "customer_id"   : "CUSTOMER_ID"});
```
