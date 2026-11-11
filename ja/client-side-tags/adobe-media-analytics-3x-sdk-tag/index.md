---
title: Adobe Media Analytics（3.x SDK）タグ構成ガイド
description: この記事では、タグ管理アカウントで Adobe Media Analytics（3.x SDK）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-media-analytics-3x-sdk-tag/
---
Adobe Media Analytics は、合計視聴回数／インプレッション数、視聴時間、完了率など、動画および広告の指標のトラッキングをサポートします。

## タグに関するヒント

* Adobe Media Analytics を使用するには、Adobe Experience Cloud ID Service と AppMeasurement for JS を先に読み込む必要があります。可能であれば、これらをバンドルしてください。
* このタグは `utag.track('video', data);` で発火します。このコードを動画イベントハンドラーに実装してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **トラッキングサーバー**：（必須）Adobe Media Analytics のトラッキングサーバー（`example.hb.omtrdc.net`）。
* **パブリッシャー**：（必須）Adobe から提供されたパブリッシャー名。
* **SSL を使用**：ハートビート呼び出しを HTTPS 経由で送信するかどうかを指定します。デフォルト値は false で、SSL は無効です。トラッキング呼び出しを安全に送信するには、値を true に構成します。
* **S オブジェクト名**：（必須）独自のカスタム S オブジェクト変数名を構成します。不明な場合は、デフォルト値を使用してください。
* **動画プラットフォーム名**：コンテンツの配信に使用するオンライン動画プラットフォームの名前。このフィールドは任意です。
* **動画プレーヤー SDK**：動画プレーヤーアプリ／SDK のバージョン。このフィールドは任意です。

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|Adobe Media Analytics トラッキングサーバー|（`tracking_server`）|
|Adobe Media Analytics パブリッシャー|（`publisher`）|
|Adobe Media Analytics SSL フラグ|（`ssl`）|
|Adobe Media Analytics チャネル|（`syndication_channel`）|
|Adobe Media Analytics 動画プラットフォーム名|（`online_video_platform_name`）|
|Adobe Media Analytics プレーヤー SDK|（`player_sdk`）|
|Adobe Media Analytics デバッグログフラグ|（`debug_logging`）|

### 動画イベント

|変数|説明|
|---|---|
|動画の読み込み（`video_load`）|`video_load`|
|動画の開始（`video_start`）|`video_start`|
|動画の再生中（`video_playing`）|`video_playing`|
|動画の一時停止（`video_pause`）|`video_pause`|
|動画の再生（`video_play`）|`video_play`|
|動画の停止（`video_stop`）|`video_stop`|
|動画の再開（`video_resume`）|`video_resume`|
|動画の完了（`video_complete`）|`video_complete`|
|動画のシーク（`video_seek`）|`video_seek`|
|動画のバッファリング（`video_buffer`）|`video_buffer`|
|動画のスキップ（`video_skip`）|`video_skip`|
|動画エラー（`video_error`）|`video_error`|

### 動画

|変数|説明|
|---|---|
|動画 ID|（`video.id`）|
|動画タイトル|（`video.title`）|
|動画の長さ|（`video.length`）|
|動画の現在の再生ヘッド位置|（`video.current_playhead`）|
|動画ストリームタイプ|（`video.stream_type`）|
|動画が完全なエピソードか|（`video.is_full_episode`）|
|動画チャネル名|（`video.channel_name`）|
|動画シリーズ名|（`video.series_name`）|
|動画プレーヤー名|（`video.player_name`）|
|動画が広告か|（`video.is_ad`）|
|動画の FPS|（`video.fps`）|
|動画のビットレート|（`video.bit_rate`）|
|動画の起動時間|（`video.startup_time`）|
|動画のドロップフレーム数|（`video.dropped_frames`）|
|動画エラー ID|（`video.error_id`）|
|動画エラーが致命的か|（`video.error_is_fatal`）|

### チャプター

|変数|説明|
|---|---|
|チャプター名|（`chapter.name`）|
|チャプターの長さ|（`chapter.length`）|
|チャプターの位置|（`chapter.position`）|
|チャプターの開始時間|（`chapter.start_time`）|
|チャプターのカスタムメタデータ|（`chapter_meta_data.custom`）|

### 広告

|変数|説明|
|---|---|
|広告ブレーク名|（`adbreak.name`）|
|広告ブレークの位置|（`adbreak.position`）|
|広告ブレークの開始時間|（`adbreak.start_time`）|
|広告 ID|（`ad.id`）|
|広告タイトル|（`ad.title`）|
|広告タイプ|（`ad.type`）|
|広告の長さ|（`ad.length`）|
|広告の位置|（`ad.position`）|

### 動画メタデータ

|変数|説明|
|---|---|
|動画のカスタムメタデータ|（`meta_data.custom`）|
|動画メタデータ：番組|（`meta_data.show`）|
|動画メタデータ：シーズン|（`meta_data.season`）|
|動画メタデータ：エピソード|（`meta_data.episode`）|
|動画メタデータ：アセット|（`meta_data.asset`）|
|動画メタデータ：ジャンル|（`meta_data.genre`）|
|動画メタデータ：放送日|（`meta_data.airDate`）|
|動画メタデータ：デジタル配信日|（`meta_data.digitalDate`）|
|動画メタデータ：レーティング|（`meta_data.rating`）|
|動画メタデータ：制作元|（`meta_data.originator`）|
|動画メタデータ：ネットワーク|（`meta_data.network`）|
|動画メタデータ：タイプ|（`meta_data.type`）|
|動画メタデータ：広告負荷|（`meta_data.adLoad`）|
|動画メタデータ：時間帯|（`meta_data.dayPart`）|
|動画メタデータ：フィード|（`meta_data.feed`）|
|動画メタデータ：形式|（`meta_data.format`）|

### 広告メタデータ

|変数|説明|
|---|---|
|広告のカスタムメタデータ|（`ad_meta_data.custom`）|
|広告メタデータ：広告主|（`ad_meta_data.advertiser`）|
|広告メタデータ：キャンペーン|（`ad_meta_data.campaign`）|
|広告メタデータ：クリエイティブ|（`ad_meta_data.creative`）|
|広告メタデータ：配置|（`ad_meta_data.placement`）|
|広告メタデータ：サイト|（`ad_meta_data.site`）|
|広告メタデータ：クリエイティブ URL|（`ad_meta_data.creativeURL`）|