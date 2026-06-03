---
title: インストール
description: UnityアプリケーションにTealiumプラグインをインストールします。
url: https://docs.tealium.com/ja/platforms/unity/install/
---
 Tealium for Unityプラグインのアクティブな開発は終了しました。このプラグインを使用していてサポートが必要な場合は、Tealiumサポートに連絡してください。 

Tealium for Unityは、iOSおよびAndroidのUnityアプリケーションでTealiumネイティブモバイルライブラリを提供します。

## 要件

* [Unity 2020.3&#43;](https://docs.unity3d.com/Manual/UnityOverview.html)
* [Tealium for Android](/ja/platforms/android-kotlin/) または [Tealium for iOS](/ja/platforms/ios-swift/)

## サンプルアプリ

iOSまたはAndroidの[サンプルアプリ](https://github.com/Tealium/unity-plugin)を探索して、Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れてください。

iOSアプリの場合は、XCodeで `Examples/TealiumUnity-iOS/Unity-iPhone.xcodeproj` ファイルを開きます。Androidアプリの場合は、Android Studioで `Examples/TealiumUnity-Android/TealiumUnity-Android.apk` ファイルを開きます。

または、`Assets/Scenes` と `Assets/Scripts` の内容をプロジェクトにドラッグして、`Tealium.unitypackage`をインポートします。

## インストール

TealiumはUnity内でAndroidおよびiOSプラットフォームのみをサポートしています。

### パッケージのインポート

推奨されるインストール方法は、`.unitypackage`として`TealiumUnityPlugin`を使用することです。

1. [GitHubのリリースページ](https://github.com/Tealium/unity-plugin/tree/release/2.0.0)にアクセスし、最新リリースから`Tealium.unitypackage`をダウンロードします。
2. 新しいUnityプロジェクトを作成するか、既存のプロジェクトを開きます。
3. **Assets &gt; Import Package &gt; Custom Package** を選択して、プロジェクトに`Tealium.unitypackage`をインポートします。
4. 次のインポートステートメントをプロジェクトに追加します：
      ```bash
      using TealiumCommon;
      ```

### マニュアル

iOSまたはAndroidのUnityアプリケーションにTealium for Unityを手動でインストールするには：

1. [GitHubリポジトリ](https://github.com/Tealium/unity-plugin)をクローンします。
2. `Assets/Plugins` と `Assets/Tealium` フォルダーをプロジェクトにコピーします。
3. 次のインポートステートメントをプロジェクトに追加します：
      ```bash
      using TealiumCommon;
      ```

### iOS

プロジェクトを初めてビルドして実行した後、XCode内でTealiumフレームワークを手動でリンクします：

1. **Unity-iPhone** プロジェクトをクリックします。
2. **Build Phases** タブをクリックします。
3. **Embedded Frameworks** セクションを展開します。
4. `Frameworks/Plugins/iOS` フォルダーにあるすべてのフレームワークを**Embedded Frameworks**セクションにコピーします。

`TealiumUnityPlugin`は、オブジェクトのシリアライズとデシリアライズにUnityプラグイン`JSON.net`に依存しています。プロジェクトに`JSON.net`がすでに含まれている場合は、競合を避けるために削除する必要があります。


## 初期化

次の例に示すように、[`Initialize()`](/ja/platforms/unity/api/#initialize)メソッドを使用してTealiumインスタンスを初期化します：

```javascript
private TealiumConfig config = new TealiumConfig(&#34;tealiummobile&#34;,
                     &#34;demo&#34;,
                     TealiumEnvironment.DEV,
                     new List&lt;Dispatchers&gt; {
                        Dispatchers.TagManagement,
                        Dispatchers.Collect,
                        Dispatchers.RemoteCommands },
                     new List&lt;Collectors&gt; {
                        Collectors.AppData,
                        Collectors.DeviceData,
                        Collectors.Lifecycle,
                        Collectors.Connectivity },
                     logLevel: LogLevel.Dev,
                     batchingEnabled: false,
                     visitorServiceEnabled: true);

TealiumUnityPlugin.Initialize(config);
```