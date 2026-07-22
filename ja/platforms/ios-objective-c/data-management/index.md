---
title: データ管理
description: 永続的なデータと揮発性のデータの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/data-management/
---
## 使用法

一部の変数はすべてのイベントで必要とされます。必要な変数データを手動で各イベントに追加するのを防ぐために、データを揮発性または永続性のいずれかで保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

永続的なデータと揮発性のデータの値は、[NSDictionary](https://developer.apple.com/documentation/foundation/nsdictionary)オブジェクトとしてデバイスに保存されます。

データ管理について[詳しく学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。


## 永続的なデータ

永続的なオブジェクトは各イベントにマージされ、アプリの起動間で保存されます。

[`addPersistentDataSources()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/addPersistentDataSources:)メソッドは、以下の例に示すように、ライブラリインスタンスの永続的なデータストアにキー値データを追加します：

```obj-c
[self.tealium addPersistentDataSources:@{@"KEY": @"VALUE"}];
NSDictionary *persistentDataSources = [self.tealium persistentDataSourcesCopy];
```


## 揮発性のデータ

揮発性のオブジェクトは、アプリを閉じて再起動すると破棄されます。

[`addVolatileDataSources()`](https://tealium.github.io/tealium-ios/Classes/Tealium.html#//api/name/addVolatileDataSources:)メソッドは、以下の例に示すように、一時的なデータソースの辞書にキー値データを追加します：

```obj-c
[self.tealium addVolatileDataSources:@{@"KEY": @"VALUE"}];
NSDictionary *volatileDataSources = [self.tealium volatileDataSourcesCopy];
```
