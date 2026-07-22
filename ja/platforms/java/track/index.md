---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/java/track/
---
## ビューのトラッキング

以下の例のように、[`track()`](https://docs.tealium.com/ja/platforms/java/api/#track)メソッドを使用してビューをトラッキングします：

```java
// イベント属性を構成
Udo data = new Udo();
data.put("KEY", "VALUE");

// オプションのコールバック付き
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // コールバックの処理
       System.out.println("Dispatch successful: " + String.valueOf(success));    
   }
}
tealium.track("EVENT_NAME", data, callback);
```

次の例はページビューをトラッキングします：

```java
tealium.track("SCREEN_VIEW", data, callback);
```

dataとcallbackの引数はオプションです。

## イベントのトラッキング

ビューのトラッキングに使用される同じ[`track()`](https://docs.tealium.com/ja/platforms/java/api/#track)メソッドを使用してイベントをトラッキングします。以下の例を参照してください：

```java
// イベント属性を構成
Udo data = new Udo();
data.put("KEY", "VALUE");

// オプションのコールバック付き
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // コールバックの処理
       System.out.println("Dispatch successful: " + String.valueOf(success));    
   }
}
tealium.track("EVENT_NAME", data, callback);
```

次の例はユーザーログインをトラッキングします：

```java
// イベント属性
Udo data = new Udo();
data.put("user_id", "0123456789");
data.put("email_address", "user@example.com");

// オプションのコールバック付き
DispatchCallBack callBack = new DispatchCallBack(){    
    public void dispatchComplete(boolean success, String error) {        
        // コールバックの処理  
    }
}
tealium.track("user_login", data, callback);
```

dataとcallbackの引数はオプションです。
