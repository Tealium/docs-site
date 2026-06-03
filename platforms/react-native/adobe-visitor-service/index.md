---
title: Adobe Visitor Service Module
description: Learn to install Tealium Adobe Visitor Service Module for React Native.
url: https://docs.tealium.com/platforms/react-native/adobe-visitor-service/
---
Tealium for React Native lets you use the Tealium mobile libraries (iOS, Android) in your React Native application.

## How It Works

Tealium mobile libraries are integrated into your React Native application using one of the following two methods:

*   NPM package (Recommended)
*   Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

## Requirements

* Access to your native build environments
* [Tealium for React Native 2.2.0&#43;](/platforms/react-native/)
* [React Native 0.63&#43;](https://github.com/Tealium/tealium-react-native) and tools installed 
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/platforms/android-kotlin/) or [Tealium for iOS](/platforms/ios-swift/)


## Install (NPM/YARN)

To install the Tealium Adobe Visitor module for React Native with NPM:

1. Follow the installation instructions for the main `tealium-react-native` library installation [here](/platforms/react-native/install/). Ensure you have installed at least version 2.2.0 or above.

2. Navigate to the root of your React Native project.

3. Download and install the `tealium-react-native-adobe-visitor` package with the following command:  
    ```bash
    yarn install tealium-react-native-adobe-visitor
    ```


## JavaScript

To import the relevant classes into your app, do the following:

```javascript
import TealiumAdobeVisitor from &#39;tealium-react-native-adobe-visitor&#39;;
import { TealiumAdobeVisitorConfig } from &#39;tealium-react-native-adobe-visitor/common&#39;;
```

## Initialize

Configure the Adobe Visitor module prior to initializing the main Tealium React Native integration.

```javascript
let adobeVisitorConfig: TealiumAdobeVisitorConfig = {
    adobeVisitorOrgId: &#34;ADOBE-ORG-ID&#34;,
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: &#34;&#34;,  // optional
}

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

Set the `adobeVisitorCustomVisitorId`, `adobeVisitorDataProviderId`, and `adobeVisitorAuthState` properties only if all three values are known at the start of the app session. Set `adobeVisitorAuthState` only when you also set `adobeVisitorCustomVisitorId`. If the visitor&#39;s ID is not known at initialization (for example, before login), omit these properties and call [`linkEcidToKnownIdentifier`](#linkecidtoknownidentifierid-providerid-authstate-callback) once the ID becomes available.

```javascript
let adobeVisitorConfig: TealiumAdobeVisitorConfig = {
    adobeVisitorOrgId: &#34;ADOBE-ORG-ID&#34;,
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: &#34;&#34;,
    adobeVisitorDataProviderId: &#34;DATA-PROVIDER-ID&#34;,
    adobeVisitorCustomVisitorId: &#34;CUSTOM-VISITOR-ID&#34;,
    adobeVisitorAuthState: AuthState.authenticated
}

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

## API Reference

After the Adobe Visitor Module and the main Tealium React Native integration have both been initialized, you can link an existing Adobe visitor.

### `linkEcidToKnownIdentifier(id, providerId, authState, callback)`

Links existing ECID to known Identifier.

```javascript
TealiumAdobeVisitor.linkEcidToKnownIdentifier(id, providerId, authState, value =&gt; {
    console.log(&#34;AdobeVisitor Data: &#34; &#43; JSON.stringify(value))
});
```

### `getAdobeVisitor(callback)`

Get the current Adobe visitor information

```javascript
TealiumAdobeVisitor.getAdobeVisitor(value =&gt; {
    console.log(&#34;Current Adobe Visitor: &#34; &#43; JSON.stringify(value))
});
```

### `decorateUrl(url, callback)`

Decorates the URL with ECID visitor data.

```javascript
TealiumAdobeVisitor.decorateUrl((&#34;https://tealium.com&#34;, value =&gt; {
    console.log(&#34;Decorated URL: &#34; &#43; value);
});
```

### `getUrlParameters(callback)`

Retrieves the Adobe Visitor URL parameters to be appended to a URL.

```javascript
TealiumAdobeVisitor.getUrlParameters(value =&gt; {
    if (value === null || value === undefined) {
        console.log(&#34;Adobe Visitor was null&#34;);
        return;
    } else {
        for (var key of Object.keys(value)) {
            // Result: key = adobe_mc
            //         value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
            console.log(&#34;Retrieved URL Parameters: &#34;, key &#43; &#34;=&#34; &#43; value[key]);
            break;
        }
    }
});
```

### `resetVisitor()`

Reset current visitor.

```javascript
TealiumAdobeVisitor.resetVisitor();
```