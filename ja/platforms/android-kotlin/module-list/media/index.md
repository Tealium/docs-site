---
title: メディアモジュール
description: メディアイベントのトラッキングデータを提供します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/media/
---
メディアモジュールは、カスタムイベントを使用してアプリ内のストリーミングメディアを追跡します。[メディアトラッキング](/ja/platforms/getting-started-mobile/media/)について詳しく学びましょう。

## サンプルアプリ

Android（Kotlin）の[メディアサンプルアプリ](https://github.com/Tealium/tealium-kotlin/tree/master/mobile)を探索して、Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装について理解を深めましょう。

## インストール

Maven（推奨）または手動でメディアモジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：  
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```
2. プロジェクトモジュールの `build.gradle` ファイルに、TealiumライブラリとCrash ReporterのMaven依存関係を追加します：  
      ```groovy
      dependencies {
          implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
          implementation &#39;com.tealium:kotlin-media:1.1.1&#39;
      }
      ```

### 手動

モジュールを手動でインストールするには：

1. Tealiumの[メディアモジュール](https://github.com/Tealium/tealium-kotlin/tree/master/media)をダウンロードします。

2. ファイル `tealium-kotlin.media-1.1.1.aar` をプロジェクトの `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
          implementation(name:&#39;tealium-kotlin.media-1.1.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## 初期化

メディアモジュールを初期化するには、[`MediaContent`](/ja/platforms/android-kotlin/api/media/#class-mediacontent)オブジェクトを作成します。

例：  

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

[メディアモジュールの実装](/ja/platforms/getting-started-mobile/media/#implement)について詳しく学びましょう。


#### メタデータ

セッションにオプションのメタデータを追加するには：  
```kotlin
metadata = [&#34;artist&#34;: &#34;Various&#34;, &#34;duration&#34;: &#34;45:00&#34;]
```

チャプターメタデータを追加するには：   
```kotlin
metadata = [&#34;artist&#34;: &#34;Aerosmith&#34;, &#34;track&#34;: &#34;5&#34;]
```

マージされたメタデータを追加するには：  
```kotlin
metadata = [&#34;artist&#34;: &#34;Aerosmith&#34;, &#34;track&#34;: &#34;5&#34;, &#34;duration&#34;: &#34;45:00&#34;]
```

[メタデータ](/ja/platforms/getting-started-mobile/media/#metadata)について詳しく学びましょう。

## トラッキング

メディアモジュールをインストールした後、メディアイベントをトラッキングします。

### メディアセッション

メディアセッションのトラッキングを開始するには、[`startSession()`](/ja/platforms/android-kotlin/api/media/#startsession)メソッドを呼び出します。メディアセッションのトラッキングを停止するには、[`endSession()`](/ja/platforms/android-kotlin/api/media/#endsession)メソッドを呼び出します：  

```kotlin
tealium?.media?.startSession(mediaContent)
//...
tealium?.media?.endSession()
```

[セッションのトラッキング](/ja/platforms/getting-started-mobile/media/#media-sessions)について詳しく学びましょう。

### プレイヤーイベント

再生や一時停止などのメディアプレイヤーイベントをトラッキングするには、適切な[プレイヤーイベントメソッド](/ja/platforms/getting-started-mobile/media/#playerevents)を呼び出します。各メディアプレイヤーイベントは、呼び出されるとデータレイヤーに `tealium_event` 変数を送信します。

メディアが再生されたときにトラッキングするには、[`play()`](/ja/platforms/android-kotlin/api/media/#play)メソッドを呼び出します：   
```kotlin
tealium?.media?.play()
```

メディアが一時停止されたときにトラッキングするには、[`pause()`](/ja/platforms/android-kotlin/api/media/#pause)メソッドを呼び出します：   
```kotlin
tealium?.media?.pause()
```

[プレイヤーイベントのトラッキング](/ja/platforms/getting-started-mobile/media/#player-events)について詳しく学びましょう。


### チャプター

メディアセッションのチャプターセグメントをトラッキングするには、[`Chapter`](/ja/platforms/android-kotlin/api/media/#class-chapter)オブジェクトを作成し、[`startChapter()`](/ja/platforms/android-kotlin/api/media/#startchapter)メソッドに渡します。チャプターのトラッキングを停止するには、[`endChapter()`](/ja/platforms/android-kotlin/api/media/#endchapter)メソッドを呼び出します。

例：  

```kotlin
val chapter1 = Chapter(name = &#34;Chapter 1&#34;, duration = 120)
tealium?.media?.startChapter(chapter1)
// ...
tealium?.media?.endChapter()
```

[チャプターのトラッキング](/ja/platforms/getting-started-mobile/media/#chapters)について詳しく学びましょう。

### 広告

広告ブレイクの開始をトラッキングするには、[`AdBreak`](/ja/platforms/android-kotlin/api/media/#class-adbreak)オブジェクトを作成し、[`startAdBreak()`](/ja/platforms/android-kotlin/api/media/#startadbreak)メソッドに渡します。広告ブレイク内の広告の開始をトラッキングするには、[`Ad`](/ja/platforms/android-kotlin/api/media/#class-ad)オブジェクトを作成し、[`startAd()`](/ja/platforms/android-kotlin/api/media/#startad)メソッドに渡します。

広告の終了をトラッキングするには、[`endAd()`](/ja/platforms/android-kotlin/api/media/#endad)メソッドを呼び出します。広告ブレイクの終了をトラッキングするには、[`endAdBreak()`](/ja/platforms/android-kotlin/api/media/#endadbreak)メソッドを呼び出します。


```kotlin
val adBreak = AdBreak(name = &#34;Ad Break 1&#34;)
tealium?.media?.startAdBreak(adBreak)

val ad1 = Ad(&#34;Ad 1&#34;)
tealium?.media?.startAd(ad1)
tealium?.media?.endAd()

val ad2 = Ad(&#34;Ad 2&#34;)
tealium?.media?.startAd(ad2)
tealium?.media?.endAd()

tealium?.media?.endAdBreak()
```

[広告のトラッキング](/ja/platforms/getting-started-mobile/media/#ads)について詳しく学びましょう。


## 例

### チャプターと広告

次の例は、チャプターと広告を含むメディアコンテンツのトラッキングを示しています：

```kotlin
val mediaContent: MediaContent = MediaContent(
  name = &#34;What is the Tealium Customer Data Hub?&#34;,
  trackingType = TrackingType.FULL_PLAYBACK,
  streamType = StreamType.VOD,
  mediaType = MediaType.VIDEO,
  qoe = QoE(1500),
  duration = 114
)

tealium?.media?.startSession(mediaContent)
tealium?.media?.startAdBreak(AdBreak(&#34;Ad Break 1&#34;))
tealium?.media?.startAd(Ad(&#34;Ad  1&#34;))
// ...
tealium?.media?.endAd()
tealium?.media?.startAd(Ad(&#34;Ad  2&#34;))
tealium?.media?.endAd()
tealium?.media?.endAdBreak()
tealium?.media?.startChapter(Chapter(&#34;Chapter 1&#34;))
tealium?.media?.endChapter()
tealium?.media?.startAdBreak(AdBreak(&#34;Ad Break 2&#34;))
tealium?.media?.startAd(Ad(&#34;Ad  3&#34;))
// ...
tealium?.media?.endAd()
tealium?.media?.endAdBreak()
tealium?.media?.startChapter(Chapter(&#34;Chapter 2&#34;))
tealium?.media?.endChapter()
tealium?.media?.startChapter(Chapter(&#34;Chapter 3&#34;))
tealium?.media?.startBuffer()
tealium?.media?.endBuffer()
tealium?.media?.endChapter()
tealium?.media?.endContent()
tealium?.media?.endSession()
```

### セッションの放棄

次の例は、ユーザーがセッションを放棄し、アプリがバックグラウンドに移行し、メディアの再生が停止する場合を示しています。メディアモジュールが有効になっていると、[`endSession()`](/ja/platforms/android-kotlin/api/media/#endsession)メソッドはセッションが終了する1分前にトリガーされます。ユーザーが再度アプリを開くと、メディアセッションが再開します。

```kotlin
val mediaContent: MediaContent = MediaContent(
  name = &#34;What is the Tealium Customer Data Hub?&#34;,
  trackingType = TrackingType.FULL_PLAYBACK,
  streamType = StreamType.VOD,
  mediaType = MediaType.VIDEO,
  qoe = QoE(1500),
  duration = 114
)
tealium?.media?.startSession(mediaContent)
tealium?.media?.startAdBreak(AdBreak(&#34;Ad Break 1&#34;))
tealium?.media?.startAd(Ad(&#34;Ad 1&#34;))
// ...
tealium?.media?.endAd()
tealium?.media?.startAd(Ad(&#34;Ad 2&#34;))
tealium?.media?.endAd()
tealium?.media?.endAdBreak()
tealium?.media?.play()
// アプリがバックグラウンドに移行し、メディアは再生を続けません
tealium?.media?.pause()
// Tealiumのバックグラウンドメディアトラッキングが有効になっているため、endSessionは1分後にトリガーされます
// ユーザーが再度アプリを開き、メディアが再開します
tealium?.media?.resumeSession() // セッションの再開
let adBreak = AdBreak(&#34;Ad Break 2&#34;)
tealium?.media?.startAdBreak(adBreak)
// ユーザーがアプリを閉じる - セッションが放棄されます（endContentイベントなし）
tealium?.media?.endSession() // セッションの終了
```

