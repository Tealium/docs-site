---
title: TealiumDataLayer
description: Tealiumによって提供されるiOS（Swift）のDataLayerクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-data-layer/
---
## クラス: `DataLayer`

以下は、iOS（Swift）の`DataLayer`クラスの一般的に使用されるメソッドとプロパティをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`add()`](#add) | 有効期限タイプに基づいてデータレイヤーにデータを追加します。 |
| [`all`](#all) | データレイヤーに保存されているすべてのデータを返します。 |
| [`allSessionData`](#allsessiondata) | アクティブなセッションのデータレイヤーに保存されているすべてのデータを返します。 |
| [`delete()`](#delete) | 指定した値を保存から削除します。 |
| [`deleteAll()`](#deleteall) | すべての値を保存から削除します。 |
| [`persistentDataStorage`](#persistentdatastorage) | 永続保存に保存されているすべてのイベントデータを返します。 |

### `add()`

[有効期限タイプ](https://docs.tealium.com/ja/platforms/ios-swift/data-layer/#data-expiration)に基づいてデータレイヤーにデータを追加します。`expiry`パラメータが提供されていない場合、有効期限タイプはデフォルトで`.session`になります。

```swift
tealium?.dataLayer.add(key, value, expiry)
```

| パラメータ             | タイプ     | 説明               |
|-----------------------|----------|---------------------------|
| `key`                 | `String` | 保存するキーの名前  |
| `value`               | `Any`    | 保存するデータ         |
| `expiry` (optional)   | `Expiry` | データの有効期限レベル     |

### `all`

データレイヤーに保存されているすべてのデータを返します。

```swift
let data: [String: Any] = tealium?.dataLayer.all
```

| 戻り値のタイプ | 説明                       |
|-------------|-----------------------------------|
| `[String]`  | データレイヤーに保存されているすべてのデータ |


### `allSessionData`

アクティブなセッションのデータレイヤーに保存されているすべてのデータを返します。

```swift
let data: [String: Any] = tealium?.dataLayer.allSessionData
```

| 戻り値のタイプ | 説明                       |
|-------------|-----------------------------------|
| `[String]`  | アクティブなセッションのデータレイヤーに保存されているすべてのデータ |


### `delete()`

特定のキーに基づいて保存から指定した値を削除します。

```swift
tealium?.dataLayer.delete(for key)
```

| パラメータ | タイプ                   | 説明                               |
|-----------|------------------------|-------------------------------------------|
| `key` | `String` | 削除する値のキー |

複数のキーに基づいて保存から複数の値を削除するには：

```swift
tealium?.dataLayer.delete(for keys)
```

| パラメータ | タイプ                   | 説明                               |
|-----------|------------------------|-------------------------------------------|
| `keys` | `[String]` | 削除する値のキー |


### `deleteAll()`

保存からすべての値を削除します。

```swift
tealium?.dataLayer.deleteAll()
```

### `persistentDataStorage`

永続保存に保存されているすべてのイベントデータを返します。

```swift
let data: Set<DataLayerItem> = tealium?.dataLayer.persistentDataStorage
```

| 戻り値のタイプ | 説明                       |
|-------------|-----------------------------------|
| `Set<DataLayerItem>`  | 永続保存に保存されているすべてのイベントデータ |

