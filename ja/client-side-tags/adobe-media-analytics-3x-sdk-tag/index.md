---
title: Adobe Media Analytics (3.x SDK) タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdobe Media Analytics (3.x SDK)タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-media-analytics-3x-sdk-tag/
---
Adobe Media Analyticsは、総視聴回数/インプレッション、視聴時間、完了率などのビデオと広告のメトリクスを追跡するためのサポートを提供します。

## タグのヒント

* Adobe Media Analyticsは、Adobe Experience Cloud ID ServiceとAppMeasurement for JSを最初にロードすることを必要とします。できればバンドルしてください。
* このタグは `utag.track('video', data);` を介して発火され、ビデオイベントハンドラに実装する必要があります。

## タグ構成

まず、タグマーケットプレイスに移動し、Adobe Media Analytics (3.x SDK)タグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **トラッキングサーバー**：Adobe Media Analyticsのトラッキングサーバー。このフィールドは必須です（`example.hb.omtrdc.net`）。
* **パブリッシャー**：Adobeから提供されるパブリッシャー名。このフィールドは必須です。
* **SSLの使用**：ハートビートコールをHTTPS経由で送信するかどうかを指定します。デフォルト値はfalseで、SSLが無効化されています。トラッキングコールを安全に送信するには、値をtrueに構成します。
* **S-オブジェクト名**：必須。独自のカスタムs-オブジェクト変数名を構成します。確信がなければデフォルトを使用します。
* **ビデオプラットフォーム名**：コンテンツが配信されるオンラインビデオプラットフォームの名前。このフィールドはオプションです。
* **ビデオプレーヤーSDK**：ビデオプレーヤーアプリ/SDKのバージョン。このフィールドはオプションです。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|Adobe Media Analytics トラッキングサーバー| (`tracking_server`)|
|Adobe Media Analytics パブリッシャー| (`publisher`)|
|Adobe Media Analytics SSLフラグ| (`ssl`)|
|Adobe Media Analytics チャンネル| (`syndication_channel`)|
|Adobe Media Analytics ビデオプラットフォーム名| (`online_video_platform_name`)|
|Adobe Media Analytics プレーヤーSDK| (`player_sdk`)|
|Adobe Media Analytics デバッグログフラグ| (`debug_logging`)|

### ビデオイベント

|変数| 説明|
|---| ---|
|ビデオロード (`video_load`)| `video_load`|
|ビデオスタート (`video_start`)| `video_start`|
|ビデオ再生中 (`video_playing`)| `video_playing`|
|ビデオ一時停止 (`video_pause`)| `video_pause`|
|ビデオ再生 (`video_play`)| `video_play`|
|ビデオ停止 (`video_stop`)| `video_stop`|
|ビデオ再開 (`video_resume`)| `video_resume`|
|ビデオ完了 (`video_complete`)| `video_complete`|
|ビデオシーク (`video_seek`)| `video_seek`|
|ビデオバッファ (`video_buffer`)| `video_buffer`|
|ビデオスキップ (`video_skip`)| `video_skip`|
|ビデオエラー (`video_error`)| `video_error`|

### ビデオ

|変数| 説明|
|---| ---|
|ビデオID| (`video.id`)|
|ビデオタイトル| (`video.title`)|
|ビデオ長| (`video.length`)|
|ビデオ現在の再生ヘッド| (`video.current_playhead`)|
|ビデオストリームタイプ| (`video.stream_type`)|
|ビデオはフルエピソードか| (`video.is_full_episode`)|
|ビデオチャンネル名| (`video.channel_name`)|
|ビデオシリーズ名| (`video.series_name`)|
|ビデオプレーヤー名| (`video.player_name`)|
|ビデオは広告か| (`video.is_ad`)|
|ビデオFPS| (`video.fps`)|
|ビデオビットレート| (`video.bit_rate`)|
|ビデオ起動時間| (`video.startup_time`)|
|ビデオドロップフレーム| (`video.dropped_frames`)|
|ビデオエラーID| (`video.error_id`)|
|ビデオエラーは致命的か| (`video.error_is_fatal`)|

### チャプター

|変数| 説明|
|---| ---|
|チャプター名| (`chapter.name`)|
|チャプター長| (`chapter.length`)|
|チャプター位置| (`chapter.position`)|
|チャプター開始時間| (`chapter.start_time`)|
|チャプターカスタムメタデータ| (`chapter_meta_data.custom`)|

### 広告

|変数| 説明|
|---| ---|
|広告ブレイク名| (`adbreak.name`)|
|広告ブレイク位置| (`adbreak.position`)|
|広告ブレイク開始時間| (`adbreak.start_time`)|
|広告ID| (`ad.id`)|
|広告タイトル| (`ad.title`)|
|広告タイプ| (`ad.type`)|
|広告長| (`ad.length`)|
|広告位置| (`ad.position`)|

### ビデオメタデータ

|変数| 説明|
|---| ---|
|ビデオカスタムメタデータ| (`meta_data.custom`)|
|ビデオメタデータショー| (`meta_data.show`)|
|ビデオメタデータシーズン| (`meta_data.season`)|
|ビデオメタデータエピソード| (`meta_data.episode`)|
|ビデオメタデータアセット| (`meta_data.asset`)|
|ビデオメタデータジャンル| (`meta_data.genre`)|
|ビデオメタデータ放送日| (`meta_data.airDate`)|
|ビデオメタデータデジタル放送日| (`meta_data.digitalDate`)|
|ビデオメタデータ評価| (`meta_data.rating`)|
|ビデオメタデータ発信者| (`meta_data.originator`)|
|ビデオメタデータネットワーク| (`meta_data.network`)|
|ビデオメタデータタイプ| (`meta_data.type`)|
|ビデオメタデータ広告ロード| (`meta_data.adLoad`)|
|ビデオメタデータデイパート| (`meta_data.dayPart`)|
|ビデオメタデータフィード| (`meta_data.feed`)|
|ビデオメタデータフォーマット| (`meta_data.format`)|

### 広告メタデータ

|変数| 説明|
|---| ---|
|広告カスタムメタデータ| (`ad_meta_data.custom`)|
|広告メタデータ広告主| (`ad_meta_data.advertiser`)|
|広告メタデータキャンペーン| (`ad_meta_data.campaign`)|
|広告メタデータクリエイティブ| (`ad_meta_data.creative`)|
|広告メタデータ配置| (`ad_meta_data.placement`)|
|広告メタデータサイト| (`ad_meta_data.site`)|
|広告メタデータクリエイティブURL| (`ad_meta_data.creativeURL`)|


