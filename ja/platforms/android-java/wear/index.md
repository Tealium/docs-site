---
title: Android Wear
description: Tealium SDKをAndroid Wearにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-java/wear/
---
## 要件

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)を使用したAndroidWearアプリ
* Android (KitKat/4.4+ / API Level 20+ for Android Wear)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)


## APIリファレンス

Android Wearのクラスとメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`com.tealium.wear`](http://tealium.github.io/tealium-android/com/tealium/wear/package-frame.html)パッケージを参照してください。


## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、Tealium for AndroidWearの[sample app](https://github.com/Tealium/tealium-android/tree/master/Modules/AndroidWear/WearSample)をダウンロードすることをお勧めします。

Tealiumの実装をアプリの他の部分から抽象化するために、[sample helper class](https://github.com/Tealium/tealium-android/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java)の使用をお勧めします。これにより、初期化とトラッキング呼び出しを行う単一のエントリポイントが提供されます。また、ヘルパーファイルのコードを更新し、すべてのJavaファイルで更新する必要がなくなります。

## インストール

Android Wearアプリ用のTealiumライブラリをインストールします：

1. [Tealium for Android Wear](https://github.com/Tealium/tealium-android/tree/master/Modules/AndroidWear)をダウンロードしてインストールします。

2. `tealium.mobile-5.x.x.aar`をアプリケーションの依存関係に追加します。

      
<blockquote>
ウェアラブルでないAndroidアプリケーションの場合、追加のコードは必要ありません。
</blockquote>


3. `Application`クラスのサブクラスを作成し、アプリの`onCreate()`メソッドに`TealiumWear`の初期化コードを追加します。以下の例を参照してください：

      ```java
      public class WearApp extends Application {

            // Main appからのインスタンス名
            public static final String TEALIUM_MAIN = "INSTANCE_NAME";

            @Override
            public void onCreate() {
              super.onCreate();
              TealiumWear.createInstance(TEALIUM_MAIN,
                  TealiumWear.Config.create(this)
                  .setLogLevel(Log.VERBOSE));
            }
      //...
      }
      ```

4. `TEALIUM_MAIN`の値は、以下の例に示すように、メインアプリケーションの初期化で使用されるインスタンス名と一致する必要があります：

      ```java  
      // Main application initialization
      Tealium.createInstance("INSTANCE_NAME", config);

      // WearApp initialization
      public static final String TEALIUM_MAIN = "INSTANCE_NAME";
      ```

## トラッキング

### ビューのトラッキング

ウェアラブルでのトラッキングは、ハンドヘルド側と似ています。唯一の違いは、カスタムデータをトラッキング呼び出しに渡す方法です。ウェアラブル側では、`Map`ではなく、[`DataMap`](https://developers.google.com/android/reference/com/google/android/gms/wearable/DataMap)オブジェクトを使用します：

[`trackView()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackview)メソッドは、以下の例に示すように、画面ビューをトラッキングします：

```java
final DataMap data = new DataMap();
// ...
TealiumWear.getInstance(WearApp.TEALIUM_MAIN)
    .trackView("SCREEN_NAME", data);
```


### イベントのトラッキング

[`trackEvent()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium/#trackevent)メソッドは、以下の例に示すように、非ビューイベントをトラッキングします：

```java
final DataMap data = new DataMap();
// ...
TealiumWear.getInstance(WearApp.TEALIUM_MAIN)
    .trackEvent("EVENT_NAME", data);
```

