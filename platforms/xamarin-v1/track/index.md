---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/xamarin-v1/track/
---For the current version, see [Tealium for Xamarin 2.x](/platforms/xamarin/).

## Track Views

The `TrackView()` method is used to track page views, as shown in the following examples:

First, get a tealium instance:

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```

Track page view event by title only:  
```csharp
tealium.TrackView(&#34;SCREEN_NAME&#34;);
```

Track a page View event with the title and page type.  
```csharp
tealium.TrackView(&#34;SCREEN_NAME&#34;, new Dictionary&lt;String, object&gt;(1){ {&#34;PAGE_TYPE&#34;, &#34;product detail page&#34;} });
```


Track a page view event with the title and page type, along with a single piece of event data (equivalent to the prior example):  
```csharp
tealium.TrackView(&#34;SCREEN_NAME&#34;, &#34;PAGE_TYPE&#34;, &#34;product detail page&#34;);
```

## Track Events

The `TrackEvent()` method is used to track non-view events. The following example demonstrates how to track an event with 3 pieces of specific event data:

First, get a tealium instance:

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```
```csharp
tealium.TrackEvent(&#34;Event Name&#34;, new Dictionary&lt;String, object&gt;(3){
    {&#34;event_category&#34;, &#34;EVENT_CATEGORY&#34;},
    {&#34;event_action&#34;, &#34;EVENT_NAME&#34;},
    {&#34;event_label&#34;, &#34;EVENT_LABEL&#34;}});
```
