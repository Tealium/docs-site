---
title: Install Referrerモジュール
description: アプリのインストールリファラー情報を（使用可能な場合に）自動的に収集し、それをデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/install-referrer/
---

## 要件

* [Tealium for Android](/ja/platforms/android-java/)（5.0.0以降）（[4.x向けソリューション](#solution-for-tealium-sdk-4-x)）

## インストール

Install ReferrerモジュールをMavenによって、または手動でインストールします。

### Maven

Install ReferrerモジュールをMavenによってインストールするには：

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenレポジトリを追加します。
```groovy
maven {
      url &#34;https://maven.tealiumiq.com/android/releases/&#34;
}
```  
2. プロジェクトモジュールの`build.gradle`ファイルに、以下のようにMavenの依存関係を追加します。
```groovy
dependencies{
      // only required if you do not have this reference
      implementation &#39;com.tealium:library:5.8.0&#39;
      implementation &#39;com.tealium:installreferrer:1.1.3&#39;
      // only required if you do not already have this reference and require lifecycle tracking
      implementation &#39;com.tealium:lifecycle:1.1.4&#39;
      // Google&#39;s Install Referrer API
      implementation &#39;com.android.installreferrer:installreferrer:1.0&#39;
}
```  
[Google Install Referrer API](https://developer.android.com/google/play/installreferrer/library)はこのモジュールの依存関係の1つですが、自動的には追加されません。ビルドにこのモジュールを追加してください。

3. （Tealiumをインスタンス化した後で）Tealiumライブラリをインスタンス化する同じブロックで、以下を追加します。

```java
// import the Tealium InstallReferrer module in the import section
import com.tealium.installreferrer.InstallReferrerReceiver;

// substitute the example instance name here with the same instance name you used when initializing the Tealium library
private static final String TEALIUM_INSTANCENAME = &#34;INSTANCE_NAME&#34;;

// call this to store the referrer as Persistent data - recommended
InstallReferrerReceiver.setReferrerPersistent(applicationContext, TEALIUM_INSTANCENAME);

// call this to store the referrer as Volatile data (reset at app restart/terminate) - not recommended in most cases
InstallReferrerReceiver.setReferrerVolatile(applicationContext, TEALIUM_INSTANCENAME);
```

### 手動

Install Referrerモジュールを手動でインストールするには：

1. Tealium [Install Referrer](https://github.com/Tealium/tealium-android/tree/master/Modules/InstallReferrer)モジュールをダウンロードします。

2. 最上位の`build.gradle`ファイルで、以下を検証します。
```groovy
allprojects {
      repositories {
        mavenCentral()
        flatDir {
            dirs &#39;libs&#39;
        }
      }
}
```  

3. ファイル `tealium.installreferrer-1.1.2.aar` をプロジェクトの `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` ディレクトリにコピーします。

4. Tealiumライブラリの依存関係をプロジェクトモジュールの`build.gradle`ファイルに追加します。
```groovy
dependencies {
      // only required if you do not already have this reference
      implementation(name:&#39;tealium-5.6.1&#39;, ext:&#39;aar&#39;)
      implementation(name:&#39;tealium.installreferrer-1.1.2&#39;, ext:&#39;aar&#39;)
      // only required if you do not already have this reference and require lifecycle tracking
      implementation(name:&#39;tealium.lifecycle-1.1.2&#39;, ext:&#39;aar&#39;)
      // Google&#39;s Install Referrer API
      implementation &#39;com.android.installreferrer:installreferrer:1.0&#39;
}
```


## 値の例

受信URLがすべての指定されたキャンペーン情報を含んでいたと仮定すると、`INSTALL_REFERRER`変数には以下のURL形式データが受信されると予想できます。

```
utm_medium=test_medium&amp;
utm_term=test_term&amp;
utm_content=test_content&amp;
utm_campaign=test_name
```

## 追加の検討事項

**保存されたリファラーの削除**
保存されたインストールリファラー文字列を削除するには、Tealiumライブラリに用意されている標準メソッドを呼び出して、永続的または揮発性保存から変数を削除します。変数のキー名は、`InstallReferrerReceiver`クラスによって公開されます。次の例では、保存されたインストールリファラーが永続性データと揮発性データの両方から削除されます。変数が存在しない場合、このコードは何も行わず、エラーも発生しません。

```java
// remove from persistent data store
instance.getDataSources().getPersistentDataSources().edit().remove(InstallReferrerReceiver.KEYNAME).apply();

// remove from volatile data store (session only)
instance.getDataSources().getVolatileDataSources().remove(InstallReferrerReceiver.KEYNAME);
```

## Tealium SDK 4.xでの対応策

Install ReferrerモジュールはTealium SDK 5.xとのみ互換性があります。

SDK 4.xでこの機能を実現するには、以下のコードを使用します。

```xml
// Android Manifest
&lt;receiver
    android:name=&#34;com.tealium.InstallReferrerReceiver&#34;
    android:exported=&#34;true&#34;&gt;
    &lt;intent-filter&gt;
        &lt;action android:name=&#34;com.android.vending.INSTALL_REFERRER&#34; /&gt;
    &lt;/intent-filter&gt;
&lt;/receiver&gt;
```

```java
// Class for retrieving install referrer
public class InstallReferrerReceiver extends BroadcastReceiver {

    private static final String INSTALL_REFERRER = &#34;INSTALL_REFERRER&#34;;

    public void onReceive(Context context, Intent intent) {
        if (intent != null) {
            return;
        }
        Bundle extras = intent.getExtras();
        if (extras == null) {
            return;
        }
        String referrer = extras.getString(&#34;referrer&#34;);

        if (StringUtils.isNotBlank(referrer)) {
            Tealium.getGlobalCustomData().edit().putString(INSTALL_REFERRER, referrer).apply();
        }
    }
}
```
## APIリファレンス

Install Referrerモジュールのメソッドの完全なリファレンスについては、Tealium SDK for Android APIの[`InstallReferrerReceiver`](https://tealium.github.io/tealium-android/com/tealium/installreferrer/InstallReferrerReceiver.html)クラスを参照してください。
