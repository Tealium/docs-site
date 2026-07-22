---
title: Ad Identifierモジュール
description: デバイスで"Ad Identifier"（ADID）を使用して、ディスプレイ広告ネットワークとのやり取りを識別できる機能を提供します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/adid/
---


## 要件

* [Google Play Services SDK](https://developers.google.com/android/guides/setup)

## インストール

Ad IdentifierモジュールをMavenによって、または手動でインストールします。

### Maven

Ad IdentifierモジュールをMavenによってインストールするには：

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenレポジトリを追加します。
```groovy
maven {
      url "https://maven.tealiumiq.com/android/releases/"
}
```

2. プロジェクトモジュールの`build.gradle`ファイルに、以下のようにMavenの依存関係を追加します。
```groovy
dependencies{
      implementation 'com.tealium:library:5.8.0' //only required if you do not have this reference
      implementation 'com.tealium:adidentifier:1.0.4'
      implementation 'com.tealium:lifecycle:1.1.4' //only required if you do not already have this reference and require lifecycle tracking
}
```

3. Tealiumをインスタンス化した後で、Tealiumライブラリをインスタンス化する同じブロックで、以下を追加します。
```java
// import the Tealium AdIdentifier module in the import section
import com.tealium.adidentifier.AdIdentifier;

// context to pass to AdIdentifier module
Context mContext = this;

// substitute the example instance name here with the same instance name you used when initializing the Tealium library
private static final String TEALIUM_INSTANCENAME = "INSTANCE_NAME";

// call this to store the referrer as Persistent data - recommended
AdIdentifier.setIdPersistent(TEALIUM_INSTANCENAME, mContext);

// call this to store the referrer as Volatile data (reset at app restart/terminate) - not recommended in most cases
AdIdentifier.setIdVolatile(TEALIUM_INSTANCENAME, mContext);
```

### 手動

Ad Identifierモジュールを手動でインストールするには：

1. Tealium [AdIdentifier](https://github.com/Tealium/tealium-android/tree/master/Modules/AdIdentifier)モジュールをダウンロードします。

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

3. ファイル`tealium.adidentifier-1.0.4.aar`をプロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

4. Tealiumライブラリの依存関係をプロジェクトモジュールの`build.gradle`ファイルに追加します。
```groovy
dependencies {
      // only required if you do not already have this reference
      implementation (name:'tealium-5.8.0', ext:'aar')
      implementation (name:'tealium.adidentifier-1.0.4', ext:'aar')
      // only required if you do not already have this reference and require lifecycle tracking
      implementation (name:'tealium.lifecycle-1.1.4', ext:'aar')
}
```

## 追加の検討事項

*  **ブロックされたアクセス**
ユーザーがAd Identifierへのアクセスを許可していない場合、モジュールは`google_adid`変数に文字列"Ad Tracking Disabled"を構成します。この文字列はTealium iQ構成で処理されて、期待されるデータをサードパーティベンダーに確実に渡すことができます。

* **Ad Identifierの削除**
保存されたAd Identifier文字列を削除するには、Tealiumライブラリに用意されている標準メソッドをコールして、永続的保存または揮発性保存から変数を削除します。変数のキー名は、`TealiumAdIdentifier`クラスによって公開されます。永続性データと揮発性データの両方から保存されたAd Identifierを削除する例を次に示します。変数が存在しない場合、このコードは何も行わず、エラーも発生しません。

```java
// import the Tealium AdIdentifier module in the import section
import com.tealium.adidentifier.AdIdentifier;

private static final String TEALIUM_INSTANCENAME = "INSTANCE_NAME";
final Tealium instance = Tealium.getInstance(TEALIUM_INSTANCENAME);

// remove from persistent data store
instance.getDataSources().getPersistentDataSources().edit().remove(AdIdentifier.KEY_GOOGLE_ADID).apply();

// remove from volatile data store (session only)
instance.getDataSources().getVolatileDataSources().remove(AdIdentifier.KEY_GOOGLE_ADID);
```

## データレイヤー

Ad Identifierモジュールは、データレイヤーに以下の変数を追加します。

| 変数 | 型| 説明| 例|
| --- | ---| --- | --- |     
| `google_adid` | `String` | Google Ad Identifier ID| `ca-app-pub-0123456789012345~0123456789` |

## APIリファレンス

Ad Identifierモジュールのメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`AdIdentifier`](https://tealium.github.io/tealium-android/com/tealium/adidentifier/AdIdentifier.html)クラスを参照してください。
