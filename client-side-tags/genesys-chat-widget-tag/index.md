---
title: Genesys Chat Widget Tag Guide
description: This article describes how to set up the Genesys Chat Widget tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/genesys-chat-widget-tag/
---## Tag tips

* Use mapping to dynamically override the standard configuration values, send custom user data or map objects and functions.
* The contents of the function can be set up in a JavaScript extension.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Version**
  * The version of the widget to load.
  * Example: 9.0
* **Region**
  * Select the nearest or appropriate region based on where you are located.
* **Theme**
  * Selects the theme to apply to Genesys Widgets from the 'themes' object.
  * Uses the property name of the theme.
* **Language**
  * Select the language to use from the 'i18n' language pack.
  * Language codes are selected by the customer.
  * Any language code format can be used as long as this property matches one of the language codes in your i18n language pack.
* **Mobile Mode**
  * Values are **true**, **false**, or **auto**.
    * A value of **true** forces Mobile mode on all devices.
    * A value of **false** disables Mobile mode completely.
    * If you use the automatic (**auto**) value Genesys Widgets Automatically switches between Mobile and Desktop modes using the 'Mobile Mode Breakpoint' property and UserAgent detection.
* **Time Format**
  * Sets the time format for the timestamps.
  * Values are **12** or **24**.
* **Mobile Mode Breakpoint**
  * The breakpoint width in pixels where Genesys Widgets will switch to Mobile mode.
* **Custom Stylesheet ID**
  * The HTML ID of a `<style>` tag that contains CSS overrides, custom themes, or other custom CSS intended for Genesys Widgets.
* **Download Google Font**
  * By default, Genesys Widgets downloads and uses the Google font 'Roboto'.
  * Values are **true** or **false**.
  * A value of **true** downloads and used the Google font Roboto.
  * To disable this download, set this value to **false**.
* **Deployment ID**
  * The string used to customize cookie names to enable multiple widget deployments to run in the same domain.
* **API Key**
  * Apigee Proxy secure token.
* **Endpoint**
  * Manually enter the endpoint to initiate chat on.
* **Data URL**
  * URL for GMS REST chat service.
  * Values are **true** or **false**.
  * Required if CometD is not enabled.
  * If `CometD Enabled` is set to **true**, this property is ignored.
* **Enable Custom Header**
  * Enables the use of the custom authorization header defined in `_genesys.widgets.main.header` static config.
  * Attaches the custom authorization header to all WebChatService request.
* **CometD Enabled**
  * Enables or disables the CometD connection method.
  * Values are **true** or **false**.
  * If set to **false** or left undefined, WebChatService connects to REST services through the `dataURL` specified.
* **CometD Comet URL**
  * URL for GMS CometD connection.
  * Values are **true** or **false**.
  * `CometD Enabled` must be set to **true** for `WebChatService` to connect to this service.
* **CometD Channel**
  * CometD channel for receiving chat messages.
* **CometD API URL**
  * URL for additional CometD services, such as file upload and download.
* **CometD Websocket Enabled**
  * Values are **true** or **false**.
    * If set to **true**, CometD attempts to connect through websockets.
    * If set to **false**, CometD only uses long-polling.
  * CometD falls back to long-polling if it cannot connect through websockets.
* **Async Enabled**
  * Enable Asynchronous Chat where a chat session can be active indefinitely.
* **Ajax Timeout**
  * Number of milliseconds to wait before AJAX timeout.
* **Poll Exception Limit**
  * Number of successive poll exceptions (chat server offline) before WebChatService publishes `chatServerWentOffline`.
* **Restore Timeout**
  * Number of milliseconds before restore timeout.
  * Prevents the chat session from restoring after a certain time away from the session
  * Example: The user navigated to a different site during chat and never ended the session.
* **Emojis**
  * Enable Emoji Menu.
* **Uploads Enabled**
  * Show the Send File button.
* **Confirm Form Close Enabled**
  * Enable displaying a confirmation message before closing WebChat if information has been entered into the registration form.
* **Actions Menu**
  * Enable actions menu next to chat message input.
* **Max Message Length**
  * Set a character limit that the user can input into the message area during a chat.
  * When the maximum message length is reached, user can no longer type.
* **Char Count Enabled**:
  * Show the number of characters remaining in the input message area while the user is typing.
* **Auto Invite Enabled**
  * Enable auto-invite feature.
  * Automatically invites user to chat after user idles on page for preset time.
* **Time To Invite Seconds**
  * Number of seconds of idle time before inviting customer to chat.
* **Timeout Seconds**
  * Number of seconds to wait after showing invite before closing the chat invite.
* **Chat Button Enabled**
  * Enable chat button on screen.
* **Chat Button Open Delay**
  * Number of milliseconds before displaying chat button on screen.
* **Chat Button Effect Duration**
  * Length of animation effect, in milliseconds.
* **Hide Chat Button During Invite**
  * When auto-invite feature is activated, hide the chat button.
  * When invite is dismissed, reveal the chat button again.
* **Minimize On Mobile Restore**
  * Enable/disable the minimized state of webchat on chat restore.
  * This option is only for mobile mode.
* **Enable Markdown**
  * Enable/disable the markdown feature for chat messages.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Main

|Variable| Description|
|---| ---|
|Themes (main.themes)| [Object]|
|Theme (main.theme)| [String]|
|Language (main.lang)| [String]|
|i18n (main.i18n)| [URL string or JSON]|
|Header (main.header)| [Object]|
|Preload (main.preload)| [Array]|
|Mobile Mode (main.mobileMode)| [Boolean/String]|
|Time Format (main.timeFormat)| [Number/String]|
|Mobile Mode Breakpoint (main.mobileModeBreakpoint)| [Number]|
|Debug (main.debug)| [Boolean]|
|Custom Stylesheet ID (main.customStylesheetID)| [String]|
|Download Google Font (main.downloadGoogleFont)| [Boolean]|
|Deployment ID (main.deploymentID)| [String]|
|Cookie Options (main.cookieOptions)| [Object]|
|onReady (mainonReady)| [Function]|
|Script URL (script\_url)| [String]|
|CSS URL (css\_url)| [String]|

### Webchat Service

|Variable| Description|
|---| ---|
|Themes (main.themes)| [Object]|
|API Key (webchat.apikey)| [String]|
|Endpoint (webchat.endpoint)| [String]|
|Data URL (webchat.dataURL)| [String]|
|EnableCustomHeader (webchat.enableCustomHeader)| [Boolean]|
|CometD (webchat.cometD)| [Object]|
|CometD.enabled (webchat.cometD.enabled)| [Boolean]|
|CometD.cometURL (webchat.cometD.cometURL)| [String]|
|CometD.channel (webchat.cometD.channel)| [String]|
|CometD.apiURL (webchat.cometD.apiURL)| [String]|
|CometD.websocketEnabled (webchat.cometD.websocketEnabled)| [Boolean]|
|CometD.logLevel (webchat.cometD.logLevel)| [String]|
|UserData (webchat.userData)| [Object]|
|AjaxTimeout (webchat.ajaxTimeout)| [Number]|
|XhrFields (webchat.xhrFields)| [Object]|
|PollExceptionLimit (webchat.pollExceptionLimit)| [Number]|
|RestoreTimeout (webchat.restoreTimeout)| [Number]|
|Async (webchat.async)| [Object]|
|Async.enabled (webchat.async.enabled)| [Boolean]|
|Async New Message Restore State (webchat.async.newMessageRestoreState)| [String]|
|Async.getSessionData (webchat.async.getSessionData)| [Function]|
|Async.setSessionData (webchat.async.setSessionData)| [Function]|

### Webchat UI

|Variable| Description|
|---| ---|
|Emojis (webchat.emojis)| [Boolean]|
|Form (webchat.form)| [Object]|
|Uploads Enabled (webchat.uploadsEnabled)| [Boolean]|
|Confirm Form Close Enabled (webchat.confirmFormCloseEnabled)| [Boolean]|
|Actions Menu (webchat.actionsMenu)| [Boolean]|
|Max Message Length (webchat.maxMessageLength)| [Number]|
|Char Count Enabled (webchat.charCountEnabled)| [Boolean]|
|Auto Invite Enabled (webchat.autoInvite.enabled)| [Boolean]|
|Auto Invite Time To Invite Seconds (webchat.autoInvite.timeToInviteSeconds)| [Number]|
|Auto Invite Invite Timeout Seconds (webchat.autoInvite.inviteTimeoutSeconds)| [Number]|
|Chat Button Enabled (webchat.chatButton.enabled)| [Boolean]|
|Chat Button Template (webchat.chatButton.template)| [String]|
|Chat Button Effect (webchat.chatButton.effect)| [String]|
|Chat Button Open Delay (webchat.chatButton.openDelay)| [Number]|
|Chat Button Effect Duration (webchat.chatButton.effectDuration)| [Number]|
|Minimize On Mobile Restore (webchat.minimizeOnMobileRestore)| [Boolean]|
|Enable Markdown (webchat.markdown)| [Boolean]|
