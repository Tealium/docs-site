---
title: Track
description: Learn about the methods for tracking game activity.
url: https://docs.tealium.com/platforms/unity-v1/track/
---

<blockquote>
This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](https://docs.tealium.com/platforms/unity/).
</blockquote>


## Track View

To track a view in a game, call the [`TrackView()`](https://docs.tealium.com/platforms/unity/api/#trackview) method:

```csharp
Dictionary<string, string> data = new Dictionary<string, string>() {
    {"user_id", "gamer123"},
    {"level": 2},
    {"total_points": 17500}};

Tealium.TrackView("level_completed_screen", data);
```


## Track Event

To track a user's interaction with a game, such as `achievement_unlocked` or `level_started`, call the [`TrackEvent()`](https://docs.tealium.com/platforms/unity/api/#trackevent) method.

```csharp
Dictionary<string, string> data = new Dictionary<string, string>() {
    {"user_id", "gamer123"},
    {"level": 2},
    {"bonus_points": 1500}};

Tealium.TrackView("level_completed", data);
```
