---
title: データレイヤー
description: アプリのライフサイクル全体でデータレイヤーの値を管理する方法を学びます。
url: https://docs.tealium.com/ja/platforms/xamarin/data-management/
---
## 仕組み

全体のデータレイヤーの値を一度に構成するために、`AddToDataLayer()` メソッドを使用します。このメソッドで追加されたデータレイヤーの値は、ライフサイクルイベントを含むすべての追跡イベントに含まれます。有効期限パラメータを値を保持する時間の長さに構成します。

[データ管理についてもっと学ぶ](/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 使用法

データレイヤーの値を構成するには、データ辞書と有効期限パラメータを使用して `AddToDataLayer()` を呼び出します。

[`AddToDataLayer()`](/ja/platforms/xamarin/api/#addtodatalayer) と [`Expiry`](/ja/platforms/xamarin/api/#expiry) についてもっと学ぶ。

```csharp
tealium.AddToDataLayer(new Dictionary&lt;string, object&gt;(1) {
    {&#34;user_language&#34;, &#34;en-EN&#34;}
  },
  Expiry.Forever
);
```

データレイヤーの値を取得するには、取得する値の名前を使用して `GetFromDataLayer()` を呼び出します。

```csharp
string myString = (string)tealium.GetFromDataLayer(&#34;user_language&#34;);
```
