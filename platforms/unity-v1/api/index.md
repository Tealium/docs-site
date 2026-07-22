---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Unity 1.x.
url: https://docs.tealium.com/platforms/unity-v1/api/
---

<blockquote>
This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](https://docs.tealium.com/platforms/unity/).
</blockquote>


## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for Unity library.

| Method         | Description                                                |
|:---------------|:-----------------------------------------------------------|
| `TrackEvent()` | Track game events with optional parameters for event data. |
| `TrackView()`  | Track game views with optional parameters for view data.   |

### `TrackEvent()`

Track a user's interaction with a game.

```csharp
Tealium.TrackEvent(event, data);
```

| Parameters | Type         | Description                                                                             | Example Value                                                   |
|:-----------|:-------------|:----------------------------------------------------------------------------------------|:----------------------------------------------------------------|
| `event`    | `String`     | The current game event, which populates the `tealium_event` variable in the data layer. | `game_started`                                                  |
| `data`     | `Dictionary` | (Optional) Data pertaining to the event.                                                | `new Dictionary < string, string > ( ) { {"weapon", "sword"} }` |


### `TrackView()`

Track game view activity.

```csharp
Tealium.TrackView(title, data);
```

| Parameters | Type         | Description                                                                               | Example Value                                            |
|:-----------|:-------------|:------------------------------------------------------------------------------------------|:---------------------------------------------------------|
| `title`    | `String`     | The current screen title, which populates the `tealium_event` variable in the data layer. | `level_1`                                                |
| `data`     | `Dictionary` | (Optional) Data pertaining to the screen.                                                 | `new Dictionary < string, int > ( ) { {"score", 1575} }` |
