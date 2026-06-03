---
title: Adobe Heartbeat Tag Setup Guide
description: This article describes how to set up the Adobe Heartbeat Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adobe-heartbeat-tag/
---
## How it Works

The Adobe Heartbeat tag lets you collect extensive data on how visitors interact with videos on your site. When your video loads on a page, Heartbeat triggers server calls every second through the length of the video, capturing its playhead positions, pause and resume actions, ad views, and several other video performance parameters. Additionally, if your implementation is integrated with the Nielsen DCR plugin, you can configure those parameters together in this tag.

## Prerequisites

* **jQuery**  
Ensure that your site has jQuery installed on it. If you are not using jQuery, you can add and configure a new jQuery tag from the Tealium iQ tag Marketplace.
* **Adobe Enterprise Cloud ID Service Tag**  
[The Adobe Cloud Service](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) generates a unique ID for every visitor on your site and persists the ID across all their Enterprise Cloud Solutions, thus preventing duplicate counts. Add and configure the tag in your profile, if you have not already done and enable the bundle flag setting for the tag so that it can be bundled into `utag.js` on all pages.
* [**AppMeasurement JavaScript Tag**](/client-side-tags/adobe-appmeasurement-for-js-tag/)  
Add and configure the tag in the same profile and enable the bundle flag, if you have not done so already. This is required for JavaScript implementations. Bundling is only required for Tag version 1.6.3, as the prior versions already have the Enterprise Cloud Service bundled by default.  
In the Tags tab, ensure that the bundled Enterprise Cloud ID tag is placed above the bundled AppMeasurement tag. This ensures the Enterprise Cloud ID tag will load first.

## Supported Vendor Libraries

* Adobe Heartbeat v2.0.2 (default)
* Adobe Heartbeat v1.6.7
* Adobe Heartbeat v1.6.7 with Nielsen v5.0 integration

## Tag Tips

* Heartbeat requires the Adobe Experience Cloud ID Service as well as AppMeasurement for JS to be loaded first, preferably bundled.
* This tag is fired with &#34;utag.track(&#39;video&#39;, data);&#34; which should be implemented in your video event handlers.
* jQuery is required by Adobe Heartbeat.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Adobe Heartbeat tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

|FIELD NAME| FIELD VALUE|
|---| ---|
|Title|  &lt;ul&gt;&lt;li&gt;(Required) Enter a unique name to identify the tag.&lt;/li&gt;&lt;li&gt;This is important if you are adding multiple instances of this tag.&lt;/li&gt;&lt;/ul&gt; |
|Tracking Server|  &lt;ul&gt;&lt;li&gt;(Required) Adobe Heartbeat tracking server.&lt;/li&gt;&lt;li&gt;Enter the server URL where all heartbeat tracking calls are sent.&lt;/li&gt;&lt;li&gt;If you do not have the URL, contact your Adobe representative.&lt;/li&gt;&lt;li&gt;For example, `.hb.omtrdc.net`&lt;/li&gt;&lt;/ul&gt; |
|Publisher|  &lt;ul&gt;&lt;li&gt;(Required) Enter your publisher name as assigned by your Adobe representative.&lt;/li&gt;&lt;/ul&gt; |
|Use SSL|  &lt;ul&gt;&lt;li&gt;This flag determines whether or not to send heartbeat calls over HTTPS.&lt;/li&gt;&lt;li&gt;The default value is `False`, meaning SSL is disabled.&lt;/li&gt;&lt;li&gt;You may toggle the value to `True` if you prefer the tracking calls are sent securely.&lt;/li&gt;&lt;/ul&gt; |
|S-Object Name|  &lt;ul&gt;&lt;li&gt;(Required) Set your own custom s-object variable name.&lt;/li&gt;&lt;li&gt;If you are unsure, use the default value of `s`.&lt;/li&gt;&lt;/ul&gt; |
|Video Platform Name|  &lt;ul&gt;&lt;li&gt;(Optional) The name of the online video platform through which content gets distributed.&lt;/li&gt;&lt;/ul&gt; |
|Video Player SDK|  &lt;ul&gt;&lt;li&gt;(Optional) The version of the video player app/SDK.&lt;/li&gt;&lt;/ul&gt; |
|Tag Version|  &lt;ul&gt;&lt;li&gt;This drop-down list lets you choose Adobe Heartbeat tracking with or without Nielsen integration.&lt;/li&gt;&lt;li&gt;The available options are:  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat 2.0.2 (default)&lt;/li&gt;&lt;li&gt;Adobe Heartbeat 1.6.7&lt;/li&gt;&lt;li&gt;Adobe Heartbeat 1.6.7 with Nielsen 5.0&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

The following fields are only required if you set the tag version to **Adobe Heartbeat 1.6.7 with Nielsen 5.0**. If you do not have the required Nielsen values, contact your Nielsen or Adobe representative.

|FIELD NAME| FIELD VALUE|
|---| ---|
|Adobe Nielsen SDK Configuration Key|  &lt;ul&gt;(Required for Nielsen) Enter the Nielsen configuration key&lt;/li&gt;&lt;li&gt;Configuration SDK key for Nielsen integration with Adobe Heartbeat.&lt;/li&gt;&lt;/ul&gt; |
|Nielsen Collection Environment|  &lt;ul&gt;(Required for Nielsen) Location of collection environment.&lt;/li&gt;&lt;li&gt;Enter the location of Nielsen&#39;s collection environment&lt;/li&gt;&lt;li&gt;For example, `eu-cert` or `eu`.&lt;/li&gt;&lt;/ul&gt; |
|Nielsen Player ID|  &lt;ul&gt;(Required for Nielsen) Enter the unique identifier assigned to the video player&lt;/li&gt;&lt;li&gt;Unique ID assigned to player/site, provided by Nielsen.&lt;/li&gt;&lt;/ul&gt; |
|Nielsen APN|  &lt;ul&gt;(Required for Nielsen) Enter a description for the player/site&lt;/li&gt;&lt;li&gt;User-defined string value for describing the player/site.&lt;/li&gt;&lt;/ul&gt; |
|Nielsen Client ID|  &lt;ul&gt;(Required for Nielsen) Enter your Nielsen client identifier&lt;/li&gt;&lt;li&gt;Unique ID for VA Beacon Measurement.&lt;/li&gt;&lt;/ul&gt; |
|Nielsen VCID|  &lt;ul&gt;(Required for Nielsen) Enter the video channel identifier.&lt;/li&gt;&lt;li&gt;Unique ID for VA Beacon Measurement.&lt;/li&gt;&lt;/ul&gt; |

## Apply Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site. The Load on All Pages rule is the default load rule. To load this tag on a specific page, create relevant rule conditions to apply to the tag.

Best Practice: Create and apply custom rules to load this tag on any pages where videos are made available.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The following sections provide detailed tables for each available category.

### Standard

The Standard category corresponds to the [configuration fields for the tag](#tag_configs). You can map values to these destinations. Dynamically send values for the tag fields that are left blank or override the current values.

|Destination Name| Description|
|---| ---|
|`tracking_server`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat Tracking Server.&lt;/li&gt;&lt;li&gt;URL of the server where all heartbeat tracking calls are sent.&lt;/li&gt;&lt;/ul&gt; |
|`publisher`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat Publisher.&lt;/li&gt;&lt;li&gt;Publisher name as assigned by your Adobe representative.&lt;/li&gt;&lt;/ul&gt; |
|`ssl`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat SSL Flag.&lt;/li&gt;&lt;li&gt;Boolean flag that determines whether or not to send heartbeat calls over HTTPS.&lt;/li&gt;&lt;li&gt;Ensure the variable you are mapping is populated with a Boolean value, either `true` or `false`.&lt;/li&gt;&lt;li&gt;Mapping overrides the current drop-down selection.&lt;/li&gt;&lt;/ul&gt; |
|`syndication_channel`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat Channel.&lt;/li&gt;&lt;li&gt;Name of the channel syndication.&lt;/li&gt;&lt;/ul&gt; |
|`online_video_platform_name`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat Video Platform Name.&lt;/li&gt;&lt;li&gt;Name of the online platform that is rendering your video content.&lt;/li&gt;&lt;/ul&gt; |
|`player_sdk`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat Player SDK.&lt;/li&gt;&lt;li&gt;Version of the video player app/SDK.&lt;/li&gt;&lt;/ul&gt; |
|`debug_logging`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat Debug Logging Flag.&lt;/li&gt;&lt;li&gt;Boolean flag to enable/disable logging of each component within the Heartbeat plugin.&lt;/li&gt;&lt;li&gt;Adobe recommends disabling this flag for the production version of your player because active logging impacts performance.&lt;/li&gt;&lt;/ul&gt; |

The following fields are only required if you set the tag version to **Adobe Heartbeat 1.6.7 with Nielsen 5.0**. If you do not have the required Nielsen values, contact your Nielsen or Adobe representative.

|Destination Name| Description|
|---| ---|
|`nielsen_config_key`|  &lt;ul&gt;&lt;li&gt;Adobe Nielsen SDK Configuration Key.&lt;/li&gt;&lt;li&gt;Nielsen configuration key to integrate with Adobe Heartbeat.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_client_id`|  &lt;ul&gt;&lt;li&gt;Nielsen Client ID.&lt;/li&gt;&lt;li&gt;Your Nielsen client identifier.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_vcid`|  &lt;ul&gt;&lt;li&gt;Nielsen VCID.&lt;/li&gt;&lt;li&gt;Video channel identifier.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_collection_environment`|  &lt;ul&gt;&lt;li&gt;Nielsen Collection Environment.&lt;/li&gt;&lt;li&gt;Location of Nielsen&#39;s collection environment.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_player_id`|  &lt;ul&gt;&lt;li&gt;Nielsen Player ID.&lt;/li&gt;&lt;li&gt;The unique identifier for the video player.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_apn`|  &lt;ul&gt;&lt;li&gt;Nielsen APN.&lt;/li&gt;&lt;li&gt;Description of the player/site, expressed as a string value.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_device_id`|  &lt;ul&gt;&lt;li&gt;Nielsen Device ID.&lt;/li&gt;&lt;li&gt;Unique identifier of mobile/tablet where you want to track the video.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_sdk_debug`|  &lt;ul&gt;&lt;li&gt;Nielsen SDK Debug Flag.&lt;/li&gt;&lt;li&gt;Boolean flag to enable/disable logging of the Nielsen integration.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_opt_out`|  &lt;ul&gt;&lt;li&gt;Nielsen Opt Out Flag.&lt;/li&gt;&lt;li&gt;Disable all Nielsen tracking for the current visitor.&lt;/li&gt;&lt;li&gt;Requires triggering the `opt-out` event.&lt;/li&gt;&lt;/ul&gt; |

### Video Events

Video event destinations are event listeners that trigger when a certain action or change occurs in the video player. To trigger an event, you must map your variable to an event in the toolbox and set the value of the variable as the trigger. The mapped event fires when the supplied trigger value is found in the data layer.

The following tables lists the available event destinations:

|Destination Name| Description|
|---| ---|
|`video_load`|  &lt;ul&gt;&lt;li&gt;Video Load.&lt;/li&gt;&lt;li&gt;Indicates the video is ready to be played.&lt;/li&gt;&lt;/ul&gt; |
|`video_start`|  &lt;ul&gt;&lt;li&gt;Video Start.&lt;/li&gt;&lt;li&gt;Indicates the video has started playing, possibly after one of the following three (3) scenarios:  &lt;ul&gt;&lt;li&gt;initial loading&lt;/li&gt;&lt;li&gt;buffering&lt;/li&gt;&lt;li&gt;ad display&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`video_playing`|  &lt;ul&gt;&lt;li&gt;Video Playing.&lt;/li&gt;&lt;li&gt;Indicates that the video is currently playing.&lt;/li&gt;&lt;li&gt;Use to update QoS data.&lt;/li&gt;&lt;li&gt;Should not be called when ads are playing.&lt;/li&gt;&lt;/ul&gt; |
|`video_pause`|  &lt;ul&gt;&lt;li&gt;Video Pause.&lt;/li&gt;&lt;li&gt;Indicates that video was paused.&lt;/li&gt;&lt;/ul&gt; |
|`video_play`|  &lt;ul&gt;&lt;li&gt;Video Play.&lt;/li&gt;&lt;li&gt;Indicates that the video is playing, possibly after the buffering or seeking has completed.&lt;/li&gt;&lt;/ul&gt; |
|`video_stop`|  &lt;ul&gt;&lt;li&gt;Video Stop.&lt;/li&gt;&lt;li&gt;Indicates that the video has been manually stopped.&lt;/li&gt;&lt;/ul&gt; |
|`video_resume`|  &lt;ul&gt;&lt;li&gt;Video Resume.&lt;/li&gt;&lt;li&gt;Indicates the viewer has unpaused the video to resume playing.&lt;/li&gt;&lt;/ul&gt; |
|`video_complete`|  &lt;ul&gt;&lt;li&gt;Video Complete.&lt;/li&gt;&lt;li&gt;Indicates that the video has ended.&lt;/li&gt;&lt;/ul&gt; |
|`video_seek`|  &lt;ul&gt;&lt;li&gt;Video Seek.&lt;/li&gt;&lt;li&gt;Indicates the viewer has started seeking the video.&lt;/li&gt;&lt;/ul&gt; |
|`video_buffer`|  &lt;ul&gt;&lt;li&gt;Video Buffer.&lt;/li&gt;&lt;li&gt;Indicates the video has started buffering.&lt;/li&gt;&lt;/ul&gt; |
|`video_skip`|  &lt;ul&gt;&lt;li&gt;Video Skip.&lt;/li&gt;&lt;li&gt;Indicates the viewer has skipped the video or ad.&lt;/li&gt;&lt;/ul&gt; |
|`video_error`|  &lt;ul&gt;&lt;li&gt;Video Error.&lt;/li&gt;&lt;li&gt;Indicates the video has encountered an error.&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_opt_out_status_changed`|  &lt;ul&gt;&lt;li&gt;Nielsen Opt Out Status Change.&lt;/li&gt;&lt;li&gt;Indicates the viewer has switched from opt-in to opt-out OR vice-versa.&lt;/li&gt;&lt;/ul&gt; |

### Video

These destinations correspond to the [Adobe Video Measurement parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html).

|Destination Name| Description|
|---| ---|
|`video.id`|  &lt;ul&gt;&lt;li&gt;Video ID.&lt;/li&gt;&lt;li&gt;Unique identifier of the video.&lt;/li&gt;&lt;/ul&gt; |
|`video.title`|  &lt;ul&gt;&lt;li&gt;Video Title.&lt;/li&gt;&lt;li&gt;Name of the video being tracked.&lt;/li&gt;&lt;/ul&gt; |
|`video.length`|  &lt;ul&gt;&lt;li&gt;Video Length.&lt;/li&gt;&lt;li&gt;The duration (in seconds) of the video asset.&lt;/li&gt;&lt;/ul&gt; |
|`video.current_playhead`|  &lt;ul&gt;&lt;li&gt;Video Current Playhead.&lt;/li&gt;&lt;li&gt;The current position of the player (in seconds) in the video, excluding ad content.&lt;/li&gt;&lt;/ul&gt; |
|`video.stream_type`|  &lt;ul&gt;&lt;li&gt;Video Stream Type.&lt;/li&gt;&lt;li&gt;Type of the video asset.&lt;/li&gt;&lt;/ul&gt; |
|`video.is_full_episode`|  &lt;ul&gt;&lt;li&gt;Video Is Full Episode.&lt;/li&gt;&lt;li&gt;Boolean flag to indicate if the video content is a full episode.  &lt;ul&gt;&lt;li&gt;`Y` for full episode.&lt;/li&gt;&lt;li&gt;`N` for a partial clip.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`video.original_air_date_nielsen`|  &lt;ul&gt;&lt;li&gt;Video Original Air Date For Nielsen.&lt;/li&gt;&lt;li&gt;The original air date of the episode, format.&lt;/li&gt;&lt;li&gt;For example, `YYYYMMDDHH24:MI:SS`&lt;/li&gt;&lt;/ul&gt; |
|`video.channel_name`|  &lt;ul&gt;&lt;li&gt;Video Channel Name.&lt;/li&gt;&lt;li&gt;Name of the program or feed being sent.&lt;/li&gt;&lt;/ul&gt; |
|`video.series_name`|  &lt;ul&gt;&lt;li&gt;Video Series Name.&lt;/li&gt;&lt;li&gt;Name of the program (series name) being viewed.&lt;/li&gt;&lt;/ul&gt; |
|`video.player_name`|  &lt;ul&gt;&lt;li&gt;Video Player Name.&lt;/li&gt;&lt;li&gt;Name of the video player that is playing the content.&lt;/li&gt;&lt;/ul&gt; |
|`video.is_ad`|  &lt;ul&gt;&lt;li&gt;Video Is Ad.&lt;/li&gt;&lt;li&gt;Boolean value to indicate whether or not the video is an advertisement.&lt;/li&gt;&lt;/ul&gt; |
|`video.fps`|  &lt;ul&gt;&lt;li&gt;Video FPS.&lt;/li&gt;&lt;li&gt;The frame rate of the media, in frames per second (FPS).&lt;/li&gt;&lt;/ul&gt; |
|`video.bit_rate`|  &lt;ul&gt;&lt;li&gt;Video Bitrate.&lt;/li&gt;&lt;li&gt;The bits per second attribute of the video content.&lt;/li&gt;&lt;/ul&gt; |
|`video.startup.time`|  &lt;ul&gt;&lt;li&gt;Video Startup Time.&lt;/li&gt;&lt;li&gt;The start time, in seconds, of the video content.&lt;/li&gt;&lt;/ul&gt; |
|`video.dropped_frames`|  &lt;ul&gt;&lt;li&gt;Video Dropped Frames.&lt;/li&gt;&lt;li&gt;The sum of all frames dropped during a playback session.&lt;/li&gt;&lt;/ul&gt; |
|`video.error_id`|  &lt;ul&gt;&lt;li&gt;Video Error ID.&lt;/li&gt;&lt;li&gt;The ID of the error encountered during playback.&lt;/li&gt;&lt;/ul&gt; |
|`video.error_is_fatal`|  &lt;ul&gt;&lt;li&gt;Video Error Is Fatal.&lt;/li&gt;&lt;li&gt;Boolean value to indicate whether or not the error prevents playback from continuing.&lt;/li&gt;&lt;/ul&gt; |

### Chapter

These destinations correspond to [Adobe Video Chapter Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html).

|Destination Name| Description|
|---| ---|
|`chapter.name`|  &lt;ul&gt;&lt;li&gt;Chapter Name.&lt;/li&gt;&lt;li&gt;Name of the individual chapters.&lt;/li&gt;&lt;/ul&gt; |
|`chapter.length`|  &lt;ul&gt;&lt;li&gt;Chapter Length.&lt;/li&gt;&lt;li&gt;Total duration of the chapter in seconds.&lt;/li&gt;&lt;/ul&gt; |
|`chapter.position`|  &lt;ul&gt;&lt;li&gt;Chapter Position.&lt;/li&gt;&lt;li&gt;Position of the chapter inside the video content.&lt;/li&gt;&lt;/ul&gt; |
|`chapter.start_time`|  &lt;ul&gt;&lt;li&gt;Chapter Start Time.&lt;/li&gt;&lt;li&gt;The offset inside the main content where the chapter starts.&lt;/li&gt;&lt;/ul&gt; |
|`chapter_meta_data.custom`|  &lt;ul&gt;&lt;li&gt;Chapter Custom Metadata.&lt;/li&gt;&lt;li&gt;Additional custom value related to the chapter.&lt;/li&gt;&lt;/ul&gt; |

### Ad

These destinations correspond to [Adobe Video Ad Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html).

|Destination Name| Description|
|---| ---|
|`adbreak.name`|  &lt;ul&gt;&lt;li&gt;Ad Break Name.&lt;/li&gt;&lt;li&gt;The name of the individual cad breaks.&lt;/li&gt;&lt;/ul&gt; |
|`adbreak.position`|  &lt;ul&gt;&lt;li&gt;Ad Break Position.&lt;/li&gt;&lt;li&gt;The position (index) of the ad break inside the video content.&lt;/li&gt;&lt;li&gt;Required when the `video.is_ad` flag is set to `True`.&lt;/li&gt;&lt;/ul&gt; |
|`dbreak.start_time`|  &lt;ul&gt;&lt;li&gt;Ad Break Start Time.&lt;/li&gt;&lt;li&gt;The offset inside the main content where the ad break starts.&lt;/li&gt;&lt;/ul&gt; |
|`ad.id`|  &lt;ul&gt;&lt;li&gt;Ad ID.&lt;/li&gt;&lt;li&gt;Unique identifier of the ad being displayed.&lt;/li&gt;&lt;/ul&gt; |
|`ad.title`|  &lt;ul&gt;&lt;li&gt;Ad Title.&lt;/li&gt;&lt;li&gt;Name of the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad.type`|  &lt;ul&gt;&lt;li&gt;Ad Type.&lt;/li&gt;&lt;li&gt;Type or category of the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad.length`|  &lt;ul&gt;&lt;li&gt;Ad Length.&lt;/li&gt;&lt;li&gt;Total duration of the ad (in seconds).&lt;/li&gt;&lt;/ul&gt; |
|`ad.position`|  &lt;ul&gt;&lt;li&gt;Ad Position.&lt;/li&gt;&lt;li&gt;The position (index) of the ad inside the video content.&lt;/li&gt;&lt;li&gt;Required when the `video.is_ad` flag is set to `True`.&lt;/li&gt;&lt;/ul&gt; |

### Video Metadata

These destinations correspond to [Adobe Standard Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html).

|Destination Name| Description|
|---| ---|
|`meta_data.custom`|  &lt;ul&gt;&lt;li&gt;Video Custom Metadata.&lt;/li&gt;&lt;li&gt;Additional custom value related to the video.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.show`|  &lt;ul&gt;&lt;li&gt;Video Metadata Show.&lt;/li&gt;&lt;li&gt;Name of the show.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.season`|  &lt;ul&gt;&lt;li&gt;Video Metadata Season.&lt;/li&gt;&lt;li&gt;The season number.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.episode`|  &lt;ul&gt;&lt;li&gt;Video Metadata Episode.&lt;/li&gt;&lt;li&gt;The episode number.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.asset`|  &lt;ul&gt;&lt;li&gt;Video Metadata Asset.&lt;/li&gt;&lt;li&gt;The video asset identifier also known as TMS ID (Tribune Media Service).&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.genre`|  &lt;ul&gt;&lt;li&gt;Video Metadata Genre.&lt;/li&gt;&lt;li&gt;Genre of the video content.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.airDate`|  &lt;ul&gt;&lt;li&gt;Video Metadata Air Date.&lt;/li&gt;&lt;li&gt;The date on which the asset was first aired on TV.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.digitalDate`|  &lt;ul&gt;&lt;li&gt;Video Metadata Digital Air Date.&lt;/li&gt;&lt;li&gt;The date on which the asset was first available as digital.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.rating`|  &lt;ul&gt;&lt;li&gt;Video Metadata Rating.&lt;/li&gt;&lt;li&gt;Ratings available for the video content.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.originator`|  &lt;ul&gt;&lt;li&gt;Video Metadata Originator.&lt;/li&gt;&lt;li&gt;Name of the video originator.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.network`|  &lt;ul&gt;&lt;li&gt;Video Metadata Network.&lt;/li&gt;&lt;li&gt;The name of the network associated with the show.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.type`|  &lt;ul&gt;&lt;li&gt;Video Metadata Type.&lt;/li&gt;&lt;li&gt;Type of the show.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.adLoad`|  &lt;ul&gt;&lt;li&gt;Video Metadata Ad Load.&lt;/li&gt;&lt;li&gt;Metadata for the ad load.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.dayPart`|  &lt;ul&gt;&lt;li&gt;Video Metadata Day Part.&lt;/li&gt;&lt;li&gt;The day part for which the ad display is scheduled.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.feed`|  &lt;ul&gt;&lt;li&gt;Video Metadata Feed.&lt;/li&gt;&lt;li&gt;The type of programming feed.&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.format`|  &lt;ul&gt;&lt;li&gt;Video Metadata Format.&lt;/li&gt;&lt;li&gt;Stream format of the video.&lt;/li&gt;&lt;/ul&gt; |

### Ad Metadata

These destinations correspond to [Adobe Standard Ad Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html).

|Destination Name| Description|
|---| ---|
|`ad_meta_data.custom`|  &lt;ul&gt;&lt;li&gt;Ad Custom Metadata.&lt;/li&gt;&lt;li&gt;Additional custom value related to the ad being displayed.&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.advertiser`|  &lt;ul&gt;&lt;li&gt;Ad Metadata Advertiser.&lt;/li&gt;&lt;li&gt;Name of the company/brand that is displaying the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.campaign`|  &lt;ul&gt;&lt;li&gt;Ad Metadata Campaign.&lt;/li&gt;&lt;li&gt;Ad campaign Identifier.&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.creative`|  &lt;ul&gt;&lt;li&gt;Ad Metadata Creative.&lt;/li&gt;&lt;li&gt;Creative asset for rendering the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.placement`|  &lt;ul&gt;&lt;li&gt;Ad Metadata Placement.&lt;/li&gt;&lt;li&gt;Metadata related to the position of the ad inside the video.&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.site`|  &lt;ul&gt;&lt;li&gt;Ad Metadata Site.&lt;/li&gt;&lt;li&gt;Site associated with the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.creativeURL`|  &lt;ul&gt;&lt;li&gt;Ad Metadata Creative URL.&lt;/li&gt;&lt;li&gt;URL of the ad being displayed.&lt;/li&gt;&lt;/ul&gt; |

## Built-in Video Data Layer Variables

Mapping is not required if your data layer is already using these values. Tealium typically sends data to the matching tag destinations. If your data layer uses different variables names from those listed in this table, then you will need to manually map.

|Built-in Variables| Toolbox Destination Variable| Description|
|---| ---| ---|
|`event_name`| [Video Event destinations](#video_events_mapping)|  If you use any of the following values in your `event_name` variable, you do not need to map again in the toolbox. &lt;ul&gt;&lt;li&gt;`load` is mapped to `video_load`&lt;/il&gt;&lt;li&gt;`start` is mapped to `video_start`&lt;/il&gt;&lt;li&gt;`playing` is mapped to `video_playing`&lt;/il&gt;&lt;li&gt;`pause` is mapped to `video_pause`&lt;/il&gt;&lt;li&gt;`play` is mapped to `video_play`&lt;/il&gt;&lt;li&gt;`stop` is mapped to `video_stop`&lt;/il&gt;&lt;li&gt;`resume` is mapped to `video_resume`&lt;/il&gt;&lt;li&gt;`complete` is mapped to `video_complete`&lt;/il&gt;&lt;li&gt;`seek` is mapped to `video_seek`&lt;/il&gt;&lt;li&gt;`buffer` is mapped to `video_buffer`&lt;/il&gt;&lt;li&gt;`optstatus` is mapped to `Nielsen_opt_out_status_changed`&lt;/li&gt;&lt;/ul&gt; |
|`video_id`| --|  &lt;ul&gt;&lt;li&gt;Unique identifier of the video.&lt;/li&gt;&lt;/ul&gt; |
|`video_name`| `video.title`|  &lt;ul&gt;&lt;li&gt;Video Title.&lt;/li&gt;&lt;li&gt;Name of the video being tracked.&lt;/li&gt;&lt;/ul&gt; |
|`video_length`| `video.length`|  &lt;ul&gt;&lt;li&gt;Video Length.&lt;/li&gt;&lt;li&gt;The duration (in seconds) of the video asset.&lt;/li&gt;&lt;/ul&gt; |
|`video_player_name`| `video.player_name`|  &lt;ul&gt;&lt;li&gt;Video Player Name.&lt;/li&gt;&lt;li&gt;Name of the video player that is playing the content.&lt;/li&gt;&lt;/ul&gt; |
|`video_current_playhead`| `video.current_playhead`|  &lt;ul&gt;&lt;li&gt;Video Current Playhead.&lt;/li&gt;&lt;li&gt;The current position of the player (in seconds) in the video, excluding ad content.&lt;/li&gt;&lt;/ul&gt; |
|`video_stream_type`| `video.stream_type`|  &lt;ul&gt;&lt;li&gt;Video Stream Type.&lt;/li&gt;&lt;li&gt;Type of the video asset.&lt;/li&gt;&lt;/ul&gt; |
|`video_fps`| `video.fps`|  &lt;ul&gt;&lt;li&gt;Video FPS.&lt;/li&gt;&lt;li&gt;The frame rate of the media, in frames per second (FPS).&lt;/li&gt;&lt;/ul&gt; |
|`video_bitrate`| `video.bit_rate`|  &lt;ul&gt;&lt;li&gt;Video Bitrate.&lt;/li&gt;&lt;li&gt;The bits per second attribute of the video content.&lt;/li&gt;&lt;/ul&gt; |
|`video_dropped_frames`| `video.dropped_frames`|  &lt;ul&gt;&lt;li&gt;Video Dropped Frames.&lt;/li&gt;&lt;li&gt;The sum of all frames dropped during a playback session.&lt;/li&gt;&lt;/ul&gt; |
|`video_is_ad`| `video.is_ad`|  &lt;ul&gt;&lt;li&gt;Video Is Ad.&lt;/li&gt;&lt;li&gt;Boolean value to indicate whether or not the video is an advertisement.&lt;/li&gt;&lt;/ul&gt; |
|`video_ad_position` - OR - `video_ad_pod_position`| `ad.position`|  &lt;ul&gt;&lt;li&gt;Ad Position.&lt;/li&gt;&lt;li&gt;The position (index) of the ad inside the video content.&lt;/li&gt;&lt;li&gt;Required when the `video.is_ad `flag is set to `true`.&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_name`| `chapter.name`|  &lt;ul&gt;&lt;li&gt;Chapter Name.&lt;/li&gt;&lt;li&gt;Name of the individual chapters.&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_length`| `chapter.length`|  &lt;ul&gt;&lt;li&gt;Chapter Length.&lt;/li&gt;&lt;li&gt;Total duration of the chapter in seconds.&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_position`| `chapter.position`|  &lt;ul&gt;&lt;li&gt;Chapter Position.&lt;/li&gt;&lt;li&gt;Position of the chapter inside the video content.&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_start_time`| `chapter.start_time`|  &lt;ul&gt;&lt;li&gt;Chapter Start Time.&lt;/li&gt;&lt;li&gt;The offset inside the main content where the chapter starts.&lt;/li&gt;&lt;/ul&gt; |
|`video_ad_pod_name`| `ad.id`|  &lt;ul&gt;&lt;li&gt;Ad ID.&lt;/li&gt;&lt;li&gt;Unique identifier of the ad being displayed.&lt;/li&gt;&lt;/ul&gt; |
|`program`| `video.series_name`|  &lt;ul&gt;&lt;li&gt;Video Series Name.&lt;/li&gt;&lt;li&gt;Name of the program (series name) being viewed.&lt;/li&gt;&lt;/ul&gt; |
|`is_full_episode`| `video.is_full_episode`|  &lt;ul&gt;&lt;li&gt;Video Is Full Episode.&lt;/li&gt;&lt;li&gt;Boolean flag to indicate if the video content is a full episode.  &lt;ul&gt;&lt;li&gt;`Y` for full episode&lt;/li&gt;&lt;li&gt;`N` for a partial clip&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`original_air_date`| `video.original_air_date_nielsen`|  &lt;ul&gt;&lt;li&gt;Video Original Air Date For Nielsen.&lt;/li&gt;&lt;li&gt;The original air date of the episode, in the following format: `YYYYMMDDHH24:MI:SS`&lt;/li&gt;&lt;/ul&gt; |

## Validation

The Heartbeat tag is event-based and leverages the `utag.track(&#34;video&#34;, data)` call to differentiate itself from other utag calls. For this reason, it is crucial to properly set up the [video event triggers in the Data Mapping toolbox](#video_events_mapping).

Once configured, the tag fires continuously every second to keep the video data current. This is accomplished by firing the &#34;playing&#34; event within your video player&#39;s &#34;playing&#34; event handler. Other video events should also be fired through their corresponding Adobe heartbeat events. Network calls are aggregated and reported to Adobe every 10 seconds; including those for event changes.

An easy way to set both the Heartbeat and Nielsen debug flags is by adding a querystring parameter to the URL of the video page. For For example, `adobe_debug=1&amp;Nielsen=1` &lt;br&gt;You can then add the Query parameter variables to your data layer in Tealium iQ and map them accordingly.&lt;br&gt;Mapping destinations for both the Heartbeat and Nielsen debug flags are available under the Standard category. See &#34;Adobe Heartbeat Debug Logging Flag&#34; and &#34;Nielsen SDK Debug Flag&#34;.&lt;br&gt;When complete, you can run the following Tealium debug command in your browser console. &lt;br&gt;
`document.cookie = &#34;utagdb=true&#34;;`

### Sample Implementation

The following examples show network calls for a sample Heartbeat implementation. Primary parameters to note are `s:event:type` and `s:asset:type`. These parameters, respectively, indicate the type of video event and which video component it pertains to. The example shows the beginning of the main video before the ad display. The `l:event:playhead`, also shown, refers to the elapsed time on the main video.

The `s:asset:type` value equals `ad` and the `l:event:playhead` value is `8`. This means that the ad started playing at 8 seconds into the video.

## Vendor Documentation

* [About Adobe Video Heartbeat](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/)
* [Video Heartbeat Library Configuration](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_setup-and-config.html)
* [Nielsen appinfo Parameters](https://marketing.adobe.com/resources/help/en_US/dtm/nielsen.html)
* [Video Measurement Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/c_vhl_ios_video_params.html)
* [Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/c_vhl_stand-metadata_params_ios.html)
* [Video Player Event](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_js_events.html)
