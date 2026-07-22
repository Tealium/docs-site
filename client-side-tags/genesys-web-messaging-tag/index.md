---
title: Genesys Web Messaging Tag Setup Guide
description: This article describes how to set up the Genesys Web Messaging tag.
url: https://docs.tealium.com/client-side-tags/genesys-web-messaging-tag/
---
Genesys Web Messaging is a feature that enables customers to converse with a bot or an agent on your website. It offers several advantages over web chat, including asynchronous conversations, inbound and outbound image attachments, and unified agent and supervisor experience across all Genesys Cloud messaging channels.

## Tag Tips

* Use mappings to dynamically override the standard configuration values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Deployment ID**:  
Genesys identifier, as provided by the user.
* **Environment**:  
The environment where the tag is being deployed.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `deploymentId` | String | Deployment ID. |
| `environment` | String | Environment. |
| `debug` | Boolean   | Debug. |
| `base_url` | String | Base URL. |

### Authentication

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `authCode` | String | The authorization code. |
| `redirectUri` | String | Redirection URI configured. |
| `nonce` | String | Random string, preferably a UUID. |
| `maxAge` | String | Elapsed time in seconds. |
| `codeVerifier` | String | Code verifier for PKCE flow. |
| `iss` | String | Issuer. |

### Database Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `customAttributes` | Object  | Custom attributes. |
| `name` | String | The object property name that you want to retrieve. |

### Cobrowse Service Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `joinCode` | String | Join code. |
| `sessionId` | String | Session ID. |

### Engagement Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `engageContent` | Object  | Engage content. |
| `engageContent.offerText` | String | Engage content offer text. |

### Journey Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pageTitle` | String | Page title. |
| `pageLocation` | String | Page location. |
| `customAttributes` | Object  | Custom attributes. |
| `traitsMapper` | Array of Objects | Traits mapper. |
| `eventName` | String | The name of the event to post when the HTML element is clicked. |
| `selector` | String | The CSS selector to track. |
| `formName` | String | Form name. |
| `captureFormDataOnAbandon` | Boolean   |  Indicates whether form data should be captured when form is abandoned. |
| `captureFormDataOnSubmit` | Boolean   |  Indicates whether form data should be captured when form is submitted.|
| `clickEvents.selector` | Array    | Click events selector. |
| `clickEvents.eventName` | Array    | Click events event name. |
| `clickEvents.customAttributes` | Array    | Click events custom attributes. |
| `idleEvents.idleAfterSeconds` | Array    | The number of seconds of user inactivity to wait before recording the event. |
| `idleEvents.eventName` | Array    | Idle events event name. |
| `idleEvents.customAttributes` | Array    | Idle events custom attributes. |
| `inViewportEvents.selector` | String | In viewport events selector. |
| `inViewportEvents.eventName` | String | In viewport events event name. |
| `inViewportEvents.customAttributes` | Object  | In viewport events custom attributes. |
| `scrollDepthEvents.percentage` | Number | Scroll depth events percentage. |
| `scrollDepthEvents.eventName` | String | Scroll depth events event name. |
| `scrollDepthEvents.customAttributes` | Object  | Scroll depth events custom attributes. |
| `actionId` | String | Action ID. |
| `actionState` | String | Action state. |
| `errorCode` | String | Error code. |
| `errorReason` | String | Error reason. |

### MessagingService Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `message` | String | The text message to send. |

### Toaster Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `title` | String | The title of the toast message. |
| `body` | String | The body text of the toast message. |
| `buttons.type` | String | The type of buttons in the toast message. Accepted values are `unary` for one button and binary for `two` buttons. |
| `buttons.primary` | String | The primary button text in the toast message. The default value is `Accept`. |
| `buttons.secondary` | String | The secondary button text in the toast message. The default value is `Accept`. |

### Event Specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `authCode` | The authorization code. |
| `redirectUri` | Redirection URI configured. |
| `nonce` | Random string, preferably a UUID. |
| `maxAge` | Elapsed time in seconds. |
| `codeVerifier` | Code verifier for PKCE flow. |
| `iss` | Issuer. |
| `customAttributes` | Custom attributes. |
| `name` | The object property name that you want to retrieve. |
| `joinCode` | Join code. |
| `sessionId` | Session ID. |
| `engageContent` | Engage content. |
| `engageContent.offerText` | Engage content offer text. |
| `pageTitle` | Page title. |
| `pageLocation` | Page location. |
| `customAttributes` | Custom attributes. |
| `traitsMapper` | Traits mapper. |
| `eventName` | The name of the event to post when the HTML element is clicked. |
| `selector` | The CSS selector to track. |
| `formName` | Form name. |
| `captureFormDataOnAbandon` | Indicates whether form data should be captured when form is abandoned. |
| `captureFormDataOnSubmit` | Indicates whether form data should be captured when form is submitted. |
| `clickEvents.selector` | Click events selector. |
| `clickEvents.eventName` | Click events event name. |
| `clickEvents.customAttributes` | Click events custom attributes. |
| `idleEvents.idleAfterSeconds` | The number of seconds of user inactivity to wait before recording the event. |
| `idleEvents.eventName` | Idle events event name. |
| `idleEvents.customAttributes` | Idle events custom attributes. |
| `inViewportEvents.selector` | In viewport events selector. |
| `inViewportEvents.eventName` | In viewport events event name. |
| `inViewportEvents.customAttributes` | In viewport events custom attributes. |
| `scrollDepthEvents.percentage` | Scroll depth events percentage. |
| `scrollDepthEvents.eventName` | Scroll depth events event name. |
| `scrollDepthEvents.customAttributes` | Scroll depth events custom attributes. |
| `actionId` | Action ID. |
| `actionState` | Action state. |
| `errorCode` | Error code. |
| `errorReason` | Error reason. |
| `message` | Message. |
| `title` | String | The title of the toast message. |
| `body` | String | The body text of the toast message. |
| `buttons.type` | String | The type of buttons in the toast message. Accepted values are `unary` for one button and binary for `two` buttons. |
| `buttons.primary` | String | The primary button text in the toast message. The default value is `Accept`. |
| `buttons.secondary` | String | The secondary button text in the toast message. The default value is `Accept`. |