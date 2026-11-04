---
title: 広告識別子モジュール
description: デバイスの「広告識別子」（ADID）を使用して、ディスプレイ広告ネットワークとのインタラクションを識別できるようにします。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/adid/
---


## 要件

* [Google Play Services SDK](https://developers.google.com/android/guides/setup)

## インストール

広告識別子モジュールは、Maven または手動でインストールします。

### Maven

Maven を使用して広告識別子モジュールをインストールするには、次の手順を実行します。

1. プロジェクトの最上位の `build.gradle` ファイルに、次の Maven リポジトリを追加します。
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. プロジェクトモジュールの `build.gradle` ファイルに、次の Maven 依存関係を追加します。
      ```groovy
      dependencies{
            implementation 'com.tealium:library:5.8.0' //only required if you do not have this reference
            implementation 'com.tealium:adidentifier:1.0.4'
            implementation 'com.tealium:lifecycle:1.1.4' //only required if you do not already have this reference and require lifecycle tracking
      }
      ```

3. Tealium ライブラリをインスタンス化するブロック内で、Tealium をインスタンス化した後に次のコードを追加します。  
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

広告識別子モジュールを手動でインストールするには、次の手順を実行します。

1. Tealium の [AdIdentifier](https://github.com/Tealium/tealium-android/tree/master/Modules/AdIdentifier) モジュールをダウンロードします。

2. 最上位の `build.gradle` ファイルで、次の構成を確認します。  
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

3. `tealium.adidentifier-1.0.4.aar` ファイルを、プロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

4. プロジェクトモジュールの `build.gradle` ファイルに、Tealium ライブラリの依存関係を追加します。
      ```groovy
      dependencies {
            // only required if you do not already have this reference
            implementation (name:'tealium-5.8.0', ext:'aar')
            implementation (name:'tealium.adidentifier-1.0.4', ext:'aar')
            // only required if you do not already have this reference and require lifecycle tracking
            implementation (name:'tealium.lifecycle-1.1.4', ext:'aar')
      }
      ```

## その他の考慮事項

* **アクセスがブロックされている場合**  
ユーザーが広告識別子へのアクセスを許可していない場合、モジュールは `google_adid` 変数を文字列「Ad Tracking Disabled」に構成します。サードパーティベンダーに想定どおりのデータが渡されるように、この値はタグ管理の構成で処理されます。

* **広告識別子の削除**  
保存されている広告識別子の文字列を削除するには、Tealium ライブラリが提供する標準メソッドを呼び出し、永続保存または揮発性保存から変数を削除します。この変数のキー名は、`TealiumAdIdentifier` クラスによって公開されています。次の例では、保存されている広告識別子を永続データと揮発性データの両方から削除します。変数が存在しない場合、このコードは何も実行せず、エラーもスローしません。

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

広告識別子モジュールは、次の変数をデータレイヤーに追加します。

| 変数 | 型 | 説明 | 例 |
| --- | --- | --- | --- |     
| `google_adid` | `String` | Google 広告識別子 ID | `ca-app-pub-0123456789012345~0123456789` |

## API リファレンス

広告識別子モジュールのメソッドに関する完全なリファレンスについては、Tealium SDK for Android API の [`AdIdentifier`](https://tealium.github.io/tealium-android/com/tealium/adidentifier/AdIdentifier.html) クラスを参照してください。