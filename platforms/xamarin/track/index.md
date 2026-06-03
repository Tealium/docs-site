---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/xamarin/track/
---
## Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent:new Dictionary&lt;string, object&gt;:)` to the [`track()`](/platforms/xamarin/api/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumView(&#34;purchase&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; },
    { &#34;order_total&#34;, 10.00 },
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;order_id&#34;, &#34;0123456789&#34; }
}));
```

## Track Events

To track non-view events, pass an instance of `TealiumEvent(tealiumEvent:new Dictionary&lt;string, object&gt;:)` to the [`track()`](/platforms/xamarin/api/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumEvent(&#34;cart_add&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; }, 
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;product_price&#34;, new[] {4.00, 6.00} }
}));
```