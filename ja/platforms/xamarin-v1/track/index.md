---
title: トラッキング
description: ユーザー活動を追跡する方法について学びます。
url: https://docs.tealium.com/ja/platforms/xamarin-v1/track/
---現在のバージョンについては、[Tealium for Xamarin 2.x](/ja/platforms/xamarin/)をご覧ください。

## ビューのトラッキング

`TrackView()` メソッドはページビューを追跡するために使用されます。以下の例を参照してください：

まず、tealiumインスタンスを取得します：

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```

タイトルのみでページビューイベントを追跡します：  
```csharp
tealium.TrackView(&#34;SCREEN_NAME&#34;);
```

タイトルとページタイプでページビューイベントを追跡します。  
```csharp
tealium.TrackView(&#34;SCREEN_NAME&#34;, new Dictionary&lt;String, object&gt;(1){ {&#34;PAGE_TYPE&#34;, &#34;product detail page&#34;} });
```

タイトルとページタイプ、そしてイベントデータ1つを含むページビューイベントを追跡します（前の例と同等）：  
```csharp
tealium.TrackView(&#34;SCREEN_NAME&#34;, &#34;PAGE_TYPE&#34;, &#34;product detail page&#34;);
```

## イベントのトラッキング

`TrackEvent()` メソッドはビュー以外のイベントを追跡するために使用されます。以下の例は、3つの特定のイベントデータを持つイベントを追跡する方法を示しています：

まず、tealiumインスタンスを取得します：

```csharp
ITealium tealium = instanceManager.GetExistingInstance(TealiumConsts.INSTANCE_ID);
```
```csharp
tealium.TrackEvent(&#34;Event Name&#34;, new Dictionary&lt;String, object&gt;(3){
    {&#34;event_category&#34;, &#34;EVENT_CATEGORY&#34;},
    {&#34;event_action&#34;, &#34;EVENT_NAME&#34;},
    {&#34;event_label&#34;, &#34;EVENT_LABEL&#34;}});
```