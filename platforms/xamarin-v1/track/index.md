---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/xamarin-v1/track/
---
<blockquote>
For the current version, see [Tealium for Xamarin 2.x](https://docs.tealium.com/platforms/xamarin/).
</blockquote>


## Track Views

The `TrackView()` method is used to track page views, as shown in the following examples:

First, get a tealium instance:

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```

Track page view event by title only:  
```csharp
tealium.TrackView("SCREEN_NAME");
```

Track a page View event with the title and page type.  
```csharp
tealium.TrackView("SCREEN_NAME", new Dictionary<String, object>(1){ {"PAGE_TYPE", "product detail page"} });
```


Track a page view event with the title and page type, along with a single piece of event data (equivalent to the prior example):  
```csharp
tealium.TrackView("SCREEN_NAME", "PAGE_TYPE", "product detail page");
```

## Track Events

The `TrackEvent()` method is used to track non-view events. The following example demonstrates how to track an event with 3 pieces of specific event data:

First, get a tealium instance:

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```
```csharp
tealium.TrackEvent("Event Name", new Dictionary<String, object>(3){
    {"event_category", "EVENT_CATEGORY"},
    {"event_action", "EVENT_NAME"},
    {"event_label", "EVENT_LABEL"}});
```
