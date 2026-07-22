---
title: Media Module
description: Provides tracking data for your media events.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/media/
---
The Media module tracks streaming media in apps through the use of custom events. Learn more about [media tracking](https://docs.tealium.com/platforms/getting-started-mobile/media/).

## Sample App

Explore the Android (Kotlin) [Media sample app](https://github.com/Tealium/tealium-kotlin/tree/master/mobile) to help familiarize yourself with the Tealium library, tracking methods, and best practice implementation.

## Install

Install the Media module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:  
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. In your project module's `build.gradle` file, add the Maven dependencies for the Tealium library and Crash Reporter:  
      ```groovy
      dependencies {
          implementation 'com.tealium:kotlin-core:1.6.0'
          implementation 'com.tealium:kotlin-media:1.1.1'
      }
      ```

### Manual

To install the module manually:

1. Download the Tealium [Media module](https://github.com/Tealium/tealium-kotlin/tree/master/media).

2. Copy the file `tealium-kotlin.media-1.1.1.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
          implementation(name:'tealium-kotlin.media-1.1.1', ext:'aar')
      }
      ```

## Initialize

To initialize the Media module, create a [`MediaContent`](https://docs.tealium.com/platforms/android-kotlin/api/media/#class-mediacontent) object.

For example:  

```kotlin
val mediaContent: MediaContent = MediaContent(
  name = "What is the Tealium Customer Data Hub?",
  trackingType = TrackingType.MILESTONE,
  streamType = StreamType.DVOD,
  mediaType = MediaType.VIDEO,
  qoe = QoE(1500),
  duration = 130
)
```  

Learn more about [implementing the Media module](https://docs.tealium.com/platforms/getting-started-mobile/media/#implement).


#### Metadata

To add optional metadata to the session:  
```kotlin
metadata = ["artist": "Various", "duration": "45:00"]
```

To add chapter metadata:   
```kotlin
metadata = ["artist": "Aerosmith", "track": "5"]
```

To add merged metadata:  
```kotlin
metadata = ["artist": "Aerosmith", "track": "5", "duration": "45:00"]
```

Learn more about [metadata](https://docs.tealium.com/platforms/getting-started-mobile/media/#metadata).

## Track

After installing the Media module, track your media events.

### Media Session

To start tracking a media session, call the [`startSession()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#startsession) method. To stop tracking a media session, call the [`endSession()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#endsession) method:  

```kotlin
tealium?.media?.startSession(mediaContent)
//...
tealium?.media?.endSession()
```

Learn more about [tracking sessions](https://docs.tealium.com/platforms/getting-started-mobile/media/#media-sessions).

### Player Events

To track media player events such as play and pause, call the appropriate [player event methods](https://docs.tealium.com/platforms/getting-started-mobile/media/#playerevents). Each media player event sends a `tealium_event` variable to the data layer when called.

To track when the media is played, call the [`play()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#play) method:   
```kotlin
tealium?.media?.play()
```

To track when the media is paused, call the [`pause()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#pause) method:   
```kotlin
tealium?.media?.pause()
```

Learn more about [tracking player events](https://docs.tealium.com/platforms/getting-started-mobile/media/#player-events).


### Chapters

To track a chapter segments in the media session, create a [`Chapter`](https://docs.tealium.com/platforms/android-kotlin/api/media/#class-chapter) object and pass it to the [`startChapter()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#startchapter) method. To stop tracking the chapter, call the [`endChapter()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#endchapter) method.

For example:  

```kotlin
val chapter1 = Chapter(name = "Chapter 1", duration = 120)
tealium?.media?.startChapter(chapter1)
// ...
tealium?.media?.endChapter()
```

Learn more about [tracking chapters](https://docs.tealium.com/platforms/getting-started-mobile/media/#chapters).

### Ads

To track the start of an ad break, create an [`AdBreak`](https://docs.tealium.com/platforms/android-kotlin/api/media/#class-adbreak) object and pass it to the [`startAdBreak()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#startadbreak) method. To track the start of an ad within the ad break, create an [`Ad`](https://docs.tealium.com/platforms/android-kotlin/api/media/#class-ad) object and pass it to the [`startAd()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#startad) method.

To track the end of an ad, call the [`endAd()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#endad) method. To track the end of the ad break, call the [`endAdBreak()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#endadbreak) method.


```kotlin
val adBreak = AdBreak(name = "Ad Break 1")
tealium?.media?.startAdBreak(adBreak)

val ad1 = Ad("Ad 1")
tealium?.media?.startAd(ad1)
tealium?.media?.endAd()

val ad2 = Ad("Ad 2")
tealium?.media?.startAd(ad2)
tealium?.media?.endAd()

tealium?.media?.endAdBreak()
```

Learn more about [tracking ads](https://docs.tealium.com/platforms/getting-started-mobile/media/#ads).


## Examples

### Chapters and Ads

The following example tracks media content with chapters and ads:

```kotlin
val mediaContent: MediaContent = MediaContent(
  name = "What is the Tealium Customer Data Hub?",
  trackingType = TrackingType.FULL_PLAYBACK,
  streamType = StreamType.VOD,
  mediaType = MediaType.VIDEO,
  qoe = QoE(1500),
  duration = 114
)

tealium?.media?.startSession(mediaContent)
tealium?.media?.startAdBreak(AdBreak("Ad Break 1"))
tealium?.media?.startAd(Ad("Ad  1"))
// ...
tealium?.media?.endAd()
tealium?.media?.startAd(Ad("Ad  2"))
tealium?.media?.endAd()
tealium?.media?.endAdBreak()
tealium?.media?.startChapter(Chapter("Chapter 1"))
tealium?.media?.endChapter()
tealium?.media?.startAdBreak(AdBreak("Ad Break 2"))
tealium?.media?.startAd(Ad("Ad  3"))
// ...
tealium?.media?.endAd()
tealium?.media?.endAdBreak()
tealium?.media?.startChapter(Chapter("Chapter 2"))
tealium?.media?.endChapter()
tealium?.media?.startChapter(Chapter("Chapter 3"))
tealium?.media?.startBuffer()
tealium?.media?.endBuffer()
tealium?.media?.endChapter()
tealium?.media?.endContent()
tealium?.media?.endSession()
```

### Session Abandonment

The following example shows when the user abandons the session, the app is backgrounded and media stops playing. With the Media module enabled, the [`endSession()`](https://docs.tealium.com/platforms/android-kotlin/api/media/#endsession) method is triggered after 1 minute before the session is terminated. When the user opens the app again, the media session resumes.

```kotlin
val mediaContent: MediaContent = MediaContent(
  name = "What is the Tealium Customer Data Hub?",
  trackingType = TrackingType.FULL_PLAYBACK,
  streamType = StreamType.VOD,
  mediaType = MediaType.VIDEO,
  qoe = QoE(1500),
  duration = 114
)
tealium?.media?.startSession(mediaContent)
tealium?.media?.startAdBreak(AdBreak("Ad Break 1"))
tealium?.media?.startAd(Ad("Ad 1"))
// ...
tealium?.media?.endAd()
tealium?.media?.startAd(Ad("Ad 2"))
tealium?.media?.endAd()
tealium?.media?.endAdBreak()
tealium?.media?.play()
// app goes into background and media does not continue playing
tealium?.media?.pause()
// Tealium's background media tracking is enabled, so the endSession is triggered after 1 minute
// User opens app again, and media continues
tealium?.media?.resumeSession() // resume event
let adBreak = AdBreak("Ad Break 2")
tealium?.media?.startAdBreak(adBreak)
// User closes app - session abandoned (no endContent event)
tealium?.media?.endSession() // end of session
```
