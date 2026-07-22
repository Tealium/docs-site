---
title: MediaSession
description: Tealiumが提供するiOS（Swift）向けのMediaクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/
---
## クラス: Media

`MediaSession`クラスは、カスタムイベントを使用してアプリ内でストリーミングメディアをトラッキングするためのメソッドを提供します。[メディアトラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/)について詳しくはこちらをご覧ください。

以下は、Tealium iOS（Swift）の`MediaSession`クラスの一般的に使用されるメソッドの概要です。

| メソッドまたはプロパティ            | 説明                                             |
|:------------------------------------|:------------------------------------------------|
| [`bitrate`](#bitrate)               | クオリティオブエクスペリエンスのビットレート値を構成します。 |
| [`clickAd()`](#clickad)             | 現在再生中の広告がクリックされました。                 |
| [`custom()`](#custom)               | カスタムイベントステータスをデータレイヤーに送信します。   |
| [`endAd()`](#endad)                 | 広告が終了しました。                                   |
| [`endAdBreak()`](#endadbreak)       | 広告ブレイクが終了しました。                             |
| [`endBuffer()`](#endbuffer)         | バッファリングが終了しました。                             |
| [`endChapter()`](#endchapter)       | 章が終了しました。                                     |
| [`endSeek()`](#endseek)             | ユーザーがシークを終了しました。                           |
| [`endSession()`](#endsession)       | 広告とコンテンツを含むセッションが終了しました。             |
| [`pause()`](#pause)                 | ユーザーがメディアを一時停止しました。                       |
| [`ping()`](#ping)                   | インターバルイベントをデータレイヤーに送信します。           |
| [`play()`](#play)                   | メディアコンテンツが再生を開始しました。                     |
| [`playerState`](#playerstate)       | プレーヤーの状態の開始または終了。                         |
| [`resumeSession()`](#resumesession) | セッションが再開されました。                               |
| [`sendMilestone()`](#sendmilestone) | マイルストーンデータをデータレイヤーに送信します。             |
| [`sendSummary()`](#sendsummary)     | サマリーデータをデータレイヤーに送信します。                 |
| [`skipAd()`](#skipad)               | 現在の広告がスキップされました。                           |
| [`skipChapter()`](#skipchapter)     | 章がスキップされました。                                 |
| [`startAdBreak()`](#startadbreak)   | 広告ブレイクが開始されました。                             |
| [`startAd()`](#startad)             | 広告が開始されました。                                   |
| [`startBuffer()`](#startbuffer)     | バッファリングが開始されました。                             |
| [`startChapter()`](#startchapter)   | 章が開始されました。                                     |
| [`startSeek()`](#startseek)         | ユーザーがシークを開始しました。                             |
| [`startSession()`](#startsession)   | セッションが開始されました。                               |


### `bitrate()`

現在のセッションのクオリティオブエクスペリエンスのビットレート値（`Int`）をキロビット/秒（kbps）で構成します。

| プロパティ  | 型    | 説明        |
|:----------|:------|:-----------|
| `bitrate` | `Int` | ビットレート値 |

```swift
mediaSession.bitrate = BITRATE_VALUE
```


### `clickAd()`

現在再生中の広告がクリックされました。

```swift
mediaSession.clickAd()
```

### `custom()`

カスタムイベントステータスをデータレイヤーに送信します。

```swift
mediaSession.custom(name)
```

| パラメータ | 型       | 説明            |
|:----------|:---------|:---------------|
| `name`    | `String` | カスタムイベント名 |



### `endAd()`

広告が終了しました。

```swift
mediaSession.endAd()
```


### `endAdBreak()`

広告ブレイクが終了しました。

```swift
mediaSession.endAdBreak()
```


### `endBuffer()`

バッファリングが終了しました。

```swift
mediaSession.endBuffer()
```


### `endChapter()`

章が終了しました。

```swift
mediaSession.endChapter()
```

### `endSeek()`

ユーザーがシークを終了しました。シークが終了した位置を記録します。

```swift
mediaSession.endSeek(at position: Int)
```

| パラメータ  | 型    | 説明                                                    |
|:-----------|:------|:-------------------------------------------------------|
| `position` | `Int` | シークが終了したメディア内の位置（秒単位）のインデックス位置。 |

例:

```swift
mediaSession.endSeek(at position: 10)
```

### `endSession()`

広告とコンテンツを含むセッションが終了しました。

```swift
mediaSession.endSession()
```

### `pause()`

ユーザーがメディアを一時停止しました。

```swift
mediaSession.pause()
```

### `ping()`

インターバルイベントをデータレイヤーに送信します。このメソッドは、`MediaContent`オブジェクトのトラッキングタイプが`interval`または`intervalMilestone`に構成されている場合、自動的に10秒ごとに呼び出されます。

```swift
mediaSession.ping()
```

[メディアトラッキングタイプ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype)について詳しくはこちらをご覧ください。

### `play()`

メディアコンテンツが再生を開始しました。

```swift
mediaSession.play()
```

### `playerstate`

プレーヤーの状態の開始または終了。

```swift
mediaSession.playerState = PLAYER_STATE
```

以下の`State`定数が使用可能です:

| 値              | 説明                    |
|:-------------------|:-------------------------------|
| `closedCaption`    | クローズドキャプションの状態タイプ     |
| `fullscreen`       | フルスクリーンの状態タイプ        |
| `inFocus`          | フォーカス中の状態タイプ           |
| `mute`             | ミュートの状態タイプ               |
| `pictureInPicture` | ピクチャインピクチャの状態タイプ |

例:

```swift
mediaSession.playerState = .mute
```

[プレーヤーの状態](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#state)について詳しくはこちらをご覧ください。

### `resumeSession()`

セッションが再開されました。

```swift
mediaSession.resumeSession()
```

### `sendMilestone()`

マイルストーンイベントをデータレイヤーに送信します。このメソッドは、コンテンツの再生率に基づいて自動的に呼び出されます。`MediaContent`オブジェクトのトラッキングタイプが`milestone`または`intervalMilestone`に構成されている場合。

```swift
mediaSession.sendMilestone(_ milestone: Milestone)
```

| パラメータ   | 型          | 説明                   |
|:------------|:------------|:----------------------|
| `milestone` | `Milestone` | コンテンツの再生率のパーセント |

マイルストーンの値:

| メディアの再生率 | マイルストーンの値 |
|:---------------|:----------------|
| 8.0 - 12.0     | `10%`           |
| 23.0 - 27.0    | `25%`           |
| 48.0 - 52.0    | `50%`           |
| 73.0 - 77.0    | `75%`           |
| 88.0 - 92.0    | `90%`           |
| 97.0 - 100.0   | `100%`          |

[メディアトラッキングタイプ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype)について詳しくはこちらをご覧ください。

### `sendSummary()`

サマリーデータをデータレイヤーに送信します。このメソッドは、`MediaContent`オブジェクトのトラッキングタイプが`summary`に構成されている場合、`endSession()`で自動的に呼び出されます。

```swift
mediaSession.sendSummary()
```

[メディアトラッキングタイプ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype)について詳しくはこちらをご覧ください。


### `skipAd()`

現在の広告がスキップされました。

```swift
mediaSession.skipAd()
```


### `skipChapter()`

章がスキップされました。

```swift
mediaSession.skipChapter()
```

### `startAd()`

広告が開始されました。広告が完了したら[`endAd()`](#endad)メソッドを呼び出します。

```swift
mediaSession.startAd(_ ad: Ad)
```

| パラメータ | 型               | 説明    |
|:----------|:-------------------|:-------|
| `ad`      | [`Ad`](#struct-ad) | 広告オブジェクト |

例:
```swift
let ad = Ad(name = "Ad 1")
session.startAd(ad)
```

### `startAdBreak()`

広告ブレイクが開始されました。広告ブレイクが完了したら[`endAdBreak()`](#endadbreak)メソッドを呼び出します。

```swift
mediaSession.startAdBreak(_ break: AdBreak)
```

| パラメータ | 型                         | 説明     |
|:----------|:-----------------------------|:--------|
| `break`   | [`AdBreak`](#struct-adbreak) | 広告ブレイクオブジェクト |

例:

```swift
let adBreak = AdBreak(name = "Ad Break 1")
mediaSession.startAdBreak(adBreak)
```

### `startBuffer()`

バッファリングが開始されました。バッファリングが完了したら[`endBuffer()`](#endbuffer)メソッドを呼び出します。

```swift
mediaSession.startBuffer()
```


### `startChapter()`

章が開始されました。章が完了したら[`endChapter()`](#endchapter)メソッドを呼び出します。

```swift
mediaSession.startChapter(_ chapter: Chapter)
```

| パラメータ | 型                         | 説明          |
|:----------|:-----------------------------|:-------------|
| `chapter` | [`Chapter`](#struct-chapter) | 章セグメント名 |

例:

```swift
let chapterOne = Chapter(name = "Chapter 1")
mediaSession.startChapter(chapterOne)
```


### `startSeek()`

ユーザーがシークを開始しました。シークが完了したら[`endSeek()`](#endseek)メソッドを呼び出します。

```swift
mediaSession.startSeek(at position: Int)
```

| パラメータ  | 型    | 説明                                                            |
|:-----------|:------|:---------------------------------------------------------------|
| `position` | `Int` | シークが開始されたメディア内の位置（秒単位）のインデックス位置。 |

例:

```swift
mediaSession.startSeek(at position: 10)
```

### `startSession()`

セッションが開始されました。セッションが完了したら[`endSession()`](#endsession)メソッドを呼び出します。

```swift
mediaSession.startSession()
```

## クラス: `MediaContent`

`MediaContent`クラスは、メディアコンテンツオブジェクトを作成します。

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

| 変数名               | 型                                                             | 説明                                                              | 必須 |
|:----------------------------|:-----------------------------------------------------------------|:-----------------------------------------------------------------|:---------|
| `uuid`                      | `UUID`                                                           | 広告の一意の識別子。                                              |          |
| `name`                      | `String`                                                         | メディアコンテンツの名前。                                          | Yes      |
| `streamType`                | [`StreamType`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#streamtype)     | メディアストリームのタイプ。                                        | Yes      |
| `mediaType`                 | [`MediaType`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#mediatype)       | メディアのタイプ（ビデオまたはオーディオ）。                        | Yes      |
| `qoe`                       | [`QoE`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#quality-of-experience) | クオリティオブエクスペリエンスのビットレート値。                  | Yes      |
| `trackingType`              | [`TrackingType`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype) | イベントトラッキングのレベル（デフォルト：`.fullPlayback`）          | Yes      |
| `milestoneInterval`         | `Double`                                                         | マイルストーンのインターバル値（デフォルト：`5.0`）                 |          |
| `contentCompletePercentage` | `Double`                                                         | コンテンツの完了パーセンテージ値。                                  |          |
| `state`                     | [`PlayerState`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#state)         | メディアプレーヤーの状態タイプ。                                    |          |
| `customId`                  | `String`                                                         | カスタム識別子名。                                                  |          |
| `duration`                  | `Int`                                                            | メディアの再生時間（秒単位）（例：`130`）                            |          |
| `playerName`                | `String`                                                         | メディアプレーヤーの名前。                                          |          |
| `channelName`               | `String`                                                         | メディアチャンネルの名前。                                          |          |
| `metadata`                  | `[String: Any]`                                                  | 追加のメディア[メタデータ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#metadata) |          |
| `summary`                   | `Summary`                                                        | メディアの`Summary`オブジェクト。                                    |          |
| `adBreaks`                  | `[AdBreak]()`                                                    | `AdBreak`オブジェクトの配列。                                        |          |
| `ads`                       | `[Ad]()`                                                         | `Ad`オブジェクトの配列。                                             |          |
| `chapters`                  | `[Chapter]()`                                                    | `Chapter`オブジェクトの配列。                                        |          |

## 構造体: `Ad`

`Ad`構造体は、広告オブジェクトを作成します。

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

| パラメータ       | 型     | 説明                                       | 必須 |
|:----------------|:---------|:------------------------------------------|:---------|
| `uuid`          | `UUID`   | 広告の一意の識別子。                       |          |
| `name`          | `String` | 広告の名前。                               | Yes      |
| `id`            | `String` | 広告の一意の識別子。                       |          |
| `duration`      | `Double` | 広告の再生時間（秒単位）。                 |          |
| `position`      | `Int`    | 広告の現在のインデックス位置（秒単位）。   |          |
| `advertiser`    | `String` | 広告の広告主。                             |          |
| `creativeId`    | `String` | 広告のクリエイティブ識別子。               |          |
| `campaignId`    | `String` | 広告のキャンペーン識別子。                 |          |
| `placementId`   | `String` | 広告の配置識別子。                         |          |
| `siteId`        | `String` | 広告のサイト識別子。                       |          |
| `creativeUrl`   | `String` | 広告のクリエイティブURL。                   |          |
| `numberOfLoads` | `Int`    | 広告の読み込み回数。                       |          |
| `pod`           | `String` | 広告のポッド。                             |          |
| `playerName`    | `String` | 広告のプレーヤー名。                       |          |

## 構造体: `AdBreak`

`AdBreak`構造体は、広告ブレイクオブジェクトを作成します。

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

| パラメータ   | 型     | 説明                                             | 必須 |
|:------------|:---------|:------------------------------------------------|:---------|
| `uuid`      | `UUID`   | 広告ブレイクの一意の識別子。                     |          |
| `name`      | `String` | 広告ブレイクの名前。                             | Yes      |
| `id`        | `String` | 広告ブレイクの一意の識別子。                     |          |
| `duration`  | `Double` | 広告ブレイクの再生時間（秒単位）。               |          |
| `index`     | `Int`    | 広告ブレイクのインデックス。                     |          |
| `position`  | `Int`    | 広告ブレイクの現在のインデックス位置（秒単位）。 |          |
| `startTime` | `Date`   | 広告ブレイクの開始時刻。                         |          |

## 構造体: `Chapter`

`Chapter`構造体は、章オブジェクトを作成します。

```swift
let chapterObject = Chapter(
  name: MEDIA_CHAPTER_NAME,
  duration: MEDIA_CHAPTER_DURATION,
  position: MEDIA_CHAPTER_POSITION,
  startTime: MEDIA_CHAPTER_START_TIME,
  metadata: MEDIA_CHAPTER_METADATA
)
```

以下は、`Chapter`オブジェクトのパラメータです。パラメータ名を使用しない場合は、パラメータを順番に指定する必要があります。

| 変数名 | 型            | 説明                                                  | 必須 |
|:--------------|:----------------|:-----------------------------------------------------|:---------|
| `name`        | `String`        | 章の名前。                                            | Yes      |
| `duration`    | `Double`        | 章の再生時間（秒単位）（例：`130`）                    |          |
| `position`    | `Int`           | 章の位置インデックス。                                |          |
| `startTime`   | `Date`          | 章の開始時刻。                                        |          |
| `metadata`    | `[String: Any]` | 追加の章のメディア[メタデータ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#metadata) |          |
