---
title: Track
description: Track events and views with the Tealium Prism SDK for Android (Kotlin), iOS (Swift), and React Native.
url: https://docs.tealium.com/platforms/prism-mobile/track/
---
Use the `track()` method to send events and views to Tealium and any configured dispatchers.

## Track events

To track events, pass an event name and optional type and data to the `track()` method. The name of the event appears in the data layer as `tealium_event`.



To track events, call [`track()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) with an event name and an optional `DataObject`:

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```

To track an event without additional data:

```kotlin
tealium.track("homepage")
```

To track an event with multiple data values:

```kotlin
tealium.track("purchase", DataObject.create {
    put("customer_id", "abc123")
    put("order_total", 149.99)
    put("order_id", "0123456789")
})
```


To track events, call [`track()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) with an event name and optional type and data layer parameters:

```swift
// Basic track with default event type and empty data layer
tealium.track("homepage")

// Track with event type and data
tealium.track("user_login", type: .event, dataLayer: ["customer_id": "1234567890"])

// Track with view type
tealium.track("homepage", type: .view)
```


To track events, call [`track()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#track):

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



## Track views

To track screen views, use the `.view` type parameter.



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



## Data objects



Use `DataObject.create` to build structured data for tracking calls. `DataObject.create` supports nested objects and typed values:

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


Pass a dictionary of key-value pairs as the `dataLayer` parameter:

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


Pass a plain JavaScript object as the third argument. Arrays and nested values are supported:

```javascript
await tealium.track("purchase", "event", {
  customer_id: "abc123",
  order_total: 249.95,
  product_id: ["PROD123", "PROD456"],
  product_price: [4.00, 6.00],
});
```


