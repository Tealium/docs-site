---
title: Install
description: Learn to install Tealium for Roku.
url: https://docs.tealium.com/platforms/roku/install/
---
This guide shows how to add Tealium to your Roku app to track user activity.

## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)
* [Roku SDK](https://sdkdocs.roku.com/display/sdkdoc/Release+Notes) 7.2+
* Active [Roku developer account](https://developer.roku.com/developer)
* Roku Device


<blockquote>
We recommend that you develop in [Visual Studio Code with the Brightscript Plugin](https://github.com/rokucommunity/vscode-brightscript-language).
</blockquote>


## Sample Apps

To help familiarize yourself with our library, the tracking methods, and best practice implementation, we recommend that you download the [Roku sample app](https://github.com/Tealium/tealium-roku/tree/master/TealiumRokuSample).

The code for the sample app is available in the [`TealiumSample.brs`](https://github.com/Tealium/tealium-roku/blob/master/TealiumRokuSample/components/TealiumSample.brs) and the [`TealiumSample.xml`](https://github.com/Tealium/tealium-roku/blob/master/TealiumRokuSample/components/TealiumSample.xml) files. The app provides examples of adding button tracking through the supplied `TealiumTask` and `TealiumTaskInterface` files.

## Install

To install the Tealium library for Roku, use one of the two following methods:

* [`ROPM`](https://github.com/rokucommunity/ropm) (Community Driven Roku dependency manager)
* Download the repo

### ROPM

If you use `ROPM`, we recommend aliasing the Tealium library. In your `package.json`, add the following dependency:

```json
{
    "dependencies": {
        "tealium": "npm:tealium-roku-plugin@2.0.0"
    }
}

```

We also recommend that you do not prefix with ROPM by adding the following code to your `package.json`:

```json
"ropm": {
    "noprefix": [
      "tealium"
    ]
  },
```

If you prefer to use prefixing and not aliasing, you can add the following line in your `package.json`: 

```
"tealium-roku-plugin": "2.0.0"
```

However, this method causes code samples in the documentation for the `brs` component to not properly match up with their references.

And finally, run the `ropm install` command.

#### Troubleshooting ROPM

* In some cases, auto path updating fails in ROPM. To resolve this issue, some manual changes need to be made in `TealiumTask.xml` 
<blockquote>
Ensure that you modify the `TealiumTask.xml` file in your project and not the one in the node module's folder.
</blockquote>


* The imports may contain an `undefined` in the path. To fix this, update `undefined` to  your alias. If you followed the installation instructions above, the alias value is `tealium`:
  ```
  <script type="text/brightscript" uri="pkg:/components/roku_modules/undefined/TealiumTask.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/undefined/createTealium.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/undefined/tealiumBuilder.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/undefined/tealiumCollect.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/undefined/tealiumCore.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/undefined/tealiumLog.brs" />
  ```

  Change this to:

  ```
  <script type="text/brightscript" uri="pkg:/components/roku_modules/tealium/TealiumTask.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/tealium/createTealium.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/tealium/tealiumBuilder.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/tealium/tealiumCollect.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/tealium/tealiumCore.brs" />
  <script type="text/brightscript" uri="pkg:/source/roku_modules/tealium/tealiumLog.brs" />
  ```

### Download repo

The second option for installing the Tealium library is to download the repo and copy all of the files in the `components` and `source` directories over to your project.

## Initialize

There are several options to using the Tealium library, but the simplest method is to initialize a builder object:

```javascript
builder = TealiumBuilder("ACCOUNT", "PROFILE", LOG_LEVEL)
builder.SetEnvironment("ENVIRONMENT")
builder.SetDatasource("DATASOURCE")
teal = builder.Build()
```

This generates a `teal` object that you can run track calls on. For more information about the `teal` object and the `TealiumBuilder` class, see [`API Reference`](https://docs.tealium.com/platforms/roku/api/).

If you are not using the supplied `TealiumTask` and `TealiumTaskInterface` code, see [`track call`](https://docs.tealium.com/platforms/roku/track/)

### Advanced control

For more advanced control, we recommend that you create and initialize your own Tealium object to be able to run anything you would like. If you are only interested in firing off tracking events, we recommend that you use the supplied `TealiumTask` and `TealiumTaskInterface`.

You can use the supplied `TealiumTask` code by adding the following line to any component:

```
  <TealiumTask id="tealiumTask"/>
```

### The brs component

You must also import the `brs` component for the interface.

```
  <script type="text/brightscript" uri="pkg:/source/roku_modules/tealium/TealiumTaskInterface.brs"/>
```


<blockquote>
If you prefixed the Tealium library instead of aliasing it, the code samples for the `brs` component will not properly match up with references in the documentation.<br><br>If you install the modules with a method other than `ROPM`, update the path in the `uri` parameter to the correct location.
</blockquote>


After you import the `brs` component, initialize your task in the `brs` code with the following code:
```javascript
task = m.top.findNode("tealiumTask")
m.tealiumTask = TealiumTask(task)
m.tealiumTask.init("tealiummobile", "demo")
```
