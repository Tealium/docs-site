---
title: トラッキング
description: ゲームアクティビティの追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/unity-v1/track/
---

<blockquote>
これはTealium for Unityの以前のバージョン（1.x）です。現行バージョンは[Tealium for Unity 2.x](https://docs.tealium.com/ja/platforms/unity/)を参照してください。
</blockquote>


## トラックビュー

ゲーム内でビューをトラッキングするには、[`TrackView()`](https://docs.tealium.com/ja/platforms/unity/api/#trackview)メソッドを呼び出します：

```csharp
Dictionary<string, string> data = new Dictionary<string, string>() {
    {"user_id", "gamer123"},
    {"level", 2},
    {"total_points", 17500}};

Tealium.TrackView("level_completed_screen", data);
```

## トラックイベント

ゲーム内でのユーザーのインタラクション、例えば `achievement_unlocked` や `level_started` をトラッキングするには、[`TrackEvent()`](https://docs.tealium.com/ja/platforms/unity/api/#trackevent) メソッドを呼び出します。

```csharp
Dictionary<string, string> data = new Dictionary<string, string>() {
    {"user_id", "gamer123"},
    {"level", 2},
    {"bonus_points", 1500}};

Tealium.TrackView("level_completed", data);
```