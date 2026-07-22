---
title: TealiumVolatileData
description: 揮発性データにアクセスするためのメソッドを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-volatile-data/
---
## クラス: `TealiumVolatileData`


以下は、iOS（Swift）の `TealiumVolatileData` クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `add()` | アクティブなセッションの残りの期間、すべてのディスパッチにデータを追加します |
| `deleteAllData()` | 揮発性データストアのすべてのデータを削除します |
| `deleteData()` | 揮発性データストアから特定の一連の既知のキーのデータを削除します |
| `getData()` | `add()` メソッドで以前に構成したすべての揮発性データを返します |
| `resetSessionId()` | 現在のセッションのセッションIDをリセットします |
| `setSessionId()` | 現在のセッションの既存のセッションIDを上書きします |

### `add()`

アクティブなセッションの残りの期間、すべてのディスパッチにデータを追加します。

```swift
tealium?.volatileData()?.add(data)
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `data`| `[String: Any]`  | 追加するデータの辞書をキーと値のペアとして | `data: ["session_id":"1234567890232"]` |  

### `deleteAllData()`

揮発性データストアのすべてのデータを削除します。

```swift
tealium?.volatileData()?.deleteAllData()
```


### `deleteData()`

揮発性データストアから特定の一連の既知のキーのデータを削除します。

```swift
tealium?.volatileData()?.deleteData(forKeys)
```

| パラメータ  | タイプ       | 説明       | 例 |
|------------  |-----------|-------------------| --- |
| `forKeys`| `[String]`  | 内部の揮発性データストアから削除するキーの配列 | `forKeys: ["a", "b"]` |  


### `getData()`

`add()` メソッドで以前に構成したすべての揮発性データを返します。

```swift
let data = tealium?.volatileData()?.getData()
```

| 戻り値 | 戻り値のタイプ |
| ------- | ----------- |
| キーと値のペアとしての揮発性データ | `[String:Any]` |

### `resetSessionId()`
現在のセッションのセッションIDをリセットします。

```swift
tealium?.volatileData()?.resetSessionId()
```


### `setSessionId()`
現在のセッションの既存のセッションIDを上書きします。

```swift
tealium?.volatileData()?.setSessionId(sessionId)
```

| パラメータ | タイプ | 説明                      | 例              |
|------------|-----|-----------------------------|---------------------------|
| `sessionId`  | `String` | 現在のセッションのセッションIDを上書きします | `"123456123456009"` |
