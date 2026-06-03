---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/xamarin-v1/data-management/
---現在のバージョンについては、[Tealium for Xamarin 2.x](/ja/platforms/xamarin/)を参照してください。

## 使用法

すべてのイベントには必要な変数が必要です。すべてのイベントに必要な変数データを手動で追加する必要をなくすために、データを揮発性または永続的として保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

[データ管理についてもっと学ぶ](/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 永続的データ

永続的データは、トラッキングコールのたびにデータ辞書に統合され、起動間でも持続します。

次の例に示すように、`AddPersistentDataSources()` メソッドは永続的データを追加します：

```csharp
tealium.AddPersistentDataSources(new Dictionary&lt;string, object&gt;(1) {
  {&#34;KEY&#34;, &#34;VALUE&#34;}});
```

## 揮発性データ

揮発性データは、トラッキングコールのたびにデータ辞書に統合されますが、アプリケーションが閉じられると揮発性データは失われ、次の起動時には存在しません。

次の例に示すように、`AddVolatileDataSources()` メソッドは揮発性データを追加します：

```csharp
tealium.AddVolatileDataSources(new Dictionary&lt;string, object&gt;(1) {
   {&#34;KEY&#34;, &#34;VALUE&#34;}});
```