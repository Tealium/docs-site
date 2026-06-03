---
title: LocationModule
description: TealiumがiOS（Swift）で提供するLocationModuleクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/location-module/
---
## クラス: LocationModule

`LocationModule`クラスは、位置データの収集、ジオフェンスの作成と監視のためのメソッドを提供します。以下に、Tealium iOS（Swift）の`LocationModule`クラスのメソッドをまとめています。これらは、Location Moduleのデフォルトの動作にカスタム変更を加えるために使用できます。詳細については、[Location](/ja/platforms/ios-swift/module-list/location/)をご覧ください。

| メソッド | 説明 |
| ----- | ------ |
| [`clearMonitoredGeofences()`](#clearmonitoredgeofences) | ロケーションクライアントから現在監視しているすべてのジオフェンスを削除します |
| [`getCreatedGeofences()`](#getcreatedgeofences) | 作成されたすべてのジオフェンスの名前を返します（現在監視しているものとそうでないもの） |
| [`getLastLocation()`](#getlastlocation) | ユーザーのデバイスの最後に知られている位置を取得します |
| [`getMonitoredGeofences()`](#getmonitoredgeofences) | 現在監視しているすべてのジオフェンスの名前を返します |
| [`requestAuthorization()`](#requestauthorization) | ユーザーに位置情報サービスの許可を有効にするように促します |
| [`requestTemporaryFullAccuracyAuthorization()`](#requesttemporaryfullaccuracyauthorization) | 精密な精度が無効になっている場合に自動的に一時的な完全精度を要求します |
| [`startLocationUpdates()`](#startlocationupdates) | ロケーションクライアントを通じて位置データの定期的な更新を有効にします |
| [`stopLocationUpdates()`](#stoplocationupdates) | ロケーションクライアントを通じて位置データの更新を停止します |
| [`startMonitoring()`](#startmonitoring) | 監視するためにジオフェンスをロケーションクライアントに追加します |
| [`stopMonitoring()`](#stopmonitoring) | ジオフェンスをロケーションクライアントが監視するのを停止します |


### `clearMonitoredGeofences()`

ロケーションクライアントから現在監視しているすべてのジオフェンスを削除します。

```swift
tealium.location?.clearMonitoredGeofences()
```


### `getCreatedGeofences()`

作成されたすべてのジオフェンスの名前を返します（現在監視しているものとそうでないもの）。

```swift
tealium.location?.getCreatedGeofences(completion: { createdGeofences in
            if let createdGeofences = createdGeofences {
                // ここでジオフェンスを使用します
            }
        })
```


### `getLastLocation()`

ユーザーのデバイスの最後に知られている位置を取得します。

```swift
tealium.location?.getLastLocation(completion: { lastLocation in
            if let lastLocation = lastLocation {
                // ここで最後の位置を使用します
            }
        })
```

### `getMonitoredGeofences()`

現在監視しているすべてのジオフェンスの名前を返します。

```swift
tealium.location?.getMonitoredGeofences(completion: { monitoredGeofences in
            if let monitoredGeofences = monitoredGeofences {
                // ここで監視しているジオフェンスを使用します
            }
        })
```

### `requestAuthorization()`

ユーザーに位置情報サービスの許可を有効にするように促します。

```swift
tealium.location?.requestAuthorization()
```

### `requestTemporaryFullAccuracyAuthorization()`

精密な精度が無効になっている場合に自動的に一時的な完全精度を要求します。

```swift
let purposeKey = &#34;a key in the NSLocationTemporaryUsageDescriptionDictionary&#34;
tealium.location?.requestTemporaryFullAccuracyAuthorization(purposeKey: purposeKey)
```

| パラメータ    | タイプ     | 説明                               |
|:--------------|:---------|:------------------------------------------|
| `purposeKey`  | `String` | アプリの`Info.plist`ファイルの`NSLocationTemporaryUsageDescriptionDictionary`辞書のキー |


### `startLocationUpdates()`

ロケーションクライアントを通じて位置データの定期的な更新を有効にします。更新頻度は、このクラスの初期化時に渡される`config.useHighAccuracy`パラメータに依存します。

```swift
tealium.location?.startLocationUpdates()
```

### `stopLocationUpdates()`

ロケーションクライアントを通じて位置データの更新を停止します。

```swift
tealium.location?.stopLocationUpdates()
```

### `startMonitoring()`

監視するためにジオフェンスをロケーションクライアントに追加します。

```swift
let myGeofences = [CLCircularRegion]() // あとで停止したい場合は、自己管理のジオフェンスをどこかに保存します
tealium.location?.startMonitoring(geofences: myGeofences)
```

| パラメータ    | タイプ     | 説明                          |
|:--------------|:---------|:-------------------------------------|
| `geofences`  | `[CLCircularRegion]()` | 追加するジオフェンス |


### `stopMonitoring()`

ジオフェンスをロケーションクライアントが監視するのを停止します。

```swift
tealium.location?.stopMonitoring(geofences: myGeofences)
```

| パラメータ    | タイプ     | 説明                          |
|:--------------|:---------|:-------------------------------------|
| `geofences`  | `[CLCircularRegion]()` | 削除するジオフェンス |
