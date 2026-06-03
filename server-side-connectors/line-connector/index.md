---
title: LINE Connector Setup Guide
description: This article describes how to set up the LINE connector.
url: https://docs.tealium.com/server-side-connectors/line-connector/
---
## Requirements

The LINE connector requires the following:

* LINE: Channel Access Token. For more information, see [Messaging API overview](https://developers.line.biz/en/docs/messaging-api/overview/).

## API Information

This connector uses the following vendor API:

* API Name: LINE Messaging API
* API Version: v2
* API Endpoint: `https://api.line.me/v2`
* Documentation: [LINE: Audience API](https://developers.line.biz/en/docs/messaging-api/)

## Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 30 minutes
* Max size of requests: 1 MB

## Supported Actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
| Add Users to Audiences | ✓ | ✗ |
| Push message - Text | ✓ | ✗ |
| Push message - Image | ✓ | ✗ |
| Push message - Video | ✓ | ✗ |
| Push message - Audio | ✓ | ✗ |
| Push message - Location | ✓ | ✗ |
| Push message - Sticker | ✓ | ✗ |
| Push Message - Imagemap | ✓ | ✗ |
| Push Message - Template message (Buttons template) | ✓ | ✗ |
| Push Message - Template message (Confirm template) | ✓ | ✗ |
| Push Message - Template message (Carousel template) | ✓ | ✗ |
| Push Message - Template message (Image carousel template) | ✓ | ✗ |
| Push Message - Flex | ✓ | ✗ |

## Configure Settings

Go to the Connector Marketplace and add a new LINE connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the connector instance.
1. Enter the channel access token that you set up with LINE for your account.
1. Provide additional notes about your implementation.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab to set up actions and trigger them.

This section describes how to set up parameters and options for each action.

### Action - Add Users to Audiences

| **Parameter** | **Description** |
| --- | --- |
| Audience Group ID | Select the audience group from the list or enter it as a custom text. |
| User ID | A user ID or IFA (Identifier For Advertising). To send multiple user IDs, map an array to this parameter. |
| Description | A description for this update action. |

### Add Users to Audiences (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience Group ID | Select the audience group from the list or enter it as a custom text. |
| User ID | A user ID or IFA. To send multiple user IDs, map an array to this parameter. |
| Description | A description for this update action. |

### Action - Push Message - Text

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL.|
| Message Data | (Required) The content of the message to send to the user. This field is limited to 2,000 characters, supports Unicode emoticons, and supports the Tealium template engine. For more information, see .|
| Template Variables  | These fields map attributes to variable names that are used in the message data. Name nested template variables with dot notation. For example, `items.name`.  For more information, see . |)

### Action - Push Message - Image

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Original Content URL | (Required) The URL of the image to send to the user. The URL must use HTTPS and must not exceed 1,000 characters. The image must be a JPEG with maximum dimensions of 1,024 pixels by 1,024 pixels and a maximum size of 1 MB. |
| Preview Image URL | (Required) The URL of the preview image to send to the user. The URL must use HTTP and must not exceed 1,000 characters. The image must be in JPEG format with a maximum dimension of 240 pixels by 240 pixels and a maximum size of 1 MB. |

### Action - Push Message - Video

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Original Content URL | (Required) The URL of the video to send to the user. The URL must use the HTTPS protocol and must not exceed 1,000 characters. The video must be in MP4 format with a maximum duration of one minute and a maximum size of 10 MB. |
| Preview Image URL | (Required) The URL of the preview image to send to the user. The URL must use HTTP and must not exceed 1,000 characters. The image must be in JPEG format with a maximum dimension of 240 pixels by 240 pixels and a maximum size of 1 MB. |

### Action - Push Message - Audio

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID |(Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL.|
| Original Content URL | (Required) The URL of the audio to send to the user. The URL must use the HTTPS protocol and must not exceed 1,000 characters. The audio must be in M4A format with a maximum duration of one minute and a maximum size of 10 MB.|
| Duration | (Required) The length of the audio file in milliseconds.|

### Action - Push Message - Location

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Title | (Required) The name of the location to send to the user.|
| Address | (Required) The address of the location to send to the user.|
| Latitude | (Required) The latitude of the location to send to the user.|
| Longitude | (Required) The longitude of the location to send to the user.|

### Action - Push Message - Sticker

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
|Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
|Package ID |(Required) The ID of the package to which a sticker belongs. |
|Sticker ID |(Required) The ID of the sticker to send to the user. |

### Push Message - Imagemap

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Base URL | (Required) The URL of the base image. The URL must use the HTTPS protocol and must not exceed 1,000 characters. |
| Alternative Text | (Required) Alternative text for the base image with a maximum of 400 characters. The alternative text appears in notifications or chat lists. |
| Base Size - Width | (Required) The width of base image in pixels. Set this value to `1040`. |
| Base Size - Height | (Required) The height of the base image in pixels. Set this value to the height of the image when its width is 1040 pixels. |

#### Actions Data

All Actions Data parameters are arrays.

| **Parameter** | **Description** |
| --- | --- |
| Type | The type of action. Possible values are `uri` and `message`. |
| Area - X | The horizontal position of the actions area relative to the left edge of the imagemap area. Minimum value is `0`. |
| Area - Y | The vertical position of the actions area relative to the top of the imagemap area. Minimum value is `0`.  |
| Area - Width | The width of the actions area. |
| Area - Height | The height of the actions area. |
| Label | The label for the action. |
| Link URI | For `uri` type actions, the URI of the link for the actions. |
| Text | For message type actions, the text for the actions. |
| Clipboard Text | The text that is copied to the clipboard. |

#### Video Data

The following parameters are required if you set a video to play on the imagemap:

| **Parameter** | **Description** |
| --- | --- |
| Original Content URL | The video file URL. The URL must not exceed 2,000 characters and must use the HTTPS protocol. The video must be in .mp4 format and cannot exceed 200 MB. |
| Preview Image URL | The preview image URL The URL must not exceed 2,000 characters and must use the HTTPS protocol. The image must use the JPEG or PNG format and cannot exceed 1 MB. |
| Area - X | The horizontal position of the video area relative to the left edge of the imagemap area. Minimum value is `0`. |
| Area - Y | The vertical position of the video area relative to the top of the imagemap area. Minimum value is `0`. |
| Area - Width | The width of the video area. |
| Area - Height | The height of the video area. |

The following parameters are required if you set a video to play on the imagemap and a label is displayed after the video ends:

| **Parameter** | **Description** |
| --- | --- |
| External Link - Link URI | The web page URL. The URL must not exceed 1,000 characters and can use the following protocols: `http`, `https`, `line`, `tel`. |
| External Link - Label | The label to display after the video is finished. The label must not exceed 30 characters. |

### Push Message - Template message (Buttons template)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL.  |
| Alternative Text | (Required) Alternative text for the message. The text must not exceed 400 characters. The text appears in notifications or chat lists. |
| Template - Text | (Required) The message text. Text without an image or title must not exceed 400 characters, and text with an image or title must not exceed 60 characters. |
| Template - Thumbnail Image URL | (Required) The URL of the image&#39;s thumbnail. The URL must not exceed 2,000 characters and must use the HTTPS protocol. |
| Template - Image Aspect Ratio | (Required) The aspect ratio of the image. Allowed values are `rectangle` or `square`. The default value is `rectangle`. |
| Template - Image Size | (Required) The size of the image. Allowed values are `cover` or `contain`. The default value is `cover`. |
| Template - Image Background Color | (Required) The background color of the image in hexadecimal format. The default value is `#FFFFFF` (white). |
| Template - Title | (Required) The title of the message. The title must not exceed 40 characters. |

#### Template - Actions

All Template - Actions parameters are arrays.

| **Parameter** | **Description** |
| --- | --- |
| Type | (Required) The type of action. Allowed values are: `postback`, `message`, `uri`, `datetimepicker`, `camera`, `cameraRoll`, `location`, `richmenuswitch`, `clipboard`. |
| Label | (Required) The label for the action. Specifications vary based on the object the action is set to. |
| Data | (Required) The string returned through the webhook in the `postback.data` property of the postback event. |
| Display Text | (Required) The text displayed on the LINE chat screen as a message sent by the user when the action is performed. |
| Text | (Required) For `message` type actions, the text sent when the action is performed. |
| URI | (Required) For `uri` type actions, the URI opened when the action is performed. The URL must use the HTTPS protocol.|
| Alternative URI - Desktop | (Required) For `uri` type actions, the URI opened on LINE for macOS and Windows when the action is performed.
| Mode | (Required) For `datetimepicker` type actions, the action mode. Allowed values are: `date`, `time`, `datetime`. |
| Initial | (Required) For `datetimepicker` type actions, the initial value of date or time. |
| Max | (Required) For `datetimepicker` type actions, the largest date or time value that can be selected. |
| Min | (Required) For `datetimepicker` type actions, the smallest date or time value that can be selected. |
| Input Option | (Required) The display method based on user action. Allowed values are: `closeRichMenu`, `openRichMenu`, `openKeyboard`, `openVoice`. |
| Fill In Text | (Required) When **Input Option** parameter is set to `openKeyboard` and the keyboard is opened, the default string in the input field.  |
| Clipboard Text | (Required) For `clipboard` type actions, the text to copy to the clipboard. |
| Rich Menu Alias ID | (Required) The rich menu alias ID to switch to. |

#### Template - Default Action

| **Parameter** | **Description** |
| --- | --- |
| Type | (Required) The type of action. Allowed values are: `postback`, `message`, `uri`, `datetimepicker`, `camera`, `cameraRoll`, `location`, `richmenuswitch`, `clipboard`. |
| Label | (Required) The label for the action. Specifications vary based on the object the action is set to. |
| Data | (Required) The string returned through the webhook in the `postback.data` property of the postback event. |
| Display Text | (Required) The text displayed on the LINE chat screen as a message sent by the user when the action is performed. |
| Text | (Required) For `message` type actions, the text sent when the action is performed. |
| URI | (Required) For `uri` type actions, the URI opened when the action is performed. The URL must use the HTTPS protocol.|
| Alternative URI - Desktop | (Required) For `uri` type actions, the URI opened on LINE for macOS and Windows when the action is performed.
| Mode | (Required) For `datetimepicker` type actions, the action mode. Allowed values are: `date`, `time`, `datetime`. |
| Initial | (Required) For `datetimepicker` type actions, the initial value of date or time. |
| Max | (Required) For `datetimepicker` type actions, the largest date or time value that can be selected. |
| Min | (Required) For `datetimepicker` type actions, the smallest date or time value that can be selected. |
| Input Option | (Required) The display method based on user action. Allowed values are: `closeRichMenu`, `openRichMenu`, `openKeyboard`, `openVoice`. |
| Fill In Text | (Required) When **Input Option** parameter is set to `openKeyboard` and the keyboard is opened, the default string in the input field.  |
| Clipboard Text | (Required) For `clipboard` type actions, the text to copy to the clipboard. |
| Rich Menu Alias ID | (Required) The rich menu alias ID to switch to. |

### Push Message - Template message (Confirm template)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Alternative Text | (Required) Alternative text for the message. The text must not exceed 400 characters. The text appears in notifications or chat lists. |
| Template - Text | (Required) The message text. Text without an image or title must not exceed 400 characters, and text with an image or title must not exceed 60 characters. |

#### Template - Actions

All Template - Actions parameters are arrays.

| **Parameter** | **Description** |
| --- | --- |
| Type | (Required) The type of action. Allowed values are: `postback`, `message`, `uri`, `datetimepicker`, `camera`, `cameraRoll`, `location`, `richmenuswitch`, and `clipboard`. |
| Label | (Required) The label for the action. Specifications vary based on the object the action is set to. |
| Data | (Required) The string returned through the webhook in the `postback.data` property of the postback event. |
| Display Text | (Required) The text displayed on the LINE chat screen as a message sent by the user when the action is performed. |
| Text | (Required) For `message` type actions, the text sent when the action is performed. |
| URI | (Required) For `uri` type actions, the URI opened when the action is performed. The URL must use the HTTPS protocol.|
| Alternative URI - Desktop | (Required) For `uri` type actions, the URI opened on LINE for macOS and Windows when the action is performed.
| Mode | (Required) For `datetimepicker` type actions, the action mode. Allowed values are: `date`, `time`, and `datetime`. |
| Initial | (Required) For `datetimepicker` type actions, the initial value of date or time. |
| Max | (Required) For `datetimepicker` type actions, the largest date or time value that can be selected. |
| Min | (Required) For `datetimepicker` type actions, the smallest date or time value that can be selected. |
| Input Option | (Required) The display method based on user action. Allowed values are: `closeRichMenu`, `openRichMenu`, `openKeyboard`, `openVoice`. |
| Fill In Text | (Required) When **Input Option** parameter is set to `openKeyboard` and the keyboard is opened, the default string in the input field.  |
| Clipboard Text | (Required) For `clipboard` type actions, the text to copy to the clipboard. |
| Rich Menu Alias ID | (Required) The rich menu alias ID to switch to. |

### Push Message - Template message (Carousel template)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Alternative Text | (Required) Alternative text for the carousel template. Maximum length of text is 400 characters. The alternative text appears in notifications or chat lists. |
| Image Aspect Ratio | (Required) The aspect ratio of the image. Allowed values are `rectangle` or `square`. The default value is `rectangle`. |
| Image Size | (Required) The size of the image. Allowed values are `cover` or `contain`. The default value is `cover`. |

#### Template - Columns

All Template - Columns parameters are arrays.

| **Parameter** | **Description** |
| --- | --- |
| Text | (Required) The message text. Text without an image or title must not exceed 120 characters, and text with an image or title must not exceed 60 characters. |
| Thumbnail Image URL | Required. The URL of the image&#39;s thumbnail. The URL must not exceed 2,000 characters and must use the HTTPS protocol. |
| Image Background Color | Required. The background color of the image in hexadecimal format. The default value is `#FFFFFF` (white). |
| Title | (Required) The title of the message. The title must not exceed 40 characters. |
| Actions | (Required) The action to execute when the item is tapped. |
| Templates | &lt;ul&gt;&lt;li&gt;Required. Provide templates to be referenced in the **Actions** parameter of the Template - Columns section. For more information, see [Templates Guide](/server-side/connectors/templates/about/)).&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

#### Template - Columns - Default Action

All Template - Columns - Default Action parameters are arrays.

| **Parameter** | **Description** |
| --- | --- |
| Type | (Required) The type of action. Allowed values are: `postback`, `message`, `uri`, `datetimepicker`, `camera`, `cameraRoll`, `location`, `richmenuswitch`, and `clipboard`. |
| Label | (Required) The label for the action. Specifications vary based on the object the action is set to. |
| Data | (Required) The string returned through the webhook in the `postback.data` property of the postback event. |
| Display Text | (Required) The text displayed on the LINE chat screen as a message sent by the user when the action is performed. |
| Text | (Required) For `message` type actions, the text sent when the action is performed. |
| URI | (Required) For `uri` type actions, the URI opened when the action is performed. The URL must use the HTTPS protocol.|
| Alternative URI - Desktop | (Required) For `uri` type actions, the URI opened on LINE for macOS and Windows when the action is performed. |
| Mode | (Required) For `datetimepicker` type actions, the action mode. Allowed values are: `date`, `time`, `datetime`. |
| Initial | Required. For `datetimepicker` type actions, the initial value of date or time. |
| Max | (Required) For `datetimepicker` type actions, the largest date or time value that can be selected. |
| Min | (Required) For `datetimepicker` type actions, the smallest date or time value that can be selected. |
| Input Option | (Required) The display method based on user action. Allowed values are: `closeRichMenu`, `openRichMenu`, `openKeyboard`, and `openVoice`. |
| Fill In Text | (Required) When **Input Option** parameter is set to `openKeyboard` and the keyboard is opened, the default string in the input field.  |
| Clipboard Text |(Required) For `clipboard` type actions, the text to copy to the clipboard. |
| Rich Menu Alias ID | (Required) The rich menu alias ID to switch to. |
| Template Variables | &lt;ul&gt;&lt;li&gt;(Required) Provide template variables as data. These fields map attributes to variable names that are used in the message data. Name nested template variables with dot notation. For example, `items.name`.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;/ul&gt; |

### Push Message - Template message (Image carousel template)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Alternative Text | (Required) Alternative text for the base image. Maximum text length is 400 characters. The alternative text appears in notifications or chat lists. |

#### Template - Columns parameters

All Template - Columns parameters are arrays.

| **Parameter** | **Description** |
| --- | --- |
| Image URL | (Required) The URL of the image&#39;s thumbnail. The URL must not exceed 2,000 characters and must use the HTTPS protocol. |
| Action - Type  | (Required) The type of action. Allowed values are: `postback`, `message`, `uri`, `datetimepicker`, `camera`, `cameraRoll`, `location`, `richmenuswitch`, and `clipboard`. |
| Action - Label | (Required) The label for the action. Specifications vary based on the object the action is set to. |
| Action - Data | (Required) The string returned through the webhook in the `postback.data` property of the postback event. |
| Action - Display Text | (Required) The text displayed on the LINE chat screen as a message sent by the user when the action is performed. |
| Action - Text | (Required) For `message` type actions, the text sent when the action is performed. |
| Action - URI | (Required) For `uri` type actions, the URI opened when the action is performed. The URL must use the HTTPS protocol. |
| Action - Alternative URI - Desktop | (Required) For `uri` type actions, the URI opened on LINE for macOS and Windows when the action is performed. |
| Action - Mode | (Required) For `datetimepicker` type actions, the action mode. Allowed values are: `date`, `time`, `datetime`. |
| Action - Initial | For `datetimepicker` type actions, the initial value of date or time. |
| Action - Max | (Required) For `datetimepicker` type actions, the largest date or time value that can be selected. |
| Action - Min | (Required) For `datetimepicker` type actions, the smallest date or time value that can be selected. |
| Action - Input Option | (Required) The display method based on user action. Allowed values are: `closeRichMenu`, `openRichMenu`, `openKeyboard`, and `openVoice`. |
| Action - Fill In Text | (Required) When **Input Option** parameter is set to `openKeyboard` and the keyboard is opened, the default string in the input field. |
| Action - Clipboard Text | (Required) For `clipboard` type actions, the text to copy to the clipboard. |
| Action - Rich Menu Alias ID | (Required) The rich menu alias ID to switch to. |

### Push Message - Flex

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Alternative Text | (Required) Alternative text for the base image. Maximum text length is 400 characters long. The alternative text appears in notifications or chat lists. |
| Contents | (Required) The contents of the flex message container. |
| Template Variables  | These fields map attributes to variable names that are used in the message data. Name nested template variables with dot notation. For example, `items.name`. For more information, see . |
| Templates | &lt;ul&gt;&lt;li&gt;(Required) Provide templates to be referenced in the Message Data section. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |
| Contact ID | (Required) This parameter is the ID received from the webhook that is configured in the **Channel Console** in the LINE Business Center. When a user performs an action such as adding an account or sending a message, an HTTPS POST request is sent to the webhook URL. |
| Alternative Text | (Required) Alternative text for the base image. Maximum text length is 400 characters long. The alternative text appears in notifications or chat lists. |
| Contents | (Required) The contents of the flex message container. |
| Template Variables  | These fields map attributes to variable names that are used in the message data. Name nested template variables with dot notation. For example, `items.name`. For more information, see . |
| Templates | &lt;ul&gt;&lt;li&gt;(Required) Provide templates to be referenced in the Message Data section. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example: `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [LINE: Developers - Messaging API](https://developers.line.biz/en/docs/messaging-api/)
* [LINE: API Reference - Webhooks](https://developers.line.biz/en/reference/messaging-api/#webhooks)
* [LINE: API Reference - Push Message](https://developers.line.biz/en/reference/messaging-api/#send-push-message)
* [LINE: API Reference - Send Message Object (Text, Image, Sticker, etc.)](https://developers.line.biz/en/docs/messaging-api/sending-messages/)

##### Additional References

* .