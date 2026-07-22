---
title: ロケーションモジュール
description: React Native用のTealiumロケーションモジュールのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/react-native/location/
---
Tealium for React Nativeは、React NativeアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を使用することを可能にします。

## 仕組み

Tealiumのモバイルライブラリは、以下の2つの方法のいずれかを使用してReact Nativeアプリケーションに統合されます：

*   NPMパッケージ（推奨）
*   手動で[GitHub](https://github.com/Tealium/tealium-react-native)から

## 必要条件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native v2.2.0+](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63+](https://github.com/Tealium/tealium-react-native)とそのツールのインストール
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)


## インストール（NPM/YARN）

React Native用のTealiumロケーションモジュールをNPMでインストールするには：

1. メインの`tealium-react-native`ライブラリのインストール手順を[こちら](https://docs.tealium.com/ja/platforms/react-native/install/)で確認し、少なくともバージョン2.2.0以上をインストールしていることを確認します。

2. React Nativeプロジェクトのルートに移動します。

3. 以下のコマンドで`tealium-react-native-location`パッケージをダウンロードしてインストールします：  
    ```bash
    yarn install tealium-react-native-location
    ```


## JavaScript

アプリに関連するクラスをインポートするには、以下のようにします：

```javascript
import TealiumLocation from 'tealium-react-native-location';
import { TealiumLocationConfig, Accuracy, DesiredAccuracy, LocationData } from 'tealium-react-native-location/common';
```

## 初期化

メインのTealium React Native統合を初期化する前に、ロケーションモジュールを構成します。

必要なすべてのオプションを1つのメソッドで構成するか、ヘルパーメソッドを個別に呼び出すことができます：

```javascript
let locationConfig: TealiumLocationConfig = {
    accuracy: Accuracy.high,
    geofenceUrl: "...",
    geofenceFile: "...",
    interval: 6000,                         // android only
    geofenceEnabled: false,                 // iOS only
    desiredAccuracy: DesiredAccuracy.best,  // iOS only
    updateDistance: 150                    // iOS only    
}

TealiumLocation.configure(locationConfig);

// または、それらを個別に呼び出します：
TealiumLocation.setAccuracy(Accuracy.high);
TealiumLocation.setGeofenceUrl(".../...");
// etc
```

## APIリファレンス

ロケーションモジュールとメインのTealium React Native統合が両方とも初期化された後、ロケーショントラッキングの開始または停止を要求したり、最新の既知のロケーションポイントデータを要求することができます。

### `startLocationTracking()`

ロケーションデータのトラッキングを開始します - ロケーショントラッキングを開始する前に、関連する権限が付与されていることを確認する必要があります。

```javascript
TealiumLocation.startLocationTracking();
```

### `stopLocationTracking()`

ロケーションデータのトラッキングを停止します - 現在ロケーションデータをトラッキングしている場合にのみ関連します。

```javascript
TealiumLocation.stopLocationTracking();
```


### `lastLocation(callback)`

最後に知られているロケーションを要求し、`lat`と`lng`キーとして緯度と経度の座標を含むオブジェクトを返します - 現在ロケーションデータをトラッキングしている場合にのみ関連します。

```javascript
TealiumLocation.lastLocation((loc) => {
    if (loc) {
        Alert.alert(`Lat: ${loc.lat} | Lng: ${loc.lng}`)
    }
})
```



