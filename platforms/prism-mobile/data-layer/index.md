---
title: Data layer
description: Get, set, and manage persistent data layer values with the Tealium Prism SDK for Android (Kotlin), iOS (Swift), and React Native.
url: https://docs.tealium.com/platforms/prism-mobile/data-layer/
---
The `dataLayer` provides a shared key-value store for adding contextual data to tracking calls. Values stored in the data layer are automatically included in every tracked event. Use the data layer for static attributes that remain consistent across events, and pass dynamic attributes directly in `track()` calls.

## Install



The DataLayer module is included in `prism-core`. No additional dependency is required.


The DataLayer module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism/Core'
```


The DataLayer module is included in `@tealium/prism-react-native`. No additional dependency is required.



## Initialize

The DataLayer module initializes automatically.


<blockquote>
You cannot disable this module, as it provides essential data storage capability. The `setEnabled(false)` method has no effect on this module.
</blockquote>


## Get data



To get a data layer value, use the [`get()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) method and subscribe to handle the result:

```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // do something with customerId
}
```


To get a data layer value, call the [`get()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:

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

To retrieve a specific data item by key:

```swift
if let userStatus = tealium.dataLayer.getDataItem(key: "user_status") as? String {
    print("User status: \(userStatus)")
}
```

To retrieve all key-value pairs in the data layer:

```swift
if let allData = tealium.dataLayer.getAll() {
    print("All data layer attributes: \(allData)")
}
```


To get a data layer value, call [`get()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#get):

```javascript
const customerId = await tealium.dataLayer.get("customer_id");
```

To retrieve all data layer values, call [`getAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#getall):

```javascript
const allData = await tealium.dataLayer.getAll();
```



## Set data

### Individual values



To set a data layer value, use the [`put()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) method:

```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```


To set a data layer value, use the [`put()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:

```swift
tealium.dataLayer.put(key: "some_key", value: "some value")
```

To set a value with an expiration:

```swift
tealium.dataLayer.put(key: "user_status", value: "active", expiry: .session)
```


To set a data layer value, call [`put()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#put):

```javascript
await tealium.dataLayer.put("my_string", "my_string_value");
```

To set a value with an expiration:

```javascript
await tealium.dataLayer.put("user_status", "active", "session"); // or "forever", "untilRestart"
```



### Objects



To set a data layer object, use `DataObject.Builder()`:

```kotlin
val globalContext = DataObject.Builder()
    .put("customer_id", "12345")
    .put("is_logged_in", true)
    .put("consent_status", "consented")
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```


To set multiple key-value pairs at once, pass a dictionary to `put(data:)`:

```swift
tealium.dataLayer.put(data: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones"]
])
```

To set multiple values with an expiration:

```swift
let data: [String: Any] = [
    "campaign": "summer_sale",
    "discount": 20
]
tealium.dataLayer.put(data: data, expiry: .untilRestart)
```


To set multiple key-value pairs at once, call [`putAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#putall):

```javascript
await tealium.dataLayer.putAll({
  customer_id: "12345",
  is_logged_in: true,
  consent_status: "consented",
});
```

To set multiple values with an expiration:

```javascript
await tealium.dataLayer.putAll({ campaign: "summer_sale", discount: 20 }, "untilRestart");
```



### Arrays



To set an array value, use `DataList.create`:

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


Arrays are passed as standard Swift arrays in the data dictionary:

```swift
tealium.dataLayer.put(data: [
    "product_category": ["electronics", "headphones"]
], expiry: .session)
```


Pass arrays as values in a `putAll()` call:

```javascript
await tealium.dataLayer.putAll({
  product_category: ["electronics", "headphones"],
});
```



## Transactional updates

Use the `transactionally` method to group multiple data layer updates into a single atomic operation. All updates are applied together, reducing the risk of partial updates.


<blockquote>
React Native does not support atomic transactional updates. Use `put()` and `putAll()` for individual or bulk writes.
</blockquote>




Use individual `put` operations only when atomicity is not required, because each call runs independently and in sequence. When setting multiple values and timing or consistency is important, use `transactionally` to apply all updates in a single atomic operation.

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


The data layer is not changed until the transaction is committed. Applying after commit does nothing. Applied but not committed edits are not reflected in the items returned by this block.

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



## Data expiration

When you set a data layer value, optionally set the expiry to determine when the value expires.



The following expiration types are available:

| Type | Value | Description |
| :--- | :--- | :--- |
| Session (default) | `Expiry.SESSION` | Expires at the end of the current session. |
| Forever | `Expiry.FOREVER` | Never expires while the app is installed. |
| Until restart | `Expiry.UNTIL_RESTART` | Expires when the app is closed or restarted. |
| Custom duration | `Expiry.afterTimeUnit(time, units)` | Expires after the specified duration. |

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


The following expiration types are available:

| Type | Value | Description |
| :--- | :--- | :--- |
| Session (default) | `.session` | Expires at the end of the current session. |
| Until restart | `.untilRestart` | Expires when the app is closed or restarted. |
| Forever | `.forever` | Never expires. |
| Custom date | `.after` | Expires on the date specified. |

```swift
tealium.dataLayer.put(key: "currency",
                      value: "USD",
                      expiry: .untilRestart)

tealium.dataLayer.put(key: "order_total",
                      value: 249.95,
                      expiry: .after(Date().advanced(by: 1000)))
```


Pass an [`Expiry`](https://docs.tealium.com/tealium-prism-react-native/types/Expiry.html) value as the last argument of `put()` or `putAll()`:

| Type | Value | Description |
| :--- | :--- | :--- |
| Session (default) | `"session"` | Expires at the end of the current session. |
| Forever | `"forever"` | Never expires while the app is installed. |
| Until restart | `"untilRestart"` | Expires when the app is closed or restarted. |
| Custom date | `new Date(...)` | Expires at the specified date and time. |

```javascript
await tealium.dataLayer.put("currency", "USD", "untilRestart");

const sevenDays = 7 * 24 * 60 * 60 * 1000;
await tealium.dataLayer.put("order_total", 249.95, new Date(Date.now() + sevenDays));
```



## Delete data



To remove a specific key from the data layer, use the `remove()` method within a transactional block or as a standalone operation.


To remove a specific key from the data layer:

```swift
tealium.dataLayer.remove(key: "user_status")
```

To remove multiple keys:

```swift
tealium.dataLayer.remove(keys: ["campaign", "discount"])
```

To clear all data layer values:

```swift
tealium.dataLayer.clear()
```


To remove a key from the data layer, call [`remove()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#remove):

```javascript
await tealium.dataLayer.remove("user_status");
```

To remove multiple keys:

```javascript
await tealium.dataLayer.remove(["campaign", "discount"]);
```

To clear all data layer values, call [`clear()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#clear):

```javascript
await tealium.dataLayer.clear();
```


