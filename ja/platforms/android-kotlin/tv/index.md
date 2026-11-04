---
title: Android TV
description: Android TV 向け Tealium SDK のインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/tv/
---
## 要件

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/) を使用する Android TV アプリ
* [モバイル向けタグ管理プロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hub アカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## API リファレンス

Android TV のクラスとメソッドの完全なリファレンスについては、Tealium SDK for Android API の [`com.tealium.library`](https://tealium.github.io/tealium-kotlin/com/tealium/library/package-summary.html) パッケージを参照してください（Android TV でも同じです）。

## インストール

Amazon Fire TV を含む、任意の Android TV デバイスに Tealium for Android TV をインストールできます。

Tealium の実装をアプリの他の部分から分離するために、[サンプルヘルパークラス](https://github.com/Tealium/tealium-kotlin/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java)の使用を推奨します。これにより、初期化とトラッキング呼び出しを行うための単一のエントリーポイントを使用できます。また、個々の Java ファイルを変更することなく、ヘルパーファイル内のコードだけを更新できます。

### Android TV デバイス

Tealium for Android TV のインストール手順は、[Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/install/) のインストールガイドに記載されている手順と同じです。

### Amazon Fire TV

Amazon の Fire TV 向け [Fire App Builder フレームワーク](https://github.com/amzn/fire-app-builder)を使用して開発する場合は、Tealium の活用を推奨します。Tealium はベンダー中立のソリューションであり、単一のベンダーに依存することなく、複数のプラットフォームにデータを送信できます。

Amazon の [Fire App Builder](https://github.com/jonwongswong/fire-app-builder) ライブラリのこのフォークをクローンして、Fire TV 向けストリーミングアプリの開発を開始し、Tealium SDK を活用してください。

## トラッキング

### ビューのトラッキング

`TealiumView` メソッドは、次の例に示すように画面ビューをトラッキングします。

```java
tealium.track(TealiumView("SCREEN_NAME", mapOf("key" to "context value")))
```

### イベントのトラッキング

`TealiumEvent` メソッドは、次の例に示すようにビュー以外のイベントをトラッキングします。

```java
tealium.track(TealiumEvent("EVENT_NAME", mapOf("key" to "context value")))
```