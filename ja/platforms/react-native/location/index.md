---
title: ロケーションモジュール
description: React Native向けTealiumロケーションモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/location/
---
Tealium for React Nativeを使用すると、React NativeアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を利用できます。

## 仕組み

Tealiumモバイルライブラリは、次のいずれかの方法でReact Nativeアプリケーションに統合します。

*   NPMパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native)を使用した手動統合

## 要件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native v2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)および関連ツールがインストールされていること
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

NPMを使用してReact Native向けTealiumロケーションモジュールをインストールするには、次の手順を実行します。

1. メインの`tealium-react-native`ライブラリについて、[こちら](https://docs.tealium.com/ja/platforms/react-native/install/)のインストール手順に従います。バージョン2.2.0以降がインストールされていることを確認してください。

2. React Nativeプロジェクトのルートディレクトリに移動します。

3. 次のコマンドを使用して、`tealium-react-native-location`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn install tealium-react-native-location
    ```

## JavaScript

関連するクラスをアプリにインポートするには、次のようにします。

```javascript
import TealiumLocation from 'tealium-react-native-location';
import { TealiumLocationConfig, Accuracy, DesiredAccuracy, LocationData } from 'tealium-react-native-location/common';
```

## 初期化

メインのTealium React Native統合を初期化する前に、ロケーションモジュールを構成します。

必要なすべてのオプションを1つのメソッドで構成することも、ヘルパーメソッドを個別に呼び出して構成することもできます。

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

// or call them individually:
TealiumLocation.setAccuracy(Accuracy.high);
TealiumLocation.setGeofenceUrl(".../...");
// etc
```

## APIリファレンス

ロケーションモジュールとメインのTealium React Native統合の両方を初期化した後、位置情報トラッキングの開始または停止を要求したり、最新の既知の位置情報データを取得したりできます。

### `startLocationTracking()`

位置情報データのトラッキングを開始します。トラッキングを開始する前に、必要な権限が付与されていることを確認してください。

```javascript
TealiumLocation.startLocationTracking();
```

### `stopLocationTracking()`

位置情報データのトラッキングを停止します。現在位置情報をトラッキングしている場合にのみ有効です。

```javascript
TealiumLocation.stopLocationTracking();
```

### `lastLocation(callback)`

最後に確認された位置情報を要求し、緯度と経度の座標をそれぞれ`lat`キーと`lng`キーとして含むオブジェクトを返します。現在位置情報をトラッキングしている場合にのみ有効です。

```javascript
TealiumLocation.lastLocation((loc) => {
    if (loc) {
        Alert.alert(`Lat: ${loc.lat} | Lng: ${loc.lng}`)
    }
})
```