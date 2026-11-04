---
title: Android TV
description: Android TV向けTealium SDKのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/android-java/tv/
---

## 要件

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)を使用するAndroid TVアプリ
* Android（Lollipop／5.0以降／Android TVではAPIレベル21以降）
* Android（Lollipop／5.1以降／Fire TVではAPIレベル22以降）
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## APIリファレンス

Android TV向けのクラスおよびメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`com.tealium.library`](https://tealium.github.io/tealium-android/com/tealium/library/package-summary.html)パッケージを参照してください（Android TVでも同じです）。


## サンプルアプリ

Tealiumライブラリ、トラッキングメソッド、ベストプラクティスに沿った実装について理解を深めるには、Tealium for Android TVの[サンプルアプリ](https://github.com/Tealium/tealium-android/tree/master/Samples/AndroidTVSample)をご覧ください。

Tealiumの実装をアプリの他の部分から分離するために、[サンプルヘルパークラス](https://github.com/Tealium/tealium-android/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java)の使用をお勧めします。これにより、初期化とトラッキング呼び出しを行うための単一のエントリポイントを使用できます。また、個々のJavaファイルを変更することなく、ヘルパーファイル内のコードだけを更新できます。

## インストール

Amazon Fire TVを含む、任意のAndroid TVデバイスにTealium for Android TVをインストールできます。

### Android TVデバイス

Tealium for Android TVのインストール手順は、[Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/install/)のインストールガイドに記載されている手順と同じです。

### Amazon Fire TV

AmazonのFire TV向け[Fire App Builderフレームワーク](https://github.com/amzn/fire-app-builder)を使用して開発する場合は、Tealiumを活用することをお勧めします。Tealiumはベンダーに依存しないソリューションであり、単一のベンダーにロックインされることなく、複数のプラットフォームへデータを送信できます。

Fire TV向けストリーミングアプリの開発を開始し、Tealium SDKを活用するには、Amazonの[Fire App Builder](https://github.com/jonwongswong/fire-app-builder)ライブラリのこのフォークをクローンしてください。

## トラッキング

### ビューのトラッキング

[`trackView()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackview)メソッドは、次の例に示すように画面ビューをトラッキングします。

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackView("SCREEN_NAME", data);
```

### イベントのトラッキング

[`trackEvent()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackevent)メソッドは、次の例に示すようにビュー以外のイベントをトラッキングします。

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackEvent("EVENT NAME"", data);
```