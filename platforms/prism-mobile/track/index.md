---
title: Track
description: Track events and views with the Tealium Prism SDK.
url: https://docs.tealium.com/platforms/prism-mobile/track/
---
## Track events

To track events, pass an event name and optional type and data to the `track()` method. The name of the event appears in the data layer as `tealium_event`.



To track events, call [`track()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html) with an event name and an optional `DataObject`:

```kotlin
tealium.track(&#34;user_login&#34;, DataObject.create {
    put(&#34;customer_id&#34;, &#34;1234567890&#34;)
})
```

To track an event without additional data:

```kotlin
tealium.track(&#34;homepage&#34;)
```

To track an event with multiple data values:

```kotlin
tealium.track(&#34;purchase&#34;, DataObject.create {
    put(&#34;customer_id&#34;, &#34;abc123&#34;)
    put(&#34;order_total&#34;, 149.99)
    put(&#34;order_id&#34;, &#34;0123456789&#34;)
})
```


To track events, call [`track()`](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) with an event name and optional type and data layer parameters:

```swift
// Basic track with default event type and empty data layer
tealium.track(&#34;homepage&#34;)

// Track with event type and data
tealium.track(&#34;user_login&#34;, type: .event, dataLayer: [&#34;customer_id&#34;: &#34;1234567890&#34;])

// Track with view type
tealium.track(&#34;homepage&#34;, type: .view)
```



## Track views

To track screen views, use the `.view` type parameter.



```kotlin
tealium.track(&#34;product_detail&#34;, DataObject.create {
    put(&#34;product_id&#34;, &#34;SKU123&#34;)
    put(&#34;product_name&#34;, &#34;Running Shoes&#34;)
    put(&#34;product_price&#34;, 89.99)
})
```


```swift
tealium.track(&#34;product_detail&#34;,
    type: .view,
    dataLayer: [
        &#34;product_id&#34;: &#34;SKU123&#34;,
        &#34;product_name&#34;: &#34;Running Shoes&#34;,
        &#34;product_price&#34;: 89.99
    ]
)
```



## Data objects



Use `DataObject.create` to build structured data for tracking calls. `DataObject.create` supports nested objects and typed values:

```kotlin
tealium.track(&#34;purchase&#34;, DataObject.create {
    put(&#34;customer_id&#34;, &#34;abc123&#34;)
    put(&#34;order_total&#34;, 249.95)
    put(&#34;product_id&#34;, DataList.create {
        add(&#34;PROD123&#34;)
        add(&#34;PROD456&#34;)
    })
    put(&#34;product_price&#34;, DataList.create {
        add(4.00)
        add(6.00)
    })
})
```


Pass a dictionary of key-value pairs as the `dataLayer` parameter:

```swift
tealium.track(&#34;purchase&#34;,
    type: .event,
    dataLayer: [
        &#34;customer_id&#34;: &#34;abc123&#34;,
        &#34;order_total&#34;: 249.95,
        &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;],
        &#34;product_price&#34;: [4.00, 6.00]
    ]
)
```


