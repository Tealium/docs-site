---
title: Install
description: Learn to install Tealium for Roku.
url: https://docs.tealium.com/platforms/roku/install/
---
This guide shows how to add Tealium to your Roku app to track user activity.

## Requirements

* [Tealium Customer Data Hub account]()
* [Roku SDK](https://sdkdocs.roku.com/display/sdkdoc/Release&#43;Notes) 7.2&#43;
* Active [Roku developer account](https://developer.roku.com/developer)
* Roku Device

We recommend that you develop in [Visual Studio Code with the Brightscript Plugin](https://github.com/rokucommunity/vscode-brightscript-language).

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
    &#34;dependencies&#34;: {
        &#34;tealium&#34;: &#34;npm:tealium-roku-plugin@2.0.0&#34;
    }
}

```

We also recommend that you do not prefix with ROPM by adding the following code to your `package.json`:

```json
&#34;ropm&#34;: {
    &#34;noprefix&#34;: [
      &#34;tealium&#34;
    ]
  },
```

If you prefer to use prefixing and not aliasing, you can add the following line in your `package.json`: 

```
&#34;tealium-roku-plugin&#34;: &#34;2.0.0&#34;
```

However, this method causes code samples in the documentation for the `brs` component to not properly match up with their references.

And finally, run the `ropm install` command.

#### Troubleshooting ROPM

* In some cases, auto path updating fails in ROPM. To resolve this issue, some manual changes need to be made in `TealiumTask.xml` Ensure that you modify the `TealiumTask.xml` file in your project and not the one in the node module&#39;s folder.

* The imports may contain an `undefined` in the path. To fix this, update `undefined` to  your alias. If you followed the installation instructions above, the alias value is `tealium`:
  ```
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/components/roku_modules/undefined/TealiumTask.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/undefined/createTealium.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/undefined/tealiumBuilder.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/undefined/tealiumCollect.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/undefined/tealiumCore.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/undefined/tealiumLog.brs&#34; /&gt;
  ```

  Change this to:

  ```
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/components/roku_modules/tealium/TealiumTask.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/tealium/createTealium.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/tealium/tealiumBuilder.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/tealium/tealiumCollect.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/tealium/tealiumCore.brs&#34; /&gt;
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/tealium/tealiumLog.brs&#34; /&gt;
  ```

### Download repo

The second option for installing the Tealium library is to download the repo and copy all of the files in the `components` and `source` directories over to your project.

## Initialize

There are several options to using the Tealium library, but the simplest method is to initialize a builder object:

```javascript
builder = TealiumBuilder(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, LOG_LEVEL)
builder.SetEnvironment(&#34;ENVIRONMENT&#34;)
builder.SetDatasource(&#34;DATASOURCE&#34;)
teal = builder.Build()
```

This generates a `teal` object that you can run track calls on. For more information about the `teal` object and the `TealiumBuilder` class, see [`API Reference`](/platforms/roku/api/).

If you are not using the supplied `TealiumTask` and `TealiumTaskInterface` code, see [`track call`](/platforms/roku/track/)

### Advanced control

For more advanced control, we recommend that you create and initialize your own Tealium object to be able to run anything you would like. If you are only interested in firing off tracking events, we recommend that you use the supplied `TealiumTask` and `TealiumTaskInterface`.

You can use the supplied `TealiumTask` code by adding the following line to any component:

```
  &lt;TealiumTask id=&#34;tealiumTask&#34;/&gt;
```

### The brs component

You must also import the `brs` component for the interface.

```
  &lt;script type=&#34;text/brightscript&#34; uri=&#34;pkg:/source/roku_modules/tealium/TealiumTaskInterface.brs&#34;/&gt;
```

If you prefixed the Tealium library instead of aliasing it, the code samples for the `brs` component will not properly match up with references in the documentation.&lt;br&gt;&lt;br&gt;If you install the modules with a method other than `ROPM`, update the path in the `uri` parameter to the correct location.

After you import the `brs` component, initialize your task in the `brs` code with the following code:
```javascript
task = m.top.findNode(&#34;tealiumTask&#34;)
m.tealiumTask = TealiumTask(task)
m.tealiumTask.init(&#34;tealiummobile&#34;, &#34;demo&#34;)
```
