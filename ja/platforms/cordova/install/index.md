---
title: インストール
description: Tealium for Cordovaのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/cordova/install/
---
## 必要条件

* Apache Cordova (9.0.0+)

## ライブラリ

このプラグインには以下のTealiumライブラリが含まれています：

* [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)

## サンプルアプリ

私たちのライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Tealium for Cordovaの[サンプルアプリ](https://github.com/Tealium/cordova-plugin/tree/master/TealiumCordovaSample)を探索してください。

## インストール


<blockquote>
`package.json`でFirebaseリモートコマンドをインストールする場合は、問題を避けるためにプラグインセクションでFirebaseの前に`tealium-cordova-plugin`がリストされていることを確認してください。
</blockquote>


Cordova用のTealiumライブラリをインストールするには、Cordovaアプリプロジェクトで以下のコマンドを実行します：




```js
cordova plugin add tealium-cordova-plugin
```




```js
ionic cordova plugin add tealium-cordova-plugin
npm install @awesome-cordova-plugins/core
npm install @awesome-cordova-plugins/tealium
```




## 初期化

[`initialize()`](https://docs.tealium.com/ja/platforms/cordova/api/#initialize)メソッドは、以下の例に示すようにTealium Cordovaプラグインを初期化します：





```js
var Environment = tealium.utils.Environment;
var Collectors = tealium.utils.Collectors;
var Dispatchers = tealium.utils.Dispatchers;
var ConsentPolicy = tealium.utils.ConsentPolicy;

var config = {
    account: 'ACCOUNT',
    profile: 'PROFILE',
    environment: Environment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentLoggingEnabled: true,
    // consentExpiry: {
    //     'time': 10,
    //     'unit': 'days'
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};
window.tealium.initialize(config, function(success) {
    if (success) {
      console.log("Tealium initialized successfully");
    }
})
```




```js
import {Collectors, Dispatchers, LogLevel, Tealium, TealiumConfig,  TealiumEnvironment, TealiumEvent, TealiumView} from '@awesome-cordova-plugins/tealium';

let config: TealiumConfig = {
    account: 'ACCOUNT',
    profile: 'PROFILE',
    environment: TealiumEnvironment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentLoggingEnabled: true,
    // consentExpiry: {
    //     'time': 10,
    //     'unit': TimeUnit.days
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};


Tealium.initialize(tealConfig).then(()=>{
    console.log("Tealium initialized successfully");
});
```



