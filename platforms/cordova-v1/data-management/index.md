---
title: Data Management
description: Learn how to manage persistent and volatile data.
url: https://docs.tealium.com/platforms/cordova-v1/data-management/
---

<blockquote>
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](https://docs.tealium.com/platforms/cordova/).
</blockquote>


## Usage

Some variables are required on every event. To prevent having to manually add required variable data to every event, you have the option to store data as either volatile or persistent. Once data is stored, it will be appended to every event, including lifecycle events.

[Learn more](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#data-management) about Data Management.

## Persistent Data

The [`addPersistent()`](https://docs.tealium.com/platforms/cordova-v1/api/#addpersistent) method adds persistent data, as shown in the following example:   
```js
tealium.addPersistent("KEY_NAME", "DATA", "INSTANCE_NAME");
```

The [`getPersistent()`](https://docs.tealium.com/platforms/cordova-v1/api/#getpersistent) method gets persistent data, with a callback, as shown in the following example:  
```js
tealium.getPersistent("KEY_NAME", "INSTANCE_NAME", function (val) {
    // this callback will be called when the persistent data source has been found
    if (val === null) {
        // returns null if data was not found
        alert("Requested persistent data could not be found");
    } else {
        alert("Persistent object data returned: " + "mypersistentvariable = " + val.toString());
    }});
```

The [`removePersistent()`](https://docs.tealium.com/platforms/cordova-v1/api/#removepersistent) method removes persistent data, as shown in the following example:
```js
tealium.removePersistent("KEY_NAME", "INSTANCE_NAME");
```

## Volatile Data

The [`addVolatile()`](https://docs.tealium.com/platforms/cordova-v1/api/#addvolatile) method adds volatile data, as shown in the following example:   
```js
tealium.addVolatile("KEY_NAME", "DATA", "INSTANCE_NAME");
```

The [`getVolatile()`](https://docs.tealium.com/platforms/cordova-v1/api/#getvolatile) method gets volatile data, with a callback, as shown in the following example:  

```js
tealium.getVolatile("KEY_NAME", "INSTANCE_NAME", function (val) {
    // this callback will be called when the volatile data source has been found
    if (val === null) {
        // returns null if data was not found
        alert("Requested volatile data could not be found");
    } else {
        alert("Volatile object data returned: " + "myvolatilevariable = " + val.toString());
    }});
```

The [`removeVolatile()`](https://docs.tealium.com/platforms/cordova-v1/api/#removevolatile) method removes volatile data, as shown in the following example:   
```js
tealium.removeVolatile("KEY_NAME", window.tealium_instance);
```
