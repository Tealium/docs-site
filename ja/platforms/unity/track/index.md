---
title: トラック
description: ゲーム活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/unity/track/
---

## ゲームイベントの追跡

ユーザーのゲームとのやり取り、例えば `achievement_unlocked` や `level_started` を追跡するには、[`TealiumEvent`](https://docs.tealium.com/ja/platforms/unity/api/#class-tealiumevent) オブジェクトを作成し、それを [`Track()`](https://docs.tealium.com/ja/platforms/unity/api/#track) メソッドに渡します。`TealiumEvent` はイベント名と、オプションのデータ辞書で構成され、追跡呼び出しでは `tealium_event` として表示されます。

```javascript
TealiumEvent event = TealiumEvent("level_completed",
    new Dictionary<string, object> {
        {"user_id", "gamer123"},
        {"level": 2},
        {"bonus_points": 1500}});
TealiumUnityPlugin.Track(event);
```

## ゲームビューの追跡

ゲーム内のビュー、例えばリーダーボード画面を追跡するには、[`TealiumView`](https://docs.tealium.com/ja/platforms/unity/api/#class-tealiumview) オブジェクトを作成し、それを [`Track()`](https://docs.tealium.com/ja/platforms/unity/api/#track) メソッドに渡します。`TealiumView` はビュー名と、オプションのデータ辞書で構成され、追跡呼び出しでは `tealium_event` として表示されます。

```javascript
TealiumView view = new TealiumView("level_completed_screen",
    new Dictionary<string, object> {
        {"user_id", "gamer123"},
        {"level": 2},
        {"total_points": 17500}});
TealiumUnityPlugin.Track(view);
```
