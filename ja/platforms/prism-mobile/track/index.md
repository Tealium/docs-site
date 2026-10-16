---
title: トラック
description: Tealium Prism SDK for Android (Kotlin)、iOS (Swift)、および React Native を使用してイベントとビューをトラックします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/track/
---
`track()` メソッドを使用して、Tealium および構成されたディスパッチャーにイベントとビューを送信します。

## イベントのトラッキング

イベントをトラッキングするには、イベント名とオプショナルなタイプおよびデータを `track()` メソッドに渡します。イベント名はデータレイヤーに `tealium_event` として表示されます。



イベントをトラッキングするには、イベント名とオプショナルな `DataObject` を指定して [`track()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) を呼び出します：

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```

追加データなしでイベントをトラッキングする場合：

```kotlin
tealium.track("homepage")
```

複数のデータ値でイベントをトラッキングする場合：

```kotlin
tealium.track("purchase", DataObject.create {
    put("customer_id", "abc123")
    put("order_total", 149.99)
    put("order_id", "0123456789")
})
```


イベントをトラッキングするには、イベント名とオプショナルなタイプおよびデータレイヤーパラメータを指定して [`track()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) を呼び出します：

```swift
// デフォルトのイベントタイプと空のデータレイヤーで基本トラック
tealium.track("homepage")

// イベントタイプとデータでトラック
tealium.track("user_login", type: .event, dataLayer: ["customer_id": "1234567890"])

// ビュータイプでトラック
tealium.track("homepage", type: .view)
```


イベントをトラッキングするには、[`track()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#track) を呼び出します：

```javascript
// データなしでイベントをトラック
await tealium.track("homepage");

// データを持つイベントをトラック
await tealium.track("user_login", "event", { customer_id: "1234567890" });

// 複数の値を持つイベントをトラック
await tealium.track("purchase", "event", {
  customer_id: "abc123",
  order_total: 149.99,
  order_id: "0123456789",
});
```



## ビューのトラッキング

画面ビューをトラッキングするには、`.view` タイプパラメータを使用します。



```kotlin
tealium.track("product_detail", DataObject.create {
    put("product_id", "SKU123")
    put("product_name", "Running Shoes")
    put("product_price", 89.99)
})
```


```swift
tealium.track("product_detail",
    type: .view,
    dataLayer: [
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



トラッキングコール用の構造化データを構築するには `DataObject.create` を使用します。`DataObject.create` はネストされたオブジェクトと型指定された値をサポートします：

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


`dataLayer` パラメータとしてキーと値のペアの辞書を渡します：

```swift
tealium.track("purchase",
    type: .event,
    dataLayer: [
        "customer_id": "abc123",
        "order_total": 249.95,
        "product_id": ["PROD123", "PROD456"],
        "product_price": [4.00, 6.00]
    ]
)
```


第三引数としてプレーンな JavaScript オブジェクトを渡します。配列やネストされた値もサポートされています：

```javascript
await tealium.track("purchase", "event", {
  customer_id: "abc123",
  order_total: 249.95,
  product_id: ["PROD123", "PROD456"],
  product_price: [4.00, 6.00],
});
```

