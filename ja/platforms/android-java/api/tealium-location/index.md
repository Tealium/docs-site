---
title: TealiumLocation
description: Tealium for Androidで提供されているTealiumLocationクラスおよびメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/tealium-location/
---

## クラス：`TealiumLocation`

以下は、一般的に使用される`TealiumLocation`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| `requestDeviceLastLocation()` | 最後に認識されたユーザーのデバイスの位置を返します|
| `setupInstance()` | ジオフェンシングを無効にしてTealiumジオロケーションインスタンスを構成します|
| `setupInstanceWithConfig()` | Tealium構成ファイルからの（Tealiumのホストデータレイヤーでホストされる）ジオフェンスを使用してTealiumジオロケーションインスタンスを構成します|
| `setupInstanceWithFile()` | アセットのJSONファイルからのジオフェンスを使用してTealiumジオロケーションインスタンスを構成します|
| `setupInstanceWithUrl()` | 未加工のJSONファイルをホストしているURLからのジオフェンスを使用してTealiumジオロケーションインスタンスを構成します|
| `startLocationUpdates()` | 位置情報の更新の精度と継続的トラッキングの更新間隔時間を構成します|
| `stopLocationUpdates()` | 継続的な位置追跡の更新を停止/無効化します|


### `requestDeviceLastLocation()`

最後に認識されたユーザーのデバイスの位置を返します。このメソッドは、デバイス上の他のアプリによって精度を確保する目的で使用されているロケーションクライアントに依存します。他のアプリが最新の位置情報を受信して​​いない場合、このメソッドは最後に認識された位置情報を返します。位置情報が使用不可の場合は`null`を返します。

```java
TealiumLocation.getInstance().requestDeviceLastLocation();
```

### `setupInstance()`

ジオフェンシングを無効にしてTealiumジオロケーションインスタンスを構成します。

```java
TealiumLocation.setupInstance(applicationContext, tealiumInstances);
```

### `setupInstanceWithConfig()`

Tealium構成ファイルからの（Tealiumのホストデータレイヤーでホストされる）ジオフェンスを使用してTealiumジオロケーションインスタンスを構成します。`"https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/geofences.json"`の形式でカスタムURLを作成します。

```java
TealiumLocation.setupInstanceWithConfig(this, tealiumInstances, mTealiumConfig);
```  

### `setupInstanceWithFile()`

アセットのJSONファイルからのジオフェンスを使用してTealiumジオロケーションインスタンスを構成します。

```java
TealiumLocation.setupInstanceWithFile(this, tealiumInstances, "geofences.json");
```

### `setupInstanceWithUrl()`

未加工のJSONファイルをホストしているURLからのジオフェンスを使用してTealiumジオロケーションインスタンスを構成します。このオプションは、公開構成URLをオーバーライドした場合に推奨されます。

```java
TealiumLocation.setupInstanceWithUrl(this, tealiumInstances, url);
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `url` | `String` | ホスト型JSONファイル（`geofences.json`など）を指すURL| `"https://DOMAIN/PATH/FILE.json"`|


### `startLocationUpdates()`

位置情報の更新の精度と継続的トラッキングの更新間隔時間を構成します。ピンポイントの位置情報の精度と高頻度の更新を有効にすると、精度は高まりますが、バッテリーの消費量が多くなります。「ブロック」精度を有効にすると、位置情報の精度を都市区画内（約100メートルの精度）に構成できます。

```java
TealiumLocation.getInstance().startLocationUpdates(isHighAccuracy, updateInterval);
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `isHighAccuracy` | `boolean` |ピンポイントの位置情報の精度の場合は`true`に構成し、「ブロック」精度の場合は`false`に構成します。| `true` |
| `updateInterval` | `double` | 位置情報の更新を取得する時間間隔（ミリ秒）。推奨される値：`10000`ミリ秒（10秒）| `10000` |

### `stopLocationUpdates()`

継続的な位置追跡の更新を無効にします。

```java
TealiumLocation.getInstance().stopLocationUpdates();
```
