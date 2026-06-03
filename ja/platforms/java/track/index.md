---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/java/track/
---
## ビューのトラッキング

以下の例のように、[`track()`](/ja/platforms/java/api/#track)メソッドを使用してビューをトラッキングします：

```java
// イベント属性を構成
Udo data = new Udo();
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);

// オプションのコールバック付き
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // コールバックの処理
       System.out.println(&#34;Dispatch successful: &#34; &#43; String.valueOf(success));    
   }
}
tealium.track(&#34;EVENT_NAME&#34;, data, callback);
```

次の例はページビューをトラッキングします：

```java
tealium.track(&#34;SCREEN_VIEW&#34;, data, callback);
```

dataとcallbackの引数はオプションです。

## イベントのトラッキング

ビューのトラッキングに使用される同じ[`track()`](/ja/platforms/java/api/#track)メソッドを使用してイベントをトラッキングします。以下の例を参照してください：

```java
// イベント属性を構成
Udo data = new Udo();
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);

// オプションのコールバック付き
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // コールバックの処理
       System.out.println(&#34;Dispatch successful: &#34; &#43; String.valueOf(success));    
   }
}
tealium.track(&#34;EVENT_NAME&#34;, data, callback);
```

次の例はユーザーログインをトラッキングします：

```java
// イベント属性
Udo data = new Udo();
data.put(&#34;user_id&#34;, &#34;0123456789&#34;);
data.put(&#34;email_address&#34;, &#34;user@example.com&#34;);

// オプションのコールバック付き
DispatchCallBack callBack = new DispatchCallBack(){    
    public void dispatchComplete(boolean success, String error) {        
        // コールバックの処理  
    }
}
tealium.track(&#34;user_login&#34;, data, callback);
```

dataとcallbackの引数はオプションです。
