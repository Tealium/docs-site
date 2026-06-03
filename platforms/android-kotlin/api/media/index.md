---
title: Media
description: Reference guide for Media class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/media/
---
## Class: Media

The `Media` class provides methods for tracking streaming media in apps through the use of custom events. Learn more about [media tracking](/platforms/getting-started-mobile/media/).

The following summarizes the commonly used methods of the `Media` class for Tealium Kotlin.

| Method                                      | Description                                         |
|:--------------------------------------------|:----------------------------------------------------|
| [`clickAd()`](#clickad)                     | The user clicked on a ad that is currently playing. |
| [`custom()`](#custom)                       | Sends a custom event status to the data layer.      |
| [`endAd()`](#endad)                         | The ad ended.                                       |
| [`endAdBreak()`](#endadbreak)               | The ad break ended.                                 |
| [`endBuffer()`](#endbuffer)                 | The buffer ended.                                   |
| [`endChapter()`](#endchapter)               | The chapter ended.                                  |
| [`endSeek()`](#endseek)                     | The user ended seeking.                             |
| [`endSession()`](#endsession)               | The session ended, including ads and content.       |
| [`pause()`](#pause)                         | The user paused the media.                          |
| [`ping()`](#ping)                           | Sends an interval event to the data layer.          |
| [`play()`](#play)                           | The media content started playing.                  |
| [`resumeSession()`](#resumesession)         | The session resumed.                                |
| [`sendMilestone()`](#sendmilestone)         | Sends milestone data to the data layer.             |
| [`sendSummary()`](#sendsummary)             | Sends summary data to the data layer.               |
| [`skipAd()`](#skipad)                       | The user skipped the current ad.                    |
| [`skipChapter()`](#skipchapter)             | The user skipped the chapter.                       |
| [`startAdBreak()`](#startadbreak)           | The ad break started.                               |
| [`startAd()`](#startad)                     | The ad started.                                     |
| [`startBuffer()`](#startbuffer)             | The buffer started.                                 |
| [`startChapter()`](#startchapter)           | The chapter started.                                |
| [`startSeek()`](#startseek)                 | The user started seeking.                           |
| [`startSession()`](#startsession)           | The session started.                                |
| [`updatePlayerState()`](#updateplayerstate) | The start or end of the player state.               |
| [`updateQOE()`](#updateqoe)                 | Sets the quality of experience bitrate value.       |


### `clickAd()`

The user clicked on a ad that is currently playing.

```java
tealium?.media?.clickAd(event)
```

### `custom()`

Sends a custom event status to the data layer.

```java
tealium?.media?.custom(name)
```

| Parameter | Type     | Description            |
|:----------|:---------|:-----------------------|
| `name`    | `String` | The custom event name. |


### `endAd()`

The ad ended.

```java
tealium?.media?.endAd()
```


### `endAdBreak()`

Ends latest ad break for the current session.  Only valid in a current ad break.

```java
tealium?.media?.endAdBreak()
```


### `endBuffer()`

The buffer ended.

```java
tealium?.media?.endBuffer()
```


### `endChapter()`

The chapter ended.

```java
tealium?.media?.endChapter()
```

### `endSeek()`

The user ended seeking. Records seek ended at given position.

```java
tealium?.media?.endSeek(position)
```

| Parameter  | Type  | Description                                                    |
|:-----------|:------|:---------------------------------------------------------------|
| `position` | `Int` | The index position in the media, in seconds, where seek ended. |

Example:

```java
tealium?.media?.startSeek(10)
```

### `endSession()`

The session ended, including ads and content.

```java
tealium?.media?.endSession()
```

### `pause()`

The user paused the media.

```java
tealium?.media?.pause()
```

### `ping()`

Sends an interval event to the data layer. This method is called automatically every 10 seconds if the tracking type for the `MediaContent` object is set to `INTERVAL` or `INTERVAL_MILESTONE`.

```java
tealium?.media?.ping()
```

Learn more about [media tracking types](/platforms/getting-started-mobile/media/#trackingtype).

### `play()`

The media content started playing.

```java
tealium?.media?.play()
```

### `resumeSession()`

The session resumed.

```java
tealium?.media?.startSession()
```


### `sendMilestone()`

Sends a milestone event to the data layer. This method is called automatically, based on the The percent of content played, the tracking type for the `MediaContent` object is set to `MILESTONE` or `INTERVAL_MILESTONE`.

```java
tealium?.media?.sendMilestone()
```

Milestone values:

| Media % Played | Milestone Value |
|:---------------|:----------------|
| 8.0 - 12.0     | `10%`           |
| 23.0 - 27.0    | `25%`           |
| 48.0 - 52.0    | `50%`           |
| 73.0 - 77.0    | `75%`           |
| 88.0 - 92.0    | `90%`           |
| 97.0 - 100.0   | `100%`          |

Learn more about [media tracking types](/platforms/getting-started-mobile/media/#trackingtype).

### `sendSummary()`

Sends summary data to the data layer. This method is called automatically on `endSession()` if  the tracking type for the `MediaContent` object is set to `SUMMARY`.

```java
tealium?.media?.sendSummary()
```

Learn more about [media tracking types](/platforms/getting-started-mobile/media/#trackingtype).

### `skipAd()`

The user skipped the current ad.

```java
tealium?.media?.skipAd()
```


### `skipChapter()`

The user skipped the chapter.

```java
tealium?.media?.skipChapter()
```

### `startAd()`

The ad started. Call the [`endAd()`](#endad) method when the ad completes.

```java
tealium?.media?.startAd(ad)
```

| Parameter | Type              | Description    |
|:----------|:------------------|:---------------|
| `ad`      | [`Ad`](#class-ad) | The ad object. |

Example:
```java
tealium?.media?.startAd(Ad(&#34;Ad  1&#34;))
```

### `startAdBreak()`

The ad break started. Call the [`endAdBreak()`](#endadbreak) method when the ad break completes.

```java
tealium?.media?.startAdBreak(break)
```

| Parameter | Type                        | Description          |
|:----------|:----------------------------|:---------------------|
| `break`   | [`AdBreak`](#class-adbreak) | The ad break object. |

Example:

```java
val adBreak = AdBreak(name = &#34;Ad Break 1&#34;)
tealium?.media?.startAdBreak(adBreak)
```

### `startBuffer()`

The buffer started. Call the [`endBuffer()`](#endbuffer) method when buffering completes.

```java
tealium?.media?.startBuffer()
```


### `startChapter()`

The chapter started. Call the [`endChapter()`](#endchapter) method when the chapter completes.

```java
tealium?.media?.startChapter(chapter)
```

| Parameter | Type                        | Description               |
|:----------|:----------------------------|:--------------------------|
| `chapter` | [`Chapter`](#class-chapter) | The chapter segment name. |

Example:

```java
tealium?.media?.startChapter(Chapter(name = &#34;Chapter 1&#34;))
```


### `startSeek()`

The user started seeking. Call the [`endSeek()`](#endseek) method when seeking completes.

```java
tealium?.media?.startSeek(position)
```

| Parameter  | Type  | Description                                                      |
|:-----------|:------|:-----------------------------------------------------------------|
| `position` | `Int` | The index position in the media, in seconds, where seek started. |


Example:

```java
tealium?.media?.startSeek(10)
```

### `startSession()`

The session started. Call the [`endSession()`](#endsession) method when session completes.

```java
tealium?.media?.startSession()
```


### `updatePlayerState()`

The start or end of the player state.

```java
tealium?.media?.updatePlayerState(state)
```

| Parameter | Type             | Description     |
|:----------|:-----------------|:----------------|
| `state`   | `State` constant | The media state |

The following `State` constants are available:

| Value                | Description                    |
|:---------------------|:-------------------------------|
| `CLOSED_CAPTION`     | Closed caption state type.     |
| `FULLSCREEN`         | Full screen state type.        |
| `IN_FOCUS`           | In focus state type.           |
| `MUTE`               | Mute state type.               |
| `PICTURE_IN_PICTURE` | Picture in picture state type. |

Example:

```java
tealium?.media?.updatePlayerState(fullscreen)
```

Learn more about the [player state](/platforms/getting-started-mobile/media/#state).

### `updateQOE()`

Sets the quality of experience bitrate value in kilobits per second (kbps) of the current session.

```java
tealium?.media?.updateQOE(rate)
```

| Parameter | Type  | Description        |
|:----------|:------|:-------------------|
| `rate`    | `Int` | The bitrate value. |

Example:

```java
tealium?.media?.updateQOE(1500)
```

## Class: `MediaContent`

The `MediaContent` class creates a media content object.

```java
val mediaContent: MediaContent = MediaContent(
  name: MEDIA_NAME,
  streamType: MEDIA_STREAM_TYPE,
  mediaType: MEDIA_TYPE,   
  qoe: MEDIA_QOE,
  trackingType: MEDIA_TRACKING_TYPE,
  state = MEDIA_STATE,
  customID = MEDIA_CUSTOM_ID,
  duration: MEDIA_DURATION,
  playerName: MEDIA_PLAYER_NAME,
  channelName: MEDIA_CHANNEL_NAME,
  metadata: MEDIA_METADATA
)
```

| Variable Name  | Type                                                             | Description                                                              | Required |
|:---------------|:-----------------------------------------------------------------|:-------------------------------------------------------------------------|:---------|
| `name`         | `String`                                                         | The name of the media content.                                           | Yes      |
| `streamType`   | [`StreamType`](/platforms/getting-started-mobile/media/#streamtype)     | The type of media stream.                                                | Yes      |
| `mediaType`    | [`MediaType`](/platforms/getting-started-mobile/media/#mediatype)       | The type of media (video or audio).                                      | Yes      |
| `qoe`          | [`QoE`](/platforms/getting-started-mobile/media/#quality-of-experience) | The quality of experience bitrate value.                                 | Yes      |
| `trackingType` | [`TrackingType`](/platforms/getting-started-mobile/media/#trackingtype) | The level of event tracking. (default: `TrackingType.FULL_PLAYBACK`)     | Yes      |
| `state`        | [`PlayerState`](/platforms/getting-started-mobile/media/#state)         | The media player state type.                                             |          |
| `customId`     | `String`                                                         | The custom identifier name.                                              |          |
| `duration`     | `Int`                                                            | The media duration, in seconds, such as `130`                            |          |
| `playerName`   | `String`                                                         | The media player name.                                                   |          |
| `channelName`  | `String`                                                         | The media channel name.                                                  |          |
| `metadata`     | `[String: Any]`                                                  | Additional media [metadata](/platforms/getting-started-mobile/media/#metadata). |          |

## Class: `Ad`

The `Ad` class creates an ad object.

```java
val ad = Ad(
  id = MEDIA_AD_ID,
  name = MEDIA_AD_NAME,
  duration = MEDIA_AD_DURATION,
  position = MEDIA_AD_POSITION,
  advertiser = MEDIA_AD_ADVERTISER,
  creativeId = MEDIA_AD_CREATIVE_ID,
  campaignId = MEDIA_AD_CAMPAIGN_ID,
  placementId = MEDIA_AD_PLACEMENT_ID,
  siteId = MEDIA_AD_SITE_ID,
  creativeUrl = MEDIA_AD_CREATIVE_URL,
  numberOfLoads = MEDIA_AD_LOAD,
  pod = MEDIA_AD_POD,
  playerName = MEDIA_AD_PLAYER_NAME
)
```

| Parameter       | Type     | Description                                       | Required |
|:----------------|:---------|:--------------------------------------------------|:---------|
| `name`          | `String` | The name of the ad.                               | Yes      |
| `duration`      | `Double` | The ad duration, in seconds, such as `130`        |          |
| `position`      | `Int`    | The current index position of the ad, in seconds. |          |
| `advertiser`    | `String` | The ad advertiser.                                |          |
| `creativeId`    | `String` | The ad creative identifier.                       |          |
| `campaignId`    | `String` | The ad campaign identifier.                       |          |
| `placementId`   | `String` | The ad placement identifier.                      |          |
| `siteId`        | `String` | The ad site identifier.                           |          |
| `creativeUrl`   | `String` | The ad creative URL.                              |          |
| `numberOfLoads` | `Int`    | The number of ad loads.                           |          |
| `pod`           | `String` | The ad pod.                                       |          |
| `playerName`    | `String` | The ad player name.                               |          |

## Class: `AdBreak`

The `AdBreak` class creates an ad break object.

```java
val adBreak = AdBreak(
  id = MEDIA_AD_BREAK_ID,
  name = MEDIA_AD_BREAK_NAME,
  duration = MEDIA_AD_BREAK_DURATION,
  index = MEDIA_AD_BREAK_INDEX,
  position = MEDIA_AD_BREAK_POSITION
)
```

| Parameter  | Type     | Description                                             | Required |
|:-----------|:---------|:--------------------------------------------------------|:---------|
| `id`       | `String` | The ad break unique identifier.                         |          |
| `name`     | `String` | The ad break name.                                      | Yes      |
| `duration` | `Double` | The ad break duration, in seconds, such as `130`        |          |
| `index`    | `Int`    | The index of the ad break.                              |          |
| `position` | `Int`    | The current index position of the ad break, in seconds. |          |


## Class: `Chapter`

The `Chapter` class creates a chapter object.

```java
val chapterObject = Chapter(
  name = MEDIA_CHAPTER_NAME,
  duration = MEDIA_CHAPTER_DURATION,
  position = MEDIA_CHAPTER_POSITION,
  metadata = MEDIA_CHAPTER_METADATA
)
```

The following are the `Chapter` object parameters. Parameters must be in order if you are not using parameter names, such as `duration =` when creating the object.

| Variable Name | Type            | Description                                                                      | Required |
|:--------------|:----------------|:---------------------------------------------------------------------------------|:---------|
| `name`        | `String`        | The name of the chapter.                                                         | Yes      |
| `duration`    | `Double`        | The chapter duration, in seconds, such as `130`                                  |          |
| `position`    | `Int`           | The chapter position index.                                                      |          |
| `metadata`    | `[String: Any]` | Additional chapter media [metadata](/platforms/getting-started-mobile/media/#metadata). |          |
