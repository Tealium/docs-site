---
title: YouTube event
description: The YouTube event sends tracking data when a visitor interacts with an embedded YouTube video on a page. You can specify event triggers for when the visitor plays, pauses, or reaches a specific playback milestone, or when the video is buffering.
url: https://docs.tealium.com/iq-tag-management/events/event-types/youtube-event/
---
## Requirements

* The YouTube IFrame Player API script. 
* To allow the YouTube event listener to track events for a video, you must set the `enablejsapi` parameter to `1` for the embedded video. You can also select the **Enable iFrame API** checkbox, which will automatically set the parameter on embedded videos that match the **Element Selector** criteria.
* If you want to track videos separately, the embedded videos must use unique `id` parameters.


<blockquote>
If a page with a YouTube event listener does not already contain the YouTube iFrame Player API script, the script will be automatically loaded on the page.
</blockquote>


### Embed parameters

The URL for the video ID `xWlEk2i9r5Q` will use the following URL:

`https://www.youtube.com/embed/xWlEk2i9r5Q`

A basic iframe embed code for this video with the `enablejsapi` parameter set to `1`, a unique `id` parameter set to `video1`, and the video ID will use the following format:

```html
<iframe id="video1" type="text/html" width="640" height="360"
 src="https://www.youtube.com/embed/xWlEk2i9r5Q?enablejsapi=1"></iframe>
```

For more information about how to set parameters on embedded YouTube videos, see [YouTube Embedded Players and Player Parameters documentation](https://developers.google.com/youtube/player_parameters).

## How it works

A YouTube event tracks when a visitor interacts with a YouTube video. When a visitor performs the action, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events](https://docs.tealium.com/manage-events/).

## Event triggers

Event triggers are the specific actions the event listener tracks.

The YouTube event can track the following event triggers:

* **Play** – Trigger the event listener when the video is played.
* **Pause** – Trigger the event listener when the video is paused.
* **Buffering** – Trigger the event listener when the video is buffering.
* **Milestones** – Trigger the event listener when a percentage or amount of time of the video has played.

The milestones event trigger lets you set one of the following thresholds:

* **Percentage Complete** – The percentage of the video that the viewer needs to watch before the event listener triggers. Enter multiple values in a comma-separated list (for example, `25, 50, 75`).
* **Time Viewed** – The total video viewing time that is required to trigger the event listener.

### Element selector

The element selector specifies which element on a page you want to trigger the event listener. For more information, see [Event element selector](https://docs.tealium.com/event-element-selector/).

### Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call. For more information, see [Event triggers](https://docs.tealium.com/event-triggers/).

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. In the **New Event > Event Configuration** screen, navigate to the **Event Trigger Variables** table and click the trigger type to view or edit the trigger variables for your event.

For example, to view the variables for the pause trigger, click the **Pause** tab:

![](https://docs.tealium.com/images/guides/iq/event_trigger_variables.png)

The YouTube event has the following default event trigger variables:

|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`tealium_event`| Tealium event name.| `video_play`| String|
|`video_id`| The video ID at YouTube.| `xWlEk2i9r5Q`| String|
|`video_name`| The video name.| `How to track videos in Tealium`| String|
|`video_length`| The total length (in seconds) of the video.| `300`| Number|
|`video_platform`| The name of the platform serving the video.| `youtube`| String|
|`video_playhead`| The playhead position (in seconds) of the video at the time of the event.| `151`| Number|
|`video_milestone`|  The percentage or time of the video played. This variable appears with the Milestones trigger. | `50`| Number|
|`milestone_type`|  The type of milestone, `percent` or `time`. This variable appears with the Milestones trigger. | `percent`| Number|
|`iq_event_id` | The UID of the event listener that sent the event.| `youtube_video_events_1` | String |

### Play

|Identifier| Description|
|---| ---|
|`tealium_event="video_play"`| The visitor played the video.|

**Example**

```json
{
   "tealium_event"  : "video_play",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "How to track videos in Tealium",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "1",
   "iq_event_id:" : "youtube_video_events_1"
}
```

### Pause

|Identifier| Description|
|---| ---|
|`tealium_event="video_pause"`| The visitor paused the video during playback.|

**Example**

```json
{
   "tealium_event"  : "video_pause",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "How to track videos in Tealium",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "30",
   "iq_event_id:" : "youtube_video_events_2"
}

```

### Buffering

|Identifier| Description|
|---| ---|
|`tealium_event="video_buffer"`| The visitor experienced buffering on the video.|

**Example**

```json
{
   "tealium_event"  : "video_buffer",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "How to track videos in Tealium",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "50",
   "iq_event_id:" : "youtube_video_events_3"
}
```

### Milestone

|Identifier| Description|
|---| ---|
|`tealium_event="video_milestone"`| The visitor played the video to a percentage or duration milestone.|

**Example**

```json
{
   "tealium_event"  : "video_milestone",
   "video_milestone" : "50",
   "milestone_type" : "percent",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "How to track videos in Tealium",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "151",
   "iq_event_id:" : "youtube_video_events_4"
}
```
