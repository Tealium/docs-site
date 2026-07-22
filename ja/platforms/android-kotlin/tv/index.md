---
title: Android TV
description: Tealium SDKをAndroid TVにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/tv/
---
## 必要条件

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)を使用したAndroid TVアプリ
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## APIリファレンス

Android TVのクラスとメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`com.tealium.library`](https://tealium.github.io/tealium-kotlin/com/tealium/library/package-summary.html)パッケージを参照してください（Android TVでも同じです）

## インストール

Tealium for Android TVをAmazon Fire TVを含む任意のAndroid TVデバイスにインストールします。

Tealiumの実装をアプリの他の部分から抽象化するために、[sample helper class](https://github.com/Tealium/tealium-kotlin/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java)の使用を推奨します。これにより、初期化およびトラッキング呼び出しを行う単一のエントリーポイントが提供されます。また、ヘルパーファイルのコードを更新し、すべてのJavaファイルで更新する必要がなくなります。

### Android TVデバイス

Tealium for Android TVをインストールするには、[Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/install/)のインストールガイドに記載されている手順と同じです。

### Amazon Fire TV

AmazonのFire TV [Fire App Builder framework](https://github.com/amzn/fire-app-builder)を使用して開発する際には、Tealiumを活用することを推奨します。Tealiumはベンダーニュートラルなソリューションであり、単一のベンダーにロックインされることなくデータを複数のプラットフォームに送信できます。

Amazonの[Fire App Builder](https://github.com/jonwongswong/fire-app-builder)ライブラリのこのフォークをクローンして、Fire TVでのストリーミングアプリの開発を開始し、Tealium SDKを活用します。

## トラッキング

### ビューのトラッキング

`TealiumView`メソッドは、次の例に示すように、画面のビューをトラッキングします：

```java
tealium.track(TealiumView("SCREEN_NAME", mapOf("key" to "context value")))
```

### イベントのトラッキング

`TealiumEvent`メソッドは、次の例に示すように、ビュー以外のイベントをトラッキングします：

```java
tealium.track(TealiumEvent("EVENT_NAME", mapOf("key" to "context value")))
```

