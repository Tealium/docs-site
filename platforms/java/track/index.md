---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/java/track/
---
## Track Views

Track views with the [`track()`](/platforms/java/api/#track) method, as shown in the following examples:

```java
// Set event attributes
Udo data = new Udo();
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);

// With optional callback
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // Callback handling
       System.out.println(&#34;Dispatch successful: &#34; &#43; String.valueOf(success));    
   }
}
tealium.track(&#34;EVENT_NAME&#34;, data, callback);
```

The following example tracks a page view:

```java
tealium.track(&#34;SCREEN_VIEW&#34;, data, callback);
```

The data and callback arguments are optional.

## Track Events

Track events with the same [`track()`](/platforms/java/api/#track) method used to track views, as shown in the following example:

```java
// Set event attributes
Udo data = new Udo();
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);

// With optional callback
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // Callback handling
       System.out.println(&#34;Dispatch successful: &#34; &#43; String.valueOf(success));    
   }
}
tealium.track(&#34;EVENT_NAME&#34;, data, callback);
```

The following example tracks a user login:

```java
// Event attributes
Udo data = new Udo();
data.put(&#34;user_id&#34;, &#34;0123456789&#34;);
data.put(&#34;email_address&#34;, &#34;user@example.com&#34;);

// With optional callback
DispatchCallBack callBack = new DispatchCallBack(){    
    public void dispatchComplete(boolean success, String error) {        
        // Callback handling  
    }
}
tealium.track(&#34;user_login&#34;, data, callback);
```

The data and callback arguments are optional.
