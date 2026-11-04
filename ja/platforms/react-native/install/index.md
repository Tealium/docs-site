---
title: インストール
description: React Native向けTealiumのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/install/
---
Tealium for React Nativeを使用すると、React NativeアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を利用できます。


<blockquote>
これはTealium for React Nativeの現行バージョン（2.x）です。  
以前のバージョンについては、[Tealium for React Native 1.x](https://docs.tealium.com/ja/platforms/react-native-v1/)を参照してください。
</blockquote>


## 仕組み

Tealiumモバイルライブラリは、次のいずれかの方法でReact Nativeアプリケーションに統合します。

*   NPMパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native)を使用して手動で統合

## 要件

* ネイティブビルド環境へのアクセス
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)および必要なツールがインストールされていること
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## サンプルアプリ

ライブラリ、トラッキングメソッド、およびベストプラクティスに沿った実装に慣れるため、[React Nativeサンプルアプリ](https://github.com/Tealium/tealium-react-native/tree/master/example)をダウンロードすることをお勧めします。

## インストール（NPM/YARN）

NPMを使用してReact Native向けTealiumライブラリをインストールするには、次の手順を実行します。

1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドを使用して、`tealium-react-native`パッケージをダウンロードしてインストールします。  
      ```bash
      yarn install tealium-react-native
      ```
3. NPMパッケージのバージョン1.0.7以降ではReact Native Autolinkingが有効になっているため、React Native 0.60以降を使用している場合は、`react-native link`を実行する必要はありません。

### Android

[Android Mavenのインストール](https://docs.tealium.com/ja/platforms/android/install/#maven-install)ドキュメントの説明に従って、Androidプロジェクトのルートにある`build.gradle`ファイルにTealiumのMavenリポジトリへの参照を追加します。プロジェクトの依存関係は、Autolinkingプロセスによって自動的に処理されます。

### iOS

React Native 0.60以降のAutolinking機能により、必要なCocoaPods依存関係がiOSアプリケーションのワークスペースに自動的に追加されます。

Podをインストールするには、次のコマンドを実行します。

```bash
// From your React Native application folder:
cd ios && pod install
```


<blockquote>
バージョン2.2.0から2.5.1では、Podfileに次の参照を追加してください：`pod "tealium-react-native-swift", :path => '../node_modules/tealium-react-native/tealium-react-native-swift.podspec'`。
バージョン2.6.0以降では、この追加の依存関係は不要になったため、削除する必要があります。
</blockquote>


場合によっては、フレームワークモジュール内で非モジュール形式のインクルードを許可するために、`clang`パラメータを有効にする必要があります。clangパラメータを有効にするには、次の手順を実行します。

1. Xcodeでアプリの`.xcworkspace`ファイルを開き、ナビゲーターから`Pods`を選択します。

2. **Targets**で**tealium-react-native**ターゲットを選択し、**Build Settings**タブをクリックします。

3. **Apple Clang - Language - Modules** > **Allow Non-modular Includes In Framework Modules**にある次の構成を見つけて更新します。  
      ```groovy
      CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES = YES;
      ```

#### ブリッジングヘッダー

`TealiumReactNative`モジュールは、[`Tealium iOS (Swift)`](https://docs.tealium.com/ja/platforms/ios-swift)ライブラリを使用します。React NativeのObjective-CファイルをSwiftに公開するには、Xcodeを使用してiOSプロジェクトにブリッジングヘッダーファイルを作成します。

1. Xcodeのメニューから**File > New > File...**を選択します。
2. テンプレートとして**Swift File**を選択し、**Next**をクリックします。
3. **Group**ドロップダウンで、アプリの最上位フォルダー（プロジェクトではありません）を選択します。
4. 「Would you like to configure an Objective-D bridging header?」というプロンプトが表示されたら、**Create Bridging Header**を選択してブリッジングヘッダーファイルを生成します。

ブリッジングヘッダーのファイル名は`YourProject-Bridging-Header.h`という形式です。Xcodeは生成されたファイル名を使用してプロジェクトを構成するため、ファイル名を変更しないでください。


<blockquote>
ブリッジングヘッダーを追加するためのプロンプトは、プロジェクトごとに一度だけ表示されます。
</blockquote>


## JavaScript

モジュールをアプリにインポートする方法は、インストール方法によって異なります。

NPMを使用してインストールした場合は、コードに次の行を追加します。

```javascript
import Tealium from 'tealium-react-native';
```

手動でインストールした場合は、[GitHubリポジトリ](https://github.com/Tealium/tealium-react-native)の`npm-package`フォルダーで`index.js`ファイルを探し、ファイル名を`TealiumModule.js`に変更して、React Native JavaScriptプロジェクトにコピーします。

インストール後、次のようにTealiumモジュールをアプリのJavaScriptコードにインポートします。

```javascript
import Tealium from 'tealium-react-native';
import { TealiumConfig, TealiumView, TealiumEvent, ConsentCategories, Dispatchers, Collectors, ConsentPolicy, Expiry, ConsentExpiry, TimeUnit, ConsentStatus, TealiumEnvironment } from 'tealium-react-native/common';
```

## 初期化

アプリへのインストールが完了したら、次の例のように[`initialize()`](https://docs.tealium.com/ja/platforms/react-native/api/#initialize)メソッドを使用して`Tealium`インスタンスを初期化します。

```javascript
let config: TealiumConfig = {
      // Replace 'ACCOUNT' with your Tealium account name
      account: 'ACCOUNT',
      // Replace 'PROFILE' with your Tealium profile name
      profile: 'PROFILE',
      environment: TealiumEnvironment.dev,
      dispatchers: [Dispatchers.Collect, Dispatchers.RemoteCommands, Dispatchers.TagManagement],
      collectors: [Collectors.AppData, Collectors.DeviceData, Collectors.Lifecycle, Collectors.Connectivity],
      consentPolicy: ConsentPolicy.gdpr,
      visitorServiceEnabled: true
};
Tealium.initialize(config);
```

詳細および追加の構成オプションについては、[APIリファレンス](https://docs.tealium.com/ja/platforms/react-native/api/)を参照してください。