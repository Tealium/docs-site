---
title: Data layer
description: Get, set, and manage persistent data layer values with the Tealium Prism SDK.
url: https://docs.tealium.com/platforms/prism-mobile/data-layer/
---
The `dataLayer` provides a shared key-value store for adding contextual data to tracking calls. Values stored in the data layer are automatically included in every tracked event. Use the data layer for static attributes that remain consistent across events, and pass dynamic attributes directly in `track()` calls.

## Install



The DataLayer module is included in `prism-core`. No additional dependency is required.


The DataLayer module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism/Core&#39;
```



## Initialize

The DataLayer module initializes automatically.

You cannot disable this module, as it provides essential data storage capability. The `setEnabled(false)` method has no effect on this module.

## Get data



To get a data layer value, use the [`get()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) method and subscribe to handle the result:

```kotlin
tealium.dataLayer.getString(&#34;customer_id&#34;).subscribe { result -&gt;
    val customerId = result.getOrNull()
    // do something with customerId
}
```


To get a data layer value, call the [`get()`](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:

```swift
tealium.dataLayer.get(key: &#34;customer_id&#34;,
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print(&#34;Value: \(String(describing: value))&#34;)
    case .failure(let error):
        print(&#34;Error: \(error)&#34;)
    }
}
```

To retrieve a specific data item by key:

```swift
if let userStatus = tealium.dataLayer.getDataItem(key: &#34;user_status&#34;) as? String {
    print(&#34;User status: \(userStatus)&#34;)
}
```

To retrieve all key-value pairs in the data layer:

```swift
if let allData = tealium.dataLayer.getAll() {
    print(&#34;All data layer attributes: \(allData)&#34;)
}
```



## Set data

### Individual values



To set a data layer value, use the [`put()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) method:

```kotlin
tealium.dataLayer.put(&#34;my_string&#34;, &#34;my_string_value&#34;)
```


To set a data layer value, use the [`put()`](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:

```swift
tealium.dataLayer.put(key: &#34;some_key&#34;, value: &#34;some value&#34;)
```

To set a value with an expiration:

```swift
tealium.dataLayer.put(key: &#34;user_status&#34;, value: &#34;active&#34;, expiry: .session)
```



### Objects



To set a data layer object, use `DataObject.Builder()`:

```kotlin
val globalContext = DataObject.Builder()
    .put(&#34;customer_id&#34;, &#34;12345&#34;)
    .put(&#34;is_logged_in&#34;, true)
    .put(&#34;consent_status&#34;, &#34;consented&#34;)
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```


To set multiple key-value pairs at once, pass a dictionary to `put(data:)`:

```swift
tealium.dataLayer.put(data: [
    &#34;customer_id&#34;: &#34;12345&#34;,
    &#34;is_logged_in&#34;: true,
    &#34;consent_status&#34;: &#34;consented&#34;,
    &#34;product_category&#34;: [&#34;electronics&#34;, &#34;headphones&#34;]
])
```

To set multiple values with an expiration:

```swift
let data: [String: Any] = [
    &#34;campaign&#34;: &#34;summer_sale&#34;,
    &#34;discount&#34;: 20
]
tealium.dataLayer.put(data: data, expiry: .untilRestart)
```



### Arrays



To set an array value, use `DataList.create`:

```kotlin
val productCategories = DataList.create {
    add(&#34;electronics&#34;)
    add(&#34;headphones&#34;)
}

dataLayer.put(
    key = &#34;product_category&#34;,
    value = productCategories,
    expiry = Expiry.SESSION
).subscribe({ }, { err -&gt; })
```


Arrays are passed as standard Swift arrays in the data dictionary:

```swift
tealium.dataLayer.put(data: [
    &#34;product_category&#34;: [&#34;electronics&#34;, &#34;headphones&#34;]
], expiry: .session)
```



## Transactional updates

Use the `transactionally` method to group multiple data layer updates into a single atomic operation. All updates are applied together, reducing the risk of partial updates.



Use individual `put` operations only when atomicity is not required, because each call runs independently and in sequence. When setting multiple values and timing or consistency is important, use `transactionally` to apply all updates in a single atomic operation.

```kotlin
tealium.dataLayer.transactionally { editor -&gt;
    editor.put(&#34;key&#34;, &#34;value&#34;.asDataItem(), Expiry.SESSION)
        .put(&#34;key2&#34;, &#34;value2&#34;.asDataItem(), Expiry.SESSION)
        .remove(&#34;key2&#34;)
        .commit()
}.onFailure {
    Log.d(&#34;DataLayer&#34;, &#34;Transactional update failed: ${it.message}&#34;)
}
```


The data layer is not changed until the transaction is committed. Applying after commit does nothing. Applied but not committed edits are not reflected in the items returned by this block.

```swift
teal.dataLayer.transactionally { apply, getDataItem, commit in
    apply(.put(&#34;key1&#34;, &#34;value&#34;, .forever))
    apply(.put(&#34;key2&#34;, &#34;value2&#34;, .untilRestart))
    apply(.remove(&#34;key3&#34;))
    if let count = getDataItem(&#34;key4&#34;)?.get(as: Int.self) {
        apply(.put(&#34;key4&#34;, count &#43; 1, .forever))
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
    key = &#34;currency&#34;,
    value = DataItem(any = &#34;USD&#34;),
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = &#34;order_total&#34;,
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
tealium.dataLayer.put(key: &#34;currency&#34;,
                      value: &#34;USD&#34;,
                      expiry: .untilRestart)

tealium.dataLayer.put(key: &#34;order_total&#34;,
                      value: 249.95,
                      expiry: .after(Date().advanced(by: 1000)))
```



## Delete data



To remove a specific key from the data layer, use the `remove()` method within a transactional block or as a standalone operation.


To remove a specific key from the data layer:

```swift
tealium.dataLayer.remove(key: &#34;user_status&#34;)
```

To remove multiple keys:

```swift
tealium.dataLayer.remove(keys: [&#34;campaign&#34;, &#34;discount&#34;])
```

To clear all data layer values:

```swift
tealium.dataLayer.clear()
```


