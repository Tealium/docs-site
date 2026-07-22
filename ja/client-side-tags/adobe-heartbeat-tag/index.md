---
title: Adobe Heartbeat タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Adobe Heartbeat タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-heartbeat-tag/
---
## 動作原理

Adobe Heartbeat タグは、訪問がサイトのビデオとどのように対話するかについての広範なデータを収集します。ページ上でビデオが読み込まれると、Heartbeat はビデオの長さを通じて毎秒サーバーコールをトリガーし、再生位置、一時停止および再開アクション、広告ビュー、その他いくつかのビデオパフォーマンスパラメータをキャプチャします。さらに、実装が Nielsen DCR プラグインと統合されている場合、このタグでそれらのパラメータを一緒に構成できます。

## 前提条件

* **jQuery**  
サイトに jQuery がインストールされていることを確認してください。jQuery を使用していない場合は、Tealium iQ タグマーケットプレイスから新しい jQuery タグを追加して構成できます。
* **Adobe Enterprise Cloud ID Service タグ**  
[Adobe Cloud Service](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) は、サイトの訪問ごとに一意の ID を生成し、すべての Enterprise Cloud ソリューション間で ID を維持し、重複カウントを防ぎます。まだ行っていない場合は、プロファイルにタグを追加して構成し、すべてのページの `utag.js` にバンドルできるようにバンドルフラグ構成を有効にしてください。
* [**AppMeasurement JavaScript タグ**](https://docs.tealium.com/ja/client-side-tags/adobe-appmeasurement-for-js-tag/)  
同じプロファイルでタグを追加して構成し、まだ行っていない場合はバンドルフラグを有効にしてください。これは JavaScript 実装に必要です。バンドルはタグバージョン 1.6.3 のみで必要であり、以前のバージョンでは既に Enterprise Cloud Service がデフォルトでバンドルされています。  

<blockquote>
タグタブで、バンドルされた Enterprise Cloud ID タグがバンドルされた AppMeasurement タグの上に配置されていることを確認してください。これにより、Enterprise Cloud ID タグが最初に読み込まれます。
</blockquote>


## サポートされるベンダーライブラリ

* Adobe Heartbeat v2.0.2 (デフォルト)
* Adobe Heartbeat v1.6.7
* Adobe Heartbeat v1.6.7 に Nielsen v5.0 を統合

## タグのヒント

* Heartbeat は、Adobe Experience Cloud ID Service および AppMeasurement for JS が最初に読み込まれる必要があります。できればバンドルされていることが望ましいです。
* このタグは "utag.track('video', data);" を介して発火され、ビデオイベントハンドラーで実装する必要があります。
* Adobe Heartbeat には jQuery が必要です。

## タグの構成

まず、Tealium のタグマーケットプレイスにアクセスして Adobe Heartbeat タグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)を参照してください）。

タグを追加した後、次の構成を構成します：

|フィールド名| フィールド値|
|---| ---|
|タイトル|  <ul><li>(必須) タグを識別するための一意の名前を入力してください。</li><li>複数のインスタンスを追加する場合は重要です。</li></ul> |
|トラッキングサーバー|  <ul><li>(必須) Adobe Heartbeat トラッキングサーバー。</li><li>すべてのハートビートトラッキングコールが送信されるサーバー URL を入力してください。</li><li>URLがわからない場合は、Adobe の担当者に連絡してください。</li><li>例：`.hb.omtrdc.net`</li></ul> |
|パブリッシャー|  <ul><li>(必須) Adobe の担当者によって割り当てられたパブリッシャー名を入力してください。</li></ul> |
|SSL の使用|  <ul><li>このフラグは、ハートビートコールを HTTPS で送信するかどうかを決定します。</li><li>デフォルト値は `False` で、SSL は無効です。</li><li>トラッキングコールを安全に送信したい場合は、値を `True` に切り替えることができます。</li></ul> |
|S-Object 名|  <ul><li>(必須) 独自のカスタム s-object 変数名を構成してください。</li><li>わからない場合は、デフォルト値の `s` を使用してください。</li></ul> |
|ビデオプラットフォーム名|  <ul><li>(オプション) コンテンツが配信されるオンラインビデオプラットフォームの名前。</li></ul> |
|ビデオプレーヤー SDK|  <ul><li>(オプション) ビデオプレーヤーアプリ/SDKのバージョン。</li></ul> |
|タグバージョン|  <ul><li>このドロップダウンリストを使用して、Nielsen 統合ありまたはなしの Adobe Heartbeat トラッキングを選択できます。</li><li>利用可能なオプションは次のとおりです：<ul><li>Adobe Heartbeat 2.0.2 (デフォルト)</li><li>Adobe Heartbeat 1.6.7</li><li>Adobe Heartbeat 1.6.7 に Nielsen 5.0 を統合</li></ul> </li></ul> |

次のフィールドは、タグバージョンを **Adobe Heartbeat 1.6.7 with Nielsen 5.0** に構成した場合のみ必要です。必要な Nielsen の値がない場合は、Nielsen または Adobe の担当者に連絡してください。

|フィールド名| フィールド値|
|---| ---|
|Adobe Nielsen SDK 構成キー|  <ul>(Nielsen 用に必須) Nielsen 構成キーを入力してください</li><li>Nielsen 統合用の構成 SDK キーです。</li></ul> |
|Nielsen コレクション環境|  <ul>(Nielsen 用に必須) コレクション環境の場所。</li><li>Nielsen のコレクション環境の場所を入力してください</li><li>例：`eu-cert` または `eu`。</li></ul> |
|Nielsen プレーヤー ID|  <ul>(Nielsen 用に必須) ビデオプレーヤーに割り当てられた一意の識別子を入力してください</li><li>Nielsen によって提供されるプレーヤー/サイトの一意の ID。</li></ul> |
|Nielsen APN|  <ul>(Nielsen 用に必須) プレーヤー/サイトの説明を入力してください</li><li>プレーヤー/サイトを説明するためのユーザー定義の文字列値。</li></ul> |
|Nielsen クライアント ID|  <ul>(Nielsen 用に必須) Nielsen クライアント識別子を入力してください</li><li>VA Beacon 測定用の一意の ID。</li></ul> |
|Nielsen VCID|  <ul>(Nielsen 用に必須) ビデオチャンネル識別子を入力してください。</li><li>VA Beacon 測定用の一意の ID。</li></ul> |

## 読み込みルールの適用

[読み込みルール](https://docs.tealium.com/about-load-rules/) は、サイト上のどのページにこのタグのインスタンスを読み込むかを決定します。すべてのページに読み込むルールがデフォルトの読み込みルールです。このタグを特定のページに読み込むためには、関連するルール条件を作成してタグに適用してください。


<blockquote>
ベストプラクティス：ビデオが提供されるページにこのタグを読み込むためのカスタムルールを作成して適用してください。
</blockquote>


## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/) からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/) を参照してください。

次のセクションでは、利用可能な各カテゴリについて詳細な表を提供します。
### 標準

標準カテゴリは[タグの構成フィールド](#tag_configs)に対応しています。これらの目的地に値をマッピングできます。空白のままのタグフィールドに動的に値を送信するか、現在の値を上書きします。

|目的地名| 説明|
|---| ---|
|`tracking_server`|  <ul><li>Adobe Heartbeat トラッキングサーバー。</li><li>すべてのハートビートトラッキングコールが送信されるサーバーのURL。</li></ul> |
|`publisher`|  <ul><li>Adobe Heartbeat パブリッシャー。</li><li>Adobe担当者によって割り当てられたパブリッシャー名。</li></ul> |
|`ssl`|  <ul><li>Adobe Heartbeat SSLフラグ。</li><li>ハートビートコールをHTTPSで送信するかどうかを決定するブール値フラグ。</li><li>マッピングする変数が `true` または `false` のブール値であることを確認してください。</li><li>マッピングは現在のドロップダウン選択を上書きします。</li></ul> |
|`syndication_channel`|  <ul><li>Adobe Heartbeat チャンネル。</li><li>チャンネルのシンジケーション名。</li></ul> |
|`online_video_platform_name`|  <ul><li>Adobe Heartbeat ビデオプラットフォーム名。</li><li>ビデオコンテンツをレンダリングするオンラインプラットフォームの名前。</li></ul> |
|`player_sdk`|  <ul><li>Adobe Heartbeat プレイヤーSDK。</li><li>ビデオプレイヤーアプリ/SDKのバージョン。</li></ul> |
|`debug_logging`|  <ul><li>Adobe Heartbeat デバッグログフラグ。</li><li>Heartbeatプラグイン内の各コンポーネントのログを有効/無効にするブール値フラグ。</li><li>Adobeは、アクティブなログがパフォーマンスに影響を与えるため、プレイヤーの製品版でこのフラグを無効にすることを推奨します。</li></ul> |

次のフィールドは、タグのバージョンを **Adobe Heartbeat 1.6.7 with Nielsen 5.0** に構成した場合にのみ必要です。必要なNielsen値がない場合は、NielsenまたはAdobeの担当者に連絡してください。

|目的地名| 説明|
|---| ---|
|`nielsen_config_key`|  <ul><li>Adobe Nielsen SDK構成キー。</li><li>Adobe Heartbeatと統合するためのNielsen構成キー。</li></ul> |
|`nielsen_client_id`|  <ul><li>NielsenクライアントID。</li><li>あなたのNielsenクライアント識別子。</li></ul> |
|`nielsen_vcid`|  <ul><li>Nielsen VCID。</li><li>ビデオチャンネル識別子。</li></ul> |
|`nielsen_collection_environment`|  <ul><li>Nielsen収集環境。</li><li>Nielsenの収集環境の場所。</li></ul> |
|`nielsen_player_id`|  <ul><li>NielsenプレイヤーID。</li><li>ビデオプレイヤーの一意の識別子。</li></ul> |
|`nielsen_apn`|  <ul><li>Nielsen APN。</li><li>プレイヤー/サイトの説明で、文字列値として表現されます。</li></ul> |
|`nielsen_device_id`|  <ul><li>NielsenデバイスID。</li><li>ビデオを追跡したいモバイル/タブレットの一意の識別子。</li></ul> |
|`nielsen_sdk_debug`|  <ul><li>Nielsen SDKデバッグフラグ。</li><li>Nielsen統合のログを有効/無効にするブール値フラグ。</li></ul> |
|`nielsen_opt_out`|  <ul><li>Nielsenオプトアウトフラグ。</li><li>現在の訪問に対してすべてのNielsenトラッキングを無効にします。</li><li>`opt-out` イベントのトリガーが必要です。</li></ul> |

### ビデオイベント

ビデオイベントの目的地は、ビデオプレイヤーで特定のアクションまたは変更が発生したときにトリガーされるイベントリスナーです。イベントをトリガーするには、変数をツールボックスのイベントにマッピングし、変数の値をトリガーとして構成する必要があります。提供されたトリガー値がデータレイヤーで見つかると、マッピングされたイベントが発火します。

以下の表は利用可能なイベントの目的地をリストしています：

|目的地名| 説明|
|---| ---|
|`video_load`|  <ul><li>ビデオロード。</li><li>ビデオが再生準備ができていることを示します。</li></ul> |
|`video_start`|  <ul><li>ビデオスタート。</li><li>ビデオが再生を開始したことを示します。次の3つのシナリオのいずれかの後に発生する可能性があります：<ul><li>初期ローディング</li><li>バッファリング</li><li>広告表示</li></ul> </li></ul> |
|`video_playing`|  <ul><li>ビデオ再生中。</li><li>ビデオが現在再生中であることを示します。</li><li>QoSデータを更新するために使用します。</li><li>広告が再生されているときには呼び出さないでください。</li></ul> |
|`video_pause`|  <ul><li>ビデオ一時停止。</li><li>ビデオが一時停止されたことを示します。</li></ul> |
|`video_play`|  <ul><li>ビデオ再生。</li><li>ビデオが再生中であることを示します。バッファリングまたはシークが完了した後に発生する可能性があります。</li></ul> |
|`video_stop`|  <ul><li>ビデオ停止。</li><li>ビデオが手動で停止されたことを示します。</li></ul> |
|`video_resume`|  <ul><li>ビデオ再開。</li><li>視聴者がビデオの一時停止を解除して再生を再開したことを示します。</li></ul> |
|`video_complete`|  <ul><li>ビデオ完了。</li><li>ビデオが終了したことを示します。</li></ul> |
|`video_seek`|  <ul><li>ビデオシーク。</li><li>視聴者がビデオのシークを開始したことを示します。</li></ul> |
|`video_buffer`|  <ul><li>ビデオバッファ。</li><li>ビデオがバッファリングを開始したことを示します。</li></ul> |
|`video_skip`|  <ul><li>ビデオスキップ。</li><li>視聴者がビデオまたは広告をスキップしたことを示します。</li></ul> |
|`video_error`|  <ul><li>ビデオエラー。</li><li>ビデオがエラーに遭遇したことを示します。</li></ul> |
|`nielsen_opt_out_status_changed`|  <ul><li>Nielsenオプトアウトステータス変更。</li><li>視聴者がオプトインからオプトアウト、またはその逆に切り替えたことを示します。</li></ul> |

### ビデオ

これらの目的地は、[Adobeビデオ測定パラメータ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html)に対応しています。

|目的地名| 説明|
|---| ---|
|`video.id`|  <ul><li>ビデオID。</li><li>ビデオの一意の識別子。</li></ul> |
|`video.title`|  <ul><li>ビデオタイトル。</li><li>追跡されているビデオの名前。</li></ul> |
|`video.length`|  <ul><li>ビデオの長さ。</li><li>ビデオアセットの期間（秒単位）。</li></ul> |
|`video.current_playhead`|  <ul><li>ビデオ現在の再生位置。</li><li>広告コンテンツを除く、ビデオのプレイヤーの現在の位置（秒単位）。</li></ul> |
|`video.stream_type`|  <ul><li>ビデオストリームタイプ。</li><li>ビデオアセットのタイプ。</li></ul> |
|`video.is_full_episode`|  <ul><li>ビデオはフルエピソードです。</li><li>ビデオコンテンツがフルエピソードであるかどうかを示すブール値フラグ。<ul><li>`Y` はフルエピソード。</li><li>`N` は部分的なクリップ。</li></ul> </li></ul> |
|`video.original_air_date_nielsen`|  <ul><li>ニールセン用ビデオのオリジナル放送日。</li><li>エピソードのオリジナル放送日、形式。</li><li>例：`YYYYMMDDHH24:MI:SS`</li></ul> |
|`video.channel_name`|  <ul><li>ビデオチャンネル名。</li><li>送信されるプログラムまたはフィードの名前。</li></ul> |
|`video.series_name`|  <ul><li>ビデオシリーズ名。</li><li>視聴されているプログラム（シリーズ名）の名前。</li></ul> |
|`video.player_name`|  <ul><li>ビデオプレイヤー名。</li><li>コンテンツを再生しているビデオプレイヤーの名前。</li></ul> |
|`video.is_ad`|  <ul><li>ビデオは広告です。</li><li>ビデオが広告であるかどうかを示すブール値。</li></ul> |
|`video.fps`|  <ul><li>ビデオFPS。</li><li>メディアのフレームレート、フレーム毎秒（FPS）。</li></ul> |
|`video.bit_rate`|  <ul><li>ビデオビットレート。</li><li>ビデオコンテンツのビット毎秒の属性。</li></ul> |
|`video.startup.time`|  <ul><li>ビデオ起動時間。</li><li>ビデオコンテンツの開始時間（秒単位）。</li></ul> |
|`video.dropped_frames`|  <ul><li>ビデオドロップフレーム。</li><li>再生セッション中にドロップされたすべてのフレームの合計。</li></ul> |
|`video.error_id`|  <ul><li>ビデオエラーID。</li><li>再生中に発生したエラーのID。</li></ul> |
|`video.error_is_fatal`|  <ul><li>ビデオエラーは致命的です。</li><li>エラーが再生の続行を防ぐかどうかを示すブール値。</li></ul> |
### チャプター

これらの目的地は [Adobe Video Chapter Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`chapter.name`|  <ul><li>チャプター名。</li><li>個々のチャプターの名前。</li></ul> |
|`chapter.length`|  <ul><li>チャプターの長さ。</li><li>チャプターの総時間（秒）。</li></ul> |
|`chapter.position`|  <ul><li>チャプターの位置。</li><li>ビデオコンテンツ内のチャプターの位置。</li></ul> |
|`chapter.start_time`|  <ul><li>チャプター開始時間。</li><li>メインコンテンツ内でチャプターが始まるオフセット。</li></ul> |
|`chapter_meta_data.custom`|  <ul><li>チャプターカスタムメタデータ。</li><li>チャプターに関連する追加のカスタム値。</li></ul> |

### 広告

これらの目的地は [Adobe Video Ad Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`adbreak.name`|  <ul><li>広告ブレイク名。</li><li>個々の広告ブレイクの名前。</li></ul> |
|`adbreak.position`|  <ul><li>広告ブレイクの位置。</li><li>ビデオコンテンツ内の広告ブレイクの位置（インデックス）。</li><li>`video.is_ad` フラグが `True` に構成されている場合に必要です。</li></ul> |
|`dbreak.start_time`|  <ul><li>広告ブレイク開始時間。</li><li>メインコンテンツ内で広告ブレイクが始まるオフセット。</li></ul> |
|`ad.id`|  <ul><li>広告ID。</li><li>表示される広告のユニークな識別子。</li></ul> |
|`ad.title`|  <ul><li>広告タイトル。</li><li>広告の名前。</li></ul> |
|`ad.type`|  <ul><li>広告タイプ。</li><li>広告のタイプまたはカテゴリー。</li></ul> |
|`ad.length`|  <ul><li>広告の長さ。</li><li>広告の総時間（秒）。</li></ul> |
|`ad.position`|  <ul><li>広告の位置。</li><li>ビデオコンテンツ内の広告の位置（インデックス）。</li><li>`video.is_ad` フラグが `True` に構成されている場合に必要です。</li></ul> |

### ビデオメタデータ

これらの目的地は [Adobe Standard Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`meta_data.custom`|  <ul><li>ビデオカスタムメタデータ。</li><li>ビデオに関連する追加のカスタム値。</li></ul> |
|`meta_data.show`|  <ul><li>ビデオメタデータショー。</li><li>ショーの名前。</li></ul> |
|`meta_data.season`|  <ul><li>ビデオメタデータシーズン。</li><li>シーズン番号。</li></ul> |
|`meta_data.episode`|  <ul><li>ビデオメタデータエピソード。</li><li>エピソード番号。</li></ul> |
|`meta_data.asset`|  <ul><li>ビデオメタデータアセット。</li><li>ビデオアセット識別子、TMS ID（Tribune Media Service）としても知られています。</li></ul> |
|`meta_data.genre`|  <ul><li>ビデオメタデータジャンル。</li><li>ビデオコンテンツのジャンル。</li></ul> |
|`meta_data.airDate`|  <ul><li>ビデオメタデータ放送日。</li><li>アセットがテレビで初めて放送された日付。</li></ul> |
|`meta_data.digitalDate`|  <ul><li>ビデオメタデータデジタル放送日。</li><li>アセットがデジタルで初めて利用可能になった日付。</li></ul> |
|`meta_data.rating`|  <ul><li>ビデオメタデータ評価。</li><li>ビデオコンテンツの評価。</li></ul> |
|`meta_data.originator`|  <ul><li>ビデオメタデータ発信者。</li><li>ビデオの発信者の名前。</li></ul> |
|`meta_data.network`|  <ul><li>ビデオメタデータネットワーク。</li><li>ショーに関連するネットワークの名前。</li></ul> |
|`meta_data.type`|  <ul><li>ビデオメタデータタイプ。</li><li>ショーのタイプ。</li></ul> |
|`meta_data.adLoad`|  <ul><li>ビデオメタデータ広告ロード。</li><li>広告ロードのメタデータ。</li></ul> |
|`meta_data.dayPart`|  <ul><li>ビデオメタデータデイパート。</li><li>広告表示が予定されている日の部分。</li></ul> |
|`meta_data.feed`|  <ul><li>ビデオメタデータフィード。</li><li>プログラミングフィードのタイプ。</li></ul> |
|`meta_data.format`|  <ul><li>ビデオメタデータフォーマット。</li><li>ビデオのストリームフォーマット。</li></ul> |

### 広告メタデータ

これらの目的地は [Adobe Standard Ad Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`ad_meta_data.custom`|  <ul><li>広告カスタムメタデータ。</li><li>表示される広告に関連する追加のカスタム値。</li></ul> |
|`ad_meta_data.advertiser`|  <ul><li>広告メタデータ広告主。</li><li>広告を表示している会社/ブランドの名前。</li></ul> |
|`ad_meta_data.campaign`|  <ul><li>広告メタデータキャンペーン。</li><li>広告キャンペーン識別子。</li></ul> |
|`ad_meta_data.creative`|  <ul><li>広告メタデータクリエイティブ。</li><li>広告をレンダリングするためのクリエイティブアセット。</li></ul> |
|`ad_meta_data.placement`|  <ul><li>広告メタデータ配置。</li><li>ビデオ内の広告の位置に関連するメタデータ。</li></ul> |
|`ad_meta_data.site`|  <ul><li>広告メタデータサイト。</li><li>広告に関連するサイト。</li></ul> |
|`ad_meta_data.creativeURL`|  <ul><li>広告メタデータクリエイティブURL。</li><li>表示される広告のURL。</li></ul> |
## ビルトイン動画データレイヤー変数

データレイヤーがすでにこれらの値を使用している場合、マッピングは必要ありません。Tealiumは通常、データを対応するタグの宛先に送信します。データレイヤーがこの表に記載されている変数名と異なる変数名を使用している場合は、手動でマップする必要があります。

|ビルトイン変数| ツールボックス宛先変数| 説明|
|---| ---| ---|
|`event_name`| [動画イベント宛先](#video_events_mapping)|  `event_name`変数で以下の値を使用している場合、ツールボックスで再度マップする必要はありません。<ul><li>`load` は `video_load` にマップされます</il><li>`start` は `video_start` にマップされます</il><li>`playing` は `video_playing` にマップされます</il><li>`pause` は `video_pause` にマップされます</il><li>`play` は `video_play` にマップされます</il><li>`stop` は `video_stop` にマップされます</il><li>`resume` は `video_resume` にマップされます</il><li>`complete` は `video_complete` にマップされます</il><li>`seek` は `video_seek` にマップされます</il><li>`buffer` は `video_buffer` にマップされます</il><li>`optstatus` は `Nielsen_opt_out_status_changed` にマップされます</li></ul> |
|`video_id`| --|  <ul><li>動画の一意の識別子。</li></ul> |
|`video_name`| `video.title`|  <ul><li>動画タイトル。</li><li>追跡されている動画の名前。</li></ul> |
|`video_length`| `video.length`|  <ul><li>動画の長さ。</li><li>動画アセットの期間（秒単位）。</li></ul> |
|`video_player_name`| `video.player_name`|  <ul><li>動画プレーヤー名。</li><li>コンテンツを再生している動画プレーヤーの名前。</li></ul> |
|`video_current_playhead`| `video.current_playhead`|  <ul><li>動画の現在の再生位置。</li><li>広告コンテンツを除く、動画内のプレーヤーの現在位置（秒単位）。</li></ul> |
|`video_stream_type`| `video.stream_type`|  <ul><li>動画ストリームタイプ。</li><li>動画アセットのタイプ。</li></ul> |
|`video_fps`| `video.fps`|  <ul><li>動画FPS。</li><li>メディアのフレームレート、フレーム毎秒（FPS）。</li></ul> |
|`video_bitrate`| `video.bit_rate`|  <ul><li>動画ビットレート。</li><li>動画コンテンツのビット毎秒の属性。</li></ul> |
|`video_dropped_frames`| `video.dropped_frames`|  <ul><li>動画ドロップフレーム。</li><li>再生セッション中にドロップされたすべてのフレームの合計。</li></ul> |
|`video_is_ad`| `video.is_ad`|  <ul><li>動画が広告かどうか。</li><li>動画が広告であるかどうかを示すブール値。</li></ul> |
|`video_ad_position` - OR - `video_ad_pod_position`| `ad.position`|  <ul><li>広告の位置。</li><li>動画コンテンツ内の広告の位置（インデックス）。</li><li>`video.is_ad`フラグが`true`に構成されている場合に必要です。</li></ul> |
|`video_chapter_name`| `chapter.name`|  <ul><li>チャプター名。</li><li>個々のチャプターの名前。</li></ul> |
|`video_chapter_length`| `chapter.length`|  <ul><li>チャプターの長さ。</li><li>チャプターの総期間（秒単位）。</li></ul> |
|`video_chapter_position`| `chapter.position`|  <ul><li>チャプターの位置。</li><li>動画コンテンツ内のチャプターの位置。</li></ul> |
|`video_chapter_start_time`| `chapter.start_time`|  <ul><li>チャプター開始時間。</li><li>チャプターが開始するメインコンテンツ内のオフセット。</li></ul> |
|`video_ad_pod_name`| `ad.id`|  <ul><li>広告ID。</li><li>表示されている広告の一意の識別子。</li></ul> |
|`program`| `video.series_name`|  <ul><li>動画シリーズ名。</li><li>視聴されているプログラム（シリーズ名）の名前。</li></ul> |
|`is_full_episode`| `video.is_full_episode`|  <ul><li>動画がフルエピソードかどうか。</li><li>動画コンテンツがフルエピソードであるかどうかを示すブールフラグ。<ul><li>`Y` はフルエピソード</li><li>`N` は部分的なクリップ</li></ul> </li></ul> |
|`original_air_date`| `video.original_air_date_nielsen`|  <ul><li>ニールセン用の動画のオリジナル放送日。</li><li>エピソードのオリジナル放送日、次の形式で: `YYYYMMDDHH24:MI:SS`</li></ul> |

## 検証

Heartbeatタグはイベントベースであり、他のutagコールと区別するために`utag.track("video", data)`コールを利用します。このため、[データマッピングツールボックスの動画イベントトリガーを適切に構成することが重要です](#video_events_mapping)。

構成後、タグは毎秒連続して発火し、動画データを最新の状態に保ちます。これは、動画プレーヤーの「playing」イベントハンドラ内で「playing」イベントを発火することによって達成されます。他の動画イベントもそれに対応するAdobe heartbeatイベントを通じて発火するべきです。ネットワークコールは集約され、イベントの変更を含む10秒ごとにAdobeに報告されます。


<blockquote>
HeartbeatとNielsenのデバッグフラグを構成する簡単な方法は、動画ページのURLにクエリ文字列パラメータを追加することです。例えば、`adobe_debug=1&Nielsen=1` <br>その後、クエリパラメータ変数をTealium iQのデータレイヤーに追加し、それに応じてマップします。<br>HeartbeatとNielsenのデバッグフラグのマッピング先はStandardカテゴリの下にあります。"Adobe Heartbeat Debug Logging Flag"と"Nielsen SDK Debug Flag"を参照してください。<br>完了したら、ブラウザコンソールで次のTealiumデバッグコマンドを実行できます。<br>
`document.cookie = "utagdb=true";`
</blockquote>


### サンプル実装

以下の例は、サンプルHeartbeat実装のネットワークコールを示しています。注意すべき主要なパラメータは`s:event:type`と`s:asset:type`です。これらのパラメータはそれぞれ、動画イベントのタイプとそれが関連する動画コンポーネントを示します。例では、広告表示前のメイン動画の始まりを示しています。また、表示される`l:event:playhead`は、メイン動画の経過時間を参照します。

`s:asset:type`の値は`ad`であり、`l:event:playhead`の値は`8`です。これは、広告が動画の8秒後に再生を開始したことを意味します。

## ベンダー文書

* [Adobe Video Heartbeatについて](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/)
* [Video Heartbeatライブラリ構成](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_setup-and-config.html)
* [Nielsen appinfoパラメータ](https://marketing.adobe.com/resources/help/en_US/dtm/nielsen.html)
* [動画測定パラメータ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/c_vhl_ios_video_params.html)
* [メタデータパラメータ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/c_vhl_stand-metadata_params_ios.html)
* [動画プレーヤーイベント](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_js_events.html)
