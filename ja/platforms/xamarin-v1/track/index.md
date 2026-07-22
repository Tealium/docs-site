---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/xamarin-v1/track/
---
<blockquote>
現在のバージョンについては、[Tealium for Xamarin 2.x](https://docs.tealium.com/ja/platforms/xamarin/)をご覧ください。
</blockquote>


## ビューのトラッキング

`TrackView()` メソッドはページビューを追跡するために使用されます。以下の例を参照してください：

まず、tealiumインスタンスを取得します：

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```

タイトルのみでページビューイベントを追跡します：  
```csharp
tealium.TrackView("SCREEN_NAME");
```

タイトルとページタイプでページビューイベントを追跡します。  
```csharp
tealium.TrackView("SCREEN_NAME", new Dictionary<String, object>(1){ {"PAGE_TYPE", "product detail page"} });
```

タイトルとページタイプ、そしてイベントデータ1つを含むページビューイベントを追跡します（前の例と同等）：  
```csharp
tealium.TrackView("SCREEN_NAME", "PAGE_TYPE", "product detail page");
```

## イベントのトラッキング

`TrackEvent()` メソッドはビュー以外のイベントを追跡するために使用されます。以下の例は、3つの特定のイベントデータを持つイベントを追跡する方法を示しています：

まず、tealiumインスタンスを取得します：

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```
```csharp
tealium.TrackEvent("Event Name", new Dictionary<String, object>(3){
    {"event_category", "EVENT_CATEGORY"},
    {"event_action", "EVENT_NAME"},
    {"event_label", "EVENT_LABEL"}});
```