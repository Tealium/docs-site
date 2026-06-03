---
title: トラッキング
description: ゲームアクティビティの追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/unity-v1/track/
---
これはTealium for Unityの以前のバージョン（1.x）です。現行バージョンは[Tealium for Unity 2.x](/ja/platforms/unity/)を参照してください。

## トラックビュー

ゲーム内でビューをトラッキングするには、[`TrackView()`](/ja/platforms/unity/api/#trackview)メソッドを呼び出します：

```csharp
Dictionary&lt;string, string&gt; data = new Dictionary&lt;string, string&gt;() {
    {&#34;user_id&#34;, &#34;gamer123&#34;},
    {&#34;level&#34;, 2},
    {&#34;total_points&#34;, 17500}};

Tealium.TrackView(&#34;level_completed_screen&#34;, data);
```

## トラックイベント

ゲーム内でのユーザーのインタラクション、例えば `achievement_unlocked` や `level_started` をトラッキングするには、[`TrackEvent()`](/ja/platforms/unity/api/#trackevent) メソッドを呼び出します。

```csharp
Dictionary&lt;string, string&gt; data = new Dictionary&lt;string, string&gt;() {
    {&#34;user_id&#34;, &#34;gamer123&#34;},
    {&#34;level&#34;, 2},
    {&#34;bonus_points&#34;, 1500}};

Tealium.TrackView(&#34;level_completed&#34;, data);
```