---
title: Basic video tracking data layer specification
description: This article provides the data layer definition for basic video tracking.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/basic-video-tracking/
---
## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`tealium_event`| Tealium event name| `video_pause`| String|
|`video_playhead`| The playhead position (in seconds) of the video at the time of the event| `75`| Number|
|`video_id`| A unique ID for the video| `xWlEk2i9r5Q`| String|
|`video_length`| The total length (in seconds) of the video.| `300`| Number|
|`video_milestone`| The percentage of video played | `25`| Number|
|`video_name`| The display name of the video| `How to track videos in Tealium`| String|
|`video_platform`| The name of the platform serving the video | `YouTube`| String|

## Event Tracking

### Video Load

|Identifier|Description|
|---|---|
|`tealium_event="video_load"`| The video was loaded and made available to the viewer.|

Sample:  
```javascript
{
   "tealium_event"  : "video_load",
   "video_id"       : "xWlEk2i9r5Q",
   "video_length"   : 300,
   "video_name"     : "How to track videos in Tealium",
   "video_platform" : "YouTube"
}
```

### Video Start

|Identifier|Description|
|---|---|
| `tealium_event="video_start"`| The video began playing for the first time (either by auto-play or user click).|

Sample:  
```javascript
{
   "tealium_event"  : "video_start",     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### Video Play

|Identifier|Description|
|---|---|
|`tealium_event="video_play"`| The video playback changed from not playing to playing.|

Sample:  
```javascript
{  
   "tealium_event"  : "video_play",     
   "video_playhead" : 75,     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### Video Pause

|Identifier|Description|
|---|---|
|`tealium_event="video_pause"`| The video playback changed to paused.|

Sample:  
```javascript
{
   "tealium_event"  : "video_pause",     
   "video_playhead" : 75,     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### Video Seek

|Identifier|Description|
|---|---|
| `tealium_event="video_seek"`| Video playback was advanced forward or backward to a new playhead.|

Sample:  
```javascript
{
   "tealium_event"  : "video_seek",     
   "video_playhead" : 75,     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### Video Complete

|Identifier|Description|
|---|---|
| `tealium_event="video_complete"`| Video playback has completed.|

Sample:  
```javascript
{
   "tealium_event"  : "video_complete",     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### Video Milestone

|Identifier|Description|
|---|---|
| `tealium_event="video_milestone"`| The video playback reached a specific percentage milestone.|

Sample:  
```javascript
{   
   "tealium_event"   : "video_milestone",     
   "video_playhead"  : 75,     
   "video_id"        : "xWlEk2i9r5Q",     
   "video_length"    : 300,     
   "video_milestone" : 25,     
   "video_name"      : "How to track videos in Tealium",     
   "video_platform"  : "YouTube"
}
```
