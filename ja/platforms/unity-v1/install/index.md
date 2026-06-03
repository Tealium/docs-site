---
title: インストール
description: UnityアプリケーションにTealium 1.xプラグインをインストールします。
url: https://docs.tealium.com/ja/platforms/unity-v1/install/
---
これはUnity用Tealiumの以前のバージョン（1.x）です。現在のバージョンについては、[Tealium for Unity 2.x](/ja/platforms/unity/)を参照してください。

Tealium for Unityを使用すると、UnityアプリケーションでTealiumのネイティブモバイルライブラリ（iOS、Android）を使用できます。

これはUnity用Tealiumの以前のバージョン（1.x）です。現在のバージョンについては、[Tealium for Unity 2.x](/ja/platforms/unity/)を参照してください。

## 必要条件

*   [Unity](https://unity.com/) 4.5以上
*   iOSまたはAndroidターゲット

## サンプルアプリ

[サンプルアプリ](https://github.com/Tealium/unity-plugin/tree/master/Sample)を探索して、Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れることができます。

## インストール

UnityアプリケーションにTealiumモバイルライブラリ（iOS/Android）を統合するには、Unityプロジェクト内の`Assets/Plugins/`ディレクトリにUnity[プラグインコード](https://github.com/Tealium/unity-plugin)のすべての内容をコピーします。

UnityプラグインがAndroidまたはiOSデバイスにデプロイされると、Tealiumイベントはそれぞれのデバイスログに記録されます。

TealiumはUnity内でAndroidおよびiOSプラットフォームのみをサポートしています。

## 初期化

Tealiumインスタンスを初期化するには、以下のパラメータを構成します：




Androidマニフェストファイル`~/Assets/Plugins/Android/AndroidManifest.xml`の以下の[meta-data](https://developer.android.com/guide/topics/manifest/meta-data-element)キーを更新して、Tealiumインスタンスを指定します。

```xml
&lt;meta-data android:name=&#34;com.tealium.library.ACCOUNT&#34; android:value=&#34;ACCOUNT&#34; /&gt;
&lt;meta-data android:name=&#34;com.tealium.library.PROFILE&#34; android:value=&#34;PROFILE&#34; /&gt;
&lt;meta-data android:name=&#34;com.tealium.library.ENVIRONMENT&#34; android:value=&#34;ENVIRONMENT&#34; /&gt;
&lt;meta-data android:name=&#34;com.tealium.library.DATA_SOURCE&#34; android:value=&#34;DATASOURCE&#34; /&gt;
&lt;!--TODO: remove for release builds--&gt;
&lt;meta-data android:name=&#34;com.tealium.library.DEBUG&#34; android:value=&#34;true&#34; /&gt;
```





`Assets/Plugins/iOS/TealiumBridge.mm`のブリッジコードファイルでTealiumアカウント情報を更新して、Tealiumインスタンスを指定します。

```swift
#define TEALIUM_INSTANCE_NAME    @&#34;TEALIUM_INSTANCE&#34;
#define TEALIUM_ACCOUNT_NAME     @&#34;ACCOUNT&#34;
#define TEALIUM_PROFILE_NAME     @&#34;PROFILE&#34;
#define TEALIUM_ENVIRONMENT_NAME @&#34;ENVIRONMENT&#34;
#define TEALIUM_DATA_SOURCE      @&#34;DATASOURCE&#34;
```




## 確認

以下のステップで、TealiumがUnityアプリケーションに正しくインストールされていることを確認します。

* Unityで、メニューから**GameObject &gt; Create Empty**を選択して新しい空の`GameObject`を作成します。`GameObject`は**Inspector**ウィンドウに表示されます。

* Unityの**Project**ウィンドウから`TealiumInitializer.cs`を選択し、**Inspector**ウィンドウにドラッグアンドドロップします。

* メニューから**Edit &gt; Project Settings &gt; Script Execution Order**を選択し、**&#43;**記号をクリックして`TealiumInitializer`スクリプトを追加します。

* `TealiumInitializer`スクリプトを既存のスクリプトのリストの一番上にドラッグし、変更を適用します。

* **Play**ボタン（または**Edit &gt; Play**）をクリックしてUnityエディタを起動し、Unityコンソールに以下のような初期化メッセージがログされていることを確認します：
      ```
      view: {
        custom_alpha : alpha
        custom_beta : beta
        screen_title : SCREEN_NAME
      }
      ```

コンソールを開くには、Unityのメインメニューから**Window &gt; General &gt; Console**を選択します。詳細を表示するには、吹き出しアイコンをクリックします。