---
title: TealiumPersistentData
description: 永続的なデータにアクセスするためのメソッドを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-persistent-data/
---
## クラス: `TealiumPersistentData`


以下は、iOS（Swift）の`TealiumPersistentData`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `add()` | アプリのライフタイム全体ですべてのトラック呼び出しに利用可能な追加の永続データを追加します。値は、指定されたキーの既存の値を上書きします。 |
| `deleteAllData()` | 永続データストアのすべてのデータを削除します。 |
| `deleteData()` | 永続データストアから特定の一連の既知のキーのデータを削除します。 |
| `getData()` | 永続データストアからデータを取得します。 |


### `add()`

アプリのライフタイム全体ですべてのトラック呼び出しに利用可能な追加の永続データを追加します。値は、指定されたキーの既存の値を上書きします。

```swift
tealium?.persistentData()?.add(data: [String: Any])
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `Any`| `[String: Any]`  | 追加するデータの辞書 | `data: [&#34;customer_id&#34;:&#34;1234567890-a&#34;]` |  


### `deleteAllData()`

永続データストアのすべてのデータを削除します。

```swift
tealium?.persistentData()?.deleteAllData()
```


### `deleteData()`

永続データストアから特定の一連の既知のキーのデータを削除します。

```swift
tealium?.persistentData()?.deleteDate(forKeys: [String])
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `forKeys`| `[String]`  | 削除するキーの配列 | `forKeys: [&#34;customer_id&#34;]` |  


### `getData()`

永続データストアからデータを取得します。

```swift
let data = tealium?.persistentData()?.getData()
```
