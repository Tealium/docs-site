---
title: インストール
description: React Native 向け Tealium のインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native-v1/install/
---

<blockquote>
これは React Native 向け Tealium の旧バージョン（1.x）です。  
現行バージョンについては、[React Native 向け Tealium 2.x](https://docs.tealium.com/ja/platforms/react-native/)を参照してください。
</blockquote>


React Native 向け Tealium を使用すると、React Native アプリケーションで Tealium のネイティブモバイルライブラリ（iOS、Android）を利用できます。



## 仕組み

Tealium モバイルライブラリは、次のいずれかの方法で React Native アプリケーションに統合します。

*   NPM パッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native) を使用した手動インストール

## 要件

* ネイティブビルド環境へのアクセス
* [React Native](https://github.com/Tealium/tealium-react-native) および関連ツールがインストールされていること
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/) または [Xcode](https://developer.apple.com/xcode/)
* [Android 向け Tealium](https://docs.tealium.com/ja/platforms/android-java/) または [iOS 向け Tealium](https://docs.tealium.com/ja/platforms/ios-swift/)

## サンプルアプリ

Tealium ライブラリ、トラッキングメソッド、および実装のベストプラクティスについて理解を深めるため、[React Native サンプルアプリ](https://github.com/Tealium/tealium-react-native/tree/master/TealiumSampleApp)をダウンロードすることを推奨します。


## インストール（NPM/YARN）

NPM を使用して React Native 向け Tealium ライブラリをインストールするには、次の手順を実行します。

1. React Native プロジェクトのルートに移動します。

2. 次のコマンドを使用して、`tealium-react-native` パッケージをダウンロードしてインストールします。  
      ```bash
      yarn install tealium-react-native
      ```
3. NPM パッケージのバージョン 1.0.7 では React Native Autolinking が有効になっているため、React Native バージョン 0.60 以降を使用している場合、`react-native link` を実行する必要はありません。

### Android

[Android Maven のインストール](https://docs.tealium.com/ja/platforms/android/install/#maven-install)ドキュメントの説明に従って、Android プロジェクトのルート `build.gradle` ファイルに Tealium の Maven リポジトリへの参照を追加します。プロジェクトの依存関係は、Autolinking プロセスによって自動的に処理されます。

### iOS

React Native 0.60 以降の Autolinking 機能により、必要な CocoaPods の依存関係が iOS アプリケーションのワークスペースに自動的に追加されます。

Pod をインストールするには、次のコマンドを実行します。

```bash
// From your React Native application folder:
cd ios && pod install
```

場合によっては、フレームワークモジュール内で非モジュール形式のインクルードを許可するために、clang パラメータを有効にする必要があります。clang パラメータを有効にするには、次の手順を実行します。

1. Xcode でアプリの `.xcworkspace` ファイルを開き、ナビゲーターから `Pods` を選択します。

2. **Targets** で **tealium-react-native** ターゲットを選択し、**Build Settings** タブをクリックします。

3. **Apple Clang - Language - Modules** > **Allow Non-modular Includes In Framework Modules** にある次の構成を探し、更新します。  
      ```groovy
      CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES = YES;
      ```



## インストール（手動）

### Android

Android アプリでは、次の手順に従って手動でインストールします。

1. Tealium を Android アプリケーションに統合するため、Tealium Maven リポジトリに次の内容を追加します。

2. プロジェクトルートの `build.gradle` に Tealium Maven URL を追加します。
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              maven {
                  url "http://maven.tealiumiq.com/android/releases/"
              }
            }
      }
      ```

3. プロジェクトモジュールの `build.gradle` ファイルに、Tealium コアライブラリの依存関係を追加します。また、必要に応じて Tealium ライフサイクルの依存関係も追加します。

      ```groovy
      dependencies {
          compile 'com.tealium:library:5.5.2'
              compile 'com.tealium:lifecycle:1.1'
      }
      ```

ブリッジロジックをコピーするには、次の手順を実行します。

1. Android フォルダーから、`TealiumModule.java` と `TealiumPackage.java` をプロジェクトファイルに追加します。

2. `MainApplication.java` ファイルの `getPackages()` メソッドに `TealiumPackage` を追加します。
      ```java
      @Override
      protected List getPackages() {
            return Arrays.asList(
                new MainReactPackage(),
                new TealiumPackage()    // <--- Add TealiumPackage
            );
      }
      ```

### iOS

React Native プロジェクトに iOS 向け Tealium を追加する手順は、ブリッジファイルを除き、React Native 以外のアプリケーションの場合と同じです。詳細については、[iOS アプリへの Tealium の追加](https://docs.tealium.com/ja/platforms/ios/)を参照してください。

コアライブラリは必須であり、オプションモジュールは必要に応じて追加します。これらは、[Tealium の iOS 向け GitHub リポジトリ](https://github.com/Tealium/tealium-ios)から入手できます。

サンプルアプリは開発者によるテストを目的としており、App Store での公開を目的としていません。そのため、`TealiumIOS.framework` および `TealiumIOSLifecycle.framework` モジュールを使用しています（シミュレーターには適していますが、公開用には適していません）。App Store での公開を目的として独自のアプリを開発する場合は、必ず[デバイス専用フォルダー](https://github.com/Tealium/tealium-ios/tree/master/DevicesOnly)内のフレームワークを使用してください。

## インストール（CocoaPods）

CocoaPods を使用してインストールすることもできます。Tealium の Pod 名は「TealiumIOS」です。詳細については、[iOS 向け Tealium ガイド](https://docs.tealium.com/ja/platforms/ios/)を参照してください。`create-react-native-app` コマンドでは Podfile が作成されないため、サンプルアプリは手動インストールを使用して構築されています。多数の依存関係を持つ複雑な本番アプリでは、CocoaPods の使用を推奨します。

#### ブリッジロジックのコピー

[GitHub リポジトリ](https://github.com/Tealium/tealium-react-native/tree/master/ios)には、Tealium のネイティブ iOS SDK と React Native アプリ内の JavaScript をブリッジするための `TealiumModule.m` と `TealiumModule.h` という 2 つのファイルがあります。

これら 2 つのファイルをアプリのメインプロジェクトにコピーします。

## JavaScript

モジュールをアプリにインポートする方法は、使用したインストール方法によって異なります。

NPM を使用してインストールした場合は、コードに次の行を追加します。

```javascript
import Tealium from 'tealium-react-native';
```

手動でインストールした場合は、[GitHub リポジトリ](https://github.com/Tealium/tealium-react-native)の `npm-package` フォルダーにある `index.js` ファイルを探し、ファイル名を `TealiumModule.js` に変更して、React Native JavaScript プロジェクトにコピーします。

次に、Tealium JavaScript モジュールをインポートするため、コードに次の行を追加します。

```javascript
import Tealium from './TealiumModule';
```
## 初期化

アプリをインストールしたら、次の例に示すように、[`initialize()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#initialize) メソッドを使用して `Tealium` インスタンスを初期化します。

```javascript
Tealium.initialize("ACCOUNT",
                   "PROFILE",
                   "ENVIRONMENT",
                   "IOS_DATA_SOURCE_KEY",
                   "ANDROID_DATA_SOURCE_KEY")
```

**同意管理**  
同意管理を使用するには、同じパラメータを指定して [`initializeWithConsentManager()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#initializewithconsentmanager) メソッドで初期化します。

詳細：

* [Android向け同意管理](https://docs.tealium.com/ja/platforms/android-java/consent-management/)
* [iOS向け同意管理](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/)


**カスタム初期化**  
すべての初期化オプションは、[`initializeCustom()`](https://docs.tealium.com/ja/platforms/react-native-v1/api/#initializecustom) メソッドで利用できます。

```javascript
Tealium.initializeCustom('ACCOUNT',
                         'PROFILE',
                         'ENVIRONMENT',
                         'IOS_DATA_SOURCE_KEY',
                         'ANDROID_DATA_SOURCE_KEY',
                         'INSTANCE',
                         ENABLE_LIFECYCLE,        // enable lifecycle tracking
                         'PUBLISH_SETTINGS_URL',  // custom publish settings URL
                         'TAG_MANAGEMENT_URL',    // custom tag management URL
                         USE_COLLECT_ENDPOINT,    // toggle between data endpoints, true: Tealium Collect, false: Visitor Data
                         ENABLE_CONSENT_MANAGER); // enable consent management
```

詳細については、[APIリファレンス](https://docs.tealium.com/ja/platforms/react-native-v1/api/)を参照してください。