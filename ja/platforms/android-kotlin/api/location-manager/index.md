---
title: LocationManager
description: TealiumのAndroid（Kotlin）用LocationManagerクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/location-manager/
---
## クラス: LocationManager

`LocationManager` クラスは、位置データの収集、ジオフェンスの作成と監視のためのメソッドを提供します。以下は、Tealium Kotlinの`LocationManager`クラスで一般的に使用されるメソッドをまとめたものです。詳細については、[Location module](/ja/platforms/android-kotlin/module-list/location/)を参照してください。

| メソッド | 説明 |
| ----- | ------ |
| [`addGeofence()`](#addgeofence) | 新しい`GeofenceLocation`をallGeofenceLocationsに作成して追加します。 |
| [`allGeofenceNames()`](#allgeofencenames) | すべての`GeofenceLocation`名のリストを返します。 |
| [`lastLocation()`](#lastlocation) | ユーザーのデバイスの最後の既知の位置情報を返します。 |
| [`lastLocationLatitude()`](#lastlocationlatitude) | 最後の位置情報の緯度を返します。 |
| [`lastLocationLongitude()`](#lastlocationlongitude) | 最後の位置情報の経度を返します。 |
| [`startLocationTracking()`](#startlocationtracking) | 望む精度と更新間隔で位置追跡を開始します。 |
| [`stopLocationTracking()`](#stoplocationtracking) | 位置追跡の更新を停止します。  |

### `addGeofence()`

手動でジオフェンスを作成し、監視用に追加する機能を提供します。

```java
tealiumInstance.location?.addGeofence(
							&#34;Tealium-HQ&#34;,
							45.0, // 緯度
							100.0, // 経度
							100, // 半径
							-1, // 有効期限
							0, // 滞在時間
							true, // ジオフェンス入場時にイベントをトリガー
							true) // ジオフェンス退出時にイベントをトリガー
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | 位置の名前 | `&#34;Tealium-HQ&#34;` |
| `latitude` | `Double` | 位置の緯度 | `45.0` |
| `longitude` | `Double` | 位置の経度 | `100.0` |
| `radius` | `Int` | ジオフェンスの半径（メートル） | `100` |
| `expireTime` | `Int` | ジオフェンスの有効期限（ミリ秒） | `-1` |
| `loiterTime` | `Int` | ジオフェンスに入ってから滞在するまでの時間（ミリ秒） | `0` |
| `triggerEnter` | `Boolean` | ジオフェンスに入った際にイベントをトリガーするか | `true` |
| `triggerExit` | `Boolean` | ジオフェンスから出た際にイベントをトリガーするか | `true` |

### `allGeofenceNames()`

監視するすべてのジオフェンス名のリストを返します。

```java
tealiumInstance.location?.allGeofenceNames()
```

### `lastLocation()`

ユーザーのデバイスの最新の位置情報を返します。位置情報が利用不可能な場合は`null`を返します。

```java
val location = tealiumInstance.location?.lastLocation()
```

### `lastLocationLatitude()`

ユーザーのデバイスの最新の位置情報の緯度を返します。

```java
val latitude = tealiumInstance.location?.lastLocationLatitude()
```

### `lastLocationLongitude()`

ユーザーのデバイスの最新の位置情報の経度を返します。

```java
val longitude = tealiumInstance.location?.lastLocationLongitude()
```

### `startLocationTracking()`

連続的な位置追跡を開始し、位置更新の精度と間隔（ミリ秒）を構成します。正確な位置情報と頻繁な位置更新間隔はバッテリー消費に影響を与える可能性があります。

```java
tealiumInstance.location?.startLocationTracking(true, 1000)
```
| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `isHighAcuracy` | `Boolean` | 高精度の位置追跡を行う場合は`true`、100メートル以内の精度で良い場合は`false` | `true` |
| `updateInterval` | `Int` | 位置更新の頻度を好みの間隔（ミリ秒）で構成 | `10000` |

### `stopLocationTracking()`

連続的な位置追跡の更新を停止します。

```java
tealiumInstance.location?.stopLocationTracking()
```