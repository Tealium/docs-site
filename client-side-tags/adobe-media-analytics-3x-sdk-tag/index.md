---
title: Adobe Media Analytics (3.x SDK) Tag Setup Guide
description: This article describes how to set up the Adobe Media Analytics (3.x SDK) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adobe-media-analytics-3x-sdk-tag/
---
Adobe Media Analytics provides support for tracking video and ad metrics, including total views/impressions, time spent, and completion rates.

## Tag Tips

* Adobe Media Analytics requires the Adobe Experience Cloud ID Service as well as AppMeasurement for JS to be loaded first, preferably bundled.
* This tag is fired with `utag.track(&#39;video&#39;, data);` which should be implemented in your video event handlers.

## Tag Configuration

First, go to the tag marketplace and add the Adobe Media Analytics (3.x SDK) tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Tracking Server**: (Required) Adobe Media Analytics tracking server. (`example.hb.omtrdc.net`).
* **Publisher**: (Required) Publisher name as provided by Adobe.
* **Use SSL**: Specifies whether or not to send heartbeat calls over HTTPS. The default value is false, meaning SSL is disabled. Set the value to true to send tracking calls securely.
* **S-Object Name**: (Required) Set your own custom s-object variable name. Use defaults if not sure.
* **Video Platform Name**: The name of the online video platform through which content gets distributed. This field is optional.
* **Video Player SDK**: The version of the video player app/SDK. This field is optional.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Adobe Media Analytics Tracking Server| (`tracking_server`)|
|Adobe Media Analytics Publisher| (`publisher`)|
|Adobe Media Analytics SSL Flag| (`ssl`)|
|Adobe Media Analytics Channel| (`syndication_channel`)|
|Adobe Media Analytics Video Platform Name| (`online_video_platform_name`)|
|Adobe Media Analytics Player SDK| (`player_sdk`)|
|Adobe Media Analytics Debug Logging Flag| (`debug_logging`)|

### Video Events

|Variable| Description|
|---| ---|
|Video Load (`video_load`)| `video_load`|
|Video Start (`video_start`)| `video_start`|
|Video Playing (`video_playing`)| `video_playing`|
|Video Pause (`video_pause`)| `video_pause`|
|Video Play (`video_play`)| `video_play`|
|Video Stop (`video_stop`)| `video_stop`|
|Video Resume (`video_resume`)| `video_resume`|
|Video Complete (`video_complete`)| `video_complete`|
|Video Seek (`video_seek`)| `video_seek`|
|Video Buffer (`video_buffer`)| `video_buffer`|
|Video Skip (`video_skip`)| `video_skip`|
|Video Error (`video_error`)| `video_error`|

### Video

|Variable| Description|
|---| ---|
|Video ID| (`video.id`)|
|Video Title| (`video.title`)|
|Video Length| (`video.length`)|
|Video Current Playhead| (`video.current_playhead`)|
|Video Stream Type| (`video.stream_type`)|
|Video Is Full Episode| (`video.is_full_episode`)|
|Video Channel Name| (`video.channel_name`)|
|Video Series Name| (`video.series_name`)|
|Video Player Name| (`video.player_name`)|
|Video Is Ad| (`video.is_ad`)|
|Video FPS| (`video.fps`)|
|Video Bit Rate| (`video.bit_rate`)|
|Video Startup Time| (`video.startup_time`)|
|Video Dropped Frames| (`video.dropped_frames`)|
|Video Error ID| (`video.error_id`)|
|Video Error Is Fatal| (`video.error_is_fatal`)|

### Chapter

|Variable| Description|
|---| ---|
|Chapter Name| (`chapter.name`)|
|Chapter Length| (`chapter.length`)|
|Chapter Position| (`chapter.position`)|
|Chapter Start Time| (`chapter.start_time`)|
|Chapter Custom Metadata| (`chapter_meta_data.custom`)|

### Ad

|Variable| Description|
|---| ---|
|Ad Break Name| (`adbreak.name`)|
|Ad Break Position| (`adbreak.position`)|
|Ad Break Start Time| (`adbreak.start_time`)|
|Ad ID| (`ad.id`)|
|Ad Title| (`ad.title`)|
|Ad Type| (`ad.type`)|
|Ad Length| (`ad.length`)|
|Ad Position| (`ad.position`)|

### Video Metadata

|Variable| Description|
|---| ---|
|Video Custom Metadata| (`meta_data.custom`)|
|Video Metadata Show| (`meta_data.show`)|
|Video Metadata Season| (`meta_data.season`)|
|Video Metadata Episode| (`meta_data.episode`)|
|Video Metadata Asset| (`meta_data.asset`)|
|Video Metadata Genre| (`meta_data.genre`)|
|Video Metadata Air Date| (`meta_data.airDate`)|
|Video Metadata Digital Air Date| (`meta_data.digitalDate`)|
|Video Metadata Rating| (`meta_data.rating`)|
|Video Metadata Originator| (`meta_data.originator`)|
|Video Metadata Network| (`meta_data.network`)|
|Video Metadata Type| (`meta_data.type`)|
|Video Metadata Ad Load| (`meta_data.adLoad`)|
|Video Metadata Day Part| (`meta_data.dayPart`)|
|Video Metadata Feed| (`meta_data.feed`)|
|Video Metadata Format| (`meta_data.format`)|

### Ad Metadata

|Variable| Description|
|---| ---|
|Ad Custom Metadata| (`ad_meta_data.custom`)|
|Ad Metadata Advertiser| (`ad_meta_data.advertiser`)|
|Ad Metadata Campaign| (`ad_meta_data.campaign`)|
|Ad Metadata Creative| (`ad_meta_data.creative`)|
|Ad Metadata Placement| (`ad_meta_data.placement`)|
|Ad Metadata Site| (`ad_meta_data.site`)|
|Ad Metadata Creative URL| (`ad_meta_data.creativeURL`)|
