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
|`tealium_event=&#34;video_load&#34;`| ビデオがロードされ、視聴者に利用可能になりました。|

サンプル:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_load&#34;,
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,
   &#34;video_length&#34;   : 300,
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### ビデオスタート

|識別子|説明|
|---|---|
| `tealium_event=&#34;video_start&#34;`| ビデオが初めて再生されました（自動再生またはユーザーのクリックによる）。|

サンプル:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_start&#34;,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### ビデオ再生

|識別子|説明|
|---|---|
|`tealium_event=&#34;video_play&#34;`| ビデオの再生が再開されました。|

サンプル:  
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

### ビデオ一時停止

|識別子|説明|
|---|---|
|`tealium_event=&#34;video_pause&#34;`| ビデオの再生が一時停止しました。|

サンプル:  
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

### ビデオシーク

|識別子|説明|
|---|---|
| `tealium_event=&#34;video_seek&#34;`| ビデオの再生位置が前後に移動しました。|

サンプル:  
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

### ビデオ完了

|識別子|説明|
|---|---|
| `tealium_event=&#34;video_complete&#34;`| ビデオの再生が完了しました。|

サンプル:  
```javascript
{
   &#34;tealium_event&#34;  : &#34;video_complete&#34;,     
   &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,     
   &#34;video_length&#34;   : 300,     
   &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,     
   &#34;video_platform&#34; : &#34;YouTube&#34;
}
```

### ビデオマイルストーン

|識別子|説明|
|---|---|
| `tealium_event=&#34;video_milestone&#34;`| ビデオの再生が特定のパーセンテージのマイルストーンに達しました。|

サンプル:  
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