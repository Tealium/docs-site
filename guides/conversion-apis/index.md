---
title: Conversion APIs
description: This guide describes what conversion APIs are and best practices for configuring a conversion API (CAPI) at Tealium.
url: https://docs.tealium.com/guides/conversion-apis/
---
## About



Conversion APIs let you ensure the accuracy, reliability, and security of conversion tracking data by combining client-side and server-side signals.

They send conversion event data to an ad platform that uses the data to improve advertising performance and return on ad spend (ROAS). Tealium provides conversion APIs from a variety of vendors, including Meta (Facebook), Google, Amazon, Snap, Pinterest, LinkedIn, and Microsoft.

Conversion APIs can receive event data from any point in the customer journey, including websites, mobile apps, and offline data from physical stores, and send data directly from servers instead of relying on web browsers.

## How it works

A conversion event occurs when a customer completes an action that provides first-party data about the customer, such as making a purchase, signing in, registering on your site, or completing an application.

Tealium securely sends the first-party data to your ad platform. The ad platform uses a combination of the client-side tags and server-side conversion API connectors. The ad platform matches the data with user interactions with ads on the platform to:

* Power ad platform AI and machine learning models with high-quality signals for bidding, optimization, and creative delivery.
* Optimize targeting and delivery of ads, improving your ROAS.
* Create conversion reports showcasing the performance of your ads.
* Improve audience building and suppression to retarget high-intent customers and reduce wasted spend.

### Hybrid solution

At Tealium, our conversion API solutions typically support a tag and connector with deduplication. We recommend a hybrid approach, where client-side tags and server-side conversion API connectors run together to:

* Capture conversions even when tags are blocked or degraded by browser settings.
* Validate and deduplicate events across tag and conversion API so platforms receive high-quality conversion signals.
* Build a more complete view of the customer journey by incorporating online and offline conversions.
* Provide richer, more consistent training data for ad platform AI and optimization algorithms.


<blockquote>
We recommend using a hybrid approach for 90 days. After the initial 90-day period, advertisers should work with their advertising partners to assess resiliency status, event match quality scores, and overall signal health. If the data shows strong reliability and accuracy, advertisers can then confidently proceed with dropping the client-side tag signal.
</blockquote>


## Client-side tags and deduplication

When a vendor supports both a client-side tag and server-side conversion API, Tealium recommends implementing both to capture as many conversion events as possible, including signals missed when third-party tags are blocked or degraded by the browser.

Sending the same conversion using the tag and conversion can result in duplicate events being sent to the ad platform. To prevent this, many conversion API implementations support deduplication, a mechanism that uses a shared event identifier to recognize when two signals represent the same conversion and count it once.

In a typical hybrid setup:

1. The tag fires on the browser, sending a client-side conversion event. In iQ Tag Management, this often uses the Generate Event ID flag in the tag configuration to create a unique identifier per event according to the ad vendor's specifications.
1. The conversion API connector sends a corresponding event with the same event identifier. Using Automatic Deduplication, or mapping the identifier, ensures the unique identifier is sent on the event.
1. The ad platform uses the shared event identifier to deduplicate and keep a single, high-quality conversion record.

The hybrid pattern improves resilience to signal loss while maintaining clean, accurate reporting. Tealium Connector Insights can then be used to monitor delivery, diagnose errors, and validate deduplication is working as expected across supported vendors.


<blockquote>
Misconfigured or missing event IDs can result in duplicate conversions being counted by the ad platform. Ensure event IDs match between client-side tags and server-side conversion API connectors.
</blockquote>


 ![](https://docs.tealium.com/images/guides/capi-data-flow.png)

## Personally identifiable information (PII)

Each advertising platform ranks customer identifiers slightly differently, but they share the same core principle: the stronger and more stable the identifier, the better the match and measurement quality. The following generalized ranking reflects common patterns across major conversion API partners:

#### Strongest

* **Email address** - Usually hashed, normalized
* **Phone number** - E.164 format, usually hashed
* **Platform or account IDs** - Login IDs, subscription IDs, stable user IDs issued by the ad platform or your system
* **Stable first-party customer IDs** - CRM or loyalty ID, often mapped as an external ID

#### Medium

* **Browser and click identifiers** - Platform click IDs, browser IDs, or similar cookies
* **Client IP address**
* **Client user agent**
* **Device identifiers**
* **Hashed name and address components** - First name, last name, street address, postcode, city, state, country

#### Lower

* **Unstructured name fields** - Full name only
* **Demographic attributes** - Gender, age range, broad location without other identifiers
* **Loose behavioral or session-only identifiers** - Not stable across visits

Stronger combinations of identifiers improve platform-level signal health metrics, such as Event Match Quality scores, which directly affect how well ad platforms can attribute conversions and optimize with AI. Combinations of signals matter more than a single field. A hashed email plus phone and a stable external ID will almost always outperform a single IP or name field.

For details on exactly which identifiers are supported and how they are ranked, refer to each vendor's conversion API documentation.

## Configuration best practices

Complete the following steps to ensure your conversion API setup is configured correctly:

1. Ensure the Tealium Collect tag has been configured and loaded last in the [load order]() after the conversion tag.
1. In the data layer, define the necessary PII data (advertising platforms use PII for matching).
1. If the conversion API vendor also provides a tag, we recommend using both. Configure the tag, and use advanced matching when it's available. We recommend loading the tag on all pages. After you have configured the tag, configure the conversion API connector.
1. Configure a data source for the conversion API connector, if it doesn't already exist.
1. Ensure the necessary event IDs are defined and the IDs are the same on the client-side (tag) and server-side (conversion API). The event IDs must be the same for deduplication to work. We recommend using the Generate Event ID flag in the client-side tag and the Automatic Deduplication feature of the server-side connector.
1. Ensure the triggers for client-side conversion events are correct. Trigger the event only after all the required data has been entered. Advertising reports and ROAS reports on the ad platform may be inaccurate if data is missing. We recommend setting up the server-side event feed based on the event ID generated on the client side, or match the client-side tag load rule exactly in the event feed conditions.

## Connector Insights

Tealium Connector Insights provide visibility into how your conversion API integrations are performing. For supported vendors, Insights surfaces key metrics such as event delivery counts, error rates, match quality indicators, and deduplication status.

We recommend using Connector Insights to:

* Verify that tag and conversion API events are being delivered and deduplicated as expected.
* Monitor signal health and match quality over time.
* Troubleshoot configuration issues before they impact ROAS or reporting.


<blockquote>
Check Connector Insights regularly after initial setup to monitor signal health and catch configuration issues early.
</blockquote>


![](https://docs.tealium.com/images/server-side-connectors/connector-insights-btn.png)

![](https://docs.tealium.com/images/server-side-connectors/facebook-api-insights-events.png)

## Supported CAPI vendors

For detailed examples of configuring conversion APIs, see the following:

* [Tealium + Google Enhanced Conversions Integration Guide]()
* [Google SA360 Enhanced Conversions Implementation Guide]()
* [Facebook Conversions Connector]()
* [LinkedIn Conversions Connector]()
* [Amazon Ads Conversions Connector]()
* [X Conversions Connector]()
* [Snapchat Conversions Connector]()
* [Reddit Conversions Connector]()
* [Microsoft UET Conversion API Connector]()

## Use cases

![](https://docs.tealium.com/images/icons/icon-globe.svg) **Web conversion attribution**



1. A shopper clicks on an ad promoting a seasonal sale and completes a purchase through the web checkout.
1. The advertising tag and conversion API are implemented in Tealium, so the purchase is captured client-side and confirmed server-side. This dual-delivery approach ensures high-fidelity tracking, even with partial cookie loss or ad blockers.
1. The ads attribute the sale back to the original click, enabling the advertiser to optimize budget allocation, measure campaign performance with greater accuracy, and build high-value audience segments for remarketing.


1. A potential customer clicks on an ad for a personal loan and fills out a pre-qualification form.
1. The advertising tag captures the form completion event, and the conversion API sends the form data server-side, ensuring the conversion is reliably recorded even if the client-side tag fails due to browser restrictions.
1. Advertising vendors can then credit the ad with generating the lead and use the data to improve bidding efficiency and better target users with similar intent.


1. A traveler clicks an ad for vacation packages, browses destinations, and completes a booking through a multi-step web checkout.
1. The tag tracks each step, and a server-side event is sent through the conversion API after the booking is finalized. Tracking each step improves attribution accuracy, especially in long-form checkouts where drop-off can interrupt tag delivery.
1. The conversion is tied back to the original click, helping the travel brand maximize ROAs and fine-tune campaign messaging by analyzing which offers are most likely to convert online.




![](https://docs.tealium.com/images/icons/icon-cash-register.svg) **Offline conversion attribution**



1. A shopper clicks on an ad, browses the website, but makes the purchase in-store later that week.
1. At checkout, their email or loyalty number is collected and linked to the original ad engagement.
1. After the transaction is recorded in the point-of-sale system, the offline conversion data is imported into Tealium and sent to the advertising platform using the conversion API.


1. A customer clicks on an ad for a mortgage refinance offer and browses loan options but does not complete a form online.
1. They call the contact center, where an agent collects their phone number or email address and completes the application.
1. Once the call center logs the conversion, it is imported into Tealium and sent to the advertising platform using the conversion API.
1. The advertising vendor is then able to attribute the refinance application back to the original ad engagement, enabling more accurate campaign performance reporting and smarter bid optimization strategies. This server-side delivery ensures that valuable offline leads and high-intent conversions are not lost due to gaps in client-side tracking or delayed digital behavior.


1. A traveler clicks on an ad for a vacation package, browses options online, then calls a travel agent to book. During the call, they provide their name, phone number, and email address.
1. This information is captured in the booking system, imported into Tealium, and a server-side conversion event is sent to the advertising platform through the conversion API.
1. The vendor matches the offline booking event to the original ad click using click ID or user identifiers.
1. The advertising vendor can attribute the offline booking back to the original ad click, offering marketers a complete picture of campaign performance, even when bookings are completed outside digital touchpoints.



![](https://docs.tealium.com/images/icons/icon-shield.svg) **Signal loss recovery**



1. A shopper clicks an ad on their mobile browser and proceeds to checkout, but their browser's tracking settings block the tag.
1. The transaction still occurs, but no client-side conversion is recorded.
1. The conversion API recovers the click ID and PII and on order confirmation, the conversion data is sent to the advertising vendor. This server-side delivery restores attribution, helping the retailer avoid under reporting and ensuring bidding optimization toward high-value purchasers.


1. A visitor researching refinancing options clicks an ad and lands on a lender’s site. 
1. They begin filling a pre-approval form but have ad blockers enabled preventing the tag from loading.
1. Tealium collects the form submission and sends the data server-side to the conversion API connector. This server-side recovery ensures the lead is correctly attributed, supporting accurate reporting and campaign ROI even in restrictive environments where client-side signals are degraded or blocked entirely.


1. A traveler taps a vendor ad for a discount travel package booking while browsing on their mobile device.
1. They explore a destination, select a package, and begin the checkout process, but before they finish, they lose their network connection.
1. Fortunately, Tealium had already captured the click ID and session context using the tag and the data was sent to the conversion API before the signal dropped.
1. Later, the traveler resumes their booking on a laptop using the same email to identify themselves, but now they have an ad blocker installed.
1. This time the tag is suppressed, preventing the client-side conversion capture.
1. However, the final booking confirmation is still sent through the Tealium Collect tag, capturing the completed transaction, and then to the conversion API. Using the click ID and user provided PII, despite multiple points of signal degradation, the advertising vendor is able to attribute the booking to the original mobile click, ensuring accurate reporting and bidding optimization.


