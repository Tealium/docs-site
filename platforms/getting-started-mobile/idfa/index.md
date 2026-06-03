---
title: Apple consent requirements
description: This article explains how to manage user consent and collect anonymous ad attribution within Apple's privacy rules.
url: https://docs.tealium.com/platforms/getting-started-mobile/idfa/
---
## How it works

When an app first launches, Apple privacy rules require that explicit consent must appear as a mandatory &#34;permission to track&#34; modal dialog on the user&#39;s device.

If a user declines consent, their IDFA is not available to the app. Not having the IDFA available makes it difficult for you to track important metrics, such as the effectiveness of ad campaigns. Also, the user will see less relevant ads.

### Terminology

This document uses the following terms:

* **IDFA**  
The IDFA is the Apple identifier for advertisers. Marketers can access the IDFA to identify a user, but they can only access it with a user&#39;s explicit consent.
* **AppTrackingTransparency**  
AppTrackingTransparency is the Apple framework that requires apps to request and receive explicit user consent before tracking their activity across other companies&#39; apps and websites. You must obtain explicit user consent through this framework when tracking users through an IDFA and linking their data with third-party sources, such as SDKs, ad networks, or data brokers like Oracle Bluekai, Lotame, and MediaMath.
* **SKAdNetwork**  
SKAdNetwork is the Apple framework for tracking installs and campaign performance at an aggregated and anonymous level. It allows advertisers to measure ad performance, even if the user has denied consent through AppTrackingTransparency or Tealium consent management.
* **Tracking**  
Apple defines tracking as:
    &gt; Tracking refers to the act of linking user or device data collected from your app with user or device data collected from other companies&#39; apps, websites, or offline properties for targeted advertising or advertising measurement purposes. Tracking also refers to sharing user or device data with data brokers.

For more information, see [Apple: App Store User privacy and data use](https://developer.apple.com/app-store/user-privacy-and-data-use/).

## Tealium and tracking

According to the Apple definition of tracking, if you are collecting data in an analytics platform that does not incorporate third-party data, then this usage does not require explicit permission. However, if your analytics platform is linked to an ad network (for example, if your Google Analytics property is linked to your Google Ads account), this usage does require explicit permission from the app user.

In the rare case that you are using the AudienceStream platform to build visitor profiles and act on this data without sending the data to another vendor, this is not considered tracking because no data brokers (DMPs) are involved and the data is not being sent anywhere outside of the Tealium platform. Tealium also does not natively provide any advertising or ad measurement capabilities.

## Tealium and visitor identification

We recommend using a known first-party identifier to identify visitors, such as a hashed email address. For more information, see .

We do not recommend using IDFA as a visitor identifier. The Tealium for iOS library does not collect the IDFA by default. Tealium offers an [optional Attribution module](/platforms/ios-swift/module-list/attribution/) that can collect the IDFA if you need it. However, if your users opt out of tracking, you will no longer have access to it.

If you are sending the IDFA to any third-party tools using connectors or tags, these integrations may stop functioning correctly if a user opts out of tracking. We recommend checking if any of the connectors or tags in your Tealium account are using the IDFA. If the vendor is using the IDFA and complies with Apple AppTrackingTransparency guidelines, contact the vendor and find out what they recommend to do when users opt out of tracking.

## AppTrackingTransparency framework

The following scenarios explain when to use the AppTrackingTransparency framework with the Tealium SDK. These are general guidelines. Consult your company&#39;s legal team to ensure your app complies with all requirements to avoid rejection during app store submission.

| Platform |  Scenario | Is Permission Required? | 
| --- | --- | --- |
| iQ Tag Management | Analytics data collected using JavaScript tags by third-party vendors. | No |
| iQ Tag Management | Analytics data collected using JavaScript tags by third-party vendors linked to an ad network for personalized ads using JavaScript tags . | Yes |
| EventStream | Forwards to analytics vendors. | No |
| EventStream  |Forwards to analytics vendors linked to an ad network for personalized ads. | Yes | 
| AudienceStream | Does not forward data to any connectors. | No |
| AudienceStream | Forwards to third-party vendors for fraud detection and prevention on your behalf. | No |
| AudienceStream | Forwards to third-party vendors for first-party context only (for example, for on-site personalization on your website or apps). | No |
| AudienceStream | Forwarding to third-party vendors for other purposes. | Yes |

## Privacy legislation

The AppTrackingTransparency framework works alongside existing privacy requirements, but using this framework alone does not guarantee compliance with local privacy laws, such as GDPR and CCPA. [client-side consent management]() is available for both iOS and Android to manage your app users&#39; consent settings at a granular level. It also supports GDPR and CCPA, and it is extensible to accommodate future privacy laws.

Depending on the requirements of the active consent policy, Tealium consent management allows your users to opt in and opt out of all tracking, or a customizable category-based opt out.

## Anonymous tracking with SKAdNetwork

The SKAdNetwork framework lets you measure the effectiveness of individual campaigns by validating app installs anonymously through a postback from the App Store to the ad network. The only data the ad network receives is confirmation that the app was successfully installed, along with the campaign ID and, optionally, conversion value.

### Attribution timing

When your app is first launched, it calls the `SKAdNetwork` framework to send an attribution postback to the ad network. Rather than sending immediately, this API starts a 24 hour timer. If no conversion events have been registered after 24 hours, the postback will fire within the next 24 hours. This means that you may wait up to 48 hours to see the results.

### Conversion value

Conversion value lets you assign a value to the app install, which shows that a particular campaign has been more valuable than another. This value can be measured in dollars, pounds, number of levels completed in a game, or another relevant metric. For example, if your ad appears in an app selling luxury watches, you might find that it generates more revenue per user than if it appeared in a social media app, even if the social media app generated more installs overall.

When your app reports a conversion event, it calls the `SKAdNetwork` with an integer value representing the conversion value. You must declare the unit of measurement with this value. Each time the conversion integer updates with a new value, it overwrites the previous value and starts a new rolling 24 hour timer.

When the last timer expires, the conversion event will be reported any time between zero and 24 hours later If the user uses your app multiple times and increases the conversion value, it could be several days before the conversion finally gets attributed. This additional delay is random every time, so the only guarantee you have is that it will be within 24 hours. Note that the time taken to report back to the ad network will increase, so it may take longer to see how successful your campaign has been.

For more information about Tealium and `SKAdNetwork` attribution, see [Tealium for iOS: Attribution module](/platforms/ios-swift/module-list/attribution/).