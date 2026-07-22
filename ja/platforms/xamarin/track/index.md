---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/xamarin/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView(tealiumEvent:new Dictionary<string, object>:)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/xamarin/api/#track) メソッドに渡します。`TealiumView` はビュー名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

```csharp
tealium.Track(new TealiumView("purchase", new Dictionary<string, object> {
    { "customer_id", "abc123" },
    { "order_total", 10.00 },
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "order_id", "0123456789" }
}));
```

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent(tealiumEvent:new Dictionary<string, object>:)` のインスタンスを [`track()`](https://docs.tealium.com/ja/platforms/xamarin/api/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "product_price", new[] {4.00, 6.00} }
}));
```