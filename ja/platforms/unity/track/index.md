---
title: トラック
description: ゲーム活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/unity/track/
---

## ゲームイベントの追跡

ユーザーのゲームとのやり取り、例えば `achievement_unlocked` や `level_started` を追跡するには、[`TealiumEvent`](/ja/platforms/unity/api/#class-tealiumevent) オブジェクトを作成し、それを [`Track()`](/ja/platforms/unity/api/#track) メソッドに渡します。`TealiumEvent` はイベント名と、オプションのデータ辞書で構成され、追跡呼び出しでは `tealium_event` として表示されます。

```javascript
TealiumEvent event = TealiumEvent(&#34;level_completed&#34;,
    new Dictionary&lt;string, object&gt; {
        {&#34;user_id&#34;, &#34;gamer123&#34;},
        {&#34;level&#34;: 2},
        {&#34;bonus_points&#34;: 1500}});
TealiumUnityPlugin.Track(event);
```

## ゲームビューの追跡

ゲーム内のビュー、例えばリーダーボード画面を追跡するには、[`TealiumView`](/ja/platforms/unity/api/#class-tealiumview) オブジェクトを作成し、それを [`Track()`](/ja/platforms/unity/api/#track) メソッドに渡します。`TealiumView` はビュー名と、オプションのデータ辞書で構成され、追跡呼び出しでは `tealium_event` として表示されます。

```javascript
TealiumView view = new TealiumView(&#34;level_completed_screen&#34;,
    new Dictionary&lt;string, object&gt; {
        {&#34;user_id&#34;, &#34;gamer123&#34;},
        {&#34;level&#34;: 2},
        {&#34;total_points&#34;: 17500}});
TealiumUnityPlugin.Track(view);
```
