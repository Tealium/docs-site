---
title: 基本的なビデオトラッキングデータレイヤー仕様
description: この記事では、基本的なビデオトラッキングのためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/basic-video-tracking/
---
## データレイヤー属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`tealium_event`| Tealiumのイベント名| `video_pause`| 文字列|
|`video_playhead`| イベント時のビデオの再生位置（秒）| `75`| 数値|
|`video_id`| ビデオのユニークID| `xWlEk2i9r5Q`| 文字列|
|`video_length`| ビデオの全長（秒）| `300`| 数値|
|`video_milestone`| ビデオ再生のパーセンテージ| `25`| 数値|
|`video_name`| ビデオの表示名| `How to track videos in Tealium`| 文字列|
|`video_platform`| ビデオを提供するプラットフォームの名前| `YouTube`| 文字列|

## イベントトラッキング

### ビデオロード

|識別子|説明|
|---|---|
|`tealium_event="video_load"`| ビデオがロードされ、視聴者に利用可能になりました。|

サンプル:  
```javascript
{
   "tealium_event"  : "video_load",
   "video_id"       : "xWlEk2i9r5Q",
   "video_length"   : 300,
   "video_name"     : "How to track videos in Tealium",
   "video_platform" : "YouTube"
}
```

### ビデオスタート

|識別子|説明|
|---|---|
| `tealium_event="video_start"`| ビデオが初めて再生されました（自動再生またはユーザーのクリックによる）。|

サンプル:  
```javascript
{
   "tealium_event"  : "video_start",     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### ビデオ再生

|識別子|説明|
|---|---|
|`tealium_event="video_play"`| ビデオの再生が再開されました。|

サンプル:  
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

### ビデオ一時停止

|識別子|説明|
|---|---|
|`tealium_event="video_pause"`| ビデオの再生が一時停止しました。|

サンプル:  
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

### ビデオシーク

|識別子|説明|
|---|---|
| `tealium_event="video_seek"`| ビデオの再生位置が前後に移動しました。|

サンプル:  
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

### ビデオ完了

|識別子|説明|
|---|---|
| `tealium_event="video_complete"`| ビデオの再生が完了しました。|

サンプル:  
```javascript
{
   "tealium_event"  : "video_complete",     
   "video_id"       : "xWlEk2i9r5Q",     
   "video_length"   : 300,     
   "video_name"     : "How to track videos in Tealium",     
   "video_platform" : "YouTube"
}
```

### ビデオマイルストーン

|識別子|説明|
|---|---|
| `tealium_event="video_milestone"`| ビデオの再生が特定のパーセンテージのマイルストーンに達しました。|

サンプル:  
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