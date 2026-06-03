---
title: Data Layer
description: Learn how to manage data layer values across the app lifecycle.
url: https://docs.tealium.com/platforms/xamarin/data-management/
---
## How it works

To set global data layer values once, instead of setting them in every tracking call, use the `AddToDataLayer()` method. Data layer values added with this method are included in every tracked event, including lifecycle events. Set the expiry parameter to the length of time to persist the value.

[Learn more about data management](/platforms/getting-started-mobile/mobile-concepts/#data-management).

## Usage

To set data layer values, call `AddToDataLayer()` with a data dictionary and an expiration parameter.

Learn more about [`AddToDataLayer()`](/platforms/xamarin/api/#addtodatalayer) and [`Expiry`](/platforms/xamarin/api/#expiry).

```csharp
tealium.AddToDataLayer(new Dictionary&lt;string, object&gt;(1) {
    {&#34;user_language&#34;, &#34;en-EN&#34;}
  },
  Expiry.Forever
);
```

To get a data layer value, call `GetFromDataLayer()` with the name of the value to retrieve.

```csharp
string myString = (string)tealium.GetFromDataLayer(&#34;user_language&#34;);
```



