---
title: データ管理
description: 永続的および揮発性データの管理方法を学びます。
url: https://docs.tealium.com/ja/platforms/cordova-v1/data-management/
---
これはTealium for Cordovaの以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for Cordova 2.x](/ja/platforms/cordova/)を参照してください。

## 使用法

すべてのイベントに必要な変数があります。すべてのイベントに必要な変数データを手動で追加する必要を避けるために、データを揮発性または永続的として保存するオプションがあります。データが保存されると、ライフサイクルイベントを含むすべてのイベントに追加されます。

[データ管理についてもっと学ぶ](/ja/platforms/getting-started-mobile/mobile-concepts/#data-management)。

## 永続的データ

次の例に示すように、[`addPersistent()`](/ja/platforms/cordova-v1/api/#addpersistent) メソッドは永続的データを追加します。
```js
tealium.addPersistent(&#34;KEY_NAME&#34;, &#34;DATA&#34;, &#34;INSTANCE_NAME&#34;);
```

次の例に示すように、[`getPersistent()`](/ja/platforms/cordova-v1/api/#getpersistent) メソッドは永続的データを取得します。
```js
tealium.getPersistent(&#34;KEY_NAME&#34;, &#34;INSTANCE_NAME&#34;, function (val) {
    // このコールバックは永続的データソースが見つかったときに呼び出されます
    if (val === null) {
        // データが見つからなかった場合はnullを返します
        alert(&#34;要求された永続的データが見つかりませんでした&#34;);
    } else {
        alert(&#34;永続的オブジェクトデータが返されました: &#34; &#43; &#34;mypersistentvariable = &#34; &#43; val.toString());
    }});
```

次の例に示すように、[`removePersistent()`](/ja/platforms/cordova-v1/api/#removepersistent) メソッドは永続的データを削除します。
```js
tealium.removePersistent(&#34;KEY_NAME&#34;, &#34;INSTANCE_NAME&#34;);
```

## 揮発性データ

次の例に示すように、[`addVolatile()`](/ja/platforms/cordova-v1/api/#addvolatile) メソッドは揮発性データを追加します。
```js
tealium.addVolatile(&#34;KEY_NAME&#34;, &#34;DATA&#34;, &#34;INSTANCE_NAME&#34;);
```

次の例に示すように、[`getVolatile()`](/ja/platforms/cordova-v1/api/#getvolatile) メソッドは揮発性データを取得します。
```js
tealium.getVolatile(&#34;KEY_NAME&#34;, &#34;INSTANCE_NAME&#34;, function (val) {
    // このコールバックは揮発性データソースが見つかったときに呼び出されます
    if (val === null) {
        // データが見つからなかった場合はnullを返します
        alert(&#34;要求された揮発性データが見つかりませんでした&#34;);
    } else {
        alert(&#34;揮発性オブジェクトデータが返されました: &#34; &#43; &#34;myvolatilevariable = &#34; &#43; val.toString());
    }});
```

次の例に示すように、[`removeVolatile()`](/ja/platforms/cordova-v1/api/#removevolatile) メソッドは揮発性データを削除します。
```js
tealium.removeVolatile(&#34;KEY_NAME&#34;, window.tealium_instance);
```