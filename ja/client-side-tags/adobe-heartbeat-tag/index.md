---
title: Adobe Heartbeatタグ構成ガイド
description: この記事では、タグ管理アカウントでAdobe Heartbeatタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-heartbeat-tag/
---
## 仕組み

Adobe Heartbeatタグを使用すると、サイト訪問が動画をどのように操作したかについて、広範なデータを収集できます。ページ上で動画が読み込まれると、Heartbeatは動画の再生中に1秒ごとにサーバー呼び出しをトリガーし、再生ヘッドの位置、一時停止と再開の操作、広告の視聴、およびその他の複数の動画パフォーマンスパラメータを取得します。また、実装がNielsen DCRプラグインと統合されている場合は、このタグでそれらのパラメータをまとめて構成できます。

## 前提条件

* **jQuery**  
サイトにjQueryがインストールされていることを確認してください。jQueryを使用していない場合は、タグ管理のタグマーケットプレイスから新しいjQueryタグを追加して構成できます。
* **Adobe Enterprise Cloud ID Serviceタグ**  
[Adobe Cloud Service](https://experienceleague.adobe.com/en/docs/id-service/using/intro/overview)は、サイトの各訪問に一意のIDを生成し、そのIDをすべてのEnterprise Cloudソリューションで保持することで、重複カウントを防止します。まだ行っていない場合は、プロファイルにタグを追加して構成し、すべてのページで`utag.js`にバンドルできるように、タグのバンドルフラグ構成を有効にします。
* [**AppMeasurement JavaScriptタグ**](https://docs.tealium.com/ja/client-side-tags/adobe-appmeasurement-for-js-tag/)  
まだ行っていない場合は、同じプロファイルにタグを追加して構成し、バンドルフラグを有効にします。これはJavaScript実装に必要です。以前のバージョンではEnterprise Cloud Serviceがデフォルトでバンドルされているため、バンドルが必要なのはタグバージョン1.6.3のみです。  

<blockquote>
「タグ」タブで、バンドルされたEnterprise Cloud IDタグが、バンドルされたAppMeasurementタグより上に配置されていることを確認してください。これにより、Enterprise Cloud IDタグが先に読み込まれます。
</blockquote>


## サポートされるベンダーライブラリ

* Adobe Heartbeat v2.0.2（デフォルト）
* Adobe Heartbeat v1.6.7
* Adobe Heartbeat v1.6.7（Nielsen v5.0統合）

## タグに関するヒント

* Heartbeatを使用するには、Adobe Experience Cloud ID ServiceとAppMeasurement for JSを先に読み込む必要があります。バンドルすることを推奨します。
* このタグは`"utag.track('video', data);"`によって発火します。これは動画イベントハンドラーに実装する必要があります。
* Adobe HeartbeatにはjQueryが必要です。

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

|フィールド名|フィールド値|
|---|---|
|タイトル|<ul><li>（必須）タグを識別するための一意の名前を入力します。</li><li>このタグのインスタンスを複数追加する場合に重要です。</li></ul>|
|トラッキングサーバー|<ul><li>（必須）Adobe Heartbeatトラッキングサーバー。</li><li>すべてのHeartbeatトラッキング呼び出しの送信先となるサーバーURLを入力します。</li><li>URLが不明な場合は、Adobe担当者にお問い合わせください。</li><li>例：`.hb.omtrdc.net`</li></ul>|
|パブリッシャー|<ul><li>（必須）Adobe担当者から割り当てられたパブリッシャー名を入力します。</li></ul>|
|SSLを使用|<ul><li>このフラグは、Heartbeat呼び出しをHTTPS経由で送信するかどうかを決定します。</li><li>デフォルト値は`False`で、SSLが無効であることを意味します。</li><li>トラッキング呼び出しを安全に送信する場合は、値を`True`に切り替えることができます。</li></ul>|
|Sオブジェクト名|<ul><li>（必須）独自のカスタムSオブジェクト変数名を構成します。</li><li>不明な場合は、デフォルト値の`s`を使用してください。</li></ul>|
|動画プラットフォーム名|<ul><li>（任意）コンテンツの配信に使用されるオンライン動画プラットフォームの名前。</li></ul>|
|動画プレーヤーSDK|<ul><li>（任意）動画プレーヤーアプリ／SDKのバージョン。</li></ul>|
|タグバージョン|<ul><li>このドロップダウンリストでは、Nielsen統合を使用するかどうかを含め、Adobe Heartbeatトラッキングを選択できます。</li><li>使用可能なオプションは次のとおりです。<ul><li>Adobe Heartbeat 2.0.2（デフォルト）</li><li>Adobe Heartbeat 1.6.7</li><li>Adobe Heartbeat 1.6.7（Nielsen 5.0対応）</li></ul></li></ul>|

次のフィールドは、タグバージョンを**Adobe Heartbeat 1.6.7（Nielsen 5.0対応）**に構成した場合にのみ必要です。必要なNielsen値が不明な場合は、NielsenまたはAdobeの担当者にお問い合わせください。

|フィールド名|フィールド値|
|---|---|
|Adobe Nielsen SDK構成キー|<ul>（Nielsenでは必須）Nielsen構成キーを入力します</li><li>Adobe HeartbeatとNielsenを統合するための構成SDKキー。</li></ul>|
|Nielsen収集環境|<ul>（Nielsenでは必須）収集環境の場所。</li><li>Nielsenの収集環境の場所を入力します</li><li>例：`eu-cert`または`eu`。</li></ul>|
|NielsenプレーヤーID|<ul>（Nielsenでは必須）動画プレーヤーに割り当てられた一意の識別子を入力します</li><li>Nielsenが提供する、プレーヤー／サイトに割り当てられた一意のID。</li></ul>|
|Nielsen APN|<ul>（Nielsenでは必須）プレーヤー／サイトの説明を入力します</li><li>プレーヤー／サイトを説明するためのユーザー定義の文字列値。</li></ul>|
|NielsenクライアントID|<ul>（Nielsenでは必須）Nielsenクライアント識別子を入力します</li><li>VA Beacon Measurement用の一意のID。</li></ul>|
|Nielsen VCID|<ul>（Nielsenでは必須）動画チャンネル識別子を入力します。</li><li>VA Beacon Measurement用の一意のID。</li></ul>|

## 読み込みルールの適用

[読み込みルール](https://docs.tealium.com/about-load-rules/)は、サイト上のどの場所で、いつこのタグのインスタンスを読み込むかを決定します。「すべてのページで読み込む」ルールがデフォルトの読み込みルールです。特定のページでこのタグを読み込むには、タグに適用する適切なルール条件を作成します。


<blockquote>
ベストプラクティス：動画を利用できるすべてのページでこのタグを読み込むためのカスタムルールを作成し、適用してください。
</blockquote>


## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

以降のセクションでは、使用可能な各カテゴリーの詳細な表を示します。
### 標準

「標準」カテゴリは、[タグの構成フィールド](#tag_configs)に対応します。これらの宛先に値をマッピングできます。空白のままになっているタグフィールドに値を動的に送信したり、現在の値を上書きしたりできます。

|宛先名|説明|
|---|---|
|`tracking_server`| <ul><li>Adobe Heartbeat トラッキングサーバー。</li><li>すべての Heartbeat トラッキング呼び出しの送信先となるサーバーの URL。</li></ul> |
|`publisher`| <ul><li>Adobe Heartbeat パブリッシャー。</li><li>Adobe の担当者によって割り当てられたパブリッシャー名。</li></ul> |
|`ssl`| <ul><li>Adobe Heartbeat SSL フラグ。</li><li>Heartbeat 呼び出しを HTTPS 経由で送信するかどうかを決定するブール値フラグ。</li><li>マッピングする変数には、`true` または `false` のいずれかのブール値が構成されていることを確認してください。</li><li>マッピングすると、現在のドロップダウンでの選択が上書きされます。</li></ul> |
|`syndication_channel`| <ul><li>Adobe Heartbeat チャネル。</li><li>シンジケーションチャネルの名前。</li></ul> |
|`online_video_platform_name`| <ul><li>Adobe Heartbeat ビデオプラットフォーム名。</li><li>ビデオコンテンツをレンダリングしているオンラインプラットフォームの名前。</li></ul> |
|`player_sdk`| <ul><li>Adobe Heartbeat Player SDK。</li><li>ビデオプレーヤーアプリ／SDK のバージョン。</li></ul> |
|`debug_logging`| <ul><li>Adobe Heartbeat デバッグログフラグ。</li><li>Heartbeat プラグイン内の各コンポーネントのログ記録を有効または無効にするブール値フラグ。</li><li>ログ記録を有効にするとパフォーマンスに影響するため、Adobe ではプレーヤーの本番バージョンでこのフラグを無効にすることを推奨しています。</li></ul> |

以下のフィールドは、タグのバージョンを **Adobe Heartbeat 1.6.7 with Nielsen 5.0** に構成した場合にのみ必要です。必要な Nielsen の値がない場合は、Nielsen または Adobe の担当者にお問い合わせください。

|宛先名|説明|
|---|---|
|`nielsen_config_key`| <ul><li>Adobe Nielsen SDK 構成キー。</li><li>Adobe Heartbeat と統合するための Nielsen 構成キー。</li></ul> |
|`nielsen_client_id`| <ul><li>Nielsen クライアント ID。</li><li>Nielsen のクライアント識別子。</li></ul> |
|`nielsen_vcid`| <ul><li>Nielsen VCID。</li><li>ビデオチャネルの識別子。</li></ul> |
|`nielsen_collection_environment`| <ul><li>Nielsen 収集環境。</li><li>Nielsen の収集環境の場所。</li></ul> |
|`nielsen_player_id`| <ul><li>Nielsen プレーヤー ID。</li><li>ビデオプレーヤーの一意の識別子。</li></ul> |
|`nielsen_apn`| <ul><li>Nielsen APN。</li><li>文字列値で表されるプレーヤー／サイトの説明。</li></ul> |
|`nielsen_device_id`| <ul><li>Nielsen デバイス ID。</li><li>ビデオをトラッキングするモバイルデバイス／タブレットの一意の識別子。</li></ul> |
|`nielsen_sdk_debug`| <ul><li>Nielsen SDK デバッグフラグ。</li><li>Nielsen 統合のログ記録を有効または無効にするブール値フラグ。</li></ul> |
|`nielsen_opt_out`| <ul><li>Nielsen オプトアウトフラグ。</li><li>現在の訪問に対するすべての Nielsen トラッキングを無効にします。</li><li>`opt-out` イベントをトリガーする必要があります。</li></ul> |

### ビデオイベント

ビデオイベントの宛先は、ビデオプレーヤーで特定の操作や変更が発生したときにトリガーされるイベントリスナーです。イベントをトリガーするには、ツールボックスで変数をイベントにマッピングし、その変数の値をトリガーとして構成する必要があります。指定されたトリガー値がデータレイヤー内で見つかると、マッピングされたイベントが発生します。

次の表に、利用可能なイベントの宛先を示します。

|宛先名|説明|
|---|---|
|`video_load`| <ul><li>ビデオの読み込み。</li><li>ビデオを再生する準備ができたことを示します。</li></ul> |
|`video_start`| <ul><li>ビデオの開始。</li><li>次の 3 つのいずれかの状況の後に、ビデオの再生が開始されたことを示します。<ul><li>初回読み込み</li><li>バッファリング</li><li>広告の表示</li></ul></li></ul> |
|`video_playing`| <ul><li>ビデオの再生中。</li><li>ビデオが現在再生中であることを示します。</li><li>QoS データの更新に使用します。</li><li>広告の再生中には呼び出さないでください。</li></ul> |
|`video_pause`| <ul><li>ビデオの一時停止。</li><li>ビデオが一時停止されたことを示します。</li></ul> |
|`video_play`| <ul><li>ビデオの再生。</li><li>バッファリングまたはシークの完了後などに、ビデオが再生されていることを示します。</li></ul> |
|`video_stop`| <ul><li>ビデオの停止。</li><li>ビデオが手動で停止されたことを示します。</li></ul> |
|`video_resume`| <ul><li>ビデオの再開。</li><li>視聴者がビデオの一時停止を解除し、再生を再開したことを示します。</li></ul> |
|`video_complete`| <ul><li>ビデオの完了。</li><li>ビデオが終了したことを示します。</li></ul> |
|`video_seek`| <ul><li>ビデオのシーク。</li><li>視聴者がビデオのシークを開始したことを示します。</li></ul> |
|`video_buffer`| <ul><li>ビデオのバッファリング。</li><li>ビデオのバッファリングが開始されたことを示します。</li></ul> |
|`video_skip`| <ul><li>ビデオのスキップ。</li><li>視聴者がビデオまたは広告をスキップしたことを示します。</li></ul> |
|`video_error`| <ul><li>ビデオエラー。</li><li>ビデオでエラーが発生したことを示します。</li></ul> |
|`nielsen_opt_out_status_changed`| <ul><li>Nielsen オプトアウトステータスの変更。</li><li>視聴者がオプトインからオプトアウト、またはその逆に切り替えたことを示します。</li></ul> |

### ビデオ

これらの宛先は、[Adobe Video Measurement のパラメーター](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters)に対応します。

|宛先名|説明|
|---|---|
|`video.id`| <ul><li>ビデオ ID。</li><li>ビデオの一意の識別子。</li></ul> |
|`video.title`| <ul><li>ビデオタイトル。</li><li>トラッキング対象のビデオの名前。</li></ul> |
|`video.length`| <ul><li>ビデオの長さ。</li><li>ビデオアセットの再生時間（秒単位）。</li></ul> |
|`video.current_playhead`| <ul><li>ビデオの現在の再生ヘッド位置。</li><li>広告コンテンツを除いた、ビデオ内のプレーヤーの現在位置（秒単位）。</li></ul> |
|`video.stream_type`| <ul><li>ビデオストリームタイプ。</li><li>ビデオアセットのタイプ。</li></ul> |
|`video.is_full_episode`| <ul><li>ビデオが完全なエピソードかどうか。</li><li>ビデオコンテンツが完全なエピソードかどうかを示すブール値フラグ。<ul><li>完全なエピソードの場合は `Y`。</li><li>部分的なクリップの場合は `N`。</li></ul></li></ul> |
|`video.original_air_date_nielsen`| <ul><li>Nielsen 用のビデオ初回放送日時。</li><li>エピソードの初回放送日時とその形式。</li><li>例：`YYYYMMDDHH24:MI:SS`</li></ul> |
|`video.channel_name`| <ul><li>ビデオチャネル名。</li><li>送信される番組またはフィードの名前。</li></ul> |
|`video.series_name`| <ul><li>ビデオシリーズ名。</li><li>視聴中の番組名（シリーズ名）。</li></ul> |
|`video.player_name`| <ul><li>ビデオプレーヤー名。</li><li>コンテンツを再生しているビデオプレーヤーの名前。</li></ul> |
|`video.is_ad`| <ul><li>ビデオが広告かどうか。</li><li>ビデオが広告であるかどうかを示すブール値。</li></ul> |
|`video.fps`| <ul><li>ビデオの FPS。</li><li>メディアのフレームレート（1 秒あたりのフレーム数（FPS））。</li></ul> |
|`video.bit_rate`| <ul><li>ビデオのビットレート。</li><li>ビデオコンテンツの 1 秒あたりのビット数を示す属性。</li></ul> |
|`video.startup.time`| <ul><li>ビデオの開始時間。</li><li>ビデオコンテンツの開始時間（秒単位）。</li></ul> |
|`video.dropped_frames`| <ul><li>ビデオのドロップフレーム。</li><li>1 回の再生セッション中にドロップしたすべてのフレームの合計。</li></ul> |
|`video.error_id`| <ul><li>ビデオエラー ID。</li><li>再生中に発生したエラーの ID。</li></ul> |
|`video.error_is_fatal`| <ul><li>ビデオエラーが致命的かどうか。</li><li>エラーによって再生を続行できなくなるかどうかを示すブール値。</li></ul> |
### チャプター

これらの送信先は、[Adobe 動画チャプターパラメーター](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/chapter-parameters)に対応しています。

|送信先名|説明|
|---|---|
|`chapter.name`| <ul><li>チャプター名。</li><li>各チャプターの名前。</li></ul> |
|`chapter.length`| <ul><li>チャプターの長さ。</li><li>チャプターの合計時間（秒単位）。</li></ul> |
|`chapter.position`| <ul><li>チャプターの位置。</li><li>動画コンテンツ内でのチャプターの位置。</li></ul> |
|`chapter.start_time`| <ul><li>チャプターの開始時間。</li><li>メインコンテンツ内でチャプターが開始される位置のオフセット。</li></ul> |
|`chapter_meta_data.custom`| <ul><li>チャプターのカスタムメタデータ。</li><li>チャプターに関連する追加のカスタム値。</li></ul> |

### 広告

これらの送信先は、[Adobe 動画広告パラメーター](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ad-parameters)に対応しています。

|送信先名|説明|
|---|---|
|`adbreak.name`| <ul><li>広告ブレーク名。</li><li>各広告ブレークの名前。</li></ul> |
|`adbreak.position`| <ul><li>広告ブレークの位置。</li><li>動画コンテンツ内での広告ブレークの位置（インデックス）。</li><li>`video.is_ad`フラグが`True`に構成されている場合は必須です。</li></ul> |
|`dbreak.start_time`| <ul><li>広告ブレークの開始時間。</li><li>メインコンテンツ内で広告ブレークが開始される位置のオフセット。</li></ul> |
|`ad.id`| <ul><li>広告 ID。</li><li>表示されている広告の一意の識別子。</li></ul> |
|`ad.title`| <ul><li>広告タイトル。</li><li>広告の名前。</li></ul> |
|`ad.type`| <ul><li>広告タイプ。</li><li>広告のタイプまたはカテゴリー。</li></ul> |
|`ad.length`| <ul><li>広告の長さ。</li><li>広告の合計時間（秒単位）。</li></ul> |
|`ad.position`| <ul><li>広告の位置。</li><li>動画コンテンツ内での広告の位置（インデックス）。</li><li>`video.is_ad`フラグが`True`に構成されている場合は必須です。</li></ul> |

### 動画メタデータ

これらの送信先は、[Adobe 標準メタデータパラメーター](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters)に対応しています。

|送信先名|説明|
|---|---|
|`meta_data.custom`| <ul><li>動画のカスタムメタデータ。</li><li>動画に関連する追加のカスタム値。</li></ul> |
|`meta_data.show`| <ul><li>動画メタデータの番組。</li><li>番組名。</li></ul> |
|`meta_data.season`| <ul><li>動画メタデータのシーズン。</li><li>シーズン番号。</li></ul> |
|`meta_data.episode`| <ul><li>動画メタデータのエピソード。</li><li>エピソード番号。</li></ul> |
|`meta_data.asset`| <ul><li>動画メタデータのアセット。</li><li>TMS ID（Tribune Media Service）とも呼ばれる動画アセットの識別子。</li></ul> |
|`meta_data.genre`| <ul><li>動画メタデータのジャンル。</li><li>動画コンテンツのジャンル。</li></ul> |
|`meta_data.airDate`| <ul><li>動画メタデータの放送日。</li><li>アセットがテレビで初めて放送された日付。</li></ul> |
|`meta_data.digitalDate`| <ul><li>動画メタデータのデジタル配信日。</li><li>アセットがデジタル形式で初めて利用可能になった日付。</li></ul> |
|`meta_data.rating`| <ul><li>動画メタデータのレーティング。</li><li>動画コンテンツに構成可能なレーティング。</li></ul> |
|`meta_data.originator`| <ul><li>動画メタデータの制作元。</li><li>動画制作元の名前。</li></ul> |
|`meta_data.network`| <ul><li>動画メタデータのネットワーク。</li><li>番組に関連付けられたネットワークの名前。</li></ul> |
|`meta_data.type`| <ul><li>動画メタデータのタイプ。</li><li>番組のタイプ。</li></ul> |
|`meta_data.adLoad`| <ul><li>動画メタデータの広告量。</li><li>広告量に関するメタデータ。</li></ul> |
|`meta_data.dayPart`| <ul><li>動画メタデータの時間帯。</li><li>広告の表示が予定されている時間帯。</li></ul> |
|`meta_data.feed`| <ul><li>動画メタデータのフィード。</li><li>番組フィードのタイプ。</li></ul> |
|`meta_data.format`| <ul><li>動画メタデータの形式。</li><li>動画のストリーム形式。</li></ul> |

### 広告メタデータ

これらの送信先は、[Adobe 標準広告メタデータパラメーター](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/ad-parameters)に対応しています。

|送信先名|説明|
|---|---|
|`ad_meta_data.custom`| <ul><li>広告のカスタムメタデータ。</li><li>表示されている広告に関連する追加のカスタム値。</li></ul> |
|`ad_meta_data.advertiser`| <ul><li>広告メタデータの広告主。</li><li>広告を表示している企業またはブランドの名前。</li></ul> |
|`ad_meta_data.campaign`| <ul><li>広告メタデータのキャンペーン。</li><li>広告キャンペーンの識別子。</li></ul> |
|`ad_meta_data.creative`| <ul><li>広告メタデータのクリエイティブ。</li><li>広告のレンダリングに使用するクリエイティブアセット。</li></ul> |
|`ad_meta_data.placement`| <ul><li>広告メタデータの配置。</li><li>動画内での広告の位置に関連するメタデータ。</li></ul> |
|`ad_meta_data.site`| <ul><li>広告メタデータのサイト。</li><li>広告に関連付けられたサイト。</li></ul> |
|`ad_meta_data.creativeURL`| <ul><li>広告メタデータのクリエイティブ URL。</li><li>表示されている広告の URL。</li></ul> |
## 組み込みの動画データレイヤー変数

データレイヤーですでに以下の値を使用している場合、マッピングは必要ありません。通常、Tealium は一致するタグの送信先にデータを送信します。データレイヤーで、この表に記載されているものとは異なる変数名を使用している場合は、手動でマッピングする必要があります。

|組み込み変数| Toolbox の送信先変数| 説明|
|---| ---| ---|
|`event_name`| [動画イベントの送信先](#video_events_mapping)| `event_name` 変数で以下のいずれかの値を使用する場合、Toolbox で再度マッピングする必要はありません。<ul><li>`load` は `video_load` にマッピングされます</il><li>`start` は `video_start` にマッピングされます</il><li>`playing` は `video_playing` にマッピングされます</il><li>`pause` は `video_pause` にマッピングされます</il><li>`play` は `video_play` にマッピングされます</il><li>`stop` は `video_stop` にマッピングされます</il><li>`resume` は `video_resume` にマッピングされます</il><li>`complete` は `video_complete` にマッピングされます</il><li>`seek` は `video_seek` にマッピングされます</il><li>`buffer` は `video_buffer` にマッピングされます</il><li>`optstatus` は `Nielsen_opt_out_status_changed` にマッピングされます</li></ul> |
|`video_id`| --| <ul><li>動画の一意の識別子。</li></ul> |
|`video_name`| `video.title`| <ul><li>動画タイトル。</li><li>トラッキング対象の動画名。</li></ul> |
|`video_length`| `video.length`| <ul><li>動画の長さ。</li><li>動画アセットの再生時間（秒単位）。</li></ul> |
|`video_player_name`| `video.player_name`| <ul><li>動画プレーヤー名。</li><li>コンテンツを再生している動画プレーヤーの名前。</li></ul> |
|`video_current_playhead`| `video.current_playhead`| <ul><li>動画の現在の再生ヘッド位置。</li><li>広告コンテンツを除いた、動画内でのプレーヤーの現在位置（秒単位）。</li></ul> |
|`video_stream_type`| `video.stream_type`| <ul><li>動画ストリームタイプ。</li><li>動画アセットのタイプ。</li></ul> |
|`video_fps`| `video.fps`| <ul><li>動画の FPS。</li><li>メディアのフレームレート（1 秒あたりのフレーム数、FPS）。</li></ul> |
|`video_bitrate`| `video.bit_rate`| <ul><li>動画のビットレート。</li><li>動画コンテンツの 1 秒あたりのビット数を示す属性。</li></ul> |
|`video_dropped_frames`| `video.dropped_frames`| <ul><li>動画のドロップフレーム数。</li><li>再生セッション中にドロップした全フレームの合計。</li></ul> |
|`video_is_ad`| `video.is_ad`| <ul><li>動画が広告であるかどうか。</li><li>動画が広告であるかどうかを示すブール値。</li></ul> |
|`video_ad_position` - または - `video_ad_pod_position`| `ad.position`| <ul><li>広告の位置。</li><li>動画コンテンツ内における広告の位置（インデックス）。</li><li>`video.is_ad ` フラグが `true` に構成されている場合は必須です。</li></ul> |
|`video_chapter_name`| `chapter.name`| <ul><li>チャプター名。</li><li>各チャプターの名前。</li></ul> |
|`video_chapter_length`| `chapter.length`| <ul><li>チャプターの長さ。</li><li>チャプターの合計再生時間（秒単位）。</li></ul> |
|`video_chapter_position`| `chapter.position`| <ul><li>チャプターの位置。</li><li>動画コンテンツ内におけるチャプターの位置。</li></ul> |
|`video_chapter_start_time`| `chapter.start_time`| <ul><li>チャプターの開始時間。</li><li>メインコンテンツ内でチャプターが開始する位置のオフセット。</li></ul> |
|`video_ad_pod_name`| `ad.id`| <ul><li>広告 ID。</li><li>表示されている広告の一意の識別子。</li></ul> |
|`program`| `video.series_name`| <ul><li>動画シリーズ名。</li><li>視聴中の番組名（シリーズ名）。</li></ul> |
|`is_full_episode`| `video.is_full_episode`| <ul><li>動画が完全なエピソードであるかどうか。</li><li>動画コンテンツが完全なエピソードであるかどうかを示すブールフラグ。<ul><li>完全なエピソードの場合は `Y`</li><li>部分的なクリップの場合は `N`</li></ul> </li></ul> |
|`original_air_date`| `video.original_air_date_nielsen`| <ul><li>Nielsen 用の動画の初回放送日時。</li><li>エピソードの初回放送日時。形式は `YYYYMMDDHH24:MI:SS` です。</li></ul> |

## 検証

Heartbeat タグはイベントベースであり、他の utag 呼び出しと区別するために `utag.track("video", data)` 呼び出しを利用します。このため、[Data Mapping Toolbox で動画イベントトリガー](#video_events_mapping)を適切に構成することが重要です。

構成後、動画データを最新の状態に保つため、タグは 1 秒ごとに継続して発火します。これは、動画プレーヤーの「playing」イベントハンドラー内で「playing」イベントを発火させることで実現します。その他の動画イベントも、対応する Adobe Heartbeat イベントを通じて発火させる必要があります。イベントの変更に関するものを含め、ネットワーク呼び出しは集約され、10 秒ごとに Adobe に送信されます。


<blockquote>
Heartbeat と Nielsen の両方のデバッグフラグを簡単に構成するには、動画ページの URL にクエリ文字列パラメータを追加します。たとえば、`adobe_debug=1&Nielsen=1` のように指定します。<br>その後、Tag Management のデータレイヤーにクエリパラメータ変数を追加し、適切にマッピングできます。<br>Heartbeat と Nielsen の両方のデバッグフラグに対応するマッピング先は、Standard カテゴリにあります。「Adobe Heartbeat Debug Logging Flag」と「Nielsen SDK Debug Flag」を参照してください。<br>構成が完了したら、ブラウザーコンソールで次の Tealium デバッグコマンドを実行できます。<br>
`document.cookie = "utagdb=true";`
</blockquote>


### 実装例

以下の例は、Heartbeat の実装例におけるネットワーク呼び出しを示しています。特に注目すべき主なパラメータは、`s:event:type` と `s:asset:type` です。これらのパラメータは、それぞれ動画イベントのタイプと、そのイベントが関連する動画コンポーネントを示します。この例では、広告が表示される前にメイン動画が開始する場面を示しています。また、`l:event:playhead` はメイン動画の経過時間を表します。

`s:asset:type` の値は `ad`、`l:event:playhead` の値は `8` です。これは、動画の開始から 8 秒後に広告の再生が始まったことを意味します。

## ベンダーのドキュメント

* [Adobe Video Heartbeat について](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview)
* [Video Heartbeat ライブラリの構成](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/overview)
* [動画測定パラメータ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters)
* [メタデータパラメータ](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters)
* [動画プレーヤーイベント](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/overview)