---
title: Orbee Tag Setup Guide
description: This article describes how to set up the Orbee tag.
url: https://docs.tealium.com/client-side-tags/orbee-tag/
---
Orbee provides a tag to its customers to enable the integration of their web analytics and data solutions with their websites. The web SDK snippet allows the customers to send event and user data to Orbee’s servers.

## Tag tips

Use mappings to:
 * Dynamically override configuration data.
 * Trigger events and set values for event parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Script Token**: The token of the script that belongs to the client's account. The Script Token is the same as SID (script identifier).
* **Host**: The domain where the script is being hosted. The default value is `scripts.orb.ee`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
| `sid` | String | Script token |
| `host` | String | Host|
| `additional_config_info.scope` | String or Array of strings | Scope |
| `additional_config_info.namespace` | String or Array of strings | Namespace | 

### Event Spec Object Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
| `action` | String | Action |
| `object` | String | Object |
| `token` | String | Token |
| `namespaces` | String or Array of strings | Namespaces |
| `vendor` | String | Vendor |
| `product` | String | Product |
| `label` | String | Label |
| `score` | Number | Score |
| `instanceID` | String | Instance ID |
| `element` | Object | Element |
| `element.classes` | Array of text | Element classes |
| `element.id` | String | Element ID |
| `element.href` | String | Element HREF |
| `element.innerText` | String | Inner text |
| `element.title` | String | Element title |
| `element.src` | String | Element SRC |
| `element.alt` | String | Element alt text |
| `element.node` | String | Element node |
| `element.value` | String | Element value |
| `element.type` | Array of objects | Element type |
| `elements` | Array of objects | Elements |
| `custom` | String | Custom |

### Facebook Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `facebook.facebookId` | String | Segment name |
| `facebook.event` | String | Segment ID |
| `facebook.params` | String | Additional configuration for the Facebook segment |
| `facebook.token` | String | Script token |

### Favorites Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `favorites.element` | String |HTML element to register |
| `favorites.config` | String |Optional parameters for the Favorite node |

### Google Ads Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `googleAds.adwordsID` | String | Google Ads segment name |
| `googleAds.event` | String | Google Ads segment ID |
| `googleAds.params` | String | Additional configuration for Google Ads segment |

### Google Analytics Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `googleAnalytics.adwordsID` | String | Google segment name |
| `googleAnalytics.event` | String | Google segment ID |
| `googleAnalytics.params` | String | Script token |

### Layout Manager Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `layoutManager.config` | String | Layout configuration of the ORB element container |
| `layoutManager.config.id` | String | Configuration ID |
| `layoutManager.config.location` | String | Configuration location |
| `layoutManager.config.position` | String | Configuration position |
| `layoutManager.config.attributes` | Object | Configuration attributes |

### Notifications Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `notifications.message` | String | Message|
| `layoutManager.config` | Object | Custom object|
| `notifications.notificationId` | String | Notification ID |

### Popup Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `popupConfig.plugin_id` | String | Plugin ID |
| `popupConfig.context_id` | String | Context ID |
| `popupConfig.css_url` | String | CSS URL |
| `popupConfig.display_type` | String | Display type |
| `popupConfig.popupTimer` | String | Popup timer |
| `popupConfig.visitThreshold` | String | Visit threshold |
| `popupConfig.scrollPersentThreshold` | String | Scroll percentage threshold |
| `popupConfig.scrollTrigger` | String | Scroll trigger |
| `popupConfig.disableConvertedUsers` | String | Disable converted users |
| `popupConfig.disaleNewVisit` | String | Disale New Visit |
| `popupConfig.maxContentDisplayCount` | String | Maximum content display count |
| `popupConfig.cookieExpirationDays` | String | Cookie expiration in days |

### Snapchat Plugin

| Variable | Type | Description |
|:---------|:------------|:------------|
| `snapchat.pixelID` | String | Snapchat pixel ID |
| `snapchat.event` | String | Name of event|
| `snapchat.params` | Object | Additional configuration |
| `snapchat.token` | String | Token |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `dropSegment` | Facebook plugin: drop segment |
| `registerFavoriteNode` | Favorites plugin: register Favorite node |
| `dropSegment` | Google Analytics plugin: drop Google Analytics segment |
| `inject` | Layout Manager plugin: inject |
| `runModules` | Metadata plugin: run modules |
| `renderNotifications` | Notifications plugin: render notifications |
| `push` | Notifications plugin: push |
| `pop` | Notifications plugin: pop |
| `closeNotification` | Notifications plugin: close notification |
| `hideNotifications` | Notifications plugin: hide notifications |
| `showNotifications` | Notifications plugin: show notifications |
| `loadPopup` | Popup plugin: load popup |
| `dropSegment` | SnapChat plugin: drop segment |
| `Custom` | Custom |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `additional_config_info.scope`| Scope  |
| `additional_config_info.namespace`| Namespace  |
| `action`| Action  |
| `object`| Object |
| `token`| Token |
| `namespaces`| Namespaces |
| `vendor`| Vendor |
| `product`| Product |
| `label`| Label |
| `score`| Score  |
| `instanceID`| Instance ID  |
| `element`| Eelement object |
| `element.classes`| Element classes |
| `element.id`| Element ID  |
| `element.href`| Element HREF |
| `element.innerText`| Inner text  |
| `element.title`| Element title |
| `element.src`| Element SRC |
| `element.alt`| Element alt text  |
| `element.node`| Element node |
| `element.value`| Element value  |
| `element.type`| Element type  |
| `elements`| Elements |
| `custom`| Custom element |
| `facebook.facebookId`| Facebook plugin: Facebook ID |
| `facebook.event`| Facebook plugin: Facebook event ID |
| `facebook.params`| Facebook plugin: additional configuration for Facebook segment  |
| `facebook.token`| Facebook plugin: Facebookscript token  |
| `favorites.element`| Favorites plugin: HTML element to register  |
| `favorites.config`| Favorites plugin: optional parameters for the Favorite node |
| `googleAds.adwordsID`| Google Ads plugin: Google Ads segment name |
| `googleAds.event`| Google Ads plugin: Google Ads segment ID |
| `googleAds.params`| Google Ads plugin: additional configuration for Google Ads segment |
| `googleAnalytics.adwordsID`| Google Analytics plugin: Google Analytics segment name  |
| `googleAnalytics.event`| Google Analytics plugin: Google Analytics segment ID |
| `googleAnalytics.params`| Google Analytics plugin: Google Analytics script token  |
| `layoutManager.config`| Layout Manager plugin: Layout Manager configuration of the ORB element container  |
| `layoutManager.config.id`| Layout Manager plugin: Layout Manager configuration ID |
| `layoutManager.config.location`| Layout Manager plugin: Layout Manager configuration location  |
| `layoutManager.config.position`| Layout Manager plugin: Layout Manager configuration position |
| `layoutManager.config.attributes`| Layout Manager plugin: Layout Manager configuration attributes |
| `notifications.message` | Notifications plugin: message |
| `notifications.config`| Notifications plugin: configuration |
| `notifications.notificationId`| Notifications plugin ID |
| `popupConfig.plugin_id` | Popup plugin: ID |
| `popupConfig.context_id`| Popup plugin: context ID  |
| `popupConfig.css_url` | Popup plugin: CSS URL |
| `popupConfig.display_type`| Popup plugin: display type |
| `popupConfig.popupTimer`| Popup plugin: timer |
| `popupConfig.visitThreshold`| Popup plugin: visit threshold |
| `popupConfig.scrollPersentThreshold`| Popup plugin: scroll percentage threshold |
| `popupConfig.scrollTrigger` | Popup plugin: scroll trigger |
| `popupConfig.disableConvertedUsers`| Popup plugin: disable converted users |
| `popupConfig.disaleNewVisit`| Popup plugin: disale new visit |
| `popupConfig.maxContentDisplayCount`| Popup plugin: maximum content display count |
| `popupConfig.cookieExpirationDays`| Popup plugin: cookie expiration in days  |
| `snapchat.pixelID`| Snapchat Snapchat pixel ID |
| `snapchat.event`| Snapchat plugin: Snapchat event name  |
| `snapchat.config`| Snapchat plugin: Snapchat additional configuration |
| `snapchat.token`| Snapchat plugin: Snapchat token |
| `Custom_Parameter`| Custom parameter |
| `facebookDropSegment`| Facebook plugin: drop Facebook segment |
| `registerFavoriteNode`| Favorite plugin: register Favorite node  |
| `googleAdsDropSegment`| Google Ads plugin: drop Google Ads segment |
| `googleAnalyticsDropSegment`| Google Analytics plugin: drop Google Analytics segment |
| `inject`| Inject in Layout Manager plugin |
| `runModules`| Run modules in MetaData plugin |
| `renderNotifications`| Render Notifications plugin |
| `push`| Notifications plugin push |
| `pop` | Notifications plugin pop |
| `closeNotification` | Notifications plugin: close notifications |
| `hideNotifications`| Notifications plugin: hide notifications |
| `showNotifications`| Notifications plugin: show notifications |
| `loadPopup` | Load Popup plugin |
| `snapchatDropSegment`| Snapchat plugin: drop Snapchat segment |
| `Custom_Event`| Custom Event |

  