---
title: メディアモジュール
description: メディアイベントのトラッキングデータを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/media/
---
メディアモジュールは、カスタムイベントを使用してアプリ内のストリーミングメディアを追跡します。[メディアトラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/)について詳しく学びましょう。

## サンプルアプリ

iOS（Swift）の[メディアサンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumMediaExample)を探索して、Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れてください。

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してメディアモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0+でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールする最も簡単で推奨される方法です：

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常、`"Up to next major"`が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`Media`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットに追加します。**Frameworks and Libraries**の下にあります。

[iOS向けのSwift Package Managerインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)について詳しく学びましょう。

### CocoaPods

CocoaPodsを使用してメディアモジュールをインストールするには、次のpodをPodfileに追加します：  
```perl
pod 'tealium-swift/Media'
```

[iOS向けのCocoaPodsインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)について詳しく学びましょう。

### Carthage

Carthageを使用してメディアモジュールをインストールするには、次の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
```perl
TealiumMedia.framework
```

[iOS向けのCarthageインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)について詳しく学びましょう。

## 初期化

メディアモジュールを初期化するには、[`MediaContent`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#class-mediacontent)オブジェクトを作成します。

例：  

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

[メディアモジュールの実装](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#implement)について詳しく学びましょう。

#### メタデータ

メディアセッションにオプションのメタデータを追加するには：  
```swift
metadata: ["artist": "various", "duration": "45:00"]
```

チャプターメタデータを追加するには：   
```swift
metadata: ["artist": "Aerosmith", "track": "5"]
```

マージされたメタデータを追加するには：  
```swift
metadata: ["artist": "Aerosmith", "track": "5", "duration": "45:00"]
```

[メタデータ](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#metadata)について詳しく学びましょう。

## トラッキング

メディアをトラッキングするための多くのメソッドとプロパティが利用可能です。

### メディアセッション

メディアセッションのトラッキングを開始するには、[`startSession()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#startsession)メソッドを呼び出します。メディアセッションのトラッキングを停止するには、[`endSession()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#endsession)メソッドを呼び出します：  

```swift
let session = tealium?.media?.createSession(from: media)                                
session.startSession()
// ...
session.end()
```

[セッションのトラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#media-sessions)について詳しく学びましょう。

### プレイヤーイベント

再生や一時停止などのメディアプレイヤーイベントをトラッキングするには、適切な[プレイヤーイベントメソッド](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#playerevents)を呼び出します。各メディアプレイヤーイベントは、呼び出されるとデータレイヤーに`tealium_event`変数を送信します。

メディアが再生されたときにトラッキングするには、[`play()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#play)メソッドを呼び出します：   
```swift
session.play()
```

メディアが一時停止されたときにトラッキングするには、[`pause()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#pause)メソッドを呼び出します：   
```swift
session.pause()
```

### チャプター

メディアセッション内のチャプターセグメントをトラッキングするには、[`Chapter`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#struct-chapter)オブジェクトを作成し、それを[`startChapter()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#startchapter)メソッドに渡します。チャプターのトラッキングを停止するには、[`endChapter()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#endchapter)メソッドを呼び出します。

```swift
let chapter1 = Chapter("Chapter 1", 120)
mediaSession.startChapter(chapter1)
// ...
mediaSession.endChapter()
```

[チャプターのトラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#chapters)について詳しく学びましょう。

### 広告

広告ブレイクの開始をトラッキングするには、[`AdBreak`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#struct-adbreak)オブジェクトを作成し、それを[`startAdBreak()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#startadbreak)メソッドに渡します。広告ブレイク内の広告の開始をトラッキングするには、[`Ad`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#struct-ad)オブジェクトを作成し、それを[`startAd()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#startad)メソッドに渡します。

広告の終了をトラッキングするには、[`endAd()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#endad)メソッドを呼び出します。広告ブレイクの終了をトラッキングするには、[`endAdBreak()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#endadbreak)メソッドを呼び出します。

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

[広告のトラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/media/#ads)について詳しく学びましょう。

## 例

### チャプターと広告

次の例は、チャプターと広告を含むメディアコンテンツのトラッキングを示しています：

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

### セッションの放棄

次の例は、ユーザーがセッションを放棄し、アプリがバックグラウンドに移行し、メディアの再生が停止する場合を示しています。メディアモジュールが有効になっていると、[`endSession()`](https://docs.tealium.com/ja/platforms/ios-swift/api/media-session/#endsession)メソッドはセッションが終了する前に1分後にトリガーされます。ユーザーが再度アプリを開くと、メディアセッションが再開します。

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
```mediaSession.endAdBreak()
mediaSession.play()
// アプリがバックグラウンドに移行し、メディアは再生を続けません
mediaSession.pause()
// Tealiumのバックグラウンドメディアトラッキングが有効になっているため、endSessionは1分後にトリガーされます
// ユーザーが再度アプリを開き、メディアが再開します
mediaSession.resumeSession() // イベントを再開
let adBreak = AdBreak("Ad Break 2")
mediaSession.startAdBreak(adBreak)
// ユーザーがアプリを閉じる - セッションが放棄されます（endContentイベントなし）
mediaSession.endSession() // セッションの終了
```