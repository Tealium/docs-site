---
title: Media Module
description: Provides tracking data for your media events.
url: https://docs.tealium.com/platforms/ios-swift/module-list/media/
---
The Media module tracks streaming media in apps through the use of custom events. Learn more about [media tracking](https://docs.tealium.com/platforms/getting-started-mobile/media/).

## Sample App

Explore the iOS (Swift) [Media sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumMediaExample) to help familiarize yourself with the Tealium library, tracking methods, and best practice implementation.

## Install

Install the Media module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0+, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `"Up to next major"` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `Media` module from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**

Learn more about the [Swift Package Manager installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended).

### CocoaPods

To install the Media module with CocoaPods, add the following pod to your Podfile:  
```perl
pod 'tealium-swift/Media'
```

Learn more about the [CocoaPods installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#cocoapods).


### Carthage

To install the Media module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
```perl
TealiumMedia.framework
```

Learn more about [Carthage installation for iOS](https://docs.tealium.com/platforms/ios-swift/install/#carthage).


## Initialize

To initialize the Media module, create a [`MediaContent`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#class-mediacontent) object.

For example:  

```swift
let media = MediaContent(
  name: "What is the Tealium Customer Data Hub?",
  trackingType: .milestone,
  streamType: .vod,
  mediaType: .video,
  qoe: QoE(bitrate: 1500),
  duration: 130
)
```

Learn more about [implementing the Media module](https://docs.tealium.com/platforms/getting-started-mobile/media/#implement).

#### Metadata

To add optional metadata to the media session:  
```swift
metadata: ["artist": "various", "duration": "45:00"]
```

To add chapter metadata:   
```swift
metadata: ["artist": "Aerosmith", "track": "5"]
```

To add merged metadata:  
```swift
metadata: ["artist": "Aerosmith", "track": "5", "duration": "45:00"]
```

Learn more about [metadata](https://docs.tealium.com/platforms/getting-started-mobile/media/#metadata).


## Track

There are many methods and properties available to track media.

### Media Session

To start tracking a media session, call the [`startSession()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#startsession) method. To stop tracking a media session, call the [`endSession()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#endsession) method:  

```swift
let session = tealium?.media?.createSession(from: media)                                
session.startSession()
// ...
session.end()
```

Learn more about [tracking sessions](https://docs.tealium.com/platforms/getting-started-mobile/media/#media-sessions).

### Player Events

To track media player events such as play and pause, call the appropriate [player event methods](https://docs.tealium.com/platforms/getting-started-mobile/media/#playerevents). Each media player event sends a `tealium_event` variable to the data layer when called.

To track when the media is played, call the [`play()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#play) method:   
```swift
session.play()
```

To track when the media is paused, call the [`pause()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#pause) method:   
```swift
session.pause()
```

### Chapters

To track a chapter segments in the media session, create a [`Chapter`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#struct-chapter) object and pass it to the [`startChapter()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#startchapter) method. To stop tracking the chapter, call the [`endChapter()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#endchapter) method

```swift
let chapter1 = Chapter("Chapter 1", 120)
mediaSession.startChapter(chapter1)
// ...
mediaSession.endChapter()
```

Learn more about [tracking chapters](https://docs.tealium.com/platforms/getting-started-mobile/media/#chapters).


### Ads

To track the start of an ad break, create an [`AdBreak`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#struct-adbreak) object and pass it to the [`startAdBreak()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#startadbreak) method. To track the start of an ad within the ad break, create an [`Ad`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#struct-ad) object and pass it to the [`startAd()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#startad) method.

To track the end of an ad, call the [`endAd()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#endad) method. To track the end of the ad break, call the [`endAdBreak()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#endadbreak) method.

```swift
let adBreak = AdBreak("Ad Break 1")
session.endAdBreak(adBreak)

let ad1 = Ad("Ad 1")
session.startAd(ad1)
session.endAd()

let ad2 = Ad("Ad 2")
session.adStart(ad2)
session.endAd()

session.endAdBreak()
```

Learn more about [tracking ads](https://docs.tealium.com/platforms/getting-started-mobile/media/#ads).

## Examples

### Chapters and Ads

The following example tracks media content with chapters and ads:

```swift
let qoe = QoE(bitrate: 1500)

let mediaSession = tealium?.media?.createSession(from: MediaContent(
  name: "What is the Tealium Customer Data Hub?",
  trackingType: .fullPlayback
  streamType: .vod,
  mediaType: .video,
  qoe: qoe,
  duration: 114
))

mediaSession.startSession()
let adBreak = AdBreak("Ad Break 1")
mediaSession.startAdBreak(adBreak)
let ad = Ad("Ad 1")
mediaSession.startAd(ad)
// ...
mediaSession.endAd()
let secondAd = Ad("Ad 2")
mediaSession.startAd(secondAd)
mediaSession.endAd()
mediaSession.endAdBreak()
let chapterOne = Chapter("Chapter 1")
mediaSession.startChapter(chapterOne)
mediaSession.endChapter()
let adBreak = AdBreak("Ad Break 2")
mediaSession.startAdBreak(adBreak)
let thirdAd = Ad("Ad 3")
mediaSession.startAd(thirdAd)
// ...
mediaSession.endAd()
mediaSession.endAdBreak()
let chapterTwo = Chapter("Chapter 2")
mediaSession.startChapter(chapterTwo)
mediaSession.endChapter()

let adBreak = AdBreak("Ad Break 3")
mediaSession.startAdBreak(adBreak)
let fourthAd = Ad("Ad 4")
mediaSession.startAd(fourthAd)
mediaSession.endAd()
let fifthAd = Ad("Ad 5")
mediaSession.startAd(fifthAd)
mediaSession.endAd()
mediaSession.endAdBreak()
let chapterThree = Chapter("Chapter 3")
mediaSession.startChapter(chapterThree)
mediaSession.startBuffer()
mediaSession.endBuffer()
mediaSession.endChapter()
mediaSession.endContent()  // end of all content and ads
mediaSession.endSession()  // end of session
```

### Session Abandonment

The following example shows when the user abandons the session, the app is backgrounded and media stops playing. With the Media module enabled, the [`endSession()`](https://docs.tealium.com/platforms/ios-swift/api/media-session/#endsession) method is triggered after 1 minute before the session is terminated. When the user opens the app again, the media session resumes.

```swift
let media = MediaContent(
  name: "What is the Tealium Customer Data Hub?",
  trackingType: .fullPlayback
  streamType: .vod,
  mediaType: .video,
  qoe: QoE(bitrate: 1500),
  duration: 114
)
let mediaSession = tealium?.media?.createSession(from: media)                                
mediaSession.startSession()
let adBreak = AdBreak("Ad Break 1")
mediaSession.startAdBreak(adBreak)
let ad = Ad("Ad 1")
mediaSession.startAd(ad)
// ...
mediaSession.endAd()
let secondAd = Ad("Ad 2")
mediaSession.startAd(secondAd)
mediaSession.endAd()
mediaSession.endAdBreak()
mediaSession.play()
// app goes into background and media does not continue playing
mediaSession.pause()
// Tealium's background media tracking is enabled, so the endSession is triggered after 1 minute
// User opens app again, and media continues
mediaSession.resumeSession() // resume event
let adBreak = AdBreak("Ad Break 2")
mediaSession.startAdBreak(adBreak)
// User closes app - session abandoned (no endContent event)
mediaSession.endSession() // end of session
```
