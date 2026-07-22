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

Implement the `TealiumVisitorServiceDelegate` as outlined in the [VisitorSevice Module](https://docs.tealium.com/platforms/ios-swift/module-list/visitor-service/) developer documentation.

```swift
**func** **profileDidUpdate**(profile: TealiumVisitorProfile?) {
        **guard let** profile = profile **else { return }**

        // Return the current Audiences for which the user is assigned
       **if let** currentVisitorAudiences = profile.audiences {
            print("Visitor audiences: \(currentVisitorAudiences)")

            // Check if an Audience is assigned to a user by id
            **if** currentVisitorAudiences[id: "106"] {
                print("Visitor is a member of audience id 106")
                // ... Visitor is a member of this audience, take appropriate action
            }

            // Check if an Audience is assigned to a user by name
            **if** currentVisitorAudiences[name: "ios users"] {
                print("Visitor is a member of audience iOS Users")
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
    * ``` id: "tealiummobile\_demo\_103", name: "iOS Users" ``` 
* **badges**
    * id: String, value: Bool 
    * ``` id: "2815", value: true ``` 

Using this information, you will create a single variable that contains the contents of these two profile attributes, in addition to any other attributes being passed to Optimizely. Once created, you can pass this attribute as a parameter with `activate`, `isFeatureEnabled`, or `getEnabledFeatures`.

#### Merge audiences and badges into a single attributes variable

Use the following example to merge audience and badges into a single attributes variable:

```swift
/*
Merged profiles.audience and profiles.badges into attributes array using array append or + notation.
NOTE: Ensure you include any existing attributes you may already be passing.
*/

let attributes = profile.audiences + profile.badges

```

#### Example: getEnabledFeatures

```swift
let enabledFeatures = optimizely.getEnabledFeatures(userId: "user_123",
  attributes: attributes)
```

#### Example: Activate

```swift
do {
	let variation = try optimizelyClient.activate("app_redesign", userId:userId, attributes: attributes )
  if (variation.variationKey == "control") {
    // Execute code for variation A
  } else if (variation.variationKey == "treatment") {
    // Execute code for variation B
  }
} catch {
  // Execute code for users who don't qualify for the experiment
}

```

### Android

A new Android SDK that will includes the VisitorService included is currently in Development.

#### Tealium Data Layer Enrichment Public API

To retrieve the Tealium profile for the current user for languages where the SDK does not implement a VisitorService, see the [Data Layer Enrichment Public API](https://docs.tealium.com/data-layer-enrichment-api/).


<blockquote>
When using the Data Layer Enrichment API with your server-side code, consider keeping the user profile stored on your local servers and have update requests occur in the background, (~100 milliseconds or less).
</blockquote>


Contact your Optimizely representative to ensure that your implementation is a good fit for your use case.

The Data Layer Enrichment API returns the visitor profile JSON, similar to the following example:

```json
{
     "metrics" : {
            "5117" : 6.0,
            "22" : 6.0
     },
     "dates" : {
            "5111" : 1420223771043
     },
     "properties" : {
            "17" : "http://tags.tiqcdn.com/utag/acct/prof/env/mobile.html",
            "account" : "tealiummobile",
            "5123" : "set",
            "profile" : "demo"
      },
      "flags" : { "5115" : true },
      "current_visit"  {
          "metrics" : {
              "7" : 6.0
           },
           "dates" : {
               "5202" : 1420225387000
           },
           "properties" : {
               "48" : "Chrome",
               "45" : "Mac OS X",
               "44" : "Chrome",
               "47" : "browser",
               "46" : "Mac desktop"
           },
          "flags" : { }
        },
       "badges" : { "5113" : true },
       "audiences" : {
            "tealiummobile_demo_101" : "Sample Audience"
       }
}
```

#### Set up attributes in Optimizely

To target a Feature Flag/Feature Experiment or Experiment to a Tealium audience or badge, create one "attribute" for each Tealium audience and each Tealium badge within the Optimizely Full Stack interface.

![](https://docs.tealium.com/images/tech-partners/optimizely-set-up-attributes.jpg)

The attributes you create should match the key elements of the JSON object. Create these attributes for the regular and consistent audiences that you want to target. For example, in the sample JSON in the previous, you would create the following attributes in Optimizely:

* Audiences: `tealium_mobile_demo_101`
* Badges: `5113`


<blockquote>
There is a 100 attribute limit for attributes per project. Only create attributes for the Tealium audiences and badges you intend to use.
</blockquote>


#### Edit attributes

Attributes are characteristics of your users that you pass in when calling Optimzely APIs that can then be used to create audiences. Click on an attribute to edit the Attribute Key or the optional Attribute Description fields and then click **Save Attribute** to save your changes.

#### Set up an Optimizely audience

After you have created the attributes within the Optimizely Full Stack interface, use the following steps to create an audience:

1. Click the **Audience** tab.
1. Click **Create New Audience**.
1. Enter a Name and Description for the audience.
1. Under Custom Attributes, select any of the Tealium attributes you created in the previous steps.  
    ![](https://docs.tealium.com/images/tech-partners/optimizely-create-new-audience.jpg)
1. Once you have configured the audience to your needs, click **Save**.

#### Pass Tealium audiences and badges to Optimizely

Within your code, parse the JSON object so that you can create an attribute parameter using the audience and badges sections that you can then pass to Optimizely, as shown in the following example.


<blockquote>
If you are already passing attributes through Optimizely, ensure that you include those elements in the attribution parameter.
</blockquote>


```js
/* Function to merge array objects */

function extend(dest, src) {
  for(var key in src) {
    dest[key] = src[key];
  }
  return dest;
}

var request = new XMLHttpRequest()
request.open('GET','https://visitor-service.tealiumiq.com/{account}/{profile}/{visitor_id}', true)

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
  "5113": 'true',
  "tealiummobile_101": "Sample Audience"
};
```

The attribute variable can now be passed to Optimizely using the getFeatureEnabled and activate function, as shown in the following example:

```js
var enabled = optimizelyClientInstance.isFeatureEnabled('mens_preview_widget', userId, attributes);
```
