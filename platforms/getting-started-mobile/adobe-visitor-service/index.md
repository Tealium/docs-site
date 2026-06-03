---
title: Adobe Visitor Service Module
description: Learn about the Adobe Visitor Service Module.
url: https://docs.tealium.com/platforms/getting-started-mobile/adobe-visitor-service/
---
The Adobe Visitor Service module interfaces directly with Adobe’s REST API to retrieve and maintain the Experience Cloud ID (ECID) for visitors. The ECID identifies the same visitor in different parts of the Adobe ecosystem, such as Adobe Target and Adobe Analytics, and identifies unique visitors.

If you are migrating from the Adobe tracking SDK to the Tealium SDK, use the Adobe Visitor Service module to pass an ECID in the tracking payload. The new ECID in the data layer may be mapped in the server-side Adobe connectors in Tealium EventStream or Tealium AudienceStream. The Adobe Visitor Service module provides a seamless transition to the Tealium SDK by reusing the existing ECID if it exists and generating a new one if it doesn&#39;t, ensuring an accurate count of visitors in your app.

## Supported platforms

The following platforms support the Adobe Visitor Service module:

- [Tealium for Android](/platforms/android-kotlin/module-list/adobe-visitor-service/)
- [Tealium for iOS](/platforms/ios-swift/module-list/adobe-visitor-service/)
- [Tealium for React Native](/platforms/react-native/adobe-visitor-service/)
- [Tealium for Flutter](/platforms/flutter/adobe-visitor-service/)

## Use Cases

### Migrating to Server-Side Analytics

Migrate your Adobe integrations server-side and map the ECID to the `marketingCloudVisitorID` parameter in the connector using Adobe Analytics server-side through EventStream, and need a valid ECID for multiple Adobe products to work together. The Tealium SDK requests the ECID from Adobe before sending any calls to EventStream, and the ECID is mapped to the `marketingCloudVisitorID` property in the Adobe Analytics connector.

### Tealium iQ Tag Management

We recommend using Tealium iQ Tag Management to generate the ECID when using the Adobe Analytics tag. This guarantees the ECID is readily available, persisted in storage, and independent of the cookie store in the hidden webview.

### Migrating from Adobe SDK to Tealium SDK

Migration from the Adobe SDK to the Tealium module is seamless. If your app currently relies on the Adobe SDK to manage the ECID, we recommend having a transition period during which the Adobe SDK is present in the app alongside the Tealium SDK. If the visitor has an existing Adobe ECID, pass it to the Tealium module through the `config.adobeVisitorExistingEcid` property. If the property is set during initialization, then the existing ECID is used. If the property is not set, the Tealium module retrieves a new one from the Adobe API.

### Tracking different visitors on the same device

If you detect different visitor accounts in your app, reset the ECID to ensure each visitor is tracked separately by calling `tealium.adobeVisitor?.resetVisitor()`. This resets the current ECID and a new one is automatically requested from the Adobe API.

### Set a known visitor ID and authentication state

Use the `adobeVisitorCustomVisitorId`, `adobeVisitorDataProviderId`, and `adobeVisitorAuthState` config properties only if all three values are known at the start of the app session. Set `adobeVisitorAuthState` only when you also set `adobeVisitorCustomVisitorId`.

If the visitor&#39;s ID is not known at initialization (for example, before the user logs in), omit these properties and call `linkEcidToKnownIdentifier` once the ID becomes available.

If all values are known at initialization, set them on the `TealiumConfig` object when the module starts:




```kotlin
config.adobeVisitorDataProviderId = &#34;01&#34; // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorCustomVisitorId = &#34;customeremail@emailprovider.com&#34;
```




```swift
config.adobeVisitorDataProviderId = &#34;01&#34; // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = .authenticated
config.adobeVisitorCustomVisitorId = &#34;customeremail@emailprovider.com&#34;
```




```javascript
config.adobeVisitorDataProviderId = &#34;01&#34; // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = AuthState.authenticated
config.adobeVisitorCustomVisitorId = &#34;customeremail@emailprovider.com&#34;
```




```dart
config.adobeVisitorDataProviderId = &#34;01&#34; // Data provider ID for this type of visitor ID
config.adobeVisitorAuthState = AuthState.authenticated
config.adobeVisitorCustomVisitorId = &#34;customeremail@emailprovider.com&#34;
```




The module automatically requests a new ID if needed, and subsequently sends an additional API call to link the ECID to the known ID supplied in the `TealiumConfig` properties.

If you need to pass the ID and authentication state when the visitor logs in, call the following method to link the visitor&#39;s known ID to the anonymous ECID:




```kotlin
tealium.adobeVisitorApi?.linkEcidToKnownIdentifier(&#34;myidentifier&#34;, &#34;123456&#34;, AdobeAuthState.AUTH_STATE_AUTHENTICATED, null)
```




```swift
tealium?.adobeVisitorApi?.linkECIDToKnownIdentifier(&#34;myidentifier&#34;, adobeDataProviderId: &#34;123456&#34;, .unknown)
```




```javascript
TealiumAdobeVisitor.linkEcidToKnownIdentifier(&#34;myidentifier&#34;, &#34;123456&#34;, AuthState.unknown, value =&gt; {
                console.log(&#34;AdobeVisitor Data: &#34; &#43; JSON.stringify(value))
});
```




```dart
TealiumAdobeVisitor.linkEcidToKnownIdentifier(&#34;myidentifier&#34;, &#34;123456&#34;, AuthState.unknown)
```




## Troubleshooting

The following lists the different API failure behaviors:

* **Missing Adobe organization ID**  
If the module is enabled but an Adobe organization ID has not been passed in the `TealiumConfig` object, the module is disabled and tracking calls continue without an Adobe ECID.

* **Invalid Adobe organization ID**  
The module attempts to retry up to the retry limit (default: 5). After the retry limit has exceeded, tracking calls continue as normal without the ECID, and any queued requests are sent immediately.

* **Adobe API returns an error or an empty response**  
In the event that an error is returned while sending a request, such as connectivity failure, the module attempts to retry up to the retry limit (default: 5). After the retry limit has exceeded, tracking calls continue as normal without the ECID, and any queued requests are sent immediately.

* The module encounters either (2) or (3) above, but the visitor&#39;s previous ECID has been provided on the `TealiumConfig` object. After the maximum retries, the module uses the provided visitor ID value and does not block any requests.

If your top priority is getting data to Tealium, then set the number of retries to 0 to skip retrieving the ECID in case of failure. The number of retries is controlled by the `config.adobeVisitorRetries` property.

## Data Layer

The following variables are added to the data layer:

| Variable       | Type     | Description                                                                                                                        |
|:---------------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------|
| `adobe_ecid`   | `String` | The Adobe ECID. If the module successfully retrieve an ECID from the Adobe Visitor API, then it is present on every tracking call. |
| `adobe_error`  | `String` | A description of the type of error encountered, such as `Org ID Not Set. ECID is not included from track requests`                 |
| `queue_reason` | `String` | Event queues by the module before the visitor ID is available.                                                                     |

## URL Decoration

Adobe products loaded in a web context, such as the Adobe Analytics JavaScript tag, automatically use an Experience Cloud ID. This ID is passed in the query string of the web page when passed in the `adobe_mc` parameter. The `adobe_mc` parameter contains multiple values, separated by the pipe character (`|`).

| Component | Description                                              | Example Value  |
|-----------|----------------------------------------------------------|----------------|
| MCMID     | Experience Cloud ID retrieved from Adobe Visitor Service | 1234           |
| MCORGID   | Adobe Org ID                                             | 12345@AdobeOrg |
| TS        | Timestamp in seconds                                     | 1655826247     |

The resulting URL is:

`https://tealium.com/?adobe_mc=MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247`

The `adobe_mc` parameter is URL-encoded.

The Adobe Visitor Service module provides two methods to support this feature, which are described below.

### Tag Management Module

The `adobe_mc` parameter is automatically appended to the URL used by the Tealium webview in the Tag Management module.

### Custom Webviews

If your app uses webviews to display content, you need to make the Adobe ECID available in that webview so that all Adobe products loaded in the webview know the user&#39;s ECID. This prevents the user from appearing as two different users in the native app and in the webview.

The Adobe Visitor Service module provides a method to decorate a webview URL with a query string parameter. This causes Adobe Analytics to use the ECID generated by the module instead of using the Experience Cloud ID Service JavaScript tag. As shown in the example, you must pass the URL to the `decorateURL` method and then load the returned URL when you want to load a webview in your app.

This method preserves any query parameters already present on the URL




```kotlin
adobeVisitorModule?.decorateUrl(
            URL(url),
            object : UrlDecoratorHandler {
                override fun onDecorateUrl(url: URL) {
                  // Resulting URL = https://tealium.com/?myparam=abc&amp;myparam2=bcd&amp;adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
                  // Only for demonstration purposes; launch your app&#39;s webview with the resulting URL
                    myApp.launchWebview(url)
                }
            }
        )
```




```swift
let url = URL(string: &#34;https://tealium.com/?myparam=abc&amp;myparam2=bcd&#34;)!
tealium.adobeVisitorApi?.decorateURL(url) { url in
    // Resulting URL = https://tealium.com/?myparam=abc&amp;myparam2=bcd&amp;adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
    // Only for demonstration purposes; launch your app&#39;s webview with the resulting URL
    myApp.launchWebview(url)
}
```




```javascript
TealiumAdobeVisitor.decorateUrl(&#34;https://tealium.com&#34;, value =&gt; {
    // Resulting URL = https://tealium.com/?myparam=abc&amp;myparam2=bcd&amp;adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
    // Only for demonstration purposes; launch your app&#39;s webview with the resulting URL
    launchUrl(value);
});
```




```
// Resulting URL = https://tealium.com/?myparam=abc&amp;myparam2=bcd&amp;adobe_mc=MCMID%3D1234%7CMCORGID%3D12345%40AdobeOrg%7CTS%3D1655826247
// Only for demonstration purposes; launch your app&#39;s webview with the resulting URL
TealiumAdobeVisitor.decorateUrl(&#34;https://tealium.com&#34;).then(
                    (value) =&gt;
                        launchUrl(value));
```




If your app loads a webview with a non-standard URL scheme, such as Angular, you can retrieve the Adobe Visitor API query parameters and manually append them to your URL. Be aware that these methods return the parameter name and value without URL encoding, so you must encode the value before appending it to your URL.




```kotlin
adobeVisitorApi?.getUrlParameters(
    object : GetUrlParametersHandler {
        override fun onRetrieveParameters(params: Map&lt;String, String&gt;?) {
            params?.let {
                params.forEach {
                    Log.d(&#34;ADB Visitor&#34;,&#34;Retrieved URL Parameters:${it.key} = ${it.value}&#34;)
                }
            }
        }
    }
)
```




```swift
tealium.adobeVisitorApi.adobeVisitorApi?.getURLParameters { params in
            guard let params = params else {
                completion(nil)
                return
            }
            // Result: params.name = adobe_mc
            //         params.value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
            print(&#34;Retrieved URL Parameters:\(params.name) = \(params.value)&#34;)
}
```




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




```
TealiumAdobeVisitor.getUrlParameters().then(
                            (value) =&gt;
                            value?.forEach((key, value) {
                                // Result: key = adobe_mc
                                //         value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
                                // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
                                print(&#34;Retrieved URL Parameters: $key = $value&#34;);
                            })
                    )
```


