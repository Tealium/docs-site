---
title: Track
description: Learn about the methods for tracking game activity.
url: https://docs.tealium.com/platforms/unity/track/
---

## Track Game Events

To track a user's interaction with a game, such as `achievement_unlocked` or `level_started`, create a [`TealiumEvent`](https://docs.tealium.com/platforms/unity/api/#class-tealiumevent) object and pass it to the [`Track()`](https://docs.tealium.com/platforms/unity/api/#track) method. `TealiumEvent` is comprised of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
TealiumEvent event = TealiumEvent("level_completed",
    new Dictionary<string, object> {
        {"user_id", "gamer123"},
        {"level": 2},
        {"bonus_points": 1500}});
TealiumUnityPlugin.Track(event);
```

## Track Game Views

To track a view in a game, such as the leaderboards screen, create a [`TealiumView`](https://docs.tealium.com/platforms/unity/api/#class-tealiumview) object and pass it to the [`Track()`](https://docs.tealium.com/platforms/unity/api/#track) method. `TealiumView` is comprised of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
TealiumView view = new TealiumView("level_completed_screen",
    new Dictionary<string, object> {
        {"user_id", "gamer123"},
        {"level": 2},
        {"total_points": 17500}});
TealiumUnityPlugin.Track(view);
```
