---
title: Firebase Cloud Messaging (FCM) Connector Setup Guide
description: This article describes how to set up the Firebase Cloud Messaging connector.
url: https://docs.tealium.com/server-side-connectors/firebase-cloud-messaging-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Google Firebase API
* API Version: v1
* API Endpoint: `https://fcm.googleapis.com/`
* Documentation: [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/concept-options)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Message to Android Device | ✓ | ✓ |
| Send Message to iOS Device | ✓ | ✓ |
| Send Message to Web App | ✓ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Firebase Project ID**  
(Required) Enter the project ID. You can find your Firebase project&#39;s ID using the Firebase console. Open [Project settings](https://console.firebase.google.com/project/_/settings/general/). The project ID appears in the top pane.
* **Client ID**  
(Required) Enter the client ID of the web application that has access to the Firebase Cloud Messaging API. Your [Google API Console Credentials Page](https://console.developers.google.com/apis/credentials) must whitelist the authorized redirect URI: `https://my.tealiumiq.com/oauth/google/callback.html`. See [Create Authorization Credentials](https://developers.google.com/identity/protocols/OAuth2InstalledApp#creatingcred).
* **Client Secret**  
(Required) Enter web application client secret.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Message to Android Device

#### Parameters

 To specify a target for the message, set **only** the one of the following parameters: `Token`, `Topic`, or `Condition`. 

| **Parameter** | **Description** |
| --- | --- |
| Token | Registration token to send a message to. |
| Topic | A subscribed topic name to send a message to. For example: `weather`. Note: Do not include the `/topics/` prefix. |
| Condition | A subscribed condition of topics to send a message to. For example: `foo in topics &amp;&amp; bar in topics`. |
| Analytics Label | Label associated with the message&#39;s analytics data. |
| Collapse Key | An identifier of a group of messages that can be collapsed, so that only the last message gets sent when delivery can be resumed. A maximum of four different collapse keys is allowed at any given time. |
| Priority | Message priority. Value can be `NORMAL` or `HIGH`. For more information, see [Setting the priority of a message](https://firebase.google.com/docs/cloud-messaging/concept-options#setting-the-priority-of-a-message). |
| Time to Live | A duration in seconds with up to nine fractional digits, ending with `s`. For example: `3.5s`. This field represents how long (in seconds) the message should be kept in FCM storage if the device is offline. The maximum supported time to live is four weeks, and the default value is four weeks if not set. Set it to `0` if you want to send the message immediately. |
| Restricted Package Name | The package name of the application, which must match the registration token to receive the message. |
| Direct Boot Ok | If set to `true`, messages will be delivered to the app while the device is in direct boot mode. See [Support Direct Boot mode](https://developer.android.com/training/articles/direct-boot) for more details.|
| Title | The notification&#39;s title. |
| Body | The notification&#39;s body text. |
| Icon | The notification&#39;s icon. Sets the notification icon to `myicon` for drawable resource `myicon`. If not specified, FCM displays the launcher icon specified in your app manifest. |
| Color | The notification icon color, expressed in `#rrggbb` format. |
| Sound | The sound to play when the device receives the notification. Supports `default` or the filename of a sound resource bundled in the app. Sound files must reside in `/res/raw/`. |
| Tag | Identifier used to replace existing notifications in the notification drawer. If not specified, each request creates a new notification. If specified and a notification with the same tag is already being shown, the new notification replaces the existing one in the notification drawer. |
| Click Action | The action associated with a user click on the notification. If specified, an activity with a matching intent filter is launched when a user clicks on the notification. |
| Body Localization Key | The key for the body string in the app resources, which is used to localize the body text to the user&#39;s current locale. See [String Resources](https://developer.android.com/guide/topics/resources/string-resource.html) for more information. |
| Body Localization Args | String values to be used in place of the format specifiers in the **Body Localization Key**, which is used to localize the body text to the user&#39;s current locale. See [Formatting and Styling](https://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling) for more information. |
| Title Localization Key | The key for the title string in the app&#39;s resources, which is used to localize the title text to the user&#39;s current locale. See [String Resources](https://developer.android.com/guide/topics/resources/string-resource.html) for more information. |
| Title Localization Args | String values to be used in place of format specifiers in the **Title Localization Key**, which is used to localize the title text to the user&#39;s current locale. See [Formatting and Styling](https://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling) for more information. |
| Channel ID | The [notification&#39;s channel ID](https://developer.android.com/develop/ui/views/notifications#ManageChannels) (new in Android O). The app must create a channel with this channel ID before any notification with this channel ID is received. If not specified, or if the provided channel ID has not yet been created by the app, FCM uses the channel ID specified in the app instead. |
| Ticker | This parameter sets the notification ticker text, which is sent to accessibility services. Prior to API level 21 (Lollipop), this parameter sets the text that is displayed in the status bar when the notification first arrives. |
| Sticky | If set to `false` or not specified, the notification is automatically dismissed when the user clicks it in the panel. When set to `true`, the notification persists even when the user clicks it. |
| Event Time | The time that the event in the notification occurred. Notifications in the panel are sorted by this time. A timestamp in RFC3339 UTC format, with nanosecond resolution and up to nine fractional digits. Examples: `2014-10-02T15:01:23Z` and `2014-10-02T15:01:23.045123456Z`. |
| Local Only | If set to `true`, indicates that the notification is relevant only to the current device. |
| Notification Priority | Set the relative priority for this notification. Priority is an indication of how critical the notification is. Value can be `PRIORITY_UNSPECIFIED`, `PRIORITY_MIN`, `PRIORITY_LOW`, `PRIORITY_DEFAULT`, `PRIORITY_HIGH`, or `PRIORITY_MAX`. |
| Default Sound | If set to `true`, use the Android framework&#39;s default sound for the notification. |
| Default Vibrate Timings | If set to `true`, use the Android framework&#39;s default vibrate pattern for the notification. |
| Default Light Settings | If set to `true`, use the Android framework&#39;s default LED light settings for the notification. |
| Vibrate Timings | Set the vibration pattern to use. A duration in seconds with up to nine fractional digits, ending with `s`. For example: `3.5s`. See [Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification). |
| Visibility | Set the [visibility](https://developer.android.com/reference/android/app/Notification#visibility) of the notification. Value can be `VISIBILITY_UNSPECIFIED`, `PRIVATE`, `PUBLIC`, or `SECRET`. |
| Notification Count | Sets the number of items within this notification. |
| Light On Duration | Along with **Light Off Duration**, define the blink rate of LED flashes. A duration in seconds with up to nine fractional digits, ending with `s`. For example: `3.5s`. |
| Light Off Duration | Along with **Light On Duration**, define the blink rate of LED flashes. A duration in seconds with up to nine fractional digits, ending with `s`. Example: `3.5s`. |
| Color Red | A value between `0` and `1` that represents the amount of Red in the overall light color. Combine this value with the values you set for Color Green and Color Blue to determine the overall color. For example, Color Red = `1`, Color Blue = `.5`, and Color Green = `0` creates fuchsia or deep pink. |
| Color Green | A value between `0` and `1` that represents the amount of Green in the overall light color. Combine this value with the values you set for Color red and Color Blue to determine the overall color. |
| Color Blue | A value between `0` and `1` that represents the amount of Blue in the overall light color. Combine this value with the values you set for Color Green and Color Red to determine the overall color. |
| Color Alpha | The fraction of this color that should be applied to the pixel. That is, the final pixel color is defined by the equation: **pixel color = alpha \* (this color) &#43; (1.0 - alpha) \* (background color)**. |
| Image | The URL of an image to be displayed in the notification. |
| Data | User-specified data in `&#34;key&#34; : &#34;value&#34;` pair
 format. |
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;ul&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | Provide templates to be referenced in **Message Options** and **Notification Options** sections. For more information, see . Templates are injected by name with double curly braces into supported fields. For example: `{{template_name}}` |

* See [Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#resource:-message), [AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig) documentation for usage examples.

* To support nested objects, use the **Templates** section to define a template. The template should be mapped using the **Custom Text** option by referencing its names with matching double curly braces: `{{template_name}}`.

### Send Message to iOS Device

#### Parameters

 To specify a target for the message, set **only** the one of the following parameters: `Token`, `Topic`, or `Condition`. 

| **Parameter** | **Description** |
| --- | --- |
| Token | Registration token to send a message to. |
| Topic | A subscribed topic name to send a message to. For example: `weather`. Note: Do not include the `/topics/` prefix. |
| Condition | A subscribed condition of topics to send a message to. For example: `foo in topics &amp;&amp; bar in topics`. |
| Analytics Label | Label associated with the message&#39;s analytics data. |
| Image | The URL of an image to be displayed in the notification. |
| Title | The title of the notification. Apple Watch displays this string in the short look notification interface. |
| Subtitle | Additional information that explains the purpose of the notification. |
| Body | The content of the alert message. |
| Launch Image | The name of the launch image file to display. |
| Title Localization Key | The key for a localized title string. Specify this key instead of the **Title** key to retrieve the title from your app&#39;s `Localizable.strings` files. The value must contain the name of a key in your strings file. |
| Title Localization Args | An array of strings containing replacement values for variables in your title string. Each `%@` character in the string specified by the **Title Localization Key** is replaced by a value from this array. The first item in the array replaces the first instance of the `%@` character in the string, the second item replaces the second instance, and so on. |
| Subtitle Localization Key | The key for a localized subtitle string. Use this key, instead of the **Subtitle** key, to retrieve the subtitle from your app&#39;s `Localizable.strings` file. The value must contain the name of a key in your strings file. |
| Subtitle Localization Args | An array of strings containing replacement values for variables in your title string. Each `%@` character in the string specified by **Subtitle Localization Key** is replaced by a value from this array. |
| Body Localization Key | The key for a localized message string. Use this key, instead of the **Body** key, to retrieve the message text from your app&#39;s `Localizable.strings` file. The value must contain the name of a key in your strings file. |
| Body Localization Args | An array of strings containing replacement values for variables in your message text. Each `%@` character in the string specified by **Body Localization Key** is replaced by a value from this array. |
| Badge | The number to display in a badge on your app&#39;s icon. Set this parameter to `0` to remove the current badge, if any. |
| Sound Critical | The critical alert flag. Set this parameter to `1` to enable the critical alert. |
| Sound File Name | The name of a sound file in your app&#39;s main bundle or in the Library/Sounds folder of your app&#39;s container directory. Set this value to the string `default` to play the system sound. |
| Sound Volume | The volume for the critical alert&#39;s sound. Set this parameter to a value between `0` (silent) and `1` (full volume). |
| Thread ID | An app-specific identifier for grouping related notifications. |
| Category | The notification&#39;s type. |
| Content Available | The background notification flag. To perform a silent background update, specify the value `1` and don&#39;t include the **Alert**, **Badge**, or **Sound** keys in your payload. |
| Mutable Content | The notification service app extension flag. If the value is 1, the system passes the notification to your notification service app extension before delivery. |
| Target Content ID | The identifier of the window brought forward. |
| Interruption Level | The importance and delivery timing of a notification. |
| Relevance Score | The relevance score, a number between `0` and `1`, that the system uses to sort the notifications from your app. |
| Filter Criteria | A string that the system evaluates to determine if it displays the notification in the current **Focus**. |
| Stale Date | The UNIX timestamp that represents the date at which a **Live Activity** becomes stale, or out of date. |
| Content State | A JSON object that contains updated or final content for a **Live Activity**. The content of this parameter must match the data you describe with your custom [ActivityAttributes](https://developer.apple.com/documentation/activitykit/activityattributes) implementation. This option supports templating. |
| Timestamp | The UNIX timestamp that specifies the time at which the remote notification will be sent to update or end a **Live Activity**. |
| Events | Specifies whether to update or end an ongoing **Live Activity** with the remote push notification. Value can be `update` or `end`. |
| Data | User-specified data in `&#34;key&#34; : &#34;value&#34;` pair
 format. |
| Headers | HTTP request headers defined in Apple Push Notification Service. See [APNs request headers](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/sending_notification_requests_to_apns) for supported headers such as **apns-expiration** and **apns-priority**. See [Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification) for details.|
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;ul&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | Provide templates to be referenced in **Message Options** and **Notification Options** sections. For more information, see . Templates are injected by name with double curly braces into supported fields. For example: `{{template_name}}` |

* See [AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig) documentation for usage examples.

* To support nested objects, use the **Templates** section to define a template. The template should be mapped using the **Custom Text** option by referencing its names with matching double curly braces: `{{template_name}}`

### Send Message to Web App

#### Parameters

 To specify a target for the message, set **only** the one of the following parameters: `Token`, `Topic`, or `Condition`. 

| **Parameter** | **Description** |
| --- | --- |
| Token | Registration token to send a message to. |
| Topic | A subscribed topic name to send a message to. For example: `weather`. Note: Do not include the `/topics/` prefix. |
| Condition | A subscribed condition of topics to send a message to. For example: `foo in topics &amp;&amp; bar in topics`. |
| Analytics Label | Label associated with the message&#39;s analytics data. |
| Link | The secure link to open when the user clicks on the notification. Value must begin with `https://`. |
| Action | A string identifying a user action to be displayed on the notification. |
| Action Title | A string containing action text to be shown to the user. |
| Action Icon | A string containing the URL of an icon to display with the action. |
| Badge | The URL of the image used to represent the notification when there is not enough space to display the notification itself. |
| Title | The title of the notification. |
| Body | The body string of the notification. |
| Data | Returns a structured clone of the notification&#39;s data. This option supports templating. |
| Direction | The text direction of the notification. |
| Icon | The URL of the image used as an icon of the notification. |
| Image | The URL of an image to be displayed as part of the notification. |
| Language | The language code of the notification. |
| Renotify | Specifies whether the user should be notified after a new notification replaces an old one. |
| Require Interaction | A boolean value indicating that a notification should remain active until the user clicks or dismisses it, rather than closing automatically. |
| Silent | Specifies whether the notification should be silent. If this parameter is set to `true`, no sounds or vibrations are issued, regardless of the device settings. |
| Tag | The ID of the notification. |
| Timestamp | Specifies the time at which a notification is created or applicable (past, present, or future). |
| Vibrate | Specifies a vibration pattern for devices with vibration hardware to emit. A duration in seconds with up to nine fractional digits, ending with `s`. For example: `3.5s`. See [Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification). |
| Data | User-specified data in `&#34;key&#34; : &#34;value&#34;` pair format. |
| Headers | HTTP headers defined in webpush protocol. Refer to [Webpush protocol](https://www.rfc-editor.org/rfc/rfc8030#section-5) for supported headers. For example: `&#34;TTL&#34;: &#34;15&#34;`. See [Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification) for details. |
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;ul&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | Provide templates to be referenced in **Message Options** and **Notification Options** sections. For more information, see . Templates are injected by name with double curly braces into supported fields. For example: `{{template_name}}` |

* See [AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig) documentation for usage examples.

* To support nested objects, use the **Templates** section to define a template. The template should be mapped using the **Custom Text** option by referencing its names with matching double curly braces: `{{template_name}}`.&lt;/li&gt;&lt;/ul&gt;