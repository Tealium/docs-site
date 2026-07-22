---
title: ロケーションマネージャーモジュール
description: イベントのデバイスの位置情報と興味のある地点のジオフェンスの追加機能を提供します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/location/
---
ロケーションマネージャーモジュールは、Androidアプリに位置情報を受信し、ジオフェンスを構成および監視する機能を提供します。[位置情報の追跡とジオフェンスについて詳しく](https://docs.tealium.com/ja/platforms/getting-started-mobile/location/)をご覧ください。

## サポートされているプラットフォーム

以下のプラットフォームがサポートされています：

* [Android](https://docs.tealium.com/ja/platforms/android-kotlin/)

## 必要条件

* Google Playサービス[Location](https://developer.android.com/training/location)（11.0.0以上）

このモジュールはFirebase Cloud Messagingをサポートしています。

<!-- ## サンプルアプリ

[Android Locationモジュールのサンプルアプリ](https://github.com/Tealium/tealium-android/tree/master/Modules/Location)を使用して、ライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れてください。 -->

## インストール

Maven（推奨）または手動でモジュールをインストールします。インストール後、次のインポートステートメントを追加します：
```groovy
<!-- import com.tealium.location.TealiumLocation; -->
```

### Maven

Mavenを使用してモジュールをインストールするには、次の手順を実行します：

1. プロジェクトのトップレベルの`build.gradle`ファイルに、次のMavenリポジトリを追加します：
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. プロジェクトモジュールの`build.gradle`ファイルに、Tealiumライブラリ、Locationモジュール、およびGoogle PlayサービスのLocation APIのMaven依存関係を追加します：
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-location:1.1.2'
            runtimeOnly 'com.google.android.gms:play-services-location:17.0.0'
      }
      ```

### 手動

Locationモジュールを手動でインストールするには、次の手順を実行します：

1. [Locationモジュール](https://github.com/Tealium/tealium-kotlin/tree/master/location)をダウンロードします。

2. トップレベルの`build.gradle`ファイルを確認します：
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
3. `tealium-kotlin.location-1.1.2.aar`ファイルをプロジェクトの`<PROJECT_ROOT>/<MODULE>/libs`ディレクトリにコピーします。

4. プロジェクトモジュールの`build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            // 既にこの参照がない場合のみ必要です
            implementation(name:'tealium-1.5.3', ext:'aar')
            // locationモジュールの参照
            implementation(name:'tealium-kotlin.location-1.1.2', ext:'aar')
            // GoogleのLocation Services APIの参照
            runtimeOnly 'com.google.android.gms:play-services-location:17.0.0'
      }
      ```

## 初期化

次の例に示すように、Locationモジュールを初期化します：

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
              ENVIRONMENT,
              collectors = mutableSetOf(Collectors.Location) // Locationモジュール
)

```

## 位置情報の追跡

Locationモジュールは、有効になっていて位置情報の許可が与えられている場合、自動的に連続的な位置情報の追跡を行います。位置情報の更新は、精度と時間間隔の2つの構成に基づいて行われます。

精度を高または低のいずれかに構成します。高精度はAndroidの構成`PRIORITY_HIGH_ACCURACY`に対応し、低精度はAndroidの構成`PRIORITY_BALANCED_POWER_ACCURACY`に対応します。

[Androidの位置情報の精度構成について詳しく](https://developer.android.com/guide/topics/location/battery#accuracy)をご覧ください。

位置情報の更新間隔は、ミリ秒単位の値で構成します。アプリにとって有用な最大の値を使用します。この間隔の値は、Androidの`setInterval()`および`setFastestInterval()`メソッドに渡されます。

[Androidの位置情報の間隔構成について詳しく](https://developer.android.com/guide/topics/location/battery#frequency)をご覧ください。

高精度と時間間隔60000ミリ秒（60秒）を使用する次の例をご覧ください：
```kotlin
tealium.location?.startLocationTracking(true, 60000)

```

連続的な追跡を無効にするには、[`stopLocationTracking()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/#stoplocationtracking)メソッドを呼び出します。

### 最後の既知の位置

連続的な追跡が無効になっている場合、[`lastLocation()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/#lastLocation)メソッドを使用して最後の既知の位置を要求します。このメソッドは、他のアプリがデバイスで位置情報の更新を受け取っている場合にのみ正確な位置情報を返します。他のアプリが位置情報の更新を受け取っていない場合、このメソッドは最後の既知の位置（または位置が利用できない場合は`null`）を返します。
```kotlin
tealium.location?.lastLocation();
```

## ジオフェンス

ジオフェンスを有効にするには、[ジオフェンスのJSONファイル](https://docs.tealium.com/ja/platforms/getting-started-mobile/location/#json-file)を提供するために次のいずれかの方法を使用します：

* **ホストされたURL**  
自分自身のホストされたジオフェンスファイルを、構成オプション[tealiumConfig.options[GEOFENCE_URL]](https://docs.tealium.com/ja/platforms/android-kotlin/api/#overridegeofenceurl)にURLとして使用します。  
このオプションは、公開構成のURLを上書きした場合や[ホストされたデータレイヤー](https://docs.tealium.com/use-case-supplementing-product-data/)を使用したい場合に推奨されます。  
    ```kotlin
    tealiumConfig.options[GEOFENCE_URL] = "https://example.com/geofences.json"
    ```

* **ローカルファイル**  
アプリのAssetsディレクトリに保存されたジオフェンスファイルを使用します。[`tealiumConfig.options[GEOFENCE_FILENAME]`](https://docs.tealium.com/ja/platforms/android-kotlin/api/#geofenceFilename)を使用します。

      ```kotlin
      tealiumConfig.options[GEOFENCE_FILENAME] = "geofences.json"
      ```

## その他の考慮事項

**アクティブなジオフェンスの数**  
ジオフェンスは動的に追加および削除され、可能な限り少ないリソースを使用します。定義されるジオフェンスの数に制限はありませんが、アクティブなジオフェンスの数はデバイスユーザーごとに100個に制限されます。

**ジオフェンスの初期化**  
ジオフェンスが作成された時点でユーザーがジオフェンス内にいる場合、"enter"のトランジションイベントは発生しません。これは、"exit"および"enter"のトランジションイベントが、境界を越えたときに発生するためです。

**バッテリー最適化機能**  
バッテリー最適化機能を実装しているAndroidデバイスは、ジオフェンスの監視に干渉する可能性があり、イベントが発生しない場合があります。

**BroadcastReceiver**  
ジオフェンスのトランジションタイプがトリガーされたときに`GEOFENCE_EVENT`ブロードキャストが送信されます。Androidは、この特定のブロードキャストに対して定義された複数の`BroadcastReceiver`がある場合でも、最初の`BroadcastReceiver`のみを呼び出します。`GEOFENCE_EVENT`ブロードキャストを処理するサードパーティのSDKの場合、"プロキシ"`BroadcastReceiver`を実装し、`GEOFENCE_EVENT`ブロードキャストの各個別レシーバーの`onReceive()`メソッドを呼び出すようにします。

**レイテンシー:**   
ジオフェンスの機能を使用する場合は、次の点に注意してください：

* ジオフェンスサービスは位置情報を連続的にクエリしないため、アラートを受け取る際にはレイテンシーが発生することがあります。レイテンシーは通常2分未満ですが、バックグラウンドの位置情報制限が構成されている場合やデバイスが一定時間停止している場合は、レイテンシーが増加します。
* ジオフェンスサービスはネットワーク位置プロバイダーとデータコネクトに依存しています。ジオフェンス内に信頼性のあるネットワーク接続がない場合、アラートがトリガーされない場合があります。
* デバイスでWi-Fiがオフになっている場合、ジオフェンスアラートを受け取らない場合があります。これは、ジオフェンスの半径、デバイスモデル、またはAndroidのバージョンなど、いくつかの構成に依存します。Android 4.3以降では、「Wi-Fiスキャンのみモード」の機能が提供されており、ユーザーがWi-Fiを無効にしても信頼性のあるネットワーク位置を受信できます。この構成を有効にするようユーザーに促すことをお勧めします。


## データレイヤー

ロケーションモジュールによってモバイルデータレイヤーの一部として次の変数が構成されます。これらの変数は、ライブラリからの各トラッキングコールに自動的に含まれます。

| 変数名 | タイプ | 説明 | 例             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | ユーザーの最新の位置の緯度 | `32.906119` |
| `longitude`    | `String` |ユーザーの最新の位置の経度 | `-117.2367` |
| `location_accuracy` | `String` | ロケーションモジュールの精度構成（`high`または`low`など） | `high`|

ジオフェンスの場合、ユーザーのトランジション状態が変化したときに位置データを含むトラッキングコールが送信されます。トランジション状態の変化には、ユーザーがジオフェンスに入る、ジオフェンスから出る、またはジオフェンス内で一定の時間滞在するというものがあります。ジオフェンスの滞在アラートが送信される前に滞在時間の期間を構成するには、Androidのメソッド[setLoiteringDelay()](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.Builder#setLoiteringDelay(int))を使用します。

次の変数がデータレイヤーに送信されます：

| 変数名 | タイプ | 説明 | 例             |
|---------------|-----|-------------|----------------------|
| `tealium_event`            | `String` | Tealiumがトラッキングしたジオフェンスイベント | `geofence_entered`、`geofence_exited`、または`geofence_dwell` |
| `geofence_name`            | `String` | ジオフェンス領域の名前 | `Tealium_San_Diego` |
| `geofence_transition_type` | `String` | ジオフェンスのトランジションイベントのタイプ | `geofence_entered`、`geofence_exited`、または`geofence_dwell` |

## APIリファレンス

ライフサイクルトラッキングモジュールで使用されるメソッドのリファレンスについては、Tealium SDK for Android APIの[`LocationManager`](https://docs.tealium.com/ja/platforms/android-kotlin/api/location-manager/)クラスを参照してください。

