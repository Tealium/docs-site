---
title: Media Tracking
description: Learn about media tracking for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/media/
---
Media tracking is the ability to track streaming media events (video or audio)  in apps. Streaming media events include sessions, chapters, advertisements (ads), and player events such as play, seek, and pause. Install the Media module to add this tracking capability to your iOS or Android app then implement the media tracking methods.


## How It Works

The Media module supports the tracking of a user&#39;s entire streaming media experience. This includes the start and end of the session, the start and end of ad breaks, and every interaction with the media player such as play, pause, and seek.

The Media module structures the tracking in a hierarchy of the following elements:

**Media Session**  
A media session is a container for all of the other elements and it defines the general information about the streaming experience. A media session is a required element for tracking.

**Chapter**  
A chapter is an optional segment that separates the session as breaks occur in the content, such as chapters of an audiobook or scenes of a movie.

**Ad Break**  
An ad break is an optional container for one or more ads. An ad break is commonly positioned at the start, middle, or end of a session.

**Ad**  
An ad is an optional element that occurs within an ad break.

Example structure of a media session:

```
└── Media Session
    ├── Ad Break 1
    │   ├── Ad 1
    │   └── Ad 2
    ├── Chapter 1
    ├── Ad Break 2
    │   ├── Ad 3
    │   └── Ad 4
    └── Chapter 2
```

## Install

To get started, install the Media module for one of the supported platforms:

- [Android (Kotlin)](/platforms/android-kotlin/module-list/media/)
- [iOS (Swift v2.x)](/platforms/ios-swift/module-list/media/)

## Initialize

After you install the Media module, initialize a `MediaContent` object:  




```kotlin
val mediaContent: MediaContent = MediaContent(
  name = &#34;What is the Tealium Customer Data Hub?&#34;,
  trackingType = TrackingType.MILESTONE,
  streamType = StreamType.DVOD,
  mediaType = MediaType.VIDEO,
  qoe = QoE(1500),
  duration = 130
)
```  




```swift
let media = MediaContent(
  name: &#34;What is the Tealium Customer Data Hub?&#34;,
  trackingType: .milestone,
  streamType: .vod,
  mediaType: .video,
  qoe: QoE(bitrate: 1500),
  duration: 130
)
```





### `TrackingType`

The tracking type determines which media events to track as Tealium events. (See [Tracking Type Overview](#tracking-type-overview).)

Use one of the following constants to set `TrackingType`:




| Type                                             | Property             | Description                                                                                                                       |
|:-------------------------------------------------|:---------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| [Full Playback](#full-playback-events)           | `FULL_PLAYBACK`      | Tracks all media events, excluding interval events.                                                                               |
| [Interval](#interval-events)                     | `INTERVAL`           | Tracks standard media events and pings every 10 seconds to check if content is playing.                                           |
| [Milestone](#milestone-events)                   | `MILESTONE`          | Tracks standard media events and measures the percent of content played.                                                          |
| [Interval Milestone](#interval-milestone-events) | `INTERVAL_MILESTONE` | Tracks both interval and milestone events.                                                                                        |
| [Summary](#summary-events)                       | `SUMMARY`            | Sends a single summary to the data layer when the session ends, including calculations for the duration of played content or ads. |




| Type                                             | Property            | Description                                                                                                                       |
|:-------------------------------------------------|:--------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| [Full Playback](#full-playback-events)           | `fullPlayback`      | Tracks all media events, excluding interval events.                                                                               |
| [Interval](#interval-events)                     | `interval`          | Tracks standard media events and pings every 10 seconds to check if content is playing.                                           |
| [Milestone](#milestone-events)                   | `milestone`         | Tracks standard media events and measures the percent of content played.                                                          |
| [Interval Milestone](#interval-milestone-events) | `intervalMilestone` | Tracks both interval and milestone events.                                                                                        |
| [Summary](#summary-events)                       | `summary`           | Sends a single summary to the data layer when the session ends, including calculations for the duration of played content or ads. |




### `StreamType`

Use one of the following constants to set `StreamType`:




| Value       | Description                              |
|:------------|:-----------------------------------------|
| `AOD`       | Stream type for audio on demand.         |
| `AUDIOBOOK` | Stream type for audio book.              |
| `CUSTOM`    | Custom stream type.                      |
| `DVOD`      | Stream type for digital video on demand. |
| `LINEAR`    | Stream type for linear content.          |
| `LIVE`      | Stream type for live content.            |
| `PODCAST`   | Stream type for podcast.                 |
| `SONG`      | Stream type for song.                    |
| `UGC`       | Stream type for user-generated content.  |
| `VOD`       | Stream type for video on demand.         |




| Value       | Description                              |
|:------------|:-----------------------------------------|
| `aod`       | Stream type for audio on demand.         |
| `audiobook` | Stream type for audio book.              |
| `custom`    | Custom stream type.                      |
| `dvod`      | Stream type for digital video on demand. |
| `linear`    | Stream type for linear content.          |
| `live`      | Stream type for live content.            |
| `podcast`   | Stream type for podcast.                 |
| `song`      | Stream type for song.                    |
| `ugc`       | Stream type for user-generated content.  |
| `vod`       | Stream type for video on demand.         |




### `MediaType`

The following are the `MediaType` constants:




| Property | Description                                |
|:---------|:-------------------------------------------|
| `ALL`    | All media types including audio and video. |
| `AUDIO`  | Media type for audio streams.              |
| `VIDEO`  | Media type for video streams.              |




| Property | Description                                |
|:---------|:-------------------------------------------|
| `all`    | All media types including audio and video. |
| `audio`  | Media type for audio streams.              |
| `video`  | Media type for audio streams.              |




### `State`

Player state tracking captures the mode of the video player during playback, such as full screen mode, closed captions, or muted volume. The player state is set to the data layer variable `media_player_state`.

Example of tracking change in player state:  



Set the state value by calling the [`updatePlayerState()`](/platforms/android-kotlin/api/media/#updateplayerstate) method:  
```kotlin
tealium?.media?.updatePlayerState(STATE_CONSTANT_VALUE)
```


Set the state value by setting the [`playerState`](/platforms/ios-swift/api/media-session/#playerstate) variable:  

```swift
mediaSession.playerState = STATE_CONSTANT_VALUE
```



Use one of the following constants to set `State`:




| Value                | Description                    |
|:---------------------|:-------------------------------|
| `CLOSED_CAPTION`     | Closed caption state type.     |
| `FULLSCREEN`         | Full screen state type.        |
| `IN_FOCUS`           | In focus state type.           |
| `MUTE`               | Mute state type.               |
| `PICTURE_IN_PICTURE` | Picture in picture state type. |




| Value              | Description                    |
|:-------------------|:-------------------------------|
| `closedCaption`    | Closed caption state type.     |
| `fullscreen`       | Full screen state type.        |
| `inFocus`          | In focus state type.           |
| `mute`             | Mute state type.               |
| `pictureInPicture` | Picture in picture state type. |




### Quality of Experience

The quality of experience for the media session, which is set to the bitrate in kilobits per second (kbps). If the current bitrate value is available during media playback, provide it as the `qoe` variable when initializing the `MediaContent` object. Setting the quality of experience triggers the `media_bitrate_change` tealium event.

Example of tracking quality of experience:   



Set the quality of experience bitrate value by calling the [`updateQOE()`](/platforms/android-kotlin/api/media/#updateqoe) method:
```kotlin
tealium?.media?.updateQOE(BITRATE_VALUE)
```


Set the quality of experience bitrate value by setting the [`bitrate`](/platforms/ios-swift/api/media-session/#bitrate) variable:  
```swift
mediaSession.bitrate = BITRATE_VALUE
```




### Metadata

Metadata is a parameter that sets additional information about an object.  When you pass metadata to the object, those key-value pairs are also set in the data layer. The following objects accept metadata: `MediaContent`, `Chapter`, `QoE`.

Since metadata can be set in multiple objects, it&#39;s possible to set the same metadata key multiple times. To resolve conflicting metadata keys in the data layer, the metadata from multiple objects are merged into the data layer using the object hierarchy: `MediaContent` &gt; `Chapter` &gt; `QoE`.

For example, if you set `feed_type` in both `MediaContent` and `Chapter`, the  value from the `Chapter` metadata will override the value from the `MediaContent` metadata in the final data layer.

Example of setting metadata:  




```kotlin
val mediaContent: MediaContent = MediaContent(
    // ...
    metadata = mutableMapOf(&#34;episode&#34; to &#34;2&#34;, &#34;network&#34; to &#34;YouTube&#34;)
)
```



```swift
let media = MediaContent(
    // ...
    metadata: [&#34;episode&#34;: &#34;2&#34;, &#34;network&#34;: &#34;YouTube&#34;]
)
```




#### Video Metadata Keys

The following are examples of common video metadata keys:

| Variable             | Description                                                                                                          |
|:---------------------|:---------------------------------------------------------------------------------------------------------------------|
| `authorized`         | The user is authenticated or not.                                                                                    |
| `episode`            | The episode name or number.                                                                                          |
| `asset_id`           | The TMS ID, which is the industry standard ID for a piece of video content.                                          |
| `daypart`            | The part of the day such as morning or primetime.                                                                    |
| `feed_type`          | The feed type such as HD, SD, or regional.                                                                           |
| `first_air_date`     | The date the media was first aired.                                                                                  |
| `first_digital_date` | The date the media was first available digitally.                                                                    |
| `genre`              | The genre.                                                                                                           |
| `media_mvpd`         | The multichannel video programming distributor. Typically a cable or satellite network such as Cox, DirecTV, or Sky. |
| `network`            | The network.                                                                                                         |
| `originator`         | The show originator.                                                                                                 |
| `rating`             | The rating.                                                                                                          |
| `season`             | The season number or name.                                                                                           |
| `show`               | The name of the show.                                                                                                |
| `show_type`          | The show type.                                                                                                       |
| `stream_format`      | The stream format: `0` is partial content, `1` is full episode.                                                      |

#### Audio Metadata Keys

The following are examples of common audio metadata keys:

| Variable       | Description                |
|:---------------|:---------------------------|
| `album`        | The album name.            |
| `artist`       | The artist name.           |
| `author`       | The audiobook author name. |
| `publisher`    | The music publisher.       |
| `record_label` | The record label name.     |
| `station`      | The radio station.         |

## Tracking Type Overview

The tracking type determines which Tealium events are triggered. Choose a tracking type based on the level of events you want to trigger.

For example, if you implement all the tracking methods and use summary tracking, only the `media_session_end` event is triggered.

### Full Playback Events

Use full playback tracking to tracks all media events, excluding interval events.

Tracked events include:

- Session events:  
  * `media_session_start`
  * `media_session_resume`
  * `media_session_end`
- Ad break events:  
  * `media_adbreak_start`
  * `media_adbreak_end`
- Ad events:  
  * `media_ad_start`
  * `media_ad_end`
  * `media_ad_click`
  * `media_ad_skip`
- Chapter events:  
  * `media_chapter_start`
  * `media_chapter_skip`
  * `media_chapter_end`
- Buffer events:  
  * `media_buffer_start`
  * `media_buffer_end`
- Player events:  
  * `media_play`
  * `media_pause`
  * `media_seek_start`
  * `media_seek_end`
- Other events
  * `media_bitrate_change`

### Interval Events

Use interval tracking to track the status of the media player at a recurring interval. When this type is used the `ping()` method is called every 10 seconds to check if content is playing, which sets `tealium_event` to `media_interval` in the data layer.

Tracked events include:

- Session events:  
  * `media_session_start`
  * `media_session_resume`
  * `media_session_end`
- Player events:  
  * `media_play`
  * `media_pause`
- Interval events:
  * `media_interval`


### Milestone Events

Use milestone tracking to track when a percentage of the content has been played. The `sendMilestone()` method is called automatically when each milestone percentage is reached, which sets `tealium_event` to `media_milestone` in the data layer.

The following milestone percentages are tracked:

| Media % Played | Value of `media_milestone` |
|:---------------|:---------------------------|
| 8.0 - 12.0     | `10%`                      |
| 23.0 - 27.0    | `25%`                      |
| 48.0 - 52.0    | `50%`                      |
| 73.0 - 77.0    | `75%`                      |
| 88.0 - 92.0    | `90%`                      |
| 97.0 - 100.0   | `100%`                     |

Tracked events include:

- Milestone events:
  * `media_milesetone`
- Session events:  
  * `media_session_start`
  * `media_session_resume`
  * `media_session_end`
- Player events:  
  * `media_play`
  * `media_pause`
  * `media_seek_start`
  * `media_seek_end`
- Ad break events:  
  * `media_adbreak_start`
  * `media_adbreak_end`

### Interval Milestone Events

Use interval milestone tracking to track both [interval](#interval-events) and [milestone](#milestone-events) events.

### Summary Events

Use summary tracking to send a single summary event when the session ends. The session summery event includes calculations for the duration of played content and ads.

Summary events include:

- Session events:  
  * `media_session_start`
  * `media_session_end`

See the full list of all [media summary variables](/platforms/getting-started-mobile/media/#media-summary-data) that are tracked.

### Comparison Chart

For a full list of the available media events, see the [Track](#track) section.

| Event                    | Full Playback | Interval | Milestone | Interval Milestone | Summary |
|:-------------------------|:--------------|:---------|:----------|:-------------------|:--------|
| Session Start/Resume/End | ✔             | ✔        | ✔         | ✔                  | ✔       |
| Chapter Start/Skip/End   | ✔             |          |           |                    |         |
| Ad Break Start/End       | ✔             |          | ✔         | ✔                  |         |
| Ad Start/Click/Skip/End  | ✔             |          |           |                    |         |
| Buffer Start/End         | ✔             |          |           |                    |         |
| Milestone                | ✔             |          | ✔         | ✔                  |         |
| Play                     | ✔             | ✔        | ✔         | ✔                  |         |
| Pause                    | ✔             |          | ✔         | ✔                  |         |
| Seek Start/End           | ✔             |          | ✔         | ✔                  |         |
| Player Bitrate Change    | ✔             |          |           |                    |         |
| Player State Change      | ✔             |          |           |                    |         |
| Interval                 |               | ✔        |           | ✔                  |         |


## Track

After you initialize the `MediaContent` object, use the following methods to track  media interactions.

### Media Sessions

A media session is the entire media content containing chapters, ad breaks, ads, and media player events.

To start tracking a media session call the `startSession()` method with a `MediaContent` object. To stop tracking a media session call the `endSession()` method.

Starting a session does not imply a `play()` event.

Example:  




```kotlin
tealium?.media?.startSession(mediaContentObject)
//...
tealium?.media?.endSession()
```




```swift
let mediaSessionObject = tealium?.media?.createSession(
      from: mediaContentObject)                                
mediaSessionObject.startSession()
// ...
mediaSessionObject.end()
```



This table lists the values of `tealium_event` for each session tracking method:




| Method                                                                  | Event Description                             | Tealium Event          |
|:------------------------------------------------------------------------|:----------------------------------------------|:-----------------------|
| [`startSession()`](/platforms/android-kotlin/api/media/#startsession)   | The session started.                          | `media_start_session`  |
| [`resumeSession()`](/platforms/android-kotlin/api/media/#resumesession) | The session resumed.                          | `media_resume_session` |
| [`endSession()`](/platforms/android-kotlin/api/media/#endsession)       | The session ended, including ads and content. | `media_session_end`    |




| Method                                                                     | Event Description                             | Tealium Event          |
|:---------------------------------------------------------------------------|:----------------------------------------------|:-----------------------|
| [`startSession()`](/platforms/ios-swift/api/media-session/#startsession)   | The session started.                          | `media_start_session`  |
| [`resumeSession()`](/platforms/ios-swift/api/media-session/#resumesession) | The session resumed.                          | `media_resume_session` |
| [`endSession()`](/platforms/ios-swift/api/media-session/#endsession)       | The session ended, including ads and content. | `media_session_end`    |






### Player Events

Media player events track interactions with the media such as play, seek, and pause.

This table lists the values of `tealium_event` for each player tracking method:




| Method                                                              | Event Description                  | Tealium Event         |
|:--------------------------------------------------------------------|:-----------------------------------|:----------------------|
| [`play()`](/platforms/android-kotlin/api/media/#play)               | The media content started playing. | `media_play`          |
| [`pause()`](/platforms/android-kotlin/api/media/#pause)             | The user paused the media.         | `media_pause`         |
| [`startSeek()`](/platforms/android-kotlin/api/media/#startseek)     | The user started seeking.          | `media_seek_start`    |
| [`endSeek()`](/platforms/android-kotlin/api/media/#endseek)         | The user ended seeking.            | `media_seek_end`      |
| [`startBuffer()`](/platforms/android-kotlin/api/media/#startbuffer) | The buffer started.                | `media_buffer_start`  |
| [`endBuffer()`](/platforms/android-kotlin/api/media/#endbuffer)     | The buffer ended.                  | `media_buffer_end`    |
| [`custom()`](/platforms/android-kotlin/api/media/#custom)           | Custom event status.               | `&lt;custom event name&gt;` |




| Method                                                                 | Event Description                  | Tealium Event         |
|:-----------------------------------------------------------------------|:-----------------------------------|:----------------------|
| [`play()`](/platforms/ios-swift/api/media-session/#play)               | The media content started playing. | `media_play`          |
| [`pause()`](/platforms/ios-swift/api/media-session/#pause)             | The user paused the media.         | `media_pause`         |
| [`startSeek()`](/platforms/ios-swift/api/media-session/#startsession)  | The user started seeking.          | `media_seek_start`    |
| [`endSeek()`](/platforms/ios-swift/api/media-session/#endseek)         | The user ended seeking.            | `media_seek_end`      |
| [`startBuffer()`](/platforms/ios-swift/api/media-session/#startbuffer) | The buffer started.                | `media_buffer_start`  |
| [`endBuffer()`](/platforms/ios-swift/api/media-session/#endbuffer)     | The buffer ended.                  | `media_buffer_end`    |
| [`custom()`](/platforms/ios-swift/api/media-session/#custom)           | Custom event status.               | `&lt;custom event name&gt;` |




### Chapters

Chapters are optional segments within the media session that represent breaks in the content such as chapters in an audiobook or scenes in a movie.

To track a chapter segment in the media session, create a `Chapter` object and pass it to the `startChapter()` method. To stop tracking the chapter, call the `endChapter()` method.

Example of tracking a chapter:




```kotlin
val chapterObject = Chapter(
  name = &#34;What is the Tealium Customer Data Hub?&#34;,
  duration = 114
)
tealium?.media?.startChapter(chapterObject)
// ...
tealium?.media?.endChapter()
```




```swift
let chapterObject = Chapter(
  name: &#34;What is the Tealium Customer Data Hub?&#34;,
  duration: 114
)
mediaSession.startChapter(chapterObject)
// ...
mediaSession.endChapter()
```




This table lists the values of `tealium_event` for each chapter tracking method:




| Method                                                                | Event Description             | Tealium Event         |
|:----------------------------------------------------------------------|:------------------------------|:----------------------|
| [`startChapter()`](/platforms/android-kotlin/api/media/#startchapter) | The chapter started.          | `media_chapter_start` |
| [`skipChapter()`](/platforms/android-kotlin/api/media/#skipchapter)   | The user skipped the chapter. | `media_chapter_skip`  |
| [`endChapter()`](/platforms/android-kotlin/api/media/#endchapter)     | The chapter ended.            | `media_chapter_end`   |




| Method                                                                   | Event Description             | Tealium Event         |
|:-------------------------------------------------------------------------|:------------------------------|:----------------------|
| [`startChapter()`](/platforms/ios-swift/api/media-session/#startchapter) | The chapter started.          | `media_chapter_start` |
| [`skipChapter()`](/platforms/ios-swift/api/media-session/#skipchapter)   | The user skipped the chapter. | `media_chapter_skip`  |
| [`endChapter()`](/platforms/ios-swift/api/media-session/#endchapter)     | The chapter ended.            | `media_chapter_end`   |





### Ads

An ad break is a sequence of one more ads.

To track the start of an ad break, create an `AdBreak` object and pass it to the `startAdBreak()` method. To track the start of an ad within the ad break, create an `Ad` object and pass it to the `startAd()` method.

To track the end of an ad, call the `endAd()` method. To track the end of the ad break, call the `endAdBreak()` method.

Example of tracking ad breaks and ads:



```kotlin
val adBreak = AdBreak(name = &#34;Ad Break&#34;)
tealium?.media?.startAdBreak(adBreak)

val ad1 = Ad(&#34;Ad 1&#34;)
tealium?.media?.startAd(ad1)
tealium?.media?.endAd()

val ad2 = Ad(&#34;Ad 2&#34;)
tealium?.media?.startAd(ad2)
tealium?.media?.endAd()

tealium?.media?.endAdBreak()
```


```swift
val adBreak = AdBreak(name: &#34;Ad Break&#34;)
session.endAdBreak(adBreak)

let ad1 = Ad(&#34;Ad 1&#34;)
session.startAd(ad1)
session.endAd()

let ad2 = Ad(&#34;Ad 2&#34;)
session.adStart(ad2)
session.endAd()

session.endAdBreak()
```



This table lists the values of `tealium_event` for each ad tracking method:




| Method                                                                | Event Description                                   | Tealium Event         |
|:----------------------------------------------------------------------|:----------------------------------------------------|:----------------------|
| [`startAdBreak()`](/platforms/android-kotlin/api/media/#startadbreak) | The ad break started.                               | `media_adbreak_start` |
| [`endAdBreak()`](/platforms/android-kotlin/api/media/#endadbreak)     | The ad break ended.                                 | `media_adbreak_end`   |
| [`startAd()`](/platforms/android-kotlin/api/media/#startad)           | The ad started.                                     | `media_ad_start`      |
| [`endAd()`](/platforms/android-kotlin/api/media/#endad)               | The ad ended.                                       | `media_ad_end`        |
| [`clickAd()`](/platforms/android-kotlin/api/media/#clickad)           | The user clicked on a ad that is currently playing. | `media_ad_click`      |
| [`skipAd()`](/platforms/android-kotlin/api/media/#skipad)             | The user skipped the current ad.                    | `media_ad_skip`       |




| Method                                                                   | Event Description                                   | Tealium Event         |
|:-------------------------------------------------------------------------|:----------------------------------------------------|:----------------------|
| [`startAdBreak()`](/platforms/ios-swift/api/media-session/#startadbreak) | The ad break started.                               | `media_adbreak_start` |
| [`endAdBreak()`](/platforms/ios-swift/api/media-session/#endadbreak)     | The ad break ended.                                 | `media_adbreak_end`   |
| [`startAd()`](/platforms/ios-swift/api/media-session/#startAd)           | The ad started.                                     | `media_ad_start`      |
| [`endAd()`](/platforms/ios-swift/api/media-session/#endad)               | The ad ended.                                       | `media_ad_end`        |
| [`clickAd()`](/platforms/ios-swift/api/media-session/#clickad)           | The user clicked on a ad that is currently playing. | `media_ad_click`      |
| [`skipAd()`](/platforms/ios-swift/api/media-session/#skipad)             | The user skipped the current ad.                    | `media_ad_skip`       |




## Data Layer

The Media module transmits different variables for each type of tracked event. The following sections list the data layer variables associated with each Tealium event.

The optional variables are only sent if they are defined.

### Media Session Data

Tealium events: `media_session_start`, `media_session_end`

| Variable                   | Description                                                                                                                    | Required |
|:---------------------------|:-------------------------------------------------------------------------------------------------------------------------------|:---------|
| `media_channel_name`       | The channel name.                                                                                                              |          |
| `media_custom_id`          | A custom ID for the media session, not auto-generated, such as `customId123`.                                                  |          |
| `media_duration`           | The media duration, in seconds, such as `130`.                                                                                 | Yes      |
| `media_milestone`          | The media milestones, measured by percent of content played. Possible values are `10%`, `25%`, `50%`, `75%`, `90%`, or `100%`. |          |
| `media_name`               | Name of the main content.                                                                                                      | Yes      |
| `media_player_name`        | The name of the media player such as Brightcove or AVPlayer.                                                                   |          |
| `media_qoe`                | The media quality of experience stream quality object.                                                                         | Yes      |
| `media_session_start_time` | The media start time (calculated if not defined).                                                                              |          |
| `media_stream_type`        | The media stream type, such as `DVoD`.                                                                                         | Yes      |
| `media_tracking_type`      | The [`TrackingType`](#trackingtype) value passed into the `MediaContent` object, such as `interval`                            | Yes      |
| `media_type`               | The media type, such as `video`.                                                                                               | Yes      |
| `media_uuid`               | The media session unique ID, auto-generated by Tealium SDK, such as `83675D85-F0D3-48BB-A1BB-18111B7A89AA`.                    | Yes      |


### Chapter Data

Tealium events: `media_chapter_start`, `media_chapter_end`

| Variable                   | Description                                                                       | Required |
|:---------------------------|:----------------------------------------------------------------------------------|:---------|
| `media_chapter_uuid`       | The unique ID of the chapter, such as `83675D85-F0D3-48BB-A1BB-18111B7A89AA`.     | Yes      |
| `media_chapter_name`       | The chapter name, such as `Chapter 2`.                                            | Yes      |
| `media_chapter_duration`   | The chapter&#39;s duration in seconds (calculated if not not defined), such as `600`. | Yes      |
| `media_chapter_position`   | The number position of the chapter within the session, starting with `0`.         |          |
| `media_chapter_start_time` | Offset in seconds from the start of the content, such as `641407641.724858`.      |          |

### Ad Break Data

Tealium events: `media_adbreak_start`, `media_adbreak_end`

| Variable                  | Description                                                                                            | Required |
|:--------------------------|:-------------------------------------------------------------------------------------------------------|:---------|
| `media_ad_break_id`       | The custom ID for the ad break.                                                                        |          |
| `media_ad_break_index`    | The index of the ad break, such as `1` for the first ad break.                                         |          |
| `media_ad_break_duration` | The ad break duration in seconds (calculated if not defined).                                          |          |
| `media_ad_break_name`     | The name of the ad break. If not provided, is automatically set to the value of `media_ad_break_uuid`. | Yes      |
| `media_ad_break_position` | The number position of the ad break within the content, starting with `0`.                             |          |
| `media_ad_break_uuid`     | The UUID for the ad break, which is auto-generated by the Tealium SDK.                                 | Yes      |

### Ad Data

Tealium events: `media_ad_start`, `media_ad_end`

| Variable                | Description                                                           | Required |
|:------------------------|:----------------------------------------------------------------------|:---------|
| `media_ad_campaign_id`  | The campaign ID for the ad.                                           |          |
| `media_ad_creative_id`  | The ID for the creative content of the ad.                            |          |
| `media_ad_creative_url` | The URL for the creative content of the ad.                           |          |
| `media_ad_duration`     | The ad duration in seconds (if not provided, calculated by the SDK).  |          |
| `media_ad_id`           | The custom ID for the ad.                                             |          |
| `media_ad_load`         | The number of ad loads.                                               |          |
| `media_ad_name`         | The name of the ad.                                                   | Yes      |
| `media_ad_placement_id` | The placement ID for the ad (typically in the header or footer).      |          |
| `media_ad_player_name`  | The player name for the ad.                                           |          |
| `media_ad_pod`          | The pod the ad belongs to.                                            |          |
| `media_ad_position`     | The number position of the ad within the ad break, starting with `0`. |          |
| `media_ad_site_id`      | The site ID for the ad.                                               |          |
| `media_ad_uuid`         | The UUID for the ad, such as `83675D85-F0D3-48BB-A1BB-18111B7A89AA`.  | Yes      |
| `media_advertiser`      | The advertiser name for the ad.                                       |          |

### Quality of Experience Data

Tealium events: `media_bitrate_change`

The quality of experience properties may be updated during the lifetime of the session if the quality changes or frames are dropped. The `media_bitrate_change` event is triggered every time the bitrate value is set.

| Variable                      | Description                                                                                     | Required |
|:------------------------------|:------------------------------------------------------------------------------------------------|:---------|
| `media_qoe_bitrate`           | The media quality of experience bitrate value in kilobits per second (kbps), such as `1500`.    | Yes      |
| `media_qoe_startup_time`      | The time taken, in milliseconds, for the content to start up.                                   |          |
| `media_qoe_frames_per_second` | The frame rate per second of the content.                                                       |          |
| `media_qoe_dropped_frames`    | The sum of all dropped frames during the session.                                               |          |
| `media_qoe_playback_speed`    | The user-selected content playback speed, such as `1.5` for 1 1/2 times the normal media speed. |          |

### Media Summary Data

Tealium events: `media_session_end` (when `TrackingType` is set to `summary`)

| Variable                            | Data Type  | Description                                                                 | Example                                                                            |
|:------------------------------------|:-----------|:----------------------------------------------------------------------------|:-----------------------------------------------------------------------------------|
| `media_ad_uuids`                    | `[String]` | An array of unique identifiers for ads played during this media session.    | `[&#34;8B51B7FA-EEC5-4754-ACAB-58B9B7643AE8&#34;, &#34;83675D85-F0D3-48BB-A1BB-18111B7A89AA&#34;]` |
| `media_percentage_ad_complete`      | `Double`   | The percentage of completed ads after starting.                             | `90.0`                                                                             |
| `media_percentage_ad_time`          | `Double`   | The percentage of ad content playback time.                                 | `23.7`                                                                             |
| `media_percentage_chapter_complete` | `Double`   | The percentage of completed chapters after starting.                        | `75.0`                                                                             |
| `media_played_to_end`               | `Boolean`  | Indicates whether or not the content entirely.                              | `true`                                                                             |
| `media_session_duration`            | `Double`   | The length of the session in seconds (from `sessionStart` to `sessionEnd`.  | `1300.0`                                                                           |
| `media_session_end_time`            | `String`   | The date and time (UTC) the session ended.                                  | `2021-01-26T16:43:53Z`                                                             |
| `media_session_start_time`          | `String`   | The date and time (UTC) the session started.                                | `2021-01-26T16:43:53Z`                                                             |
| `media_total_ad_skips`              | `Int`      | The number of times the `skipAd()` method was called.                       | `3`                                                                                |
| `media_total_ad_time`               | `Double`   | The total seconds ad content played.                                        | `30.0`                                                                             |
| `media_total_ads`                   | `Int`      | The number of times the `startAd()` method was called.                      | `4`                                                                                |
| `media_total_buffer_time`           | `Double`   | The total seconds the content was buffering (`startBuffer` to `endBuffer`). | `2.1`                                                                              |
| `media_total_chapter_skips`         | `Int`      | The number of times the `chapterSkip()` method was called.                  | `1`                                                                                |
| `media_total_pauses`                | `Int`      | The number of times the `pause()` method was called.                        | `1`                                                                                |
| `media_total_play_time`             | `Double`   | The total seconds the content was playing.                                  | `9300.2`                                                                           |
| `media_total_plays`                 | `Int`      | The number of times the `play()` method was called.                         | `2`                                                                                |
| `media_total_seek_time`             | `Double`   | The total seconds in seek (`seekStart` to `seekEnd`).                       | `46.5`                                                                             |
