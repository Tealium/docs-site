---
title: Data Management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/cordova-v1/data-management/
---
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](/platforms/cordova/).

## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.

## Persistent Data

The [`addPersistent()`](/platforms/cordova-v1/api/#addpersistent) method adds persistent data, as shown in the following example:   
```js
tealium.addPersistent(&#34;KEY_NAME&#34;, &#34;DATA&#34;, &#34;INSTANCE_NAME&#34;);
```

The [`getPersistent()`](/platforms/cordova-v1/api/#getpersistent) method gets persistent data, with a callback, as shown in the following example:  
```js
tealium.getPersistent(&#34;KEY_NAME&#34;, &#34;INSTANCE_NAME&#34;, function (val) {
    // this callback will be called when the persistent data source has been found
    if (val === null) {
        // returns null if data was not found
        alert(&#34;Requested persistent data could not be found&#34;);
    } else {
        alert(&#34;Persistent object data returned: &#34; &#43; &#34;mypersistentvariable = &#34; &#43; val.toString());
    }});
```

The [`removePersistent()`](/platforms/cordova-v1/api/#removepersistent) method removes persistent data, as shown in the following example:
```js
tealium.removePersistent(&#34;KEY_NAME&#34;, &#34;INSTANCE_NAME&#34;);
```

## Volatile Data

The [`addVolatile()`](/platforms/cordova-v1/api/#addvolatile) method adds volatile data, as shown in the following example:   
```js
tealium.addVolatile(&#34;KEY_NAME&#34;, &#34;DATA&#34;, &#34;INSTANCE_NAME&#34;);
```

The [`getVolatile()`](/platforms/cordova-v1/api/#getvolatile) method gets volatile data, with a callback, as shown in the following example:  

```js
tealium.getVolatile(&#34;KEY_NAME&#34;, &#34;INSTANCE_NAME&#34;, function (val) {
    // this callback will be called when the volatile data source has been found
    if (val === null) {
        // returns null if data was not found
        alert(&#34;Requested volatile data could not be found&#34;);
    } else {
        alert(&#34;Volatile object data returned: &#34; &#43; &#34;myvolatilevariable = &#34; &#43; val.toString());
    }});
```

The [`removeVolatile()`](/platforms/cordova-v1/api/#removevolatile) method removes volatile data, as shown in the following example:   
```js
tealium.removeVolatile(&#34;KEY_NAME&#34;, window.tealium_instance);
```
