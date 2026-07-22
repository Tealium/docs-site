---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/cordova-v1/data-management/
---

<blockquote>
これはTealium for Cordovaの以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for Cordova 2.x](https://docs.tealium.com/ja/platforms/cordova/)を参照してください。
</blockquote>


## 使用法

すべてのイベントに必要な変数があります。すべてのイベントに必要な変数データを手動で追加する必要を避けるために、データを揮発性または永続的として保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

[データ管理についてもっと学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 永続的データ

次の例に示すように、[`addPersistent()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#addpersistent) メソッドは永続的データを追加します。
```js
tealium.addPersistent("KEY_NAME", "DATA", "INSTANCE_NAME");
```

次の例に示すように、[`getPersistent()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#getpersistent) メソッドは永続的データを取得します。
```js
tealium.getPersistent("KEY_NAME", "INSTANCE_NAME", function (val) {
    // このコールバックは永続的データソースが見つかったときに呼び出されます
    if (val === null) {
        // データが見つからなかった場合はnullを返します
        alert("要求された永続的データが見つかりませんでした");
    } else {
        alert("永続的オブジェクトデータが返されました: " + "mypersistentvariable = " + val.toString());
    }});
```

次の例に示すように、[`removePersistent()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#removepersistent) メソッドは永続的データを削除します。
```js
tealium.removePersistent("KEY_NAME", "INSTANCE_NAME");
```

## 揮発性データ

次の例に示すように、[`addVolatile()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#addvolatile) メソッドは揮発性データを追加します。
```js
tealium.addVolatile("KEY_NAME", "DATA", "INSTANCE_NAME");
```

次の例に示すように、[`getVolatile()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#getvolatile) メソッドは揮発性データを取得します。
```js
tealium.getVolatile("KEY_NAME", "INSTANCE_NAME", function (val) {
    // このコールバックは揮発性データソースが見つかったときに呼び出されます
    if (val === null) {
        // データが見つからなかった場合はnullを返します
        alert("要求された揮発性データが見つかりませんでした");
    } else {
        alert("揮発性オブジェクトデータが返されました: " + "myvolatilevariable = " + val.toString());
    }});
```

次の例に示すように、[`removeVolatile()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#removevolatile) メソッドは揮発性データを削除します。
```js
tealium.removeVolatile("KEY_NAME", window.tealium_instance);
```