---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/java/track/
---
## Track Views

Track views with the [`track()`](https://docs.tealium.com/platforms/java/api/#track) method, as shown in the following examples:

```java
// Set event attributes
Udo data = new Udo();
data.put("KEY", "VALUE");

// With optional callback
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // Callback handling
       System.out.println("Dispatch successful: " + String.valueOf(success));    
   }
}
tealium.track("EVENT_NAME", data, callback);
```

The following example tracks a page view:

```java
tealium.track("SCREEN_VIEW", data, callback);
```

The data and callback arguments are optional.

## Track Events

Track events with the same [`track()`](https://docs.tealium.com/platforms/java/api/#track) method used to track views, as shown in the following example:

```java
// Set event attributes
Udo data = new Udo();
data.put("KEY", "VALUE");

// With optional callback
DispatchCallBack callback = new DispatchCallBack() {
    public void dispatchComplete(boolean success, String encodedURLString, String error){
       // Callback handling
       System.out.println("Dispatch successful: " + String.valueOf(success));    
   }
}
tealium.track("EVENT_NAME", data, callback);
```

The following example tracks a user login:

```java
// Event attributes
Udo data = new Udo();
data.put("user_id", "0123456789");
data.put("email_address", "user@example.com");

// With optional callback
DispatchCallBack callBack = new DispatchCallBack(){    
    public void dispatchComplete(boolean success, String error) {        
        // Callback handling  
    }
}
tealium.track("user_login", data, callback);
```

The data and callback arguments are optional.
