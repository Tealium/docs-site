---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/xamarin/track/
---
## 画面ビューの追跡

画面ビューを追跡するには、`TealiumView(tealiumEvent:new Dictionary&lt;string, object&gt;:)` のインスタンスを [`track()`](/ja/platforms/xamarin/api/#track) メソッドに渡します。`TealiumView` はビュー名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

```csharp
tealium.Track(new TealiumView(&#34;purchase&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; },
    { &#34;order_total&#34;, 10.00 },
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;order_id&#34;, &#34;0123456789&#34; }
}));
```

## イベントの追跡

ビュー以外のイベントを追跡するには、`TealiumEvent(tealiumEvent:new Dictionary&lt;string, object&gt;:)` のインスタンスを [`track()`](/ja/platforms/xamarin/api/#track) メソッドに渡します。`TealiumEvent` はイベント名を含み、追跡呼び出しで `tealium_event` として表示され、オプションのデータ辞書があります。

```csharp
tealium.Track(new TealiumEvent(&#34;cart_add&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; }, 
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;product_price&#34;, new[] {4.00, 6.00} }
}));
```