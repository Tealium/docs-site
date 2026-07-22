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
* [**AppMeasurement JavaScript Tag**](https://docs.tealium.com/client-side-tags/adobe-appmeasurement-for-js-tag/)  
Add and configure the tag in the same profile and enable the bundle flag, if you have not done so already. This is required for JavaScript implementations. Bundling is only required for Tag version 1.6.3, as the prior versions already have the Enterprise Cloud Service bundled by default.  

<blockquote>
In the Tags tab, ensure that the bundled Enterprise Cloud ID tag is placed above the bundled AppMeasurement tag. This ensures the Enterprise Cloud ID tag will load first.
</blockquote>


## Supported Vendor Libraries

* Adobe Heartbeat v2.0.2 (default)
* Adobe Heartbeat v1.6.7
* Adobe Heartbeat v1.6.7 with Nielsen v5.0 integration

## Tag Tips

* Heartbeat requires the Adobe Experience Cloud ID Service as well as AppMeasurement for JS to be loaded first, preferably bundled.
* This tag is fired with "utag.track('video', data);" which should be implemented in your video event handlers.
* jQuery is required by Adobe Heartbeat.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Adobe Heartbeat tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

|FIELD NAME| FIELD VALUE|
|---| ---|
|Title|  <ul><li>(Required) Enter a unique name to identify the tag.</li><li>This is important if you are adding multiple instances of this tag.</li></ul> |
|Tracking Server|  <ul><li>(Required) Adobe Heartbeat tracking server.</li><li>Enter the server URL where all heartbeat tracking calls are sent.</li><li>If you do not have the URL, contact your Adobe representative.</li><li>For example, `.hb.omtrdc.net`</li></ul> |
|Publisher|  <ul><li>(Required) Enter your publisher name as assigned by your Adobe representative.</li></ul> |
|Use SSL|  <ul><li>This flag determines whether or not to send heartbeat calls over HTTPS.</li><li>The default value is `False`, meaning SSL is disabled.</li><li>You may toggle the value to `True` if you prefer the tracking calls are sent securely.</li></ul> |
|S-Object Name|  <ul><li>(Required) Set your own custom s-object variable name.</li><li>If you are unsure, use the default value of `s`.</li></ul> |
|Video Platform Name|  <ul><li>(Optional) The name of the online video platform through which content gets distributed.</li></ul> |
|Video Player SDK|  <ul><li>(Optional) The version of the video player app/SDK.</li></ul> |
|Tag Version|  <ul><li>This drop-down list lets you choose Adobe Heartbeat tracking with or without Nielsen integration.</li><li>The available options are:  <ul><li>Adobe Heartbeat 2.0.2 (default)</li><li>Adobe Heartbeat 1.6.7</li><li>Adobe Heartbeat 1.6.7 with Nielsen 5.0</li></ul> </li></ul> |

The following fields are only required if you set the tag version to **Adobe Heartbeat 1.6.7 with Nielsen 5.0**. If you do not have the required Nielsen values, contact your Nielsen or Adobe representative.

|FIELD NAME| FIELD VALUE|
|---| ---|
|Adobe Nielsen SDK Configuration Key|  <ul>(Required for Nielsen) Enter the Nielsen configuration key</li><li>Configuration SDK key for Nielsen integration with Adobe Heartbeat.</li></ul> |
|Nielsen Collection Environment|  <ul>(Required for Nielsen) Location of collection environment.</li><li>Enter the location of Nielsen's collection environment</li><li>For example, `eu-cert` or `eu`.</li></ul> |
|Nielsen Player ID|  <ul>(Required for Nielsen) Enter the unique identifier assigned to the video player</li><li>Unique ID assigned to player/site, provided by Nielsen.</li></ul> |
|Nielsen APN|  <ul>(Required for Nielsen) Enter a description for the player/site</li><li>User-defined string value for describing the player/site.</li></ul> |
|Nielsen Client ID|  <ul>(Required for Nielsen) Enter your Nielsen client identifier</li><li>Unique ID for VA Beacon Measurement.</li></ul> |
|Nielsen VCID|  <ul>(Required for Nielsen) Enter the video channel identifier.</li><li>Unique ID for VA Beacon Measurement.</li></ul> |

## Apply Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site. The Load on All Pages rule is the default load rule. To load this tag on a specific page, create relevant rule conditions to apply to the tag.


<blockquote>
Best Practice: Create and apply custom rules to load this tag on any pages where videos are made available.
</blockquote>


## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The following sections provide detailed tables for each available category.

### Standard

The Standard category corresponds to the [configuration fields for the tag](#tag_configs). You can map values to these destinations. Dynamically send values for the tag fields that are left blank or override the current values.

|Destination Name| Description|
|---| ---|
|`tracking_server`|  <ul><li>Adobe Heartbeat Tracking Server.</li><li>URL of the server where all heartbeat tracking calls are sent.</li></ul> |
|`publisher`|  <ul><li>Adobe Heartbeat Publisher.</li><li>Publisher name as assigned by your Adobe representative.</li></ul> |
|`ssl`|  <ul><li>Adobe Heartbeat SSL Flag.</li><li>Boolean flag that determines whether or not to send heartbeat calls over HTTPS.</li><li>Ensure the variable you are mapping is populated with a Boolean value, either `true` or `false`.</li><li>Mapping overrides the current drop-down selection.</li></ul> |
|`syndication_channel`|  <ul><li>Adobe Heartbeat Channel.</li><li>Name of the channel syndication.</li></ul> |
|`online_video_platform_name`|  <ul><li>Adobe Heartbeat Video Platform Name.</li><li>Name of the online platform that is rendering your video content.</li></ul> |
|`player_sdk`|  <ul><li>Adobe Heartbeat Player SDK.</li><li>Version of the video player app/SDK.</li></ul> |
|`debug_logging`|  <ul><li>Adobe Heartbeat Debug Logging Flag.</li><li>Boolean flag to enable/disable logging of each component within the Heartbeat plugin.</li><li>Adobe recommends disabling this flag for the production version of your player because active logging impacts performance.</li></ul> |

The following fields are only required if you set the tag version to **Adobe Heartbeat 1.6.7 with Nielsen 5.0**. If you do not have the required Nielsen values, contact your Nielsen or Adobe representative.

|Destination Name| Description|
|---| ---|
|`nielsen_config_key`|  <ul><li>Adobe Nielsen SDK Configuration Key.</li><li>Nielsen configuration key to integrate with Adobe Heartbeat.</li></ul> |
|`nielsen_client_id`|  <ul><li>Nielsen Client ID.</li><li>Your Nielsen client identifier.</li></ul> |
|`nielsen_vcid`|  <ul><li>Nielsen VCID.</li><li>Video channel identifier.</li></ul> |
|`nielsen_collection_environment`|  <ul><li>Nielsen Collection Environment.</li><li>Location of Nielsen's collection environment.</li></ul> |
|`nielsen_player_id`|  <ul><li>Nielsen Player ID.</li><li>The unique identifier for the video player.</li></ul> |
|`nielsen_apn`|  <ul><li>Nielsen APN.</li><li>Description of the player/site, expressed as a string value.</li></ul> |
|`nielsen_device_id`|  <ul><li>Nielsen Device ID.</li><li>Unique identifier of mobile/tablet where you want to track the video.</li></ul> |
|`nielsen_sdk_debug`|  <ul><li>Nielsen SDK Debug Flag.</li><li>Boolean flag to enable/disable logging of the Nielsen integration.</li></ul> |
|`nielsen_opt_out`|  <ul><li>Nielsen Opt Out Flag.</li><li>Disable all Nielsen tracking for the current visitor.</li><li>Requires triggering the `opt-out` event.</li></ul> |

### Video Events

Video event destinations are event listeners that trigger when a certain action or change occurs in the video player. To trigger an event, you must map your variable to an event in the toolbox and set the value of the variable as the trigger. The mapped event fires when the supplied trigger value is found in the data layer.

The following tables lists the available event destinations:

|Destination Name| Description|
|---| ---|
|`video_load`|  <ul><li>Video Load.</li><li>Indicates the video is ready to be played.</li></ul> |
|`video_start`|  <ul><li>Video Start.</li><li>Indicates the video has started playing, possibly after one of the following three (3) scenarios:  <ul><li>initial loading</li><li>buffering</li><li>ad display</li></ul> </li></ul> |
|`video_playing`|  <ul><li>Video Playing.</li><li>Indicates that the video is currently playing.</li><li>Use to update QoS data.</li><li>Should not be called when ads are playing.</li></ul> |
|`video_pause`|  <ul><li>Video Pause.</li><li>Indicates that video was paused.</li></ul> |
|`video_play`|  <ul><li>Video Play.</li><li>Indicates that the video is playing, possibly after the buffering or seeking has completed.</li></ul> |
|`video_stop`|  <ul><li>Video Stop.</li><li>Indicates that the video has been manually stopped.</li></ul> |
|`video_resume`|  <ul><li>Video Resume.</li><li>Indicates the viewer has unpaused the video to resume playing.</li></ul> |
|`video_complete`|  <ul><li>Video Complete.</li><li>Indicates that the video has ended.</li></ul> |
|`video_seek`|  <ul><li>Video Seek.</li><li>Indicates the viewer has started seeking the video.</li></ul> |
|`video_buffer`|  <ul><li>Video Buffer.</li><li>Indicates the video has started buffering.</li></ul> |
|`video_skip`|  <ul><li>Video Skip.</li><li>Indicates the viewer has skipped the video or ad.</li></ul> |
|`video_error`|  <ul><li>Video Error.</li><li>Indicates the video has encountered an error.</li></ul> |
|`nielsen_opt_out_status_changed`|  <ul><li>Nielsen Opt Out Status Change.</li><li>Indicates the viewer has switched from opt-in to opt-out OR vice-versa.</li></ul> |

### Video

These destinations correspond to the [Adobe Video Measurement parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html).

|Destination Name| Description|
|---| ---|
|`video.id`|  <ul><li>Video ID.</li><li>Unique identifier of the video.</li></ul> |
|`video.title`|  <ul><li>Video Title.</li><li>Name of the video being tracked.</li></ul> |
|`video.length`|  <ul><li>Video Length.</li><li>The duration (in seconds) of the video asset.</li></ul> |
|`video.current_playhead`|  <ul><li>Video Current Playhead.</li><li>The current position of the player (in seconds) in the video, excluding ad content.</li></ul> |
|`video.stream_type`|  <ul><li>Video Stream Type.</li><li>Type of the video asset.</li></ul> |
|`video.is_full_episode`|  <ul><li>Video Is Full Episode.</li><li>Boolean flag to indicate if the video content is a full episode.  <ul><li>`Y` for full episode.</li><li>`N` for a partial clip.</li></ul> </li></ul> |
|`video.original_air_date_nielsen`|  <ul><li>Video Original Air Date For Nielsen.</li><li>The original air date of the episode, format.</li><li>For example, `YYYYMMDDHH24:MI:SS`</li></ul> |
|`video.channel_name`|  <ul><li>Video Channel Name.</li><li>Name of the program or feed being sent.</li></ul> |
|`video.series_name`|  <ul><li>Video Series Name.</li><li>Name of the program (series name) being viewed.</li></ul> |
|`video.player_name`|  <ul><li>Video Player Name.</li><li>Name of the video player that is playing the content.</li></ul> |
|`video.is_ad`|  <ul><li>Video Is Ad.</li><li>Boolean value to indicate whether or not the video is an advertisement.</li></ul> |
|`video.fps`|  <ul><li>Video FPS.</li><li>The frame rate of the media, in frames per second (FPS).</li></ul> |
|`video.bit_rate`|  <ul><li>Video Bitrate.</li><li>The bits per second attribute of the video content.</li></ul> |
|`video.startup.time`|  <ul><li>Video Startup Time.</li><li>The start time, in seconds, of the video content.</li></ul> |
|`video.dropped_frames`|  <ul><li>Video Dropped Frames.</li><li>The sum of all frames dropped during a playback session.</li></ul> |
|`video.error_id`|  <ul><li>Video Error ID.</li><li>The ID of the error encountered during playback.</li></ul> |
|`video.error_is_fatal`|  <ul><li>Video Error Is Fatal.</li><li>Boolean value to indicate whether or not the error prevents playback from continuing.</li></ul> |

### Chapter

These destinations correspond to [Adobe Video Chapter Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html).

|Destination Name| Description|
|---| ---|
|`chapter.name`|  <ul><li>Chapter Name.</li><li>Name of the individual chapters.</li></ul> |
|`chapter.length`|  <ul><li>Chapter Length.</li><li>Total duration of the chapter in seconds.</li></ul> |
|`chapter.position`|  <ul><li>Chapter Position.</li><li>Position of the chapter inside the video content.</li></ul> |
|`chapter.start_time`|  <ul><li>Chapter Start Time.</li><li>The offset inside the main content where the chapter starts.</li></ul> |
|`chapter_meta_data.custom`|  <ul><li>Chapter Custom Metadata.</li><li>Additional custom value related to the chapter.</li></ul> |

### Ad

These destinations correspond to [Adobe Video Ad Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html).

|Destination Name| Description|
|---| ---|
|`adbreak.name`|  <ul><li>Ad Break Name.</li><li>The name of the individual cad breaks.</li></ul> |
|`adbreak.position`|  <ul><li>Ad Break Position.</li><li>The position (index) of the ad break inside the video content.</li><li>Required when the `video.is_ad` flag is set to `True`.</li></ul> |
|`dbreak.start_time`|  <ul><li>Ad Break Start Time.</li><li>The offset inside the main content where the ad break starts.</li></ul> |
|`ad.id`|  <ul><li>Ad ID.</li><li>Unique identifier of the ad being displayed.</li></ul> |
|`ad.title`|  <ul><li>Ad Title.</li><li>Name of the ad.</li></ul> |
|`ad.type`|  <ul><li>Ad Type.</li><li>Type or category of the ad.</li></ul> |
|`ad.length`|  <ul><li>Ad Length.</li><li>Total duration of the ad (in seconds).</li></ul> |
|`ad.position`|  <ul><li>Ad Position.</li><li>The position (index) of the ad inside the video content.</li><li>Required when the `video.is_ad` flag is set to `True`.</li></ul> |

### Video Metadata

These destinations correspond to [Adobe Standard Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html).

|Destination Name| Description|
|---| ---|
|`meta_data.custom`|  <ul><li>Video Custom Metadata.</li><li>Additional custom value related to the video.</li></ul> |
|`meta_data.show`|  <ul><li>Video Metadata Show.</li><li>Name of the show.</li></ul> |
|`meta_data.season`|  <ul><li>Video Metadata Season.</li><li>The season number.</li></ul> |
|`meta_data.episode`|  <ul><li>Video Metadata Episode.</li><li>The episode number.</li></ul> |
|`meta_data.asset`|  <ul><li>Video Metadata Asset.</li><li>The video asset identifier also known as TMS ID (Tribune Media Service).</li></ul> |
|`meta_data.genre`|  <ul><li>Video Metadata Genre.</li><li>Genre of the video content.</li></ul> |
|`meta_data.airDate`|  <ul><li>Video Metadata Air Date.</li><li>The date on which the asset was first aired on TV.</li></ul> |
|`meta_data.digitalDate`|  <ul><li>Video Metadata Digital Air Date.</li><li>The date on which the asset was first available as digital.</li></ul> |
|`meta_data.rating`|  <ul><li>Video Metadata Rating.</li><li>Ratings available for the video content.</li></ul> |
|`meta_data.originator`|  <ul><li>Video Metadata Originator.</li><li>Name of the video originator.</li></ul> |
|`meta_data.network`|  <ul><li>Video Metadata Network.</li><li>The name of the network associated with the show.</li></ul> |
|`meta_data.type`|  <ul><li>Video Metadata Type.</li><li>Type of the show.</li></ul> |
|`meta_data.adLoad`|  <ul><li>Video Metadata Ad Load.</li><li>Metadata for the ad load.</li></ul> |
|`meta_data.dayPart`|  <ul><li>Video Metadata Day Part.</li><li>The day part for which the ad display is scheduled.</li></ul> |
|`meta_data.feed`|  <ul><li>Video Metadata Feed.</li><li>The type of programming feed.</li></ul> |
|`meta_data.format`|  <ul><li>Video Metadata Format.</li><li>Stream format of the video.</li></ul> |

### Ad Metadata

These destinations correspond to [Adobe Standard Ad Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html).

|Destination Name| Description|
|---| ---|
|`ad_meta_data.custom`|  <ul><li>Ad Custom Metadata.</li><li>Additional custom value related to the ad being displayed.</li></ul> |
|`ad_meta_data.advertiser`|  <ul><li>Ad Metadata Advertiser.</li><li>Name of the company/brand that is displaying the ad.</li></ul> |
|`ad_meta_data.campaign`|  <ul><li>Ad Metadata Campaign.</li><li>Ad campaign Identifier.</li></ul> |
|`ad_meta_data.creative`|  <ul><li>Ad Metadata Creative.</li><li>Creative asset for rendering the ad.</li></ul> |
|`ad_meta_data.placement`|  <ul><li>Ad Metadata Placement.</li><li>Metadata related to the position of the ad inside the video.</li></ul> |
|`ad_meta_data.site`|  <ul><li>Ad Metadata Site.</li><li>Site associated with the ad.</li></ul> |
|`ad_meta_data.creativeURL`|  <ul><li>Ad Metadata Creative URL.</li><li>URL of the ad being displayed.</li></ul> |

## Built-in Video Data Layer Variables

Mapping is not required if your data layer is already using these values. Tealium typically sends data to the matching tag destinations. If your data layer uses different variables names from those listed in this table, then you will need to manually map.

|Built-in Variables| Toolbox Destination Variable| Description|
|---| ---| ---|
|`event_name`| [Video Event destinations](#video_events_mapping)|  If you use any of the following values in your `event_name` variable, you do not need to map again in the toolbox. <ul><li>`load` is mapped to `video_load`</il><li>`start` is mapped to `video_start`</il><li>`playing` is mapped to `video_playing`</il><li>`pause` is mapped to `video_pause`</il><li>`play` is mapped to `video_play`</il><li>`stop` is mapped to `video_stop`</il><li>`resume` is mapped to `video_resume`</il><li>`complete` is mapped to `video_complete`</il><li>`seek` is mapped to `video_seek`</il><li>`buffer` is mapped to `video_buffer`</il><li>`optstatus` is mapped to `Nielsen_opt_out_status_changed`</li></ul> |
|`video_id`| --|  <ul><li>Unique identifier of the video.</li></ul> |
|`video_name`| `video.title`|  <ul><li>Video Title.</li><li>Name of the video being tracked.</li></ul> |
|`video_length`| `video.length`|  <ul><li>Video Length.</li><li>The duration (in seconds) of the video asset.</li></ul> |
|`video_player_name`| `video.player_name`|  <ul><li>Video Player Name.</li><li>Name of the video player that is playing the content.</li></ul> |
|`video_current_playhead`| `video.current_playhead`|  <ul><li>Video Current Playhead.</li><li>The current position of the player (in seconds) in the video, excluding ad content.</li></ul> |
|`video_stream_type`| `video.stream_type`|  <ul><li>Video Stream Type.</li><li>Type of the video asset.</li></ul> |
|`video_fps`| `video.fps`|  <ul><li>Video FPS.</li><li>The frame rate of the media, in frames per second (FPS).</li></ul> |
|`video_bitrate`| `video.bit_rate`|  <ul><li>Video Bitrate.</li><li>The bits per second attribute of the video content.</li></ul> |
|`video_dropped_frames`| `video.dropped_frames`|  <ul><li>Video Dropped Frames.</li><li>The sum of all frames dropped during a playback session.</li></ul> |
|`video_is_ad`| `video.is_ad`|  <ul><li>Video Is Ad.</li><li>Boolean value to indicate whether or not the video is an advertisement.</li></ul> |
|`video_ad_position` - OR - `video_ad_pod_position`| `ad.position`|  <ul><li>Ad Position.</li><li>The position (index) of the ad inside the video content.</li><li>Required when the `video.is_ad `flag is set to `true`.</li></ul> |
|`video_chapter_name`| `chapter.name`|  <ul><li>Chapter Name.</li><li>Name of the individual chapters.</li></ul> |
|`video_chapter_length`| `chapter.length`|  <ul><li>Chapter Length.</li><li>Total duration of the chapter in seconds.</li></ul> |
|`video_chapter_position`| `chapter.position`|  <ul><li>Chapter Position.</li><li>Position of the chapter inside the video content.</li></ul> |
|`video_chapter_start_time`| `chapter.start_time`|  <ul><li>Chapter Start Time.</li><li>The offset inside the main content where the chapter starts.</li></ul> |
|`video_ad_pod_name`| `ad.id`|  <ul><li>Ad ID.</li><li>Unique identifier of the ad being displayed.</li></ul> |
|`program`| `video.series_name`|  <ul><li>Video Series Name.</li><li>Name of the program (series name) being viewed.</li></ul> |
|`is_full_episode`| `video.is_full_episode`|  <ul><li>Video Is Full Episode.</li><li>Boolean flag to indicate if the video content is a full episode.  <ul><li>`Y` for full episode</li><li>`N` for a partial clip</li></ul> </li></ul> |
|`original_air_date`| `video.original_air_date_nielsen`|  <ul><li>Video Original Air Date For Nielsen.</li><li>The original air date of the episode, in the following format: `YYYYMMDDHH24:MI:SS`</li></ul> |

## Validation

The Heartbeat tag is event-based and leverages the `utag.track("video", data)` call to differentiate itself from other utag calls. For this reason, it is crucial to properly set up the [video event triggers in the Data Mapping toolbox](#video_events_mapping).

Once configured, the tag fires continuously every second to keep the video data current. This is accomplished by firing the "playing" event within your video player's "playing" event handler. Other video events should also be fired through their corresponding Adobe heartbeat events. Network calls are aggregated and reported to Adobe every 10 seconds; including those for event changes.


<blockquote>
An easy way to set both the Heartbeat and Nielsen debug flags is by adding a querystring parameter to the URL of the video page. For For example, `adobe_debug=1&Nielsen=1` <br>You can then add the Query parameter variables to your data layer in Tealium iQ and map them accordingly.<br>Mapping destinations for both the Heartbeat and Nielsen debug flags are available under the Standard category. See "Adobe Heartbeat Debug Logging Flag" and "Nielsen SDK Debug Flag".<br>When complete, you can run the following Tealium debug command in your browser console. <br>
`document.cookie = "utagdb=true";`
</blockquote>


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
