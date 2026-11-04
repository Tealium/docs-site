---
title: トラッキング
description: Android（Kotlin）、iOS（Swift）、React Native向けのTealium Prism SDKを使用して、イベントとビューをトラッキングします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/track/
---
`track()`メソッドを使用して、イベントとビューをTealiumおよび構成済みのディスパッチャーに送信します。

## イベントのトラッキング

イベントをトラッキングするには、イベント名と、任意のタイプおよびデータを`track()`メソッドに渡します。イベント名は、データレイヤーに`tealium_event`として表示されます。



イベントをトラッキングするには、イベント名と`DataObject`を指定して[`track()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html)を呼び出します。

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```

追加データなしでイベントをトラッキングするには、次のようにします。

```kotlin
tealium.track("homepage", DataObject.EMPTY_OBJECT)
```

複数のデータ値を含むイベントをトラッキングするには、次のようにします。

```kotlin
tealium.track("purchase", DataObject.create {
    put("customer_id", "abc123")
    put("order_total", 149.99)
    put("order_id", "0123456789")
})
```


イベントをトラッキングするには、イベント名と、任意のタイプおよびデータパラメータを指定して[`track()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html)を呼び出します。

```swift
// Basic track with default event type and no data
tealium.track("homepage")

// Track with event type and data
tealium.track("user_login", type: .event, data: ["customer_id": "1234567890"])

// Track with view type
tealium.track("homepage", type: .view)
```


イベントをトラッキングするには、[`track()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#track)を呼び出します。

```javascript
// Track an event without data
await tealium.track("homepage");

// Track an event with data
await tealium.track("user_login", "event", { customer_id: "1234567890" });

// Track an event with multiple values
await tealium.track("purchase", "event", {
  customer_id: "abc123",
  order_total: 149.99,
  order_id: "0123456789",
});
```



## ビューのトラッキング

画面ビューをトラッキングするには、`.view`タイプパラメータを使用します。



```kotlin
tealium.track("product_detail", DispatchType.View, DataObject.create {
    put("product_id", "SKU123")
    put("product_name", "Running Shoes")
    put("product_price", 89.99)
})
```


```swift
tealium.track("product_detail",
    type: .view,
    data: [
        "product_id": "SKU123",
        "product_name": "Running Shoes",
        "product_price": 89.99
    ]
)
```


```javascript
await tealium.track("product_detail", "view", {
  product_id: "SKU123",
  product_name: "Running Shoes",
  product_price: 89.99,
});
```



## データオブジェクト



`DataObject.create`を使用して、トラッキング呼び出し用の構造化データを作成します。`DataObject.create`は、ネストされたオブジェクトと型付きの値をサポートします。

```kotlin
tealium.track("purchase", DataObject.create {
    put("customer_id", "abc123")
    put("order_total", 249.95)
    put("product_id", DataList.create {
        add("PROD123")
        add("PROD456")
    })
    put("product_price", DataList.create {
        add(4.00)
        add(6.00)
    })
})
```


イベントデータを辞書リテラルとして渡します。Swiftは、解析処理を行わず、型付きの値から`DataObject`を直接作成します。

```swift
tealium.track("purchase", data: [
    "order_id": "0123456789",
    "order_total": 149.99,
    "product": ["id": "SKU123", "price": 89.99] as DataObject,
    "tags": ["new", "sale"]
])
```

ネストされたオブジェクトには`as DataObject`を、オブジェクトの配列には`as [DataObject]`を指定します。一部の値がオプショナルの場合は、`DataObject(compacting:)`を使用します。

データがすでに`[String: Any]`辞書である場合（解析済みのJSONやクロスプラットフォームブリッジから取得した値など）は、`try DataObject(jsonObject:)`を使用します。このメソッドはJSONへのラウンドトリップによって辞書を検証するため、リテラルよりも呼び出しごとのコストが高くなります。動的データにのみ使用してください。


プレーンなJavaScriptオブジェクトを3番目の引数として渡します。配列とネストされた値がサポートされています。

```javascript
await tealium.track("purchase", "event", {
  customer_id: "abc123",
  order_total: 249.95,
  product_id: ["PROD123", "PROD456"],
  product_price: [4.00, 6.00],
});
```

