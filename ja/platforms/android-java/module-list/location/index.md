---
title: Locationモジュール
description: イベントのデバイス位置データに加え、目標物の周囲にジオフェンスを追加する機能を提供します。
url: https://docs.tealium.com/ja/platforms/android-java/module-list/location/
---
Locationモジュールを使用すると、Androidアプリが位置情報を受信し、ジオフェンスを構成および監視できるようになります。位置追跡とジオフェンシングの詳細については、[こちら](https://docs.tealium.com/ja/platforms/getting-started/location/)を参照してください。

## サポートされているプラットフォーム

以下のプラットフォームがサポートされています。

* [Android](https://docs.tealium.com/ja/platforms/android-java/)
* [Android TV](https://docs.tealium.com/ja/platforms/android-java/tv/)
* [Android Wear](https://docs.tealium.com/ja/platforms/android-java/wear/)

## 要件

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)（5.6.0以降）
* Google Play Services [Location](https://developer.android.com/training/location)（11.0.0以降）

このモジュールはFirebase Cloud Messagingをサポートしています。

## サンプルアプリ

当社のライブラリ、トラッキングメソッド、ベストプラクティスの実装に精通していただけるよう、[Android Locationモジュールのサンプルアプリ](https://github.com/Tealium/tealium-android/tree/master/Modules/Location)をご確認いただけるようになっています。

## インストール

このモジュールをMavenによって（推奨）、または手動でインストールします。インストールした後で、次のインポートステートメントを追加します。
```groovy
import com.tealium.location.TealiumLocation;
```

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトの最上位の`build.gradle`ファイルに、次のMavenレポジトリを追加します。
```groovy
maven {
      url "https://maven.tealiumiq.com/android/releases/"
}
```
2. プロジェクトモジュールの`build.gradle`ファイルに、Tealiumライブラリ、Locationモジュール、およびGoogle Play Services Location APIのMaven依存関係を追加します。
```groovy
dependencies {
      implementation 'com.tealium:library:5.8.0'
      implementation 'com.tealium:location:1.0.0'
      runtimeOnly 'com.google.android.gms:play-services-location:17.0.0'
}
```

### 手動

Locationモジュールを手動でインストールするには：

1. [Locationモジュール](https://github.com/Tealium/tealium-android/tree/master/Modules/Location)をダウンロードします。


2. 最上位の`build.gradle`ファイルで、以下を検証します。
```groovy
allprojects {
      repositories {
          ...
          google()
          flatDir {
              dirs 'libs'
          }
          ...
      }
}
```
3. ファイル`tealium.location-1.0.0.aar`をプロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

4. Tealiumライブラリの依存関係をプロジェクトモジュールの`build.gradle`ファイルに追加します。
```groovy
dependencies {
      // only required if you do not already have this reference
      implementation(name:'tealium-5.6.0', ext:'aar')
      // location module reference
      implementation(name:'tealium.location-1.0.0', ext:'aar')
      // Google's Location Services API reference
      runtimeOnly 'com.google.android.gms:play-services-location:17.0.0'
  }
```

## 初期化

Tealium インスタンス名を [`TealiumLocation.setupInstance()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#setupinstance)に渡して、Location モジュールを初期化します。

```java
Set<String> tealiumInstances = new HashSet<>();
tealiumInstances.add(TealiumHelper.TEALIUM_MAIN);

mInstance = TealiumLocation.setupInstance(this, tealiumInstances);
```

## 位置追跡

Location モジュールは、有効化され、 [位置情報へのアクセス許可](#location-permissions) を付与されると、継続的な位置追跡を自動的に実行します。位置情報の更新は、精度と時間間隔という2つの構成に基づいています。

精度は高または低に構成できます。高精度はAndroid構成の`PRIORITY_HIGH_ACCURACY`に対応し、低精度はAndroid構成の`PRIORITY_BALANCED_POWER_ACCURACY`に対応します。

Android位置情報の精度構成の詳細については、[こちら](https://developer.android.com/guide/topics/location/battery#accuracy)を参照してください。

位置情報の更新間隔は、ミリ秒単位の値で構成されます。アプリにとって好適な範囲内で可能な限り高い値を使用してください。間隔の値は、Androidの`setInterval()`および`setFastestInterval()`メソッドに渡されます。

Android位置情報の間隔構成の詳細については、[こちら](https://developer.android.com/guide/topics/location/battery#frequency)を参照してください。

位置追跡を開始するには、 [`TealiumLocation.startLocationUpdates()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#startlocationupdates)を呼び出します。最初のパラメータを高精度のトラッキングの場合は`true`、精度を下げたトラッキングの場合は`false`に構成します。

次の例では、高精度と60000ミリ秒（60秒）の時間間隔を使用します。
```java
TealiumLocation.getInstance().startLocationUpdates(true, 60000);

```

継続的な位置追跡を無効にするには、 `TealiumLocation.destroyInstance()` または [`TealiumLocation.stopLocationUpdates()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#stoplocationupdates)メソッドを呼び出します。

### 位置情報へのアクセス許可

アプリで、位置情報へのアクセス許可を付与するには:

1. 位置情報リクエスト コードの定数変数を構成するには:
```java
public static final int LOCATION_REQUEST_CODE = 101;
```

2. アプリの `MainActivity` クラスに次のメソッドを追加します:　
```java
public void requestLocationPermission() {
        if (ContextCompat.checkSelfPermission(getApplicationContext(),
        Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            ActivityCompat.requestPermissions(this,
              new String[]{
                  Manifest.permission.ACCESS_FINE_LOCATION,
                  Manifest.permission.ACCESS_COARSE_LOCATION
              }, LOCATION_REQUEST_CODE);
        }
    }
```

3. `requestLocationPermission()` メソッドを `onCreate()` メソッド (`MainActivity` クラス) の中で呼び出します。
```java
if ((ContextCompat.checkSelfPermission(getApplicationContext(),
      Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
      && ContextCompat.checkSelfPermission(getApplicationContext(),
      Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
          requestLocationPermission();
  }
```

4. 任意で、位置情報へのアクセス許可が付与されたことを確認するには、 `onRequestPermissionsResult`() メソッドをオーバーライドします:
```java
@Override
public void onRequestPermissionsResult(int requestCode,
      String[] permissions,
      int[] grantResults) {
        String message;
        if (requestCode == LOCATION_REQUEST_CODE) {
            // If request is cancelled, the result arrays are empty.
            if ((grantResults.length > 0) && (grantResults[0]
              == PackageManager.PERMISSION_GRANTED)) {
                message = "Location Permission Granted";
            } else {
                message = "Location Permission Not Granted";
            }
        } else {
            message = "Location Permission Not Granted";
        }
        showToast(message);
  }

private void showToast(String message) {
      Toast.makeText(getApplicationContext(),
      message,
      Toast.LENGTH_LONG).show();
}
```

### 最後に認識された位置

継続的な位置追跡が無効になっている場合は、メソッド [`TealiumLocation.requestDeviceLastLocation()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#requestdevicelastlocation)を使用して、最後に認識された位置をリクエストします。このメソッドは、デバイス上の他のアプリによって精度を確保する目的で使用されているロケーションクライアントに依存します。他のアプリが最新の位置情報を受信して​​いない場合、このメソッドは最後に認識された位置情報（またはその位置情報が使用不可の場合は`null`）を返します。
```java
TealiumLocation.getInstance().requestDeviceLastLocation();
```

## ジオフェンシング

ジオフェンシングを有効にして初期化するには、次のいずれかの方法で、[ジオフェンスJSONファイル](https://docs.tealium.com/ja/platforms/getting-started/location/#json-file)をセットアップメソッドに指定します。

* **ホスト型URL**
メソッド [`TealiumLocation.setupInstanceWithUrl()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#setupinstancewithurl)への URL として指定されている独自のホスト型ジオフェンス ファイルを使用します。
このオプションは、公開構成URLをオーバーライドした場合、または[ホスト型データレイヤー](https://community.tealiumiq.com/t5/iQ-Tag-Management/About-Hosted-Data-Layer/ta-p/17572)を使用する必要がある場合に推奨されます。
```java
TealiumLocation.setupInstanceWithUrl(this, tealiumInstances, "https://example.com/geofences.json");
```
* **ローカルファイル**
アプリの Assets ディレクトリに保存されているジオフェンス ファイルを [`TealiumLocation.setupInstanceWithFile()`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#setupinstancewithfile)で使用します。
```java
TealiumLocation.setupInstanceWithFile(this, tealiumInstances, "geofences.json");
```

## 追加の検討事項

**バッテリー最適化機能**
バッテリー最適化機能を実装しているAndroidデバイスは、ジオフェンスモニタリングに支障をきたし、イベントが発動しない原因になる可能性があります。

**BroadcastReceiver**
ジオフェンス遷移タイプがトリガーされると、`GEOFENCE_EVENT`ブロードキャストが送信されます。Androidは、複数の`BroadcastReceiver`が定義されている場合でも、_最初_のレシーバのみをこの特定のブロードキャストに対して呼び出します。`GEOFENCE_EVENT`ブロードキャストに対応したサードパーティSDKの場合は、`GEOFENCE_EVENT`ブロードキャストの各レシーバの`onReceive()`メソッドを呼び出す「プロキシ」`BroadcastReceiver`を実装します。

**ジオフェンスの初期化**
作成時にユーザーがジオフェンス内にいる場合、`"enter"`遷移イベントはトリガーされません。これは、`"exit"`および`"enter"`の遷移イベントが境界を横断するときにトリガーされ、境界内に存在するときにはトリガーされないためです。

**遅延：**
ジオフェンシング機能を使用するときは、次の点を考慮してください。

* ジオフェンスサービスは位置情報を継続的に照会しないため、アラートを受信する際に遅延が生じることが予想されます。遅延は通常2分未満ですが、バックグラウンドの位置情報制限が構成されている場合、またはデバイスが一定の期間静止していた場合は、遅延が増加します。
* ジオフェンスサービスは、ネットワーク位置情報プロバイダーとデータコネクトに依存しています。ジオフェンス内に信頼できるネットワーク接続がない場合は、アラートがトリガーされない可能性があります。
* Wi-Fiがデバイスでオフになっている場合、ジオフェンスの半径、デバイスモデル、Androidのバージョンなどの構成によっては、アプリケーションがジオフェンスアラートを受信しないことがあります。Android 4.3以降では、「Wi-Fiスキャンのみモード」機能が提供され、ユーザーはWi-Fiを無効にしても、信頼性の高いネットワーク位置情報を受信できるようになっています。この構成を有効にするようユーザーに促すことをお勧めします。

**アクティブなジオフェンスの数**
ジオフェンスは、可能な限り少ないリソースを使用して動的に追加および削除されます。定義できるジオフェンスの数に制限はありませんが、アクティブなジオフェンスの数は、実行中の_全_アプリケーションにわたって、デバイスユーザーあたり100個までに制限されています。

## データレイヤー

以下の変数は、モバイルデータレイヤーの一部としてLocationモジュールによって値が入力されます。これらの変数はライブラリから自動的に各トラッキングコールに含まれます。

| 変数名       | 型| 説明| 例|
|:--------------------|:---------|:--------------------------------------------------------------------------|:--------------|
| `latitude`          | `String` | 最後に記録されたユーザーの位置の緯度| `"32.906119"` |
| `longitude`         | `String` | 最後に記録されたユーザーの位置の経度| `"-117.2367"` |
| `location_accuracy` | `String` | Locationモジュールの精度構成（`"high"`、`"low"`など）| `"high"`      |

ジオフェンシング中にユーザーの遷移状態が変化すると、位置データを含むトラッキングコールが送信されます。遷移状態の変化には、指定された期間にユーザーがジオフェンス内に進入、退出、滞留することなどが含まれます。Androidメソッド[setLoiteringDelay()](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.Builder#setLoiteringDelay(int))を使用して、滞留アラート送信の基準とする徘徊期間を構成する必要があります。

以下の変数がデータレイヤーに送信されます。

| 変数名              | 型| 説明| 例|
|:---------------------------|:---------|:--------------------------------------|:-----------------------------------------------------------------|
| `tealium_event`            | `String` | Tealiumのトラッキング対象ジオフェンスイベント| `"geofence_entered"`、`"geofence_exited"`、または`"geofence_dwell"`|
| `geofence_name`            | `String` | ジオフェンス地域の名前| `"Tealium_San_Diego"`                                            |
| `geofence_transition_type` | `String` | ジオフェンス遷移イベントのタイプ| `"geofence_entered"`、`"geofence_exited"`、または`"geofence_dwell"`|

## APIリファレンス

Location モジュールで使用されるメソッドのリファレンスについては、Tealium SDK for Android API の [`TealiumLocation`](https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/#class-tealiumlocation) クラスを参照してください。

