---
title: Data Layer
description: Learn how to manage data layer values across the app lifecycle.
url: https://docs.tealium.com/platforms/dotnet-maui/data-layer/
---
## How it works

To set global data layer values once instead of setting them in every tracking call, use the `AddToDataLayer()` method. Data layer values added with this method are included in every tracked event, including lifecycle events. Set the `expiry` parameter to the length of time to persist the value.

[Learn more about data management](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#data-management).

## Usage

To set data layer values, call `AddToDataLayer()` with a data dictionary and an expiration parameter.

To learn more, see [`AddToDataLayer()`](https://docs.tealium.com/platforms/dotnet-maui/api/#addtodatalayer) and [`Expiry`](https://docs.tealium.com/platforms/dotnet-maui/api/#expiry).

```csharp
tealium.AddToDataLayer(new Dictionary<string, object>(1) {
    {"user_language", "en-EN"}
  },
  Expiry.Forever
);
```

To get a data layer value, call `GetFromDataLayer()` with the name of the value to retrieve.

```csharp
string myString = (string)tealium.GetFromDataLayer("user_language");
```



