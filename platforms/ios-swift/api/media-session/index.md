---
title: MediaSession
description: Reference guide for Media class and methods provided by Tealium for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift/api/media-session/
---
## Class: Media

The `MediaSession` class provides methods for tracking streaming media in apps through the use of custom events. Learn more about [media tracking](https://docs.tealium.com/platforms/getting-started-mobile/media/).

The following summarizes the commonly used methods of the `MediaSession` class for Tealium iOS (Swift).

| Method or Property                  | Description                                         |
|:------------------------------------|:----------------------------------------------------|
| [`bitrate`](#bitrate)               | Sets the quality of experience bitrate value.       |
| [`clickAd()`](#clickad)             | The user clicked on a ad that is currently playing. |
| [`custom()`](#custom)               | Sends a custom event status to the data layer.      |
| [`endAd()`](#endad)                 | The ad ended.                                       |
| [`endAdBreak()`](#endadbreak)       | The ad break ended.                                 |
| [`endBuffer()`](#endbuffer)         | The buffer ended.                                   |
| [`endChapter()`](#endchapter)       | The chapter ended.                                  |
| [`endSeek()`](#endseek)             | The user ended seeking.                             |
| [`endSession()`](#endsession)       | The session ended, including ads and content.       |
| [`pause()`](#pause)                 | The user paused the media.                          |
| [`ping()`](#ping)                   | Sends an interval event to the data layer.          |
| [`play()`](#play)                   | The media content started playing.                  |
| [`playerState`](#playerstate)       | The start or end of the player state.               |
| [`resumeSession()`](#resumesession) | The session resumed.                                |
| [`sendMilestone()`](#sendmilestone) | Sends milestone data to the data layer.             |
| [`sendSummary()`](#sendsummary)     | Sends summary data to the data layer.               |
| [`skipAd()`](#skipad)               | The user skipped the current ad.                    |
| [`skipChapter()`](#skipchapter)     | The user skipped the chapter.                       |
| [`startAdBreak()`](#startadbreak)   | The ad break started.                               |
| [`startAd()`](#startad)             | The ad started.                                     |
| [`startBuffer()`](#startbuffer)     | The buffer started.                                 |
| [`startChapter()`](#startchapter)   | The chapter started.                                |
| [`startSeek()`](#startseek)         | The user started seeking.                           |
| [`startSession()`](#startsession)   | The session started.                                |


### `bitrate()`

Sets the quality of experience bitrate value (`Int`) in kilobits per second (kbps) of the current session.

| Property  | Type  | Description        |
|:----------|:------|:-------------------|
| `bitrate` | `Int` | The bitrate value. |

```swift
mediaSession.bitrate = BITRATE_VALUE
```


### `clickAd()`

The user clicked on a ad that is currently playing.

```swift
mediaSession.clickAd()
```

### `custom()`

Sends a custom event status to the data layer.

```swift
mediaSession.custom(name)
```

| Parameter | Type     | Description            |
|:----------|:---------|:-----------------------|
| `name`    | `String` | The custom event name. |



### `endAd()`

The ad ended.  

```swift
mediaSession.endAd()
```


### `endAdBreak()`

The ad break ended.

```swift
mediaSession.endAdBreak()
```


### `endBuffer()`

The buffer ended.

```swift
mediaSession.endBuffer()
```


### `endChapter()`

The chapter ended.

```swift
mediaSession.endChapter()
```

### `endSeek()`

The user ended seeking. Records seek ended at given position.

```swift
mediaSession.endSeek(at position: Int)
```

| Parameter  | Type  | Description                                                    |
|:-----------|:------|:---------------------------------------------------------------|
| `position` | `Int` | The index position in the media, in seconds, where seek ended. |

Example:

```swift
mediaSession.endSeek(at position: 10)
```

### `endSession()`

The session ended, including ads and content.

```swift
mediaSession.endSession()
```

### `pause()`

The user paused the media.

```swift
mediaSession.pause()
```

### `ping()`

Sends an interval event to the data layer. This method is called automatically every 10 seconds if the tracking type for the `MediaContent` object is set to `interval` or `intervalMilestone`.

```swift
mediaSession.ping()
```

Learn more about [media tracking types](https://docs.tealium.com/platforms/getting-started-mobile/media/#trackingtype).

### `play()`

The media content started playing.

```swift
mediaSession.play()
```

### `playerstate`

The start or end of the player state.

```swift
mediaSession.playerState = PLAYER_STATE
```

The following `State` constants are available:

| Value              | Description                    |
|:-------------------|:-------------------------------|
| `closedCaption`    | Closed caption state type.     |
| `fullscreen`       | Full screen state type.        |
| `inFocus`          | In focus state type.           |
| `mute`             | Mute state type.               |
| `pictureInPicture` | Picture in picture state type. |

Example:

```swift
mediaSession.playerState = .mute
```

Learn more about the [player state](https://docs.tealium.com/platforms/getting-started-mobile/media/#state).

### `resumeSession()`

The session resumed.

```swift
mediaSession.resumeSession()
```

### `sendMilestone()`

Sends a milestone event to the data layer. This method is called automatically, based on the percent of content played, the tracking type for the `MediaContent` object is set to `milestone` or `intervalMilestone`.

```swift
mediaSession.sendMilestone(_ milestone: Milestone)
```

| Parameter   | Type        | Description                   |
|:------------|:------------|:------------------------------|
| `milestone` | `Milestone` | The percent of content played |

Milestone values:

| Media % Played | Milestone Value |
|:---------------|:----------------|
| 8.0 - 12.0     | `10%`           |
| 23.0 - 27.0    | `25%`           |
| 48.0 - 52.0    | `50%`           |
| 73.0 - 77.0    | `75%`           |
| 88.0 - 92.0    | `90%`           |
| 97.0 - 100.0   | `100%`          |

Learn more about [media tracking types](https://docs.tealium.com/platforms/getting-started-mobile/media/#trackingtype).

### `sendSummary()`

Sends summary data to the data layer. This method is called automatically on `endSession()` if  the tracking type for the `MediaContent` object is set to `summary`.

```swift
mediaSession.sendSummary()
```

Learn more about [media tracking types](https://docs.tealium.com/platforms/getting-started-mobile/media/#trackingtype).


### `skipAd()`

The user skipped the current ad.

```swift
mediaSession.skipAd()
```


### `skipChapter()`

The user skipped the chapter.

```swift
mediaSession.skipChapter()
```

### `startAd()`

The ad started. Call the [`endAd()`](#endad) method when the ad completes.

```swift
mediaSession.startAd(_ ad: Ad)
```

| Parameter | Type               | Description    |
|:----------|:-------------------|:---------------|
| `ad`      | [`Ad`](#struct-ad) | The ad object. |

Example:
```swift
let ad = Ad(name = "Ad 1")
session.startAd(ad)
```

### `startAdBreak()`

The ad break started. Call the [`endAdBreak()`](#endadbreak) method when the ad break completes.

```swift
mediaSession.startAdBreak(_ break: AdBreak)
```

| Parameter | Type                         | Description     |
|:----------|:-----------------------------|:----------------|
| `break`   | [`AdBreak`](#struct-adbreak) | Ad break object |

Example:

```swift
let adBreak = AdBreak(name = "Ad Break 1")
mediaSession.startAdBreak(adBreak)
```

### `startBuffer()`

The buffer started. Call the [`endBuffer()`](#endbuffer) method when the buffering completes.

```swift
mediaSession.startBuffer()
```


### `startChapter()`

The chapter started. Call the [`endChapter()`](#endchapter) method when the chapter completes.

```swift
mediaSession.startChapter(_ chapter: Chapter)
```

| Parameter | Type                         | Description          |
|:----------|:-----------------------------|:---------------------|
| `chapter` | [`Chapter`](#struct-chapter) | Chapter segment name |

Example:

```swift
let chapterOne = Chapter(name = "Chapter 1")
mediaSession.startChapter(chapterOne)
```


### `startSeek()`

The user started seeking. Call the [`endSeek()`](#endseek) method when seeking completes.

```swift
mediaSession.startSeek(at position: Int)
```

| Parameter  | Type  | Description                                                      |
|:-----------|:------|:-----------------------------------------------------------------|
| `position` | `Int` | The index position in the media, in seconds, where seek started. |


Example:

```swift
mediaSession.startSeek(at position: 10)
```

### `startSession()`

The session started. Call the [`endSession()`](#endsession) method when session completes.

```swift
mediaSession.startSession()
```

## Class: `MediaContent`

The `MediaContent` class creates an media content object.

```swift
let media = MediaContent(
  uuid: MEDIA_UUID,
  name: MEDIA_NAME,
  streamType: MEDIA_STREAM_TYPE,
  mediaType: MEDIA_TYPE,   
  qoe: MEDIA_QOE,
  trackingType: MEDIA_TRACKING_TYPE,
  milestoneInterval: MEDIA_MILESTONE,
  contentCompletePercentage: MEDIA_CONTENT_COMPLETE_PERCENTAGE,
  startTime = MEDIA_START_TIME,
  state = MEDIA_STATE,
  customID = MEDIA_CUSTOM_ID,
  duration: MEDIA_DURATION,
  playerName: MEDIA_PLAYER_NAME,
  channelName: MEDIA_CHANNEL_NAME,
  metadata: MEDIA_METADATA,
  milestone: MEDIA_MILESTONE,
  summary: MEDIA_SUMMARY,
  adBreaks: MEDIA_AD_BREAKS,
  ads: MEDIA_ADS,
  chapters: MEDIA_CHAPTERS
)
```

| Variable Name               | Type                                                             | Description                                                              | Required |
|:----------------------------|:-----------------------------------------------------------------|:-------------------------------------------------------------------------|:---------|
| `uuid`                      | `UUID`                                                           | The ad universally unique identifier.                                    |          |
| `name`                      | `String`                                                         | The name of the media content.                                           | Yes      |
| `streamType`                | [`StreamType`](https://docs.tealium.com/platforms/getting-started-mobile/media/#streamtype)     | The type of media stream.                                                | Yes      |
| `mediaType`                 | [`MediaType`](https://docs.tealium.com/platforms/getting-started-mobile/media/#mediatype)       | The type of media (video or audio).                                      | Yes      |
| `qoe`                       | [`QoE`](https://docs.tealium.com/platforms/getting-started-mobile/media/#quality-of-experience) | The quality of experience bitrate value.                                 | Yes      |
| `trackingType`              | [`TrackingType`](https://docs.tealium.com/platforms/getting-started-mobile/media/#trackingtype) | The level of event tracking. (default: `.fullPlayback`)                  | Yes      |
| `milestoneInterval`         | `Double`                                                         | The milestone interval value. (default: `5.0`)                           |          |
| `contentCompletePercentage` | `Double`                                                         | The content complete percentage value.                                   |          |
| `state`                     | [`PlayerState`](https://docs.tealium.com/platforms/getting-started-mobile/media/#state)         | The media player state type.                                             |          |
| `customId`                  | `String`                                                         | The custom identifier name.                                              |          |
| `duration`                  | `Int`                                                            | The media duration, in seconds, such as `130`                            |          |
| `playerName`                | `String`                                                         | The media player name.                                                   |          |
| `channelName`               | `String`                                                         | The media channel name.                                                  |          |
| `metadata`                  | `[String: Any]`                                                  | Additional media [metadata](https://docs.tealium.com/platforms/getting-started-mobile/media/#metadata). |          |
| `summary`                   | `Summary`                                                        | A media `Summary` object.                                                |          |
| `adBreaks`                  | `[AdBreak]()`                                                    | Array of `AdBreak` objects.                                              |          |
| `ads`                       | `[Ad]()`                                                         | Array of `Ad` objects.                                                   |          |
| `chapters`                  | `[Chapter]()`                                                    | Array of `Chapter` objects.                                              |          |

## Struct: `Ad`

The `Ad` struct creates an ad object.

```swift
let ad = Ad(
  uuid: MEDIA_AD_UUID,
  name: MEDIA_AD_NAME,
  id: MEDIA_AD_ID,
  duration: MEDIA_AD_DURATION,
  position: MEDIA_AD_POSITION,
  advertiser: MEDIA_AD_ADVERTISER,
  creativeId: MEDIA_AD_CREATIVE_ID,
  campaignId: MEDIA_AD_CAMPAIGN_ID,
  placementId: MEDIA_AD_PLACEMENT_ID,
  siteId: MEDIA_AD_SITE_ID,
  creativeUrl: MEDIA_AD_CREATIVE_URL,
  numberOfLoads: MEDIA_AD_LOAD,
  pod: MEDIA_AD_POD,
  playerName: MEDIA_AD_PLAYER_NAME
)
```

| Parameter       | Type     | Description                                       | Required |
|:----------------|:---------|:--------------------------------------------------|:---------|
| `uuid`          | `UUID`   | The ad universally unique identifier.             |          |
| `name`          | `String` | The name of the ad.                               | Yes      |
| `id`            | `String` | The ad unique identifier.                         |          |
| `duration`      | `Double` | The ad duration length in seconds.                |          |
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

## Struct: `AdBreak`

The `AdBreak` struct creates an ad break object.

```swift
let adBreak = AdBreak(
  uuid: MEDIA_AD_BREAK_UUID,
  name: MEDIA_AD_BREAK_NAME,
  id: MEDIA_AD_BREAK_ID,
  duration: MEDIA_AD_BREAK_DURATION,
  position: MEDIA_AD_BREAK_POSITION,
  startTime: MEDIA_AD_BREAK_START_TIME
)
```

| Parameter   | Type     | Description                                             | Required |
|:------------|:---------|:--------------------------------------------------------|:---------|
| `uuid`      | `UUID`   | The ad break universally unique identifier.             |          |
| `name`      | `String` | The ad break name.                                      | Yes      |
| `id`        | `String` | The ad break unique identifier.                         |          |
| `duration`  | `Double` | The ad break duration length in seconds.                |          |
| `index`     | `Int`    | The index of the ad break.                              |          |
| `position`  | `Int`    | The current index position of the ad break, in seconds. |          |
| `startTime` | `Date`   | The ad break start time.                                |          |

## Struct: `Chapter`

The `Chapter` struct creates a chapter object.

```swift
let chapterObject = Chapter(
  name: MEDIA_CHAPTER_NAME,
  duration: MEDIA_CHAPTER_DURATION,
  position: MEDIA_CHAPTER_POSITION,
  startTime: MEDIA_CHAPTER_START_TIME,
  metadata: MEDIA_CHAPTER_METADATA
)
```

The following are the `Chapter` object parameters. Parameters must be in order if you are not using parameter names, such as `duration:`,  when creating the object.

| Variable Name | Type            | Description                                                                      | Required |
|:--------------|:----------------|:---------------------------------------------------------------------------------|:---------|
| `name`        | `String`        | The name of the chapter.                                                         | Yes      |
| `duration`    | `Double`        | The chapter duration, in seconds, such as `130`                                  |          |
| `position`    | `Int`           | The chapter position index.                                                      |          |
| `startTime`   | `Date`          | The chapter start time.                                                          |          |
| `metadata`    | `[String: Any]` | Additional chapter media [metadata](https://docs.tealium.com/platforms/getting-started-mobile/media/#metadata). |          |
