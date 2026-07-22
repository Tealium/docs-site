---
title: インストール
description: Tealium for Cordovaのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/cordova-v1/install/
---

<blockquote>
これはTealium for Cordovaの以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for Cordova 2.x](https://docs.tealium.com/ja/platforms/cordova/)を参照してください。
</blockquote>


## 必要条件

* Apache Cordova (7.0.0以上)
* CocoaPods

## ライブラリ

このプラグインには以下のTealiumライブラリが含まれています：

* [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-objective-c/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)


<blockquote>
バージョン1.1.1以降、フレームワークファイルはプラグインに含まれなくなりました。代わりに、iOSとAndroidのそれぞれの依存関係マネージャーが使用されます。
</blockquote>


## サンプルアプリ

ライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Tealium for Cordovaの[サンプルアプリ](https://github.com/Tealium/cordova-plugin/tree/master/TealiumSample)を探索してください。

## インストール

NPMまたは手動でTealium for Cordovaをインストールします。

### NPM

Nodeパッケージマネージャー（NPM）は推奨されるインストールタイプです。パッケージ名は`tealium-cordova-plugin`です。

NPMを介してプラグインをインストールするには、プロジェクトディレクトリ内で以下のコマンドを実行します：

```bash
cordova plugin add tealium-cordova-plugin
```

### 手動

NPMを使用できない場合は、プラグインを手動でインストールすることができます。

コマンドラインインターフェース（CLI）で以下のコマンドを実行します：

```bash
cd <YOUR_PROJECT_FOLDER>/
cordova platform add <PLATFORM>
cordova plugin add </LOCAL_PATH_TO_TEALIUM_PLUGIN/>
cordova build <PLATFORM>
```

## 初期化

以下の例に示すように、[`init()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#init)メソッドはTealium Cordovaプラグインを初期化します：

```js
tealium.init({
    account                : "ACCOUNT",
    profile                : "PROFILE",
    environment            : "ENVIRONMENT",
    datasource             : "DATASOURCE",
    instance               : "INSTANCE",
    isLifecycleEnabled     : "TRUE_OR_FALSE",
    isCrashReporterEnabled : "TRUE_OR_FALSE",
    logLevel               : tealium.logLevels.DEV,
    collectDispatchProfile : "DISPATCH_PROFILE",
    collectDispatchURL     : "DISPATCH_URL"});
```

デフォルトでは、コアiOSおよびAndroidライブラリはTealium Collectデータをアカウントの「main」プロファイルに送信します。Tealium Collectを別のエンドポイントに指示するには、プロファイルまたはエンドポイントURLを上書きします。

プロファイルの上書き例：  
```js
tealium.init({
    account                : "ACCOUNT",
    profile                : "PROFILE",
    environment            : "ENVIRONMENT",
    instance               : window.tealium_instance,
    collectDispatchProfile : "PROFILE"});
```

エンドポイントURLの上書き例：  
```js
tealium.init({
    account            : "ACCOUNT",
    profile            : "PROFILE",
    environment        : "ENVIRONMENT",
    instance           : window.tealium_instance,
    collectDispatchURL : "https://collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE"});
```

## ビルドのヒント

アプリのビルドに問題がある場合、プラットフォームを削除して再追加する必要がある場合は、次のコマンドを実行します。ここで、`PLATFORM`は`"android"`または`"ios"`のいずれかです：
```bash
cordova platform rm PLATFORM
cordova platform add PLATFORM
```

これは通常、物理デバイスでのビルド時に発生するXCodeの署名エラーを解決します。

ビルド実行中にCocoaPodsで問題が発生した場合、ローカルのCocoaPodsキャッシュをクリアするには、次のコマンドを実行します：
```bash
pod cache clean --all && pod repo update
```

## アンインストール

Tealiumプラグインを削除するには、次のコマンドを実行します：
```bash
cordova plugin rm tealium-cordova-plugin
```

インストールされている場合は、補足的なTealiumモジュールも削除します：

- `tealium-cordova-crashreporter`
- `tealium-cordova-adidentifier`
- `tealium-cordova-installreferrer`

## Ionicフレームワーク

TealiumのCordovaプラグインは[Ionicフレームワーク](https://ionicframework.com/docs/native/tealium)をサポートしています。インストールするには、次のコマンドを実行します：  
```bash
ionic cordova plugin add tealium-cordova-plugin
npm install @ionic-native/tealium
```

次の例は、Ionicフレームワークの使用方法を示しています：

```js
import { Tealium, TealConfig } from '@ionic-native/tealium/ngx';

constructor(private tealium: Tealium) { }

//...

let tealConfig: TealConfig = {
   account: "ACCOUNT",
   profile: "PROFILE",
   environment: "ENVIRONMENT",      // "dev", "qa", "prod"のいずれか
   isLifecycleEnabled: "true",      // ライフサイクルトラッキングを有効にする
   isCrashReporterEnabled: "false", // クラッシュレポーターを無効にする（Androidのみ）
   instance: "INSTANCE"             // すべての後続のAPI呼び出しで同じインスタンス名を使用する
}

this.tealium.init(tealConfig).then(()=>{
   this.tealium.trackView({"screen_name": "homescreen"});
});
```
