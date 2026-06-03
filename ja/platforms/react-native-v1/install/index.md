---
title: インストール
description: React Native用Tealiumのインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/react-native-v1/install/
---
これはReact Native用Tealiumの以前のバージョン（1.x）です。  
現在のバージョンについては、[React Native用Tealium 2.x](/ja/platforms/react-native/)を参照してください。

React Native用Tealiumを使用すると、React NativeアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を使用できます。



## 動作原理

Tealiumモバイルライブラリは、以下のいずれかの方法でReact Nativeアプリケーションに統合されます：

*   NPMパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native)を通じて手動で

## 要件

* ネイティブビルド環境へのアクセス
* [React Native](https://github.com/Tealium/tealium-react-native)およびツールがインストールされていること
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/ja/platforms/android-java/)または[Tealium for iOS](/ja/platforms/ios-swift/)

## サンプルアプリ

ライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、[React Nativeサンプルアプリ](https://github.com/Tealium/tealium-react-native/tree/master/TealiumSampleApp)をダウンロードすることをお勧めします。

## インストール（NPM/YARN）

React Native用TealiumライブラリをNPMでインストールするには：

1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドで`tealium-react-native`パッケージをダウンロードしてインストールします：  
      ```bash
      yarn install tealium-react-native
      ```
3. NPMパッケージのバージョン1.0.7ではReact Native Autolinkingが有効になっており、React Nativeのバージョン0.60&#43;を使用している場合、`react-native link`を実行する必要はありません。

### Android

Androidプロジェクトのルート`build.gradle`ファイルにTealiumのMavenリポジトリへの参照を追加します。これは[Android Mavenインストール](/ja/platforms/android/install/#maven-install)のドキュメントで説明されています。プロジェクトの依存関係はAutolinkingプロセスによって自動的に処理されます。

### iOS

React Native 0.60&#43;のAutolinking機能は、必要なCocoaPods依存関係を自動的にiOSアプリケーションワークスペースに追加します。

ポッドをインストールするには、次のコマンドを実行します：

```bash
// React Nativeアプリケーションフォルダーから：
cd ios &amp;&amp; pod install
```

場合によっては、フレームワークモジュール内の非モジュラーなインクルードを許可するためにclangパラメータを有効にする必要があります。clangパラメータを有効にするには：

1. Xcodeでアプリの`.xcworkspace`ファイルを開き、ナビゲーターから`Pods`を選択します。

2. **Targets**の下で**tealium-react-native**ターゲットを選択し、**Build Settings**タブをクリックします。

3. **Apple Clang - Language - Modules** &gt; **Allow Non-modular Includes In Framework Modules**の下で次の構成を見つけて更新します：  
      ```groovy
      CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES = YES;
      ```


## インストール（手動）

### Android

Androidアプリの場合、以下の手動インストール手順に従います：

1. AndroidアプリケーションにTealiumを統合するには、Tealium Mavenリポジトリを追加します：

2. プロジェクトのルート`build.gradle`にTealium Maven URLを追加します：
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              maven {
                  url &#34;http://maven.tealiumiq.com/android/releases/&#34;
              }
            }
      }
      ```

3. プロジェクトモジュールの`build.gradle`ファイルにTealiumコアライブラリの依存関係を追加します。必要に応じてTealiumライフサイクル依存関係も追加します：

      ```groovy
      dependencies {
          compile &#39;com.tealium:library:5.5.2&#39;
              compile &#39;com.tealium:lifecycle:1.1&#39;
      }
      ```

ブリッジングロジックのコピー：

1. Androidフォルダから、`TealiumModule.java`と`TealiumPackage.java`をプロジェクトファイルに追加します。

2. `MainApplication.java`ファイルの`getPackages()`メソッドに`TealiumPackage`を含めます。
      ```java
      @Override
      protected List getPackages() {
            return Arrays.asList(
                new MainReactPackage(),
                new TealiumPackage()    // &lt;--- TealiumPackageを追加
            );
      }
      ```

### iOS

React NativeプロジェクトにiOS用Tealiumを追加するには、ブリッジングファイルを除いて、非React Nativeアプリケーションに追加するのと同じ手順が必要です。したがって、完全な詳細については[iOSアプリにTealiumを追加する](/ja/platforms/ios/)を参照してください。

コアライブラリが必要で、必要に応じてオプショナルモジュールが追加されます。これらは[iOS用のGitHubリポジトリ](https://github.com/Tealium/tealium-ios)から入手できます。

サンプルアプリは開発者の実験用であり、App Storeに公開するためのものではないため、`TealiumIOS.framework`と`TealiumIOSLifecycle.framework`のモジュールを使用しています（シミュレーターに適していますが、公開には適していません）。App Storeに公開するための自分のアプリを作業する際には、[デバイス専用フォルダ](https://github.com/Tealium/tealium-ios/tree/master/DevicesOnly)のフレームワークを使用してください。

## インストール（CocoaPods）

CocoaPodsはインストールを行う別の方法です。私たちのポッドは「TealiumIOS」という名前です。完全な詳細については[iOS用Tealiumガイド](/ja/platforms/ios/)を参照してください。コマンド`create-react-native-app`はPodfileを作成しないため、サンプルアプリは手動インストールを使用して構築されました。多くの依存関係を持つ複雑な本番アプリの場合、CocoaPodsが推奨される方法です。

#### ブリッジングロジックのコピー

[GitHubリポジトリ](https://github.com/Tealium/tealium-react-native/tree/master/ios)には、TealiumネイティブiOS SDKとReact NativeアプリのJavascript間のブリッジングを提供する2つのファイル、`TealiumModule.m`と`TealiumModule.h`があります。

これらの2つのファイルをアプリのメインプロジェクトにコピーします。

## JavaScript

モジュールをアプリにインポートする方法は、インストール方法によって異なります。

NPMを介してインストールした場合、コードにこの行を追加します：

```javascript
import Tealium from &#39;tealium-react-native&#39;;
```

手動でインストールした場合、[GitHubリポジトリ](https://github.com/Tealium/tealium-react-native)の`npm-package`フォルダから`index.js`ファイルを見つけ、`TealiumModule.js`に名前を変更してReact Native JavaScriptプロジェクトにコピーします。

次に、Tealium JavaScriptモジュールをインポートするためにコードにこの行を追加します：

```javascript
import Tealium from &#39;./TealiumModule&#39;;
```
## 初期化

アプリがインストールされたら、以下の例に示すように[`initialize()`](/ja/platforms/react-native-v1/api/#initialize)メソッドを使用して`Tealium`インスタンスを初期化します：

```javascript
Tealium.initialize(&#34;ACCOUNT&#34;,
                   &#34;PROFILE&#34;,
                   &#34;ENVIRONMENT&#34;,
                   &#34;IOS_DATA_SOURCE_KEY&#34;,
                   &#34;ANDROID_DATA_SOURCE_KEY&#34;)
```

**コンセント管理**  
コンセント管理を使用するには、同じパラメータを使用して[`initializeWithConsentManager()`](/ja/platforms/react-native-v1/api/#initializewithconsentmanager)メソッドで初期化します。

詳細はこちら：

* [Androidのコンセントマネージャー](/ja/platforms/android-java/consent-management/)
* [iOSのコンセントマネージャー](/ja/platforms/ios-swift/consent-management/)


**カスタム初期化**  
すべての初期化オプションは、[`initializeCustom()`](/ja/platforms/react-native-v1/api/#initializecustom)メソッドで利用可能です。

```javascript
Tealium.initializeCustom(&#39;ACCOUNT&#39;,
                         &#39;PROFILE&#39;,
                         &#39;ENVIRONMENT&#39;,
                         &#39;IOS_DATA_SOURCE_KEY&#39;,
                         &#39;ANDROID_DATA_SOURCE_KEY&#39;,
                         &#39;INSTANCE&#39;,
                         ENABLE_LIFECYCLE,        // ライフサイクル追跡を有効にする
                         &#39;PUBLISH_SETTINGS_URL&#39;,  // カスタム公開構成URL
                         &#39;TAG_MANAGEMENT_URL&#39;,    // カスタムタグ管理URL
                         USE_COLLECT_ENDPOINT,    // データエンドポイント間で切り替える、true: Tealium Collect, false: Visitor Data
                         ENABLE_CONSENT_MANAGER); // コンセント管理を有効にする
```

詳細は[APIリファレンス](/ja/platforms/react-native-v1/api/)をご覧ください。
