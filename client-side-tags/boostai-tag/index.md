---
title: Boost.ai Tag Setup Guide
description: This article describes how to set up the boost.ai tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/boostai-tag/
---
Boost.ai helps you build, implement, and operate conversational AI chatbots to simplify your interactions using market-leading machine learning.

## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Server Name**: Your server URL should resemble: `https://[your-server-name].boost.ai`.
* **Target Element**: Enter the HTML element name where the chat panel is be injected on your website.
  * If the target element is a class, use the period (`.`) precursor. For example, if the class is `chat-container` enter `.chat-container`.
  * If the target element is an ID, use a hash (`#`) precursor. For example, if the ID is `chat-container`, enter `#chat-container`.
* **Automatic Chat Opening**: Automatically opens the chat upon load.

## Load rules

Load the tag on all pages or set conditions for when your tag  loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `serverName`  | String | Server Name (overrides tag configuration) | 
| `targetElement`  |String| Target Element (overrides tag configuration) |
|  `autoChatOpening`  | String | Automatic chat opening (overrides tag configuration) |
|  `filter_values`  | String | Filter values |
|  `once`  | Boolean | Once |
|  `contextIntentId`  | Number |  Context intent ID |
|  `authType`  | String | Auth type  |
|  `authContent`  | String | Auth content |
|  `actionId`  | Number | Action ID  |
|  `customPayload`  | String | Custom payload  |
|  `newTitle`  | String | New title  |
|  `newConversationId`  | Boolean | New Conversation ID |

### Options

| Variable | Type | Description |
|:---------|:------------|:------------|
| `contextTopicIntentId` |  Number  | Context topic intent ID |
| `conversationId`  | String | Conversation ID |
| `startLanguage` | String  | Start language |
| `openTextLinksInNewTab` | Boolean | Open text links in new tab |
| `showLinkClickAsChatBubble` | Boolean | Show link click as chat bubble |
| `messageFeedbackOnFirstAction`  | Boolean | Message feedback on first action |
| `startTriggerActionId`  | String  | Start trigger action ID |
| `authStartTriggerActionId`  | String |  Auth start trigger action ID  |
| `skill`  | String |  Skill |
| `startNewConversationOnResumeFailure`  | Boolean | Start new conversation on resume failure  |
| `fileUploadServiceEndpointUrl`  | String | File upload service endpoint URL |
| `requestFeedback`  | Boolean | Request feedback  |
| `pageUrl`  | String | Page URL  |
| `triggerActionOnResume`  | Boolean | Trigger action on resume  |
| `enableProactivityForSmallDevices`  | Boolean | Enable proactivity for small devices  |
| `removeRememberedConversationOnChatPanelClose`  | Boolean | Remove remembered conversation on chat panel close  |
| `alwaysFullscreen`  | Boolean | Always fullscreen |

### Emit Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
| `emitEvent` | Object  | Emit event  |
| `emitOnResume`  | Boolean  | Emit on resume |
| `detail`  | Object  | Detail  |
| `type`  | String  | Type  |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `chatPanelOpened` | chatPanelOpened |
| `chatPanelClosed` | chatPanelClosed |
| `chatPanelMinimized` | chatPanelMinimized |
| `conversationIdChanged` | conversationIdChanged |
| `messageSent` | messageSent |
| `menuOpened` | menuOpened |
| `menuClosed` | menuClosed |
| `conversationDownloaded` | conversationDownloaded |
| `conversationDeleted` | conversationDeleted |
| `actionLinkClicked` | actionLinkClicked |
| `externalLinkClicked` | externalLinkClicked |
| `conversationReferenceChanged` | conversationReferenceChanged |
| `filterValuesChanged` | filterValuesChanged |
| `authStatusChanged` | authStatusChanged |
| `vanLinkClicked` | vanLinkClicked |
| `conversationTransferredToHuman` | conversationTransferredToHuman |
| `conversationTransferredToVirtualAgent` | conversationTransferredToVirtualAgent |
| `custom` | custom |
| `getVisibility` | getVisibility |
| `loginEvent` | loginEvent |
| `logoutEvent` | logoutEvent |
| `minimize` | minimize |
| `removeEventListener` | removeEventListener |
| `reportAbTestSuccess` | reportAbTestSuccess |
| `setContextIntentId` | setContextIntentId |
| `setConversationId` | setConversationId |
| `setCustomPayload` | setCustomPayload |
| `setFilterValues` | setFilterValues |
| `setSkill` | setSkill |
| `setTitle` | setTitle |
| `show` | show |
| `triggerAction` | triggerAction |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `chatPanelOpened` | chatPanelOpened |
| `chatPanelClosed` | chatPanelClosed |
| `chatPanelMinimized` | chatPanelMinimized |
| `conversationIdChanged` | conversationIdChanged |
| `messageSent` | messageSent |
| `menuOpened` | menuOpened |
| `menuClosed` | menuClosed |
| `conversationDownloaded` | conversationDownloaded |
| `conversationDeleted` | conversationDeleted |
| `actionLinkClicked` | actionLinkClicked |
| `externalLinkClicked` | externalLinkClicked |
| `conversationReferenceChanged` | conversationReferenceChanged |
| `filterValuesChanged` | filterValuesChanged |
| `authStatusChanged` | authStatusChanged |
| `vanLinkClicked` | vanLinkClicked |
| `conversationTransferredToHuman` | conversationTransferredToHuman |
| `conversationTransferredToVirtualAgent` | conversationTransferredToVirtualAgent |
| `custom` | custom |
| `getVisibility` | getVisibility |
| `loginEvent` | loginEvent |
| `logoutEvent` | logoutEvent |
| `minimize` | minimize |
| `removeEventListener` | removeEventListener |
| `reportAbTestSuccess` | reportAbTestSuccess |
| `setContextIntentId` | setContextIntentId |
| `setConversationId` | setConversationId |
| `setCustomPayload` | setCustomPayload |
| `setFilterValues` | setFilterValues |
| `setSkill` | setSkill |
| `setTitle` | setTitle |
| `show` | show |
| `triggerAction` | triggerAction |

    