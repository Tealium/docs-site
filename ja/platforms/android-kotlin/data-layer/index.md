---
title: データレイヤー
description: 各モジュールが提供するデータと共通のデータレイヤーの値の管理方法について学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/
---
## カスタムデータ

すべてのイベントで一般的なデータレイヤーの値が必要な場合がよくあります。これらの値をすべてのトラッキングコールに追加する必要がないようにするために、`tealium.dataLayer`メソッドを使用して、すべてのトラッキングコールに適用されるデータレイヤーの値を永続化します。値が保存されると、自動的にすべてのトラッキングイベントに含まれます。


<blockquote>
`tealium.dataLayer`が提供するメソッドは、カスタムの値を読み書きすることができますが、[モジュールデータ](#module-data)にはアクセスできません。
</blockquote>


### 値の構成と取得

データレイヤーの値を構成、取得、削除するためのいくつかのユーティリティメソッドがあります。カスタムのデータレイヤーの値を構成および取得するためのメソッドは型付きですが、データレイヤーに格納されている変数の型がわからない場合は、型指定されていないメソッドを使用することもできます。

たとえば、文字列の値を構成するには、[`putString()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putstring)を呼び出します:  
```java
tealium.dataLayer.putString("my_string", "my_string_value")
```
型が指定されていない場合は、[`get()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#get)を呼び出して値を取得します:  

```java
tealium.dataLayer.get("my_string")
```

### データの型

データレイヤーは次のデータ型をサポートしています:

* `Boolean`
* `String`
* `Integer`
* `Long`
* `Double`
* `JSONObject`
* `JSONArray`
* `Array<Boolean>`
* `Array<String>`
* `Array<Integer>`
* `Array<Long>`
* `Array<Double>`

長い数値の値を構成するには、[`putLong()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putlong)を呼び出します:  
```java
val launchTime = System.currentTimeMillis()
tealium.dataLayer.putLong("launch_time", launchTime)
```

文字列の配列を構成するには、[`putStringArray()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#putstringarray)を呼び出します:  
```java
val lastThreeProductsViewed = arrayOf("SKU-1", "SKU-2", "SKU-3")
tealium.dataLayer.putStringArray("last_three_products", lastThreeProductsViewed)
```

### データの有効期限

データレイヤーの値には有効期限があり、有効期限が切れるとデータレイヤーから削除されます。カスタムのデータレイヤーの値を構成する際に、値の有効期間をオプションで構成することができます。デフォルトの有効期間は現在のセッションです。

次の有効期限のタイプが利用できます:

| タイプ | 値 | 説明 |
| :-- | :-- | :-- |
| セッション (デフォルト) | `Expiry.SESSION` | 現在のセッションの終了時に有効期限が切れます |
| 永久 | `Expiry.FOREVER` | アプリがインストールされている間は有効期限が切れません |
| カスタム期間 | `Expiry.afterTimeUnit(time, units)` | 指定された期間後に有効期限が切れます。指定できる期間の単位は次のとおりです: `NANOSECONDS`、`MICROSECONDS`、`MILLISECONDS`、`SECONDS`、`MINUTES`、`HOURS`、`DAYS` |

#### セッションデータ

セッションデータの値はセッションの間永続化されます。セッションは、一定の時間枠内でのユーザーのアクティビティによって決定されます。セッションは、ユーザーの非アクティビティが30分続いた後に終了します。

たとえば、期限切れにならない値を構成するには:  
```java
val userId = "my_id"
tealium.dataLayer.putString("user_id", userId, Expiry.FOREVER)
```

現在のセッションの終了時に値が期限切れになるように明示的に構成するには (デフォルトの動作):  
```java
val sessionProductViews = 10
tealium.dataLayer.putInt("product_views", sessionProductViews, Expiry.SESSION)
```

1日後に値が期限切れになるように構成するには:  
```java
val frequentVisitor = tealium.dataLayer.getBoolean("frequent_visitor") ?: false

tealium.dataLayer.putBoolean("frequent_visitor",
        frequentVisitor,
        Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

### 例

使用可能なすべてのメソッドの完全なリストについては、[Class: DataLayer](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/)を参照してください。

データレイヤーに変数が含まれているかどうかを確認するには、[`contains()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#contains)を呼び出します:

```java
tealium.dataLayer.contains("my_string")
```

値を削除するには、[`remove()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#remove)を呼び出します:  
```java
tealium.dataLayer.remove("my_string")
```

データレイヤー内のすべてのキー名をリストするには、[`keys()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#keys)を呼び出します:  

```java
tealium.dataLayer.keys()
```

データレイヤー内の変数の数を取得するには、[`count()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#count)を呼び出します:  
```java
tealium.dataLayer.count()
```

変数の有効期限を取得するには、[`getExpiry()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#getexpiry)を呼び出します:  
```java
tealium.dataLayer.getExpiry("my_string")
```

すべてのデータレイヤー変数を取得するには、[`all()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#all)を呼び出します。これにより、`mapOf()`が返されます:  
```java
tealium.dataLayer.all()
```

すべてのデータレイヤー変数を削除するには、[`clear()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/#clear)を呼び出します:  
```java
tealium.dataLayer.clear()
```

## モジュールデータ

### 広告識別子

[広告識別子](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/adid/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数 | 型 | 説明 | 例 |
| --- | --- | --- | --- |     
| `google_adid` | `String` | Google広告識別子 | `ca-app-pub-0123456789012345~0123456789` |
| `google_limit_ad_tracking` | `Boolean` | デバイスで広告の追跡が制限されている場合は`true`、それ以外の場合は`false` | `true` |

### アプリコレクター

[アプリコレクター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collectors/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `app_build` | アプリのビルドバージョン | `1`|
| `app_name` | アプリケーション名 ([アプリケーションマニフェスト属性 `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)から取得) | `My App`|
| `app_memory_usage` | アプリプロセスが使用しているメモリ (MB) | `57` |
| `app_rdns` | ルートマニフェスト属性 `package` から取得した逆DNSアプリケーションID | `com.example.myapp` |
| `app_uuid` | ランダムな`uuid`。永続保存モジュールのいずれかも有効になっている場合、アプリのインストールの期間中は永続化され、アプリがアンインストールされるとリセットされます | `123e4567-e89b-12d3-a456-556642440000`|
| `app_version` | アプリのバージョン | `version 1.0`|

### 接続コレクター

[接続コレクター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collectors/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `carrier`                    | モバイルネットワークキャリア名| `EE`|
| `carrier_iso`                | モバイルキャリアISO| `gb`|
| `carrier_mcc`                | キャリアのモバイル国コード| `234`|
| `carrier_mnc`                | キャリアのモバイルネットワークコード| `34`|
| `connection_type`            | 現在の接続タイプ| `wifi`, `cellular`|

### クラッシュレポーター

[クラッシュレポーター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/crash-reporter/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数 | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `crash_cause` | `String` | 例外のタイプ | `java.lang.RuntimeException` |
| `crash_count` | `Number` | インストール後の各クラッシュごとにインクリメントされるカウンター | `1` |
| `crash_name` | `String` | 例外のメッセージ |`"Connection refused by server"` |
| `crash_threads` | `[String]` | クラッシュしたスレッドのデータを含むJSON文字列の配列。スレッドIDとスタックトレースを含みます| ` ['{ "crashed": "true", "state": "RUNNABLE", "threadNumber": "1", "threadId": "main", "priority": "5", "stack":  [ { "fileName": "MainActivity.java", "className": "com.tealium.libraryproject.MainActivity$1", "methodName": "onClick", "lineNumber": "38" }] }']` |
| `crash_uuid` | `String` | 各クラッシュイベントの16文字の一意のID | `3c91d707-949e-445f-8ad1-4d6e200bfd6f` |

### デバイスコレクター

[デバイスコレクター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collectors/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `device` | デバイスの種類 | `Samsung G955f` |
| `device_android_runtime` | Androidランタイムのバージョン | `2.1.0` |
| `device_available_external_storage` | デバイスの利用可能な外部保存の合計容量 (バイト単位) | `273772544`|
| `device_available_system_storage` | デバイスの利用可能な保存の合計容量 |`273772544` |
| `device_architecture` | デバイスのビットアーキテクチャ | `64` |
| `device_battery_percent` | デバイスの残りの電力を整数パーセントで表したもの | `50` |
| `device_cputype` | CPUの種類 | `i686` |
| `device_free_external_storage` | デバイスの利用可能な外部保存の合計容量 (バイト単位) | `273772544`|
| `device_free_system_storage` | デバイスの利用可能な保存の合計容量 |`273772544` |
| `device_ischarging` | デバイスが充電中かどうか | `true`, `false` |
| `device_language` | 現在のデバイスの言語 | `en-US` |
| `device_logical_resolution` | 論理的な画面解像度 (幅 x 高さ) | `414x896` |
| `device_orientation` | 呼び出し時のデバイスの向き | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown` |
| `device_os_build` | オペレーティングシステムのビルドバージョン | `4499259` |
| `device_os_version` | デバイスのオペレーティングシステムのバージョン | `7.0` |
| `device_resolution` | ディスプレイの解像度 (ピクセル単位) | `1920x1080` |
| `origin` | マッピングでモバイルとWebの実装を区別するために使用される定数 | `mobile` |
| `platform` | モバイルプラットフォーム | `Android` |

### Core

`Core Library`によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `tealium_event` | トラッキングされているイベントの名前| `cart_add`|
| `tealium_event_type` | ディスパッチされているイベントタイプを示す文字列 | `view` または `event` |
| `tealium_library_name` | インストールされているTealiumライブラリの名前 | `android-kotlin` |
| `tealium_library_version` | インストールされているTealiumライブラリのバージョン | `1.2` |

### ライフサイクルモジュール

[ライフサイクルモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/lifecycle-tracking/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `lifecycle_dayofweek_local` | 呼び出しが行われたローカルの曜日。1=日曜日、2=月曜日など | `4` |
| `lifecycle_dayssincelastwake` | 直近の起動からの日数 (整数) | `1` |
| `lifecycle_dayssincelaunch` | 最初の起動からの日数 (整数) | `23` |
| `lifecycle_dayssinceupdate` | 直近のアプリバージョンの更新からの日数 (整数) | `46` |
| `lifecycle_diddetect_crash` | この起動/起床イベント中にクラッシュが検出された場合にのみ存在する (trueの場合のみ) | `true` |
| `lifecycle_firstlaunchdate` | 最初の検出された起動/起床のGMTタイムスタンプ。ISO 8601形式でUTC時間から取得 | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | MM/DD/YYYY形式にフォーマットされたGMTタイムスタンプ| `01/17/2012 `|
| `lifecycle_hourofday_local` | 呼び出しが行われたローカルの時刻 (24時間形式)| `true` |
| `lifecycle_isfirstlaunch` | 呼び出しが最初の起動/起床呼び出しである場合にのみ存在する| `true` |
| `lifecycle_isfirstlaunchupdate` | 呼び出しが最初の起動/起床呼び出しであり、更新が検出された後である場合にのみ存在する| `true`, `false` |
| `lifecycle_isfirstwakemonth` | 呼び出しが月の最初の起動/起床呼び出しである場合にのみ存在する| `true` |
| `lifecycle_isfirstwaketoday` | 呼び出しが日の最初の起動/起床呼び出しである場合にのみ存在する| `true` |
| `lifecycle_launchcount` | アプリのこのバージョンの起動の総数 (最後の更新以降)| `3` |
| `lifecycle_priorsecondsawake` | 直前の起動のみ、アプリが起動していた秒数。以前のすべての起動からの合計。`lifecycle_type:launch`の呼び出しでのみ送信されます。| `126` |
| `lifecycle_secondsawake` | 直近の起動/起床からのアプリの起動していた秒数| `30` |
| `lifecycle_sleepcount` | アプリがバックグラウンドに移行した回数の合計 (更新されるとリセットされる)| `5` |
| `lifecycle_totalcrashcount` | インストール後にカウントされたクラッシュの総数 (アプリが削除されるまでリセットされない)| `21` |
| `lifecycle_totallaunchcount` | インストール後の起動の総数 (アプリが削除されるまでリセットされない)| `3` |
| `lifecycle_totalsecondsawake` | アプリがインストールされてからのアプリの起動/アクティブ状態の合計秒数 (アプリが削除されるまでリセットされない)| `36` |
| `lifecycle_totalsleepcount` | アプリがインストールされてからのバックグラウンドに移行した回数の合計 (アプリが削除されるまでリセットされない)| `400` |
| `lifecycle_totalwakecount` | インストール後の起動数 + 起床数の合計 (アプリが削除されるまでリセットされない)| `563` |
| `lifecycle_type` | ライフサイクル呼び出しのタイプ| `launch`, `wake`, `sleep`|
| `lifecycle_updatelaunchdate` | バージョン更新が検出された後の最初の起動/起床のGMTタイムスタンプ| `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount` | このバージョンのアプリの起動数 + 起床数の合計 (更新されるとリセットされる)| `29` |

### 位置情報コレクター

[位置情報コレクター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/location/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `latitude`     | ユーザーの最新の記録された位置の緯度 | `32.906119` |
| `longitude`    | ユーザーの最新の記録された位置の経度 | `-117.2367` |
| `location_accuracy` | 位置情報モジュールの精度構成 | `high`, `low`|
| `tealium_event`            | トラッキングされるTealiumのジオフェンスイベント | `geofence_entered`, `geofence_exited`, `geofence_dwell` |
| `geofence_name`            | ジオフェンス領域の名前 | `Tealium_San_Diego` |
| `geofence_transition_type` | ジオフェンスのトランジションイベントのタイプ | `geofence_entered`, `geofence_exited`, `geofence_dwell` |

### Tealiumコレクター

[Tealiumコレクター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collectors/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `tealium_account` | `TealiumConfig`からのTealiumアカウント名 | `tealium` |
| `tealium_profile` | `TealiumConfig`からのTealiumプロファイル名 | `mobile` |
| `tealium_environment` | `TealiumConfig`からのTealium環境 | `dev` |
| `tealium_datasource` | `TealiumConfig`からのTealiumデータソース名 | `abc123` |
| `tealium_visitor_id` | TealiumビジターID | `t3aL...1uM` |
| `tealium_random` | 各イベントごとに生成されるランダムな数値 | `1234567890` |
| `was_queued` | このイベントがデバイス上でキューに入れられたことを示す | `true` |

### タイムコレクター

[タイムコレクター](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/collectors/)によってデータレイヤーに追加される変数は次のとおりです。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `timestamp` | イベント発生時のタイムスタンプ (秒単位) [ISO 8601形式、UTC時間] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | イベント発生時のローカルタイムスタンプ (オフセットなしのISO 8601形式) | `2013-07-11T19:57:47` |
| `timestamp_offset` | デバイスの場所のローカルタイムゾーンオフセット (時間単位) | `-3` |
| `timestamp_unix` | イベント発生時のGMT/UTC Unixタイムスタンプ |`1373498679` |
| `timestamp_unix_milliseconds` | イベント発生時のGMT/UTC Unixタイムスタンプ (ミリ秒単位) | `1373498679123` |

### 廃止予定

[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/data-layer/)の次のデータレイヤー変数は、Tealium for Android (Kotlin)では名前が変更されたり削除されたりしました。

| Tealium for Android (Java) | Tealium for Android (Kotlin) |
|:---------------|:---------------------|
| `call_type`    | `tealium_event_type` |
| `event_name`   | `tealium_event`      |
| `link_id`      | `tealium_event`      |
| `orientation`  | `device_orientation` |
| `os_version`   | `device_os_version`  |
| `page_type`    | (含まれていません)       |
| `tealium_vid`  | `tealium_visitor_id` |
| `uuid`         | `app_uuid`           |
| `visitor_id`   | `tealium_visitor_id` |
