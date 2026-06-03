---
title: Track
description: Learn about the methods for tracking game activity.
url: https://docs.tealium.com/platforms/unity-v1/track/
---
This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](/platforms/unity/).

## Track View

To track a view in a game, call the [`TrackView()`](/platforms/unity/api/#trackview) method:

```csharp
Dictionary&lt;string, string&gt; data = new Dictionary&lt;string, string&gt;() {
    {&#34;user_id&#34;, &#34;gamer123&#34;},
    {&#34;level&#34;: 2},
    {&#34;total_points&#34;: 17500}};

Tealium.TrackView(&#34;level_completed_screen&#34;, data);
```


## Track Event

To track a user&#39;s interaction with a game, such as `achievement_unlocked` or `level_started`, call the [`TrackEvent()`](/platforms/unity/api/#trackevent) method.

```csharp
Dictionary&lt;string, string&gt; data = new Dictionary&lt;string, string&gt;() {
    {&#34;user_id&#34;, &#34;gamer123&#34;},
    {&#34;level&#34;: 2},
    {&#34;bonus_points&#34;: 1500}};

Tealium.TrackView(&#34;level_completed&#34;, data);
```
