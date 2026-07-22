---
title: メディア
description: Android（Kotlin）用のTealiumが提供するMediaクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/media/
---
## クラス: Media

`Media`クラスは、カスタムイベントを使用してアプリ内でストリーミングメディアをトラッキングするためのメソッドを提供します。[メディアトラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/)について詳しくはこちらをご覧ください。

以下は、Tealium Kotlinの`Media`クラスでよく使用されるメソッドの概要です。

| メソッド                                      | 説明                                         |
|:--------------------------------------------|:--------------------------------------------|
| [`clickAd()`](#clickad)                     | 現在再生中の広告がクリックされました。       |
| [`custom()`](#custom)                       | カスタムイベントステータスをデータレイヤーに送信します。 |
| [`endAd()`](#endad)                         | 広告が終了しました。                         |
| [`endAdBreak()`](#endadbreak)               | 広告ブレイクが終了しました。                   |
| [`endBuffer()`](#endbuffer)                 | バッファが終了しました。                       |
| [`endChapter()`](#endchapter)               | 章が終了しました。                             |
| [`endSeek()`](#endseek)                     | ユーザーがシークを終了しました。                 |
| [`endSession()`](#endsession)               | セッションが終了しました（広告とコンテンツを含む）。 |
| [`pause()`](#pause)                         | ユーザーがメディアを一時停止しました。           |
| [`ping()`](#ping)                           | インターバルイベントをデータレイヤーに送信します。 |
| [`play()`](#play)                           | メディアコンテンツの再生が開始されました。       |
| [`resumeSession()`](#resumesession)         | セッションが再開されました。                     |
| [`sendMilestone()`](#sendmilestone)         | マイルストーンデータをデータレイヤーに送信します。 |
| [`sendSummary()`](#sendsummary)             | サマリーデータをデータレイヤーに送信します。       |
| [`skipAd()`](#skipad)                       | ユーザーが現在の広告をスキップしました。         |
| [`skipChapter()`](#skipchapter)             | ユーザーが章をスキップしました。                 |
| [`startAdBreak()`](#startadbreak)           | 広告ブレイクが開始されました。                   |
| [`startAd()`](#startad)                     | 広告が開始されました。                         |
| [`startBuffer()`](#startbuffer)             | バッファが開始されました。                       |
| [`startChapter()`](#startchapter)           | 章が開始されました。                           |
| [`startSeek()`](#startseek)                 | ユーザーがシークを開始しました。                 |
| [`startSession()`](#startsession)           | セッションが開始されました。                     |
| [`updatePlayerState()`](#updateplayerstate) | プレーヤーの状態の開始または終了。               |
| [`updateQOE()`](#updateqoe)                 | クオリティオブエクスペリエンスのビットレート値を構成します。 |

### `clickAd()`

現在再生中の広告がクリックされました。

```java
tealium?.media?.clickAd(event)
```

### `custom()`

カスタムイベントステータスをデータレイヤーに送信します。

```java
tealium?.media?.custom(name)
```

| パラメーター | タイプ     | 説明            |
|:----------|:---------|:-----------------------|
| `name`    | `String` | カスタムイベント名。 |

### `endAd()`

広告が終了しました。

```java
tealium?.media?.endAd()
```

### `endAdBreak()`

現在のセッションの最新の広告ブレイクが終了します。現在の広告ブレイクでのみ有効です。

```java
tealium?.media?.endAdBreak()
```

### `endBuffer()`

バッファが終了しました。

```java
tealium?.media?.endBuffer()
```

### `endChapter()`

章が終了しました。

```java
tealium?.media?.endChapter()
```

### `endSeek()`

ユーザーがシークを終了しました。指定された位置でシークが終了したことを記録します。

```java
tealium?.media?.endSeek(position)
```

| パラメーター  | タイプ  | 説明                                                    |
|:-----------|:------|:-------------------------------------------------------|
| `position` | `Int` | シークが終了したメディア内の位置（秒単位）のインデックス位置。 |

例:

```java
tealium?.media?.startSeek(10)
```

### `endSession()`

セッションが終了しました（広告とコンテンツを含む）。

```java
tealium?.media?.endSession()
```

### `pause()`

ユーザーがメディアを一時停止しました。

```java
tealium?.media?.pause()
```

### `ping()`

インターバルイベントをデータレイヤーに送信します。このメソッドは、`MediaContent`オブジェクトのトラッキングタイプが`INTERVAL`または`INTERVAL_MILESTONE`に構成されている場合、自動的に10秒ごとに呼び出されます。

```java
tealium?.media?.ping()
```

[メディアトラッキングタイプ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype)について詳しくはこちらをご覧ください。

### `play()`

メディアコンテンツの再生が開始されました。

```java
tealium?.media?.play()
```

### `resumeSession()`

セッションが再開されました。

```java
tealium?.media?.startSession()
```

### `sendMilestone()`

マイルストーンデータをデータレイヤーに送信します。このメソッドは、コンテンツの再生率に基づいて自動的に呼び出されます。`MediaContent`オブジェクトのトラッキングタイプが`MILESTONE`または`INTERVAL_MILESTONE`に構成されている場合です。

```java
tealium?.media?.sendMilestone()
```

マイルストーンの値:

| メディア再生率 | マイルストーン値 |
|:---------------|:----------------|
| 8.0 - 12.0     | `10%`           |
| 23.0 - 27.0    | `25%`           |
| 48.0 - 52.0    | `50%`           |
| 73.0 - 77.0    | `75%`           |
| 88.0 - 92.0    | `90%`           |
| 97.0 - 100.0   | `100%`          |

[メディアトラッキングタイプ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype)について詳しくはこちらをご覧ください。

### `sendSummary()`

サマリーデータをデータレイヤーに送信します。このメソッドは、`MediaContent`オブジェクトのトラッキングタイプが`SUMMARY`に構成されている場合、`endSession()`で自動的に呼び出されます。

```java
tealium?.media?.sendSummary()
```

[メディアトラッキングタイプ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype)について詳しくはこちらをご覧ください。

### `skipAd()`

ユーザーが現在の広告をスキップしました。

```java
tealium?.media?.skipAd()
```

### `skipChapter()`

ユーザーが章をスキップしました。

```java
tealium?.media?.skipChapter()
```

### `startAd()`

広告が開始されました。広告が完了したら[`endAd()`](#endad)メソッドを呼び出します。

```java
tealium?.media?.startAd(ad)
```

| パラメーター | タイプ              | 説明    |
|:----------|:------------------|:-------|
| `ad`      | [`Ad`](#class-ad) | 広告オブジェクト。 |

例:
```java
tealium?.media?.startAd(Ad("広告  1"))
```

### `startAdBreak()`

広告ブレイクが開始されました。広告ブレイクが完了したら[`endAdBreak()`](#endadbreak)メソッドを呼び出します。

```java
tealium?.media?.startAdBreak(break)
```

| パラメーター | タイプ                        | 説明          |
|:----------|:----------------------------|:-------------|
| `break`   | [`AdBreak`](#class-adbreak) | 広告ブレイクオブジェクト。 |

例:

```java
val adBreak = AdBreak(name = "広告ブレイク 1")
tealium?.media?.startAdBreak(adBreak)
```

### `startBuffer()`

バッファが開始されました。バッファリングが完了したら[`endBuffer()`](#endbuffer)メソッドを呼び出します。

```java
tealium?.media?.startBuffer()
```

### `startChapter()`

章が開始されました。章が完了したら[`endChapter()`](#endchapter)メソッドを呼び出します。

```java
tealium?.media?.startChapter(chapter)
```

| パラメーター | タイプ                        | 説明               |
|:----------|:----------------------------|:------------------|
| `chapter` | [`Chapter`](#class-chapter) | 章セグメント名。 |

例:

```java
tealium?.media?.startChapter(Chapter(name = "章 1"))
```

### `startSeek()`

ユーザーがシークを開始しました。シークが完了したら[`endSeek()`](#endseek)メソッドを呼び出します。

```java
tealium?.media?.startSeek(position)
```

| パラメーター  | タイプ  | 説明                                                      |
|:-----------|:------|:---------------------------------------------------------|
| `position` | `Int` | シークが開始されたメディア内の位置（秒単位）のインデックス位置。 |

例:

```java
tealium?.media?.startSeek(10)
```

### `startSession()`

セッションが開始されました。セッションが完了したら[`endSession()`](#endsession)メソッドを呼び出します。

```java
tealium?.media?.startSession()
```

### `updatePlayerState()`

プレーヤーの状態の開始または終了。

```java
tealium?.media?.updatePlayerState(state)
```

| パラメーター | タイプ             | 説明     |
|:----------|:-----------------|:--------|
| `state`   | `State` 定数 | メディアの状態 |

以下の`State`定数が使用可能です:

| 値                | 説明                    |
|:---------------------|:-------------------------------|
| `CLOSED_CAPTION`     | 閉じたキャプションの状態。     |
| `FULLSCREEN`         | フルスクリーンの状態。        |
| `IN_FOCUS`           | フォーカスされた状態。           |
| `MUTE`               | ミュートの状態。               |
| `PICTURE_IN_PICTURE` | ピクチャインピクチャの状態。 |

例:

```java
tealium?.media?.updatePlayerState(fullscreen)
```

[プレーヤーの状態](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#state)について詳しくはこちらをご覧ください。

### `updateQOE()`

現在のセッションのクオリティオブエクスペリエンスのビットレート値を構成します（キロビット/秒）。

```java
tealium?.media?.updateQOE(rate)
```

| パラメーター | タイプ  | 説明        |
|:----------|:------|:-----------|
| `rate`    | `Int` | ビットレート値。 |

例:

```java
tealium?.media?.updateQOE(1500)
```

## クラス: `MediaContent`

`MediaContent`クラスは、メディアコンテンツオブジェクトを作成します。

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

| 変数名  | タイプ                                                             | 説明                                                              | 必須 |
|:---------------|:-----------------------------------------------------------------|:-------------------------------------------------------------------------|:---------|
| `name`         | `String`                                                         | メディアコンテンツの名前。                                           | Yes      |
| `streamType`   | [`StreamType`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#streamtype)     | メディアストリームのタイプ。                                                | Yes      |
| `mediaType`    | [`MediaType`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#mediatype)       | メディアのタイプ（ビデオまたはオーディオ）。                                      | Yes      |
| `qoe`          | [`QoE`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#quality-of-experience) | クオリティオブエクスペリエンスのビットレート値。                                 | Yes      |
| `trackingType` | [`TrackingType`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#trackingtype) | イベントトラッキングのレベル（デフォルト：`TrackingType.FULL_PLAYBACK`）     | Yes      |
| `state`        | [`PlayerState`](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#state)         | メディアプレーヤーの状態のタイプ。                                             |          |
| `customId`     | `String`                                                         | カスタム識別子名。                                              |          |
| `duration`     | `Int`                                                            | メディアの再生時間（秒単位）（例：`130`）                            |          |
| `playerName`   | `String`                                                         | メディアプレーヤーの名前。                                                   |          |
| `channelName`  | `String`                                                         | メディアチャンネルの名前。                                                  |          |
| `metadata`     | `[String: Any]`                                                  | 追加のメディア[メタデータ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#metadata)。 |          |

## クラス: `Ad`

`Ad`クラスは、広告オブジェクトを作成します。

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

| パラメーター       | タイプ     | 説明                                       | 必須 |
|:----------------|:---------|:--------------------------------------------|:---------|
| `name`          | `String` | 広告の名前                                   | Yes      |
| `duration`      | `Double` | 広告の再生時間（秒単位）（例：`130`）        |          |
| `position`      | `Int`    | 広告の現在のインデックス位置（秒単位）         |          |
| `advertiser`    | `String` | 広告の広告主                                |          |
| `creativeId`    | `String` | 広告のクリエイティブ識別子                      |          |
| `campaignId`    | `String` | 広告のキャンペーン識別子                      |          |
| `placementId`   | `String` | 広告の配置識別子                             |          |
| `siteId`        | `String` | 広告のサイト識別子                            |          |
| `creativeUrl`   | `String` | 広告のクリエイティブURL                        |          |
| `numberOfLoads` | `Int`    | 広告の読み込み回数                            |          |
| `pod`           | `String` | 広告のポッド                                |          |
| `playerName`    | `String` | 広告のプレーヤー名                            |          |

## クラス: `AdBreak`

`AdBreak`クラスは、広告ブレイクオブジェクトを作成します。

```java
val adBreak = AdBreak(
  id = MEDIA_AD_BREAK_ID,
  name = MEDIA_AD_BREAK_NAME,
  duration = MEDIA_AD_BREAK_DURATION,
  index = MEDIA_AD_BREAK_INDEX,
  position = MEDIA_AD_BREAK_POSITION
)
```

| パラメーター  | タイプ     | 説明                                             | 必須 |
|:-----------|:---------|:------------------------------------------------|:---------|
| `id`       | `String` | 広告ブレイクの一意の識別子                         |          |
| `name`     | `String` | 広告ブレイクの名前                                 | Yes      |
| `duration` | `Double` | 広告ブレイクの再生時間（秒単位）（例：`130`）        |          |
| `index`    | `Int`    | 広告ブレイクのインデックス                          |          |
| `position` | `Int`    | 広告ブレイクの現在のインデックス位置（秒単位）         |          |


## クラス: `Chapter`

`Chapter`クラスは、章オブジェクトを作成します。

```java
val chapterObject = Chapter(
  name = MEDIA_CHAPTER_NAME,
  duration = MEDIA_CHAPTER_DURATION,
  position = MEDIA_CHAPTER_POSITION,
  metadata = MEDIA_CHAPTER_METADATA
)
```

以下は、`Chapter`オブジェクトのパラメーターです。パラメーター名を使用しない場合は、パラメーターを順番に指定する必要があります（例：`duration =`）。

| 変数名 | タイプ            | 説明                                                                      | 必須 |
|:--------------|:----------------|:-------------------------------------------------------------------------|:---------|
| `name`        | `String`        | 章の名前。                                                                 | Yes      |
| `duration`    | `Double`        | 章の再生時間（秒単位）（例：`130`）                                        |          |
| `position`    | `Int`           | 章の位置インデックス。                                                      |          |
| `metadata`    | `[String: Any]` | 追加の章のメディア[メタデータ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#metadata)。 |          |

## クラス: `Ad`

`Ad`クラスは、広告オブジェクトを作成します。

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

| パラメーター       | タイプ     | 説明                                       | 必須 |
|:----------------|:---------|:--------------------------------------------|:---------|
| `name`          | `String` | 広告の名前                                   | Yes      |
| `duration`      | `Double` | 広告の再生時間（秒単位）（例：`130`）        |          |
| `position`      | `Int`    | 広告の現在のインデックス位置（秒単位）         |          |
| `advertiser`    | `String` | 広告の広告主                                |          |
| `creativeId`    | `String` | 広告のクリエイティブ識別子                      |          |
| `campaignId`    | `String` | 広告のキャンペーン識別子                      |          |
| `placementId`   | `String` | 広告の配置識別子                             |          |
| `siteId`        | `String` | 広告のサイト識別子                            |          |
| `creativeUrl`   | `String` | 広告のクリエイティブURL                        |          |
| `numberOfLoads` | `Int`    | 広告の読み込み回数                            |          |
| `pod`           | `String` | 広告のポッド                                |          |
| `playerName`    | `String` | 広告のプレーヤー名                            |          |

## クラス: `AdBreak`

`AdBreak`クラスは、広告ブレイクオブジェクトを作成します。

```java
val adBreak = AdBreak(
  id = MEDIA_AD_BREAK_ID,
  name = MEDIA_AD_BREAK_NAME,
  duration = MEDIA_AD_BREAK_DURATION,
  index = MEDIA_AD_BREAK_INDEX,
  position = MEDIA_AD_BREAK_POSITION
)
```

| パラメーター  | タイプ     | 説明                                             | 必須 |
|:-----------|:---------|:------------------------------------------------|:---------|
| `id`       | `String` | 広告ブレイクの一意の識別子                         |          |
| `name`     | `String` | 広告ブレイクの名前                                 | Yes      |
| `duration` | `Double` | 広告ブレイクの再生時間（秒単位）（例：`130`）        |          |
| `index`    | `Int`    | 広告ブレイクのインデックス                          |          |
| `position` | `Int`    | 広告ブレイクの現在のインデックス位置（秒単位）         |          |


## クラス: `Chapter`

`Chapter`クラスは、章オブジェクトを作成します。

```java
val chapterObject = Chapter(
  name = MEDIA_CHAPTER_NAME,
  duration = MEDIA_CHAPTER_DURATION,
  position = MEDIA_CHAPTER_POSITION,
  metadata = MEDIA_CHAPTER_METADATA
)
```

以下は、`Chapter`オブジェクトのパラメーターです。パラメーター名を使用しない場合は、パラメーターを順番に指定する必要があります（例：`duration =`）。

| 変数名 | タイプ            | 説明                                                                      | 必須 |
|:--------------|:----------------|:-------------------------------------------------------------------------|:---------|
| `name`        | `String`        | 章の名前。                                                                 | Yes      |
| `duration`    | `Double`        | 章の再生時間（秒単位）（例：`130`）                                        |          |
| `position`    | `Int`           | 章の位置インデックス。                                                      |          |
| `metadata`    | `[String: Any]` | 追加の章のメディア[メタデータ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#metadata)。 |          |
