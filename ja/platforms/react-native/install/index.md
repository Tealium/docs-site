---
title: インストール
description: React Native用Tealiumのインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/react-native/install/
---
Tealium for React Nativeは、React NativeアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を使用できます。

これはReact Native用Tealiumの現行バージョン（2.x）です。
以前のバージョンについては、[Tealium for React Native 1.x](/ja/platforms/react-native-v1/)を参照してください。

## 動作原理

Tealiumモバイルライブラリは、以下の2つの方法のいずれかを使用してReact Nativeアプリケーションに統合されます：

*   NPMパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native)経由で手動

## 要件

* ネイティブビルド環境へのアクセス
* [React Native 0.63&#43;](https://github.com/Tealium/tealium-react-native)およびツールがインストールされていること。
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/ja/platforms/android-kotlin/)または[Tealium for iOS](/ja/platforms/ios-swift/)

## サンプルアプリ

ライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、[React Nativeサンプルアプリ](https://github.com/Tealium/tealium-react-native/tree/master/example)をダウンロードすることをお勧めします。

## インストール（NPM/YARN）

NPMを使用してReact Native用Tealiumライブラリをインストールするには：

1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドで`tealium-react-native`パッケージをダウンロードしてインストールします：
      ```bash
      yarn install tealium-react-native
      ```
3. NPMパッケージのバージョン1.0.7からReact Native Autolinkingが有効になり、React Nativeのバージョン0.60&#43;を使用している場合、`react-native link`を実行する必要はありません。

### Android

Androidプロジェクトのルート`build.gradle`ファイルにTealiumのMavenリポジトリへの参照を追加します。これは[Android Maven Install](/ja/platforms/android/install/#maven-install)のドキュメントに記載されています。プロジェクトの依存関係はAutolinkingプロセスによって自動的に処理されます。

### iOS

React Native 0.60&#43;のAutolinking機能は、必要なCocoaPods依存関係を自動的にiOSアプリケーションワークスペースに追加します。

ポッドをインストールするには、次のコマンドを実行します：

```bash
// React Nativeアプリケーションフォルダーから：
cd ios &amp;&amp; pod install
```

バージョン2.2.0から2.5.1までは、Podfileに次の参照を追加します：`pod &#34;tealium-react-native-swift&#34;, :path =&gt; &#39;../node_modules/tealium-react-native/tealium-react-native-swift.podspec&#39;`。
バージョン2.6.0以降では、この追加の依存関係は不要になり、削除する必要があります。

場合によっては、フレームワークモジュール内の非モジュラーなインクルードを許可するために`clang`パラメータを有効にする必要があります。clangパラメータを有効にするには：

1. Xcodeでアプリの`.xcworkspace`ファイルを開き、ナビゲーターから`Pods`を選択します。

2. **Targets**の下で**tealium-react-native**ターゲットを選択し、**Build Settings**タブをクリックします。

3. **Apple Clang - Language - Modules** &gt; **Allow Non-modular Includes In Framework Modules**の下で次の構成を見つけて更新します：
      ```groovy
      CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES = YES;
      ```

#### ブリッジングヘッダ

`TealiumReactNative`モジュールは[`Tealium iOS (Swift)`](/ja/platforms/ios-swift)ライブラリを使用します。React NativeからSwiftにObjective-Cファイルを公開するには、Xcodeを使用してiOSプロジェクトにブリッジングヘッダーファイルを作成します。

1. Xcodeで**File &gt; New &gt; File...**を選択します。
2. テンプレートとして**Swift File**を選択し、**Next**をクリックします。
3. **Group**ドロップダウンで、アプリのトップレベルフォルダを選択します（プロジェクトではありません）。
4. &#34;Objective-Dブリッジングヘッダーを構成しますか？&#34;というプロンプトが表示されたら、**Create Bridging Header**を選択してブリッジングヘッダーファイルを生成します。

ブリッジングヘッダーファイル名は`YourProject-Bridging-Header.h`の形式です。Xcodeが生成したファイル名でプロジェクトを構成するため、ファイル名を変更しないでください。

ブリッジングヘッダーの追加はプロジェクトごとに一度だけ求められます。

## JavaScript

モジュールをアプリにインポートする方法は、インストール方法によって異なります。

NPM経由でインストールした場合、次の行をコードに追加します：

```javascript
import Tealium from &#39;tealium-react-native&#39;;
```

手動でインストールした場合は、[GitHubリポジトリ](https://github.com/Tealium/tealium-react-native)の`npm-package`フォルダ内の`index.js`ファイルを見つけ、`TealiumModule.js`に名前を変更してReact Native JavaScriptプロジェクトにコピーします。

インストール後、次のようにTealiumモジュールをアプリのJavaScriptコードにインポートします：

```javascript
import Tealium from &#39;tealium-react-native&#39;;
import { TealiumConfig, TealiumView, TealiumEvent, ConsentCategories, Dispatchers, Collectors, ConsentPolicy, Expiry, ConsentExpiry, TimeUnit, ConsentStatus, TealiumEnvironment } from &#39;tealium-react-native/common&#39;;
```

## 初期化

アプリがインストールされたら、次の例に示すように[`initialize()`](/ja/platforms/react-native/api/#initialize)メソッドを使用して`Tealium`インスタンスを初期化します：

```javascript
let config: TealiumConfig = {
      // &#39;ACCOUNT&#39;をあなたのTealiumアカウント名に置き換えてください
      account: &#39;ACCOUNT&#39;,
      // &#39;PROFILE&#39;をあなたのTealiumプロファイル名に置き換えてください
      profile: &#39;PROFILE&#39;,
      environment: TealiumEnvironment.dev,
      dispatchers: [Dispatchers.Collect, Dispatchers.RemoteCommands, Dispatchers.TagManagement],
      collectors: [Collectors.AppData, Collectors.DeviceData, Collectors.Lifecycle, Collectors.Connectivity],
      consentPolicy: ConsentPolicy.gdpr,
      visitorServiceEnabled: true
};
Tealium.initialize(config);
```
詳細および追加の構成オプションについては、[APIリファレンス](/ja/platforms/react-native/api/)を参照してください。
