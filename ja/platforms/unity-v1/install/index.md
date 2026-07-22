---
title: インストール
description: UnityアプリケーションにTealium 1.xプラグインをインストールします。
url: https://docs.tealium.com/ja/platforms/unity-v1/install/
---

<blockquote>
これはUnity用Tealiumの以前のバージョン（1.x）です。現在のバージョンについては、[Tealium for Unity 2.x](https://docs.tealium.com/ja/platforms/unity/)を参照してください。
</blockquote>


Tealium for Unityを使用すると、UnityアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を使用できます。


<blockquote>
これはUnity用Tealiumの以前のバージョン（1.x）です。現在のバージョンについては、[Tealium for Unity 2.x](https://docs.tealium.com/ja/platforms/unity/)を参照してください。
</blockquote>


## 必要条件

*   [Unity](https://unity.com/) 4.5以上
*   iOSまたはAndroidターゲット

## サンプルアプリ

[サンプルアプリ](https://github.com/Tealium/unity-plugin/tree/master/Sample)を探索して、Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れることができます。

## インストール

UnityアプリケーションにTealiumモバイルライブラリ（iOS/Android）を統合するには、Unityプロジェクト内の`Assets/Plugins/`ディレクトリにUnity[プラグインコード](https://github.com/Tealium/unity-plugin)のすべての内容をコピーします。

UnityプラグインがAndroidまたはiOSデバイスにデプロイされると、Tealiumイベントはそれぞれのデバイスログに記録されます。


<blockquote>
TealiumはUnity内でAndroidおよびiOSプラットフォームのみをサポートしています。
</blockquote>


## 初期化

Tealiumインスタンスを初期化するには、以下のパラメータを構成します：




Androidマニフェストファイル`~/Assets/Plugins/Android/AndroidManifest.xml`の以下の[meta-data](https://developer.android.com/guide/topics/manifest/meta-data-element)キーを更新して、Tealiumインスタンスを指定します。

```xml
<meta-data android:name="com.tealium.library.ACCOUNT" android:value="ACCOUNT" />
<meta-data android:name="com.tealium.library.PROFILE" android:value="PROFILE" />
<meta-data android:name="com.tealium.library.ENVIRONMENT" android:value="ENVIRONMENT" />
<meta-data android:name="com.tealium.library.DATA_SOURCE" android:value="DATASOURCE" />
<!--TODO: remove for release builds-->
<meta-data android:name="com.tealium.library.DEBUG" android:value="true" />
```





`Assets/Plugins/iOS/TealiumBridge.mm`のブリッジコードファイルでTealiumアカウント情報を更新して、Tealiumインスタンスを指定します。

```swift
#define TEALIUM_INSTANCE_NAME    @"TEALIUM_INSTANCE"
#define TEALIUM_ACCOUNT_NAME     @"ACCOUNT"
#define TEALIUM_PROFILE_NAME     @"PROFILE"
#define TEALIUM_ENVIRONMENT_NAME @"ENVIRONMENT"
#define TEALIUM_DATA_SOURCE      @"DATASOURCE"
```




## 確認

以下のステップで、TealiumがUnityアプリケーションに正しくインストールされていることを確認します。

* Unityで、メニューから**GameObject > Create Empty**を選択して新しい空の`GameObject`を作成します。`GameObject`は**Inspector**ウィンドウに表示されます。

* Unityの**Project**ウィンドウから`TealiumInitializer.cs`を選択し、**Inspector**ウィンドウにドラッグアンドドロップします。

* メニューから**Edit > Project Settings > Script Execution Order**を選択し、**+**記号をクリックして`TealiumInitializer`スクリプトを追加します。

* `TealiumInitializer`スクリプトを既存のスクリプトのリストの一番上にドラッグし、変更を適用します。

* **Play**ボタン（または**Edit > Play**）をクリックしてUnityエディタを起動し、Unityコンソールに以下のような初期化メッセージがログされていることを確認します：
      ```
      view: {
        custom_alpha : alpha
        custom_beta : beta
        screen_title : SCREEN_NAME
      }
      ```


<blockquote>
コンソールを開くには、Unityのメインメニューから**Window > General > Console**を選択します。詳細を表示するには、吹き出しアイコンをクリックします。
</blockquote>
