---
title: Android TV
description: Tealium SDKをAndroid TVにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-java/tv/
---

## 必要条件

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)を使用したAndroid TVアプリ
* Android (Lollipop/5.0+ / API Level 21+ for Android TV)
* Android (Lollipop/5.1+ / API Level 22+ for Fire TV)
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## APIリファレンス

Android TVのクラスとメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`com.tealium.library`](https://tealium.github.io/tealium-android/com/tealium/library/package-summary.html)パッケージを参照してください（Android TVでも同じです）。

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、Tealium for Android TVの[sample app](https://github.com/Tealium/tealium-android/tree/master/Samples/AndroidTVSample)を探索してみてください。

アプリの残りの部分からTealiumの実装を抽象化するために、[sample helper class](https://github.com/Tealium/tealium-android/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java)の使用をお勧めします。これにより、初期化およびトラッキング呼び出しを行う単一のエントリポイントが提供されます。また、ヘルパーファイルのコードを更新し、すべてのJavaファイルで更新することなく行うことができます。

## インストール

Amazon Fire TVを含む任意のAndroid TVデバイスにTealium for Android TVをインストールします。

### Android TVデバイス

Tealium for Android TVをインストールするには、[Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/install/)のインストールガイドに記載されている手順と同じです。

### Amazon Fire TV

AmazonのFire TV [Fire App Builder framework](https://github.com/amzn/fire-app-builder)を使用して開発する際には、Tealiumを活用することをお勧めします。Tealiumはベンダーニュートラルなソリューションであり、単一のベンダーにロックインされることなく、データを複数のプラットフォームに送信することができます。

Fire TVでストリーミングアプリを開発し、Tealium SDKを活用するために、Amazonの[Fire App Builder](https://github.com/jonwongswong/fire-app-builder)ライブラリのこのフォークをクローンします。

## トラッキング

### ビューのトラッキング

[`trackView()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackview)メソッドは、次の例に示すように、画面のビューをトラッキングします：

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackView("SCREEN_NAME", data);
```

### イベントのトラッキング

[`trackEvent()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackevent)メソッドは、次の例に示すように、ビュー以外のイベントをトラッキングします：

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackEvent("EVENT NAME"", data);
```

