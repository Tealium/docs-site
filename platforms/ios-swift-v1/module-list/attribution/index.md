---
title: Attribution Module
description: Adds the user-resettable advertising identifier (IDFA) to each tracking call and, optionally, implements the Apple Search Ads API to gather attribution information.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/attribution/
---

## Usage

The Attribution module adds the user-resettable advertising identifier (IDFA) to each tracking call and, optionally, implements the Apple Search Ads API to gather attribution information. [Learn more](https://searchads.apple.com/v/advanced/help/pdf/attribution-api.pdf) for details about Apple Search Ads.

Usage of this module is optional. Take the time to read about its functionality and decide if you need it, as it introduces additional dependencies. You are required to explain to Apple why you are using IDFA when you submit your app. If you do not state that you are using IDFA, Apple rejects your app. [Learn more](https://developer.apple.com/app-store/review/rejections/) about IDFA usage and rejections.

The following platforms are supported:

* iOS

## Requirements

* UIKit
* AdSupport
* iAd

## Install

Install the Attribution module with CocoaPods or Carthage.

### CocoaPods

To install the Attribution module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod &#39;tealium-swift/TealiumAttribution&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the Attribution module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
    ```ruby
    TealiumAttribution.framework
    ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.


## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable Name | Description | Example |
| --- | --- | --- |
| `ad_campaign_id` | The corresponding ad&#39;s campaign ID | `1234567890` |
| `ad_campaign_name` |  The corresponding ad&#39;s campaign name | `CampaignName` |
| `ad_creativeset_id` | The ID of the Creative Set which the corresponding ad was part of. | `456093` |
| `ad_creativeset_name` | The name of the Creative Set which the corresponding ad was part of.| `Beast Images` |
| `ad_group_id` |  The corresponding ad&#39;s campaign group ID | `1234567890` |
| `ad_group_name` |  The corresponding ad&#39;s campaign group name| `AdGroupName` |
| `ad_keyword` | The keyword that drove the ad impression which led to the corresponding ad click| `Keyword` |
| `ad_keyword_matchtype` | This may either be Broad, Exact or Search Match. | `Exact` |
| `ad_org_id` |  The corresponding ad&#39;s campaign organization ID | `OrgID` |
| `ad_org_name` |  The corresponding ad&#39;s campaign organization name | `OrgName` |
| `ad_purchase_date` | Date and time the user first downloaded your app. In the case where `iadconversion-type = &#34;Redownload&#34;`, this represents the original purchase date. This may or may not have been associated with an Apple Search Ad.| `2016-12-05T17:31:40Z` |
| `ad_region` | Identifies the country or region associated with the campaign which drove this install. | `US` |
| `ad_user_clicked_ last_30_days` | Boolean indicating if user clicked on a Search Ads impression within 30 days prior to app download | [`true`, `false`] |
| `ad_user_conversion_type` | Identifies new download or re-download of the app| `Download` |
| `ad_user_date_ clicked` | Date and time the user clicked on a corresponding ad| `2016-12-05T17:31:40Z` |
| `ad_user_date_ converted` | Date and time the user downloaded the app| `2016-12-05T17:31:40Z` |
| `device_advertising_ enabled` | Boolean indicating if the user allowed ad tracking (if `false`, the advertising ID appears as a string of zeroes)| [`true`, `false`] |
| `device_advertising_ id` | User-resettable advertising identifier (IDFA)| `6D92078A-8246...` |
| `device_advertising_ vendor_id` | Unique ID guaranteed to be the same across all apps on the same device from a single vendor (apps with the same first two parts of the RDNS bundle identifier. For example, com.tealium or com.acme)| `6D92078A-8246...` |


The variables prefixed with `ad_` are only enabled if Search Ads has been explicitly enabled in the [TealiumConfig](/platforms/ios-swift-v1/api/tealium-config/) object. These variables are only retrieved from Apple&#39;s servers once during the app&#39;s lifetime, but they are stored as persistent variables so they are available on future app launches.
