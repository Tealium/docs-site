---
title: データレイヤー
description: Android（Kotlin）、iOS（Swift）、React Native向けTealium Prism SDKを使用して、永続的なデータレイヤーの値を取得、構成、管理します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/data-layer/
---
`dataLayer`は、トラッキング呼び出しにコンテキストデータを追加するための共有キーバリューストアを提供します。データレイヤーに保存された値は、トラッキングされるすべてのイベントに自動的に含まれます。イベント間で一貫している静的属性にはデータレイヤーを使用し、動的属性は`track()`呼び出しに直接渡します。

## インストール



DataLayerモジュールは`prism-core`に含まれています。追加の依存関係は必要ありません。


DataLayerモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```


DataLayerモジュールは`@tealium/prism-react-native`に含まれています。追加の依存関係は必要ありません。



## 初期化

DataLayerモジュールは自動的に初期化されます。


<blockquote>
このモジュールは重要なデータ保存機能を提供するため、無効にすることはできません。`setEnabled(false)`メソッドは、このモジュールには影響しません。
</blockquote>


データレイヤーの値を含めるイベントを制限するには、モバイルプロファイルにDataLayerモジュールを追加し、ルールを割り当てます。詳細については、[ルール](https://docs.tealium.com/rules/)を参照してください。

## データの取得



データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html)メソッドを使用し、結果を処理するためにサブスクライブします。

```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // do something with customerId
}
```


データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html)メソッドを呼び出します。

```swift
tealium.dataLayer.get(key: "customer_id",
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print("Value: \(String(describing: value))")
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

キーを指定して特定のデータ項目を取得するには、次のようにします。

```swift
tealium.dataLayer.getDataItem(key: "user_status").onSuccess { item in
    if let userStatus = item?.get(as: String.self) {
        print("User status: \(userStatus)")
    }
}
```

データレイヤー内のすべてのキーバリューペアを取得するには、次のようにします。

```swift
tealium.dataLayer.getAll().onSuccess { allData in
    print("All data layer attributes: \(allData)")
}
```


データレイヤーの値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#get)を呼び出します。

```javascript
const customerId = await tealium.dataLayer.get("customer_id");
```

すべてのデータレイヤーの値を取得するには、[`getAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#getall)を呼び出します。

```javascript
const allData = await tealium.dataLayer.getAll();
```



## データの構成

### 個別の値



データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html)メソッドを使用します。

```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```


データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html)メソッドを使用します。

```swift
tealium.dataLayer.put(key: "some_key", value: "some value")
```

有効期限付きの値を構成するには、次のようにします。

```swift
tealium.dataLayer.put(key: "user_status", value: "active", expiry: .session)
```


データレイヤーの値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#put)を呼び出します。

```javascript
await tealium.dataLayer.put("my_string", "my_string_value");
```

有効期限付きの値を構成するには、次のようにします。

```javascript
await tealium.dataLayer.put("user_status", "active", "session"); // or "forever", "untilRestart"
```



### オブジェクト



データレイヤーオブジェクトを構成するには、`DataObject.Builder()`を使用します。

```kotlin
val globalContext = DataObject.Builder()
    .put("customer_id", "12345")
    .put("is_logged_in", true)
    .put("consent_status", "consented")
    .build()

dataLayer.putAll(globalContext, Expiry.FOREVER)
```


複数のキーバリューペアを一度に構成するには、`DataObject`を`putAll(dataObject:)`に渡します。

```swift
tealium.dataLayer.putAll(dataObject: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones"]
])
```

有効期限付きで複数の値を構成するには、次のようにします。

```swift
let data: DataObject = [
    "campaign": "summer_sale",
    "discount": 20
]
tealium.dataLayer.putAll(dataObject: data, expiry: .untilRestart)
```


複数のキーバリューペアを一度に構成するには、[`putAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#putall)を呼び出します。

```javascript
await tealium.dataLayer.putAll({
  customer_id: "12345",
  is_logged_in: true,
  consent_status: "consented",
});
```

有効期限付きで複数の値を構成するには、次のようにします。

```javascript
await tealium.dataLayer.putAll({ campaign: "summer_sale", discount: 20 }, "untilRestart");
```



### 配列



配列値を構成するには、`DataList.create`を使用します。

```kotlin
val productCategories = DataList.create {
    add("electronics")
    add("headphones")
}

dataLayer.put(
    key = "product_category",
    value = productCategories,
    expiry = Expiry.SESSION
).onFailure { err -> }
```


配列は、`DataObject`内で標準のSwift配列として渡します。

```swift
tealium.dataLayer.putAll(dataObject: [
    "product_category": ["electronics", "headphones"]
], expiry: .session)
```


配列を`putAll()`呼び出しの値として渡します。

```javascript
await tealium.dataLayer.putAll({
  product_category: ["electronics", "headphones"],
});
```


## トランザクション更新

`transactionally` メソッドを使用して、データレイヤーに対する複数の更新を単一のアトミック操作にまとめます。すべての更新がまとめて適用されるため、一部のみが更新されるリスクを軽減できます。


<blockquote>
React Native はアトミックなトランザクション更新をサポートしていません。個別または一括の書き込みには、`put()` および `putAll()` を使用してください。
</blockquote>




各呼び出しは独立して順番に実行されるため、アトミック性が不要な場合にのみ個別の `put` 操作を使用してください。複数の値を構成する際にタイミングや整合性が重要な場合は、`transactionally` を使用して、すべての更新を単一のアトミック操作として適用します。

```kotlin
tealium.dataLayer.transactionally { editor ->
    editor.put("key", "value".asDataItem(), Expiry.SESSION)
        .put("key2", "value2".asDataItem(), Expiry.SESSION)
        .remove("key2")
        .commit()
}.onFailure {
    Log.d("DataLayer", "Transactional update failed: ${it.message}")
}
```


トランザクションがコミットされるまで、データレイヤーは変更されません。コミット後に変更を適用しても何も起こりません。適用されていてもコミットされていない編集内容は、このブロックから返される項目には反映されません。

```swift
tealium.dataLayer.transactionally { transaction in
    transaction.put(key: "key1", value: "value", expiry: .forever)
    transaction.put(key: "key2", value: "value2", expiry: .untilRestart)
    transaction.remove(key: "key3")
    if let count = transaction.get(key: "key4", as: Int.self) {
        transaction.put(key: "key4", value: count + 1, expiry: .forever)
    }
    do {
        try transaction.commit()
    } catch {
        print(error)
    }
}
```



## データの有効期限

データレイヤーの値を構成する際、必要に応じて有効期限を構成し、その値が失効するタイミングを指定します。



以下の有効期限タイプを使用できます。

| タイプ | 値 | 説明 |
| :--- | :--- | :--- |
| セッション | `Expiry.SESSION` | 現在のセッションの終了時に失効します。 |
| 無期限（デフォルト） | `Expiry.FOREVER` | アプリがインストールされている間は失効しません。 |
| 再起動まで | `Expiry.UNTIL_RESTART` | アプリを終了または再起動すると失効します。 |
| カスタム期間 | `Expiry.afterTimeUnit(time, units)` | 指定した期間が経過すると失効します。 |

```kotlin
dataLayer.put(
    key = "currency",
    value = "USD",
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = "order_total",
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```


以下の有効期限タイプを使用できます。

| タイプ | 値 | 説明 |
| :--- | :--- | :--- |
| セッション | `.session` | 現在のセッションの終了時に失効します。 |
| 再起動まで | `.untilRestart` | アプリを終了または再起動すると失効します。 |
| 無期限（デフォルト） | `.forever` | 失効しません。 |
| カスタム日付 | `.after` | 指定した日付に失効します。 |

```swift
tealium.dataLayer.put(key: "currency",
                      value: "USD",
                      expiry: .untilRestart)

tealium.dataLayer.put(key: "order_total",
                      value: 249.95,
                      expiry: .after(Date().advanced(by: 1000)))
```


`put()` または `putAll()` の最後の引数として、[`Expiry`](https://docs.tealium.com/tealium-prism-react-native/types/Expiry.html) 値を渡します。

| タイプ | 値 | 説明 |
| :--- | :--- | :--- |
| セッション | `"session"` | 現在のセッションの終了時に失効します。 |
| 無期限（デフォルト） | `"forever"` | アプリがインストールされている間は失効しません。 |
| 再起動まで | `"untilRestart"` | アプリを終了または再起動すると失効します。 |
| カスタム日付 | `new Date(...)` | 指定した日時に失効します。 |

```javascript
await tealium.dataLayer.put("currency", "USD", "untilRestart");

const sevenDays = 7 * 24 * 60 * 60 * 1000;
await tealium.dataLayer.put("order_total", 249.95, new Date(Date.now() + sevenDays));
```



## データの削除



データレイヤーから特定のキーを削除するには、トランザクションブロック内または単独の操作として `remove()` メソッドを使用します。


データレイヤーから特定のキーを削除するには、次のようにします。

```swift
tealium.dataLayer.remove(key: "user_status")
```

複数のキーを削除するには、次のようにします。

```swift
tealium.dataLayer.remove(keys: ["campaign", "discount"])
```

データレイヤーのすべての値を消去するには、次のようにします。

```swift
tealium.dataLayer.clear()
```


データレイヤーからキーを削除するには、[`remove()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#remove) を呼び出します。

```javascript
await tealium.dataLayer.remove("user_status");
```

複数のキーを削除するには、次のようにします。

```javascript
await tealium.dataLayer.remove(["campaign", "discount"]);
```

データレイヤーのすべての値を消去するには、[`clear()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#clear) を呼び出します。

```javascript
await tealium.dataLayer.clear();
```

