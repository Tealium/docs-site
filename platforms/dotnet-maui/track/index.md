---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/dotnet-maui/track/
---
## Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent:new Dictionary<string, object>:)` to the [`track()`](https://docs.tealium.com/platforms/dotnet-maui/api/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumView("purchase", new Dictionary<string, object> {
    { "customer_id", "abc123" },
    { "order_total", 10.00 },
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "order_id", "0123456789" }
}));
```

## Track Events

To track non-view events, pass an instance of `TealiumEvent(tealiumEvent:new Dictionary<string, object>:)` to the [`track()`](https://docs.tealium.com/platforms/dotnet-maui/api/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "product_price", new[] {4.00, 6.00} }
}));
```