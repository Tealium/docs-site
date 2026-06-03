---
title: インストール
description: Tealium for Cordovaのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/cordova/install/
---
## 必要条件

* Apache Cordova (9.0.0&#43;)

## ライブラリ

このプラグインには以下のTealiumライブラリが含まれています：

* [Tealium for iOS](/ja/platforms/ios-swift)
* [Tealium for Android](/ja/platforms/android-kotlin/)

## サンプルアプリ

私たちのライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Tealium for Cordovaの[サンプルアプリ](https://github.com/Tealium/cordova-plugin/tree/master/TealiumCordovaSample)を探索してください。

## インストール

`package.json`でFirebaseリモートコマンドをインストールする場合は、問題を避けるためにプラグインセクションでFirebaseの前に`tealium-cordova-plugin`がリストされていることを確認してください。

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

[`initialize()`](/ja/platforms/cordova/api/#initialize)メソッドは、以下の例に示すようにTealium Cordovaプラグインを初期化します：





```js
var Environment = tealium.utils.Environment;
var Collectors = tealium.utils.Collectors;
var Dispatchers = tealium.utils.Dispatchers;
var ConsentPolicy = tealium.utils.ConsentPolicy;

var config = {
    account: &#39;ACCOUNT&#39;,
    profile: &#39;PROFILE&#39;,
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
    //     &#39;time&#39;: 10,
    //     &#39;unit&#39;: &#39;days&#39;
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};
window.tealium.initialize(config, function(success) {
    if (success) {
      console.log(&#34;Tealium initialized successfully&#34;);
    }
})
```




```js
import {Collectors, Dispatchers, LogLevel, Tealium, TealiumConfig,  TealiumEnvironment, TealiumEvent, TealiumView} from &#39;@awesome-cordova-plugins/tealium&#39;;

let config: TealiumConfig = {
    account: &#39;ACCOUNT&#39;,
    profile: &#39;PROFILE&#39;,
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
    //     &#39;time&#39;: 10,
    //     &#39;unit&#39;: TimeUnit.days
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};


Tealium.initialize(tealConfig).then(()=&gt;{
    console.log(&#34;Tealium initialized successfully&#34;);
});
```



