---
title: インストール
description: Tealium for Cordovaのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/cordova-v1/install/
---
これはTealium for Cordovaの以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for Cordova 2.x](/ja/platforms/cordova/)を参照してください。

## 必要条件

* Apache Cordova (7.0.0以上)
* CocoaPods

## ライブラリ

このプラグインには以下のTealiumライブラリが含まれています：

* [Tealium for iOS](/ja/platforms/ios-objective-c/)
* [Tealium for Android](/ja/platforms/android-java/)

バージョン1.1.1以降、フレームワークファイルはプラグインに含まれなくなりました。代わりに、iOSとAndroidのそれぞれの依存関係マネージャーが使用されます。

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
cd &lt;YOUR_PROJECT_FOLDER&gt;/
cordova platform add &lt;PLATFORM&gt;
cordova plugin add &lt;/LOCAL_PATH_TO_TEALIUM_PLUGIN/&gt;
cordova build &lt;PLATFORM&gt;
```

## 初期化

以下の例に示すように、[`init()`](/ja/platforms/cordova-v1/api/#init)メソッドはTealium Cordovaプラグインを初期化します：

```js
tealium.init({
    account                : &#34;ACCOUNT&#34;,
    profile                : &#34;PROFILE&#34;,
    environment            : &#34;ENVIRONMENT&#34;,
    datasource             : &#34;DATASOURCE&#34;,
    instance               : &#34;INSTANCE&#34;,
    isLifecycleEnabled     : &#34;TRUE_OR_FALSE&#34;,
    isCrashReporterEnabled : &#34;TRUE_OR_FALSE&#34;,
    logLevel               : tealium.logLevels.DEV,
    collectDispatchProfile : &#34;DISPATCH_PROFILE&#34;,
    collectDispatchURL     : &#34;DISPATCH_URL&#34;});
```

デフォルトでは、コアiOSおよびAndroidライブラリはTealium Collectデータをアカウントの「main」プロファイルに送信します。Tealium Collectを別のエンドポイントに指示するには、プロファイルまたはエンドポイントURLを上書きします。

プロファイルの上書き例：  
```js
tealium.init({
    account                : &#34;ACCOUNT&#34;,
    profile                : &#34;PROFILE&#34;,
    environment            : &#34;ENVIRONMENT&#34;,
    instance               : window.tealium_instance,
    collectDispatchProfile : &#34;PROFILE&#34;});
```

エンドポイントURLの上書き例：  
```js
tealium.init({
    account            : &#34;ACCOUNT&#34;,
    profile            : &#34;PROFILE&#34;,
    environment        : &#34;ENVIRONMENT&#34;,
    instance           : window.tealium_instance,
    collectDispatchURL : &#34;https://collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&amp;tealium_profile=PROFILE&#34;});
```

## ビルドのヒント

アプリのビルドに問題がある場合、プラットフォームを削除して再追加する必要がある場合は、次のコマンドを実行します。ここで、`PLATFORM`は`&#34;android&#34;`または`&#34;ios&#34;`のいずれかです：
```bash
cordova platform rm PLATFORM
cordova platform add PLATFORM
```

これは通常、物理デバイスでのビルド時に発生するXCodeの署名エラーを解決します。

ビルド実行中にCocoaPodsで問題が発生した場合、ローカルのCocoaPodsキャッシュをクリアするには、次のコマンドを実行します：
```bash
pod cache clean --all &amp;&amp; pod repo update
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
import { Tealium, TealConfig } from &#39;@ionic-native/tealium/ngx&#39;;

constructor(private tealium: Tealium) { }

//...

let tealConfig: TealConfig = {
   account: &#34;ACCOUNT&#34;,
   profile: &#34;PROFILE&#34;,
   environment: &#34;ENVIRONMENT&#34;,      // &#34;dev&#34;, &#34;qa&#34;, &#34;prod&#34;のいずれか
   isLifecycleEnabled: &#34;true&#34;,      // ライフサイクルトラッキングを有効にする
   isCrashReporterEnabled: &#34;false&#34;, // クラッシュレポーターを無効にする（Androidのみ）
   instance: &#34;INSTANCE&#34;             // すべての後続のAPI呼び出しで同じインスタンス名を使用する
}

this.tealium.init(tealConfig).then(()=&gt;{
   this.tealium.trackView({&#34;screen_name&#34;: &#34;homescreen&#34;});
});
```
