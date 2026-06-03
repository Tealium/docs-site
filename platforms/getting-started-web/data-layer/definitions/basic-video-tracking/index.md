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
|`tealium_event=&#34;video_load&#34;`| The video was loaded and made available to the viewer.|

Sample:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_load&#34;,
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,
   &#34;video_length&#34;   : 300,
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### Video Start

|Identifier|Description|
|---|---|
| `tealium_event=&#34;video_start&#34;`| The video began playing for the first time (either by auto-play or user click).|

Sample:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_start&#34;,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### Video Play

|Identifier|Description|
|---|---|
|`tealium_event=&#34;video_play&#34;`| The video playback changed from not playing to playing.|

Sample:  
```javascript
{  
   &#34;tealium_event&#34;  : &#34;video_play&#34;,     
   &#34;video_playhead&#34; : 75,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### Video Pause

|Identifier|Description|
|---|---|
|`tealium_event=&#34;video_pause&#34;`| The video playback changed to paused.|

Sample:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_pause&#34;,     
   &#34;video_playhead&#34; : 75,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### Video Seek

|Identifier|Description|
|---|---|
| `tealium_event=&#34;video_seek&#34;`| Video playback was advanced forward or backward to a new playhead.|

Sample:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_seek&#34;,     
   &#34;video_playhead&#34; : 75,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### Video Complete

|Identifier|Description|
|---|---|
| `tealium_event=&#34;video_complete&#34;`| Video playback has completed.|

Sample:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_complete&#34;,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### Video Milestone

|Identifier|Description|
|---|---|
| `tealium_event=&#34;video_milestone&#34;`| The video playback reached a specific percentage milestone.|

Sample:  
```javascript
{   
   &#34;tealium_event&#34;   : &#34;video_milestone&#34;,     
   &#34;video_playhead&#34;  : 75,     
   &#34;video_id&#34;        : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;    : 300,     
   &#34;video_milestone&#34; : 25,     
   &#34;video_name&#34;      : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34;  : &#34;YouTube&#34;
}
```
