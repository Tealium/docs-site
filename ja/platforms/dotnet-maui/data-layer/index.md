---
title: データレイヤー
description: アプリライフサイクル全体でデータレイヤーの値を管理する方法を学びます。
url: https://docs.tealium.com/ja/platforms/dotnet-maui/data-layer/
---
## 仕組み

すべてのトラッキング呼び出しで構成するのではなく、一度にグローバルデータレイヤー値を構成するには、`AddToDataLayer()` メソッドを使用します。このメソッドで追加されたデータレイヤーの値は、ライフサイクルイベントを含むすべてのトラッキングイベントに含まれます。`expiry` パラメータを値を保持する時間の長さに構成します。

[データ管理について詳しく学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 使用法

データレイヤーの値を構成するには、データ辞書と有効期限パラメータを使用して `AddToDataLayer()` を呼び出します。

詳しくは、[`AddToDataLayer()`](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#addtodatalayer) と [`Expiry`](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#expiry) を参照してください。

```csharp
tealium.AddToDataLayer(new Dictionary<string, object>(1) {
    {"user_language", "en-EN"}
  },
  Expiry.Forever
);
```

データレイヤーの値を取得するには、取得する値の名前を指定して `GetFromDataLayer()` を呼び出します。

```csharp
string myString = (string)tealium.GetFromDataLayer("user_language");
```
