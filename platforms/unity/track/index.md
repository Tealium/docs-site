---
title: Track
description: Learn about the methods for tracking game activity.
url: https://docs.tealium.com/platforms/unity/track/
---

## Track Game Events

To track a user&#39;s interaction with a game, such as `achievement_unlocked` or `level_started`, create a [`TealiumEvent`](/platforms/unity/api/#class-tealiumevent) object and pass it to the [`Track()`](/platforms/unity/api/#track) method. `TealiumEvent` is comprised of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
TealiumEvent event = TealiumEvent(&#34;level_completed&#34;,
    new Dictionary&lt;string, object&gt; {
        {&#34;user_id&#34;, &#34;gamer123&#34;},
        {&#34;level&#34;: 2},
        {&#34;bonus_points&#34;: 1500}});
TealiumUnityPlugin.Track(event);
```

## Track Game Views

To track a view in a game, such as the leaderboards screen, create a [`TealiumView`](/platforms/unity/api/#class-tealiumview) object and pass it to the [`Track()`](/platforms/unity/api/#track) method. `TealiumView` is comprised of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
TealiumView view = new TealiumView(&#34;level_completed_screen&#34;,
    new Dictionary&lt;string, object&gt; {
        {&#34;user_id&#34;, &#34;gamer123&#34;},
        {&#34;level&#34;: 2},
        {&#34;total_points&#34;: 17500}});
TealiumUnityPlugin.Track(view);
```
