---
title: データレイヤー
description: Tealium Prism SDK for Android (Kotlin)、iOS (Swift)、および React Native で永続的なデータレイヤー値を取得、構成、および管理します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/data-layer/
---
`dataLayer` は、トラッキングコールにコンテキストデータを追加するための共有キーバリューストアを提供します。データレイヤーに保存された値は、追跡されるすべてのイベントに自動的に含まれます。イベント間で一貫性のある静的属性にデータレイヤーを使用し、動的属性は `track()` コールで直接渡します。

## インストール



DataLayer モジュールは `prism-core` に含まれています。追加の依存関係は必要ありません。


DataLayer モジュールは `TealiumPrismCore` に含まれています。Swift Package Manager 依存関係として repo URL `https://github.com/Tealium/tealium-prism-swift` を使用して追加するか、CocoaPods の Podfile に追加してください：

```ruby
pod 'tealium-prism/Core'
```


DataLayer モジュールは `@tealium/prism-react-native` に含まれています。追加の依存関係は必要ありません。



## 初期化

DataLayer モジュールは自動的に初期化されます。


<blockquote>
このモジュールは、必要なデータ保存機能を提供するため、無効にすることはできません。`setEnabled(false)` メソッドはこのモジュールには効果がありません。
</blockquote>


## データの取得



データレイヤー値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) メソッドを使用し、結果を処理するためにサブスクライブします：

```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // customerId を使って何かをする
}
```


データレイヤー値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを呼び出します：

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

特定のデータ項目をキーで取得するには：

```swift
if let userStatus = tealium.dataLayer.getDataItem(key: "user_status") as? String {
    print("User status: \(userStatus)")
}
```

データレイヤーのすべてのキーバリューペアを取得するには：

```swift
if let allData = tealium.dataLayer.getAll() {
    print("All data layer attributes: \(allData)")
}
```


データレイヤー値を取得するには、[`get()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#get) を呼び出します：

```javascript
const customerId = await tealium.dataLayer.get("customer_id");
```

データレイヤーのすべての値を取得するには、[`getAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#getall) を呼び出します：

```javascript
const allData = await tealium.dataLayer.getAll();
```



## データの構成

### 個々の値



データレイヤー値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) メソッドを使用します：

```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```


データレイヤー値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) メソッドを使用します：

```swift
tealium.dataLayer.put(key: "some_key", value: "some value")
```

有効期限を構成して値を構成する：

```swift
tealium.dataLayer.put(key: "user_status", value: "active", expiry: .session)
```


データレイヤー値を構成するには、[`put()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#put) を呼び出します：

```javascript
await tealium.dataLayer.put("my_string", "my_string_value");
```

有効期限を構成して値を構成する：

```javascript
await tealium.dataLayer.put("user_status", "active", "session"); // または "forever", "untilRestart"
```



### オブジェクト



データレイヤーオブジェクトを構成するには `DataObject.Builder()` を使用します：

```kotlin
val globalContext = DataObject.Builder()
    .put("customer_id", "12345")
    .put("is_logged_in", true)
    .put("consent_status", "consented")
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```


一度に複数のキーバリューペアを構成するには、辞書を `put(data:)` に渡します：

```swift
tealium.dataLayer.put(data: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones"]
])
```

有効期限を構成して複数の値を構成する：

```swift
let data: [String: Any] = [
    "campaign": "summer_sale",
    "discount": 20
]
tealium.dataLayer.put(data: data, expiry: .untilRestart)
```


一度に複数のキーバリューペアを構成するには、[`putAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#putall) を呼び出します：

```javascript
await tealium.dataLayer.putAll({
  customer_id: "12345",
  is_logged_in: true,
  consent_status: "consented",
});
```

有効期限を構成して複数の値を構成する：

```javascript
await tealium.dataLayer.putAll({ campaign: "summer_sale", discount: 20 }, "untilRestart");
```



### 配列



配列値を構成するには `DataList.create` を使用します：

```kotlin
val productCategories = DataList.create {
    add("electronics")
    add("headphones")
}

dataLayer.put(
    key = "product_category",
    value = productCategories,
    expiry = Expiry.SESSION
).subscribe({ }, { err -> })
```


配列は標準の Swift 配列としてデータ辞書に渡されます：

```swift
tealium.dataLayer.put(data: [
    "product_category": ["electronics", "headphones"]
], expiry: .session)
```


`putAll()` コールで配列を値として渡します：

```javascript
await tealium.dataLayer.putAll({
  product_category: ["electronics", "headphones"],
});
```



## トランザクション更新

`transactionally` メソッドを使用して、複数のデータレイヤー更新を単一の原子操作にグループ化します。すべての更新は一緒に適用され、部分的な更新のリスクが減少します。


<blockquote>
React Native は原子的なトランザクション更新をサポートしていません。個別または一括書き込みには `put()` と `putAll()` を使用してください。
</blockquote>




原子性が必要ない場合のみ個々の `put` 操作を使用します。各コールは独立して順番に実行されます。複数の値を構成し、タイミングや一貫性が重要な場合は、`transactionally` を使用してすべての更新を単一の原子操作で適用します。

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


トランザクションがコミットされるまでデータレイヤーは変更されません。コミット後に適用しても何も起こりません。適用されたがコミットされていない編集は、このブロックで返されるアイテムに反映されません。

```swift
teal.dataLayer.transactionally { apply, getDataItem, commit in
    apply(.put("key1", "value", .forever))
    apply(.put("key2", "value2", .untilRestart))
    apply(.remove("key3"))
    if let count = getDataItem("key4")?.get(as: Int.self) {
        apply(.put("key4", count + 1, .forever))
    }
    do {
        try commit()
    } catch {
        print(error)
    }
}
```


## データの有効期限

データレイヤーの値を構成する際に、オプションで有効期限を構成して、値の有効期限が切れるタイミングを決定します。



以下の有効期限タイプが利用可能です：

| タイプ | 値 | 説明 |
| :--- | :--- | :--- |
| セッション（デフォルト） | `Expiry.SESSION` | 現在のセッションの終了時に期限切れになります。 |
| 永続 | `Expiry.FOREVER` | アプリがインストールされている間は期限切れになりません。 |
| 再起動まで | `Expiry.UNTIL_RESTART` | アプリが閉じられたり再起動された時に期限切れになります。 |
| カスタム期間 | `Expiry.afterTimeUnit(time, units)` | 指定された期間後に期限切れになります。 |

```kotlin
dataLayer.put(
    key = "currency",
    value = DataItem(any = "USD"),
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = "order_total",
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```


以下の有効期限タイプが利用可能です：

| タイプ | 値 | 説明 |
| :--- | :--- | :--- |
| セッション（デフォルト） | `.session` | 現在のセッションの終了時に期限切れになります。 |
| 再起動まで | `.untilRestart` | アプリが閉じられたり再起動された時に期限切れになります。 |
| 永続 | `.forever` | 期限切れになりません。 |
| カスタム日付 | `.after` | 指定された日付に期限切れになります。 |

```swift
tealium.dataLayer.put(key: "currency",
                      value: "USD",
                      expiry: .untilRestart)

tealium.dataLayer.put(key: "order_total",
                      value: 249.95,
                      expiry: .after(Date().advanced(by: 1000)))
```


[`Expiry`](https://docs.tealium.com/tealium-prism-react-native/types/Expiry.html) 値を `put()` または `putAll()` の最後の引数として渡します：

| タイプ | 値 | 説明 |
| :--- | :--- | :--- |
| セッション（デフォルト） | `"session"` | 現在のセッションの終了時に期限切れになります。 |
| 永続 | `"forever"` | アプリがインストールされている間は期限切れになりません。 |
| 再起動まで | `"untilRestart"` | アプリが閉じられたり再起動された時に期限切れになります。 |
| カスタム日付 | `new Date(...)` | 指定された日付と時間に期限切れになります。 |

```javascript
await tealium.dataLayer.put("currency", "USD", "untilRestart");

const sevenDays = 7 * 24 * 60 * 60 * 1000;
await tealium.dataLayer.put("order_total", 249.95, new Date(Date.now() + sevenDays));
```



## データの削除



データレイヤーから特定のキーを削除するには、トランザクショナルブロック内または単独の操作として `remove()` メソッドを使用します。


データレイヤーから特定のキーを削除するには：

```swift
tealium.dataLayer.remove(key: "user_status")
```

複数のキーを削除するには：

```swift
tealium.dataLayer.remove(keys: ["campaign", "discount"])
```

すべてのデータレイヤーの値をクリアするには：

```swift
tealium.dataLayer.clear()
```


データレイヤーからキーを削除するには、[`remove()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#remove) を呼び出します：

```javascript
await tealium.dataLayer.remove("user_status");
```

複数のキーを削除するには：

```javascript
await tealium.dataLayer.remove(["campaign", "discount"]);
```

すべてのデータレイヤーの値をクリアするには、[`clear()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#clear) を呼び出します：

```javascript
await tealium.dataLayer.clear();
```

