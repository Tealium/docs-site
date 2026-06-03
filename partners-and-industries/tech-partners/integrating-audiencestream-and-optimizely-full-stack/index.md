---
title: Integrating AudienceStream and Optimizely Full Stack
description: This article describes best practices used to integrate Tealium AudienceStream and Optimizely Full Stack.
url: https://docs.tealium.com/partners-and-industries/tech-partners/integrating-audiencestream-and-optimizely-full-stack/
---## Prerequisites

* The Visitor ID for the visitor profile in Tealium
* The User ID for the Optimizely feature or experiment

## How it works

Leveraging Tealium AudienceStream audiences and badges within Optimizely Full Stack lets you target specific features or experiments to a subset of your users.


## Limitations and considerations

* Calling the Data Layer enrichment API adds network latency and should be done outside of the critical path using a profile cached locally within your environment.
* Optimizely Full Stack projects have a 100 attribute limit.

## Tealium SDK: VisitorService

The VisitorService within the Tealium Software Development Kit (SDK) is a wrapper for the Data Layer Enrichment API that can be used to manage the complexity of updating and caching Data Layer Enrichment calls on your behalf.

The following Tealium SDKs have a built-in Data Layer Enrichment profile:

### Swift for iOS

Implement the `TealiumVisitorServiceDelegate` as outlined in the [VisitorSevice Module](/platforms/ios-swift/module-list/visitor-service/) developer documentation.

```swift
**func** **profileDidUpdate**(profile: TealiumVisitorProfile?) {
        **guard let** profile = profile **else { return }**

        // Return the current Audiences for which the user is assigned
       **if let** currentVisitorAudiences = profile.audiences {
            print(&#34;Visitor audiences: \(currentVisitorAudiences)&#34;)

            // Check if an Audience is assigned to a user by id
            **if** currentVisitorAudiences[id: &#34;106&#34;] {
                print(&#34;Visitor is a member of audience id 106&#34;)
                // ... Visitor is a member of this audience, take appropriate action
            }

            // Check if an Audience is assigned to a user by name
            **if** currentVisitorAudiences[name: &#34;ios users&#34;] {
                print(&#34;Visitor is a member of audience iOS Users&#34;)
                // ... Visitor is a member of this audience, take appropriate action
            }
        }
}
```

#### Retrieve most recent visitor profile

Use `getCachedProfile` to retrieve the most recent visitor profile, as shown in the following example:

```swift
**self**.tealium?.visitorService()?.getCachedProfile(completion: {
prfile **in**
  **guard let** profile = profile **else** { **return** }
})
```

From the profile, you will need the following attribute information from `audiences` and `badges`:

* **audiences**
    * id: String, name: String 
    * ``` id: &#34;tealiummobile\_demo\_103&#34;, name: &#34;iOS Users&#34; ``` 
* **badges**
    * id: String, value: Bool 
    * ``` id: &#34;2815&#34;, value: true ``` 

Using this information, you will create a single variable that contains the contents of these two profile attributes, in addition to any other attributes being passed to Optimizely. Once created, you can pass this attribute as a parameter with `activate`, `isFeatureEnabled`, or `getEnabledFeatures`.

#### Merge audiences and badges into a single attributes variable

Use the following example to merge audience and badges into a single attributes variable:

```swift
/*
Merged profiles.audience and profiles.badges into attributes array using array append or &#43; notation.
NOTE: Ensure you include any existing attributes you may already be passing.
*/

let attributes = profile.audiences &#43; profile.badges

```

#### Example: getEnabledFeatures

```swift
let enabledFeatures = optimizely.getEnabledFeatures(userId: &#34;user_123&#34;,
  attributes: attributes)
```

#### Example: Activate

```swift
do {
	let variation = try optimizelyClient.activate(&#34;app_redesign&#34;, userId:userId, attributes: attributes )
  if (variation.variationKey == &#34;control&#34;) {
    // Execute code for variation A
  } else if (variation.variationKey == &#34;treatment&#34;) {
    // Execute code for variation B
  }
} catch {
  // Execute code for users who don&#39;t qualify for the experiment
}

```

### Android

A new Android SDK that will includes the VisitorService included is currently in Development.

#### Tealium Data Layer Enrichment Public API

To retrieve the Tealium profile for the current user for languages where the SDK does not implement a VisitorService, see the [Data Layer Enrichment Public API]().

When using the Data Layer Enrichment API with your server-side code, consider keeping the user profile stored on your local servers and have update requests occur in the background, (~100 milliseconds or less).

Contact your Optimizely representative to ensure that your implementation is a good fit for your use case.

The Data Layer Enrichment API returns the visitor profile JSON, similar to the following example:

```json
{
     &#34;metrics&#34; : {
            &#34;5117&#34; : 6.0,
            &#34;22&#34; : 6.0
     },
     &#34;dates&#34; : {
            &#34;5111&#34; : 1420223771043
     },
     &#34;properties&#34; : {
            &#34;17&#34; : &#34;http://tags.tiqcdn.com/utag/acct/prof/env/mobile.html&#34;,
            &#34;account&#34; : &#34;tealiummobile&#34;,
            &#34;5123&#34; : &#34;set&#34;,
            &#34;profile&#34; : &#34;demo&#34;
      },
      &#34;flags&#34; : { &#34;5115&#34; : true },
      &#34;current_visit&#34;  {
          &#34;metrics&#34; : {
              &#34;7&#34; : 6.0
           },
           &#34;dates&#34; : {
               &#34;5202&#34; : 1420225387000
           },
           &#34;properties&#34; : {
               &#34;48&#34; : &#34;Chrome&#34;,
               &#34;45&#34; : &#34;Mac OS X&#34;,
               &#34;44&#34; : &#34;Chrome&#34;,
               &#34;47&#34; : &#34;browser&#34;,
               &#34;46&#34; : &#34;Mac desktop&#34;
           },
          &#34;flags&#34; : { }
        },
       &#34;badges&#34; : { &#34;5113&#34; : true },
       &#34;audiences&#34; : {
            &#34;tealiummobile_demo_101&#34; : &#34;Sample Audience&#34;
       }
}
```

#### Set up attributes in Optimizely

To target a Feature Flag/Feature Experiment or Experiment to a Tealium audience or badge, create one &#34;attribute&#34; for each Tealium audience and each Tealium badge within the Optimizely Full Stack interface.

![](/images/tech-partners/optimizely-set-up-attributes.jpg)

The attributes you create should match the key elements of the JSON object. Create these attributes for the regular and consistent audiences that you want to target. For example, in the sample JSON in the previous, you would create the following attributes in Optimizely:

* Audiences: `tealium_mobile_demo_101`
* Badges: `5113`

There is a 100 attribute limit for attributes per project. Only create attributes for the Tealium audiences and badges you intend to use.

#### Edit attributes

Attributes are characteristics of your users that you pass in when calling Optimzely APIs that can then be used to create audiences. Click on an attribute to edit the Attribute Key or the optional Attribute Description fields and then click **Save Attribute** to save your changes.

#### Set up an Optimizely audience

After you have created the attributes within the Optimizely Full Stack interface, use the following steps to create an audience:

1. Click the **Audience** tab.
1. Click **Create New Audience**.
1. Enter a Name and Description for the audience.
1. Under Custom Attributes, select any of the Tealium attributes you created in the previous steps.  
    ![](/images/tech-partners/optimizely-create-new-audience.jpg)
1. Once you have configured the audience to your needs, click **Save**.

#### Pass Tealium audiences and badges to Optimizely

Within your code, parse the JSON object so that you can create an attribute parameter using the audience and badges sections that you can then pass to Optimizely, as shown in the following example.

If you are already passing attributes through Optimizely, ensure that you include those elements in the attribution parameter.

```js
/* Function to merge array objects */

function extend(dest, src) {
  for(var key in src) {
    dest[key] = src[key];
  }
  return dest;
}

var request = new XMLHttpRequest()
request.open(&#39;GET&#39;,&#39;https://visitor-service.tealiumiq.com/{account}/{profile}/{visitor_id}&#39;, true)

request.onload = function() {
var tealium_audiences = JSON.parse(this.response);
var attributes = tealium_audiences.audiences
attributes = extend(attributes, tealium_audiences.badges);
}

// Send request
request.send()

```

The results of the above example are similar to the following:

```js
var attributes = {
  &#34;5113&#34;: &#39;true&#39;,
  &#34;tealiummobile_101&#34;: &#34;Sample Audience&#34;
};
```

The attribute variable can now be passed to Optimizely using the getFeatureEnabled and activate function, as shown in the following example:

```js
var enabled = optimizelyClientInstance.isFeatureEnabled(&#39;mens_preview_widget&#39;, userId, attributes);
```
