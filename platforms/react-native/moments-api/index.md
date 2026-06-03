---
title: Moments API Module
description: Learn how to install the Tealium Moments API module for React Native.
url: https://docs.tealium.com/platforms/react-native/moments-api/
---
## How it works

Tealium mobile libraries are integrated into your React Native application using one of the following methods:

* NPM package (Recommended)
* Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

After you install the Moments API module, import the necessary classes into your app and initialize the Moments API module.

## Requirements

The Tealium Moments API module requires the following:

* Access to your native build environments
* [Tealium for React Native 2.2.0 or later](/platforms/react-native/)
* [React Native 0.63 or later](https://github.com/Tealium/tealium-react-native) and tools 
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/platforms/android-kotlin/) or [Tealium for iOS](/platforms/ios-swift/)

## Install (NPM/YARN)

To install the Tealium Moments API module for React Native with NPM:

1. Follow the [installation instructions](/platforms/react-native/install/) for the main `tealium-react-native` library installation. Ensure that you have installed at least version 2.2.0 or later.
1. Go to the root directory of your React Native project.
1. Download and install the `tealium-react-native-moments-api` package with the following command:  
    ```bash
    yarn install tealium-react-native-moments-api
    ```

## JavaScript

To import the relevant classes into your app, add the following code:

```javascript
import TealiumMomentsApi from &#39;tealium-react-native-moments-api&#39;;
import { TealiumMomentsApiConfig, MomentsApiRegion} from &#39;tealium-react-native-moments-api/common&#39;;
```

## Initialize

Configure the `Moments API` module prior to initializing the main Tealium React Native integration. Use `TealiumMomentsApiConfig` parameters to enable settings as needed. 

```javascript
let momentsApiConfig: TealiumMomentsApiConfig = {
    region: MomentsApiRegion.UsEast,   // Setting a region is mandatory. The Moments API module will not initialize if it is missing.
    referrer: &#34;https://tealium.com&#34;    // Optional - specify a referrer URL. This URL must match the “Domain Allow List” in the Tealium UI, or the Moments API will not return any data.
}

TealiumMomentsApi.configure(momentsApiConfig);
```

## API Reference

After the Moments API Module and the main Tealium React Native integration have both been initialized, you can retrieve engine data by ID.

### `fetchEngineResponse(engineId, callback)`

Retrieves the engine response for the given engine ID. 

```javascript
TealiumMomentsApi.fetchEngineResponse(
    id,
    value =&gt; {
        console.log(&#34;Engine Response data: &#34; &#43; JSON.stringify(value))
    }
);
```
