---
title: Optimizely X Trackingモジュール
description: Optimizely XとTealium Collectの統合をもたらします。このモジュールは、Optimizely Xライブラリによってトリガーされるイベントを監視し、イベントデータをTealium Collectに渡します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/optimizely-x-tracking/
---
## 要件

* [Optimizely X Android SDK](https://developers.optimizely.com/classic/android/getting-started/index.html)がアプリに追加されていること


## インストール

Optimizely X TrackingモジュールをMavenによって、または手動でインストールします。

### Maven

Optimizely X TrackingモジュールをMavenによってインストールするには：

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenレポジトリを追加します。
```groovy
maven {
      url "https://maven.tealiumiq.com/android/releases/"
}
```

2. プロジェクトモジュールの`build.gradle`ファイルに、以下のようにMavenの依存関係を追加します。
```groovy
dependencies{
      //only required if you do not have this reference
      implementation 'com.tealium:library:5.8.0'
      implementation 'com.tealium:optimizelylistener:1.1.2'
      //only required if you do not already have this reference and require lifecycle tracking
      implementation 'com.tealium:lifecycle:1.1.4'
}
```

### 手動

Optimizely Xモジュールを手動でインストールするには：

1. Tealium [OptimizelyListener](https://github.com/Tealium/tealium-android/tree/master/Modules/Optimizely)モジュールをダウンロードします。

2. 最上位の`build.gradle`ファイルで、以下を検証します。
```groovy
allprojects {
      repositories {
         mavenCentral()
         flatDir {
              dirs 'libs'
         }
      }
}
```

3. ファイル`tealium.optimizelylistener-1.1.1.aar`をプロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

4. Tealiumライブラリの依存関係をプロジェクトモジュールの`build.gradle`ファイルに追加します。
```groovy
dependencies {
      // only required if you do not already have this reference
      implementation(name:'tealium-5.6.1', ext:'aar')
      implementation(name:'tealium.optimizelylistener-1.1.1', ext:'aar')
      // only required if you do not already have this reference and require lifecycle tracking
      implementation(name:'tealium.lifecycle-1.1.2', ext:'aar')
}
```

## 初期化

このモジュールは、`OptimizelyManager`の初期化が完了した後に初期化する必要があります。不適切なタイミングで初期化した場合、一部または全部のイベントがトラッキングされない可能性があります。

`Optimizely`には、`OptimizelyManager`が初期化されるとすぐに呼び出されるリスナーが用意されています。

```java
// import the Tealium OptimizelyListener module in the import section
import com.tealium.optimizelylistener.TealiumOptimizelyEventListener;
//...

// substitute the example instance name here with the same instance name you used when initializing the Tealium library
private static final String TEALIUM_INSTANCENAME = "teal";

myOptlyManager.initialize(getApplicationContext(), new OptimizelyStartListener() {
    @Override public void onStart(OptimizelyClient optimizely) {
        // call this to init the Optimizely listener with a valid OptimizelyManager instance
        // myOptlyManager is your own reference to the global OptimizelyManager instance
        TealiumOptimizelyEventListener.init(TEALIUM_INSTANCENAME, myOptlyManager);
        // activate experiment AFTER initializing the Tealium listener.
        // tracking calls are missed if not done in this order.
        Variation v = optimizely.activate("tealiumtest", "userid");
    }
});
```

モジュールの初期化が完了した後は、特に追加の構成は必要ありません。モジュールは`Optimizely` SDKからの通知を監視するようになり、必要に応じてTealium SDKにデータを渡します。


## 自動トラッキングされるイベント

Tealium Collectに渡される`Optimizely`イベントは、実験とカスタムイベントの2種類です。 

これらのイベントは、`tealium_event`変数に値とともに構成されます。

* **Optimizely Experiment Started**
`Optimizely` SDKが実験を有効化したとき。
* **Optimizely Event Tracked**
`Optimizely` SDKがカスタムイベントを受け取ったとき（`Optimizely`の`track`メソッドを手動で呼び出すことで生成）。

## データレイヤー

トラッキングされる`Optimizely`イベントには、以下のイベント属性が含まれます。

| 変数 | スコープ| 説明| 例|
| --- | ---| --- | --- |
| `optimizely_ experiment_key` | 揮発性（セッション）| `Optimizely`実験名| `"Homescreen MVT"` |
| `optimizely_ variation_key` | 揮発性（セッション）|  `Optimizely`変数名| `"Variation A"` |
| `optimizely_ user_id` | 揮発性（セッション）| `Optimizely`ユーザーID| `"[alice@tealium.com](mailto:alice@tealium.com)"`|
| `optimizely_ event _key` | ヒット（単一イベント）| `Optimizely`イベント名| `"purchase"` |
| `optimizely_ event _value` | ヒット（単一イベント）| `Optimizely`イベント値| `"123"`（整数のみ）|
| `optimizely_ XXX` | ヒット（単一イベント）| すべての`Optimizely`カスタム属性の先頭に`"optimizely_"`がエンリッチメントされ、Tealiumに直接渡されます| |

### 変数名の上書き（オプション）

異なる名前付け規則を使用したい場合は、デフォルトの変数名を簡単にオーバーライドできます。変数名のオーバーライドは、`TealiumOptimizelyEventListener`クラスの一連のパブリックプロパティを変更することによって行われます。

```java
import com.tealium.optimizelylistener;
//...

TealiumOptimizelyEventListener.OPTIMIZELY_EXPERIMENT_KEYNAME = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_VARIATION_KEYNAME = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_USERID_KEYNAME = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_EVENTKEY_KEYNAME = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_EVENTVALUE_KEYNAME = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_EXPERIMENT_STARTED = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_EVENT_TRACKED = <your new value>;
TealiumOptimizelyEventListener.OPTIMIZELY_ATTRIBUTE_PREFIX = <your new value>;
```

## APIリファレンス

Optimizely X Trackingモジュールのメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`TealiumOptimizelyEventListener`](https://tealium.github.io/tealium-android/com/tealium/optimizelylistener/TealiumOptimizelyEventListener.html)クラスを参照してください。

