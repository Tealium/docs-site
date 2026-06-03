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
* [**AppMeasurement JavaScript タグ**](/ja/client-side-tags/adobe-appmeasurement-for-js-tag/)  
同じプロファイルでタグを追加して構成し、まだ行っていない場合はバンドルフラグを有効にしてください。これは JavaScript 実装に必要です。バンドルはタグバージョン 1.6.3 のみで必要であり、以前のバージョンでは既に Enterprise Cloud Service がデフォルトでバンドルされています。  
タグタブで、バンドルされた Enterprise Cloud ID タグがバンドルされた AppMeasurement タグの上に配置されていることを確認してください。これにより、Enterprise Cloud ID タグが最初に読み込まれます。

## サポートされるベンダーライブラリ

* Adobe Heartbeat v2.0.2 (デフォルト)
* Adobe Heartbeat v1.6.7
* Adobe Heartbeat v1.6.7 に Nielsen v5.0 を統合

## タグのヒント

* Heartbeat は、Adobe Experience Cloud ID Service および AppMeasurement for JS が最初に読み込まれる必要があります。できればバンドルされていることが望ましいです。
* このタグは &#34;utag.track(&#39;video&#39;, data);&#34; を介して発火され、ビデオイベントハンドラーで実装する必要があります。
* Adobe Heartbeat には jQuery が必要です。

## タグの構成

まず、Tealium のタグマーケットプレイスにアクセスして Adobe Heartbeat タグを追加します（[タグの追加方法についてはこちら]()を参照してください）。

タグを追加した後、次の構成を構成します：

|フィールド名| フィールド値|
|---| ---|
|タイトル|  &lt;ul&gt;&lt;li&gt;(必須) タグを識別するための一意の名前を入力してください。&lt;/li&gt;&lt;li&gt;複数のインスタンスを追加する場合は重要です。&lt;/li&gt;&lt;/ul&gt; |
|トラッキングサーバー|  &lt;ul&gt;&lt;li&gt;(必須) Adobe Heartbeat トラッキングサーバー。&lt;/li&gt;&lt;li&gt;すべてのハートビートトラッキングコールが送信されるサーバー URL を入力してください。&lt;/li&gt;&lt;li&gt;URLがわからない場合は、Adobe の担当者に連絡してください。&lt;/li&gt;&lt;li&gt;例：`.hb.omtrdc.net`&lt;/li&gt;&lt;/ul&gt; |
|パブリッシャー|  &lt;ul&gt;&lt;li&gt;(必須) Adobe の担当者によって割り当てられたパブリッシャー名を入力してください。&lt;/li&gt;&lt;/ul&gt; |
|SSL の使用|  &lt;ul&gt;&lt;li&gt;このフラグは、ハートビートコールを HTTPS で送信するかどうかを決定します。&lt;/li&gt;&lt;li&gt;デフォルト値は `False` で、SSL は無効です。&lt;/li&gt;&lt;li&gt;トラッキングコールを安全に送信したい場合は、値を `True` に切り替えることができます。&lt;/li&gt;&lt;/ul&gt; |
|S-Object 名|  &lt;ul&gt;&lt;li&gt;(必須) 独自のカスタム s-object 変数名を構成してください。&lt;/li&gt;&lt;li&gt;わからない場合は、デフォルト値の `s` を使用してください。&lt;/li&gt;&lt;/ul&gt; |
|ビデオプラットフォーム名|  &lt;ul&gt;&lt;li&gt;(オプション) コンテンツが配信されるオンラインビデオプラットフォームの名前。&lt;/li&gt;&lt;/ul&gt; |
|ビデオプレーヤー SDK|  &lt;ul&gt;&lt;li&gt;(オプション) ビデオプレーヤーアプリ/SDKのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|タグバージョン|  &lt;ul&gt;&lt;li&gt;このドロップダウンリストを使用して、Nielsen 統合ありまたはなしの Adobe Heartbeat トラッキングを選択できます。&lt;/li&gt;&lt;li&gt;利用可能なオプションは次のとおりです：&lt;ul&gt;&lt;li&gt;Adobe Heartbeat 2.0.2 (デフォルト)&lt;/li&gt;&lt;li&gt;Adobe Heartbeat 1.6.7&lt;/li&gt;&lt;li&gt;Adobe Heartbeat 1.6.7 に Nielsen 5.0 を統合&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

次のフィールドは、タグバージョンを **Adobe Heartbeat 1.6.7 with Nielsen 5.0** に構成した場合のみ必要です。必要な Nielsen の値がない場合は、Nielsen または Adobe の担当者に連絡してください。

|フィールド名| フィールド値|
|---| ---|
|Adobe Nielsen SDK 構成キー|  &lt;ul&gt;(Nielsen 用に必須) Nielsen 構成キーを入力してください&lt;/li&gt;&lt;li&gt;Nielsen 統合用の構成 SDK キーです。&lt;/li&gt;&lt;/ul&gt; |
|Nielsen コレクション環境|  &lt;ul&gt;(Nielsen 用に必須) コレクション環境の場所。&lt;/li&gt;&lt;li&gt;Nielsen のコレクション環境の場所を入力してください&lt;/li&gt;&lt;li&gt;例：`eu-cert` または `eu`。&lt;/li&gt;&lt;/ul&gt; |
|Nielsen プレーヤー ID|  &lt;ul&gt;(Nielsen 用に必須) ビデオプレーヤーに割り当てられた一意の識別子を入力してください&lt;/li&gt;&lt;li&gt;Nielsen によって提供されるプレーヤー/サイトの一意の ID。&lt;/li&gt;&lt;/ul&gt; |
|Nielsen APN|  &lt;ul&gt;(Nielsen 用に必須) プレーヤー/サイトの説明を入力してください&lt;/li&gt;&lt;li&gt;プレーヤー/サイトを説明するためのユーザー定義の文字列値。&lt;/li&gt;&lt;/ul&gt; |
|Nielsen クライアント ID|  &lt;ul&gt;(Nielsen 用に必須) Nielsen クライアント識別子を入力してください&lt;/li&gt;&lt;li&gt;VA Beacon 測定用の一意の ID。&lt;/li&gt;&lt;/ul&gt; |
|Nielsen VCID|  &lt;ul&gt;(Nielsen 用に必須) ビデオチャンネル識別子を入力してください。&lt;/li&gt;&lt;li&gt;VA Beacon 測定用の一意の ID。&lt;/li&gt;&lt;/ul&gt; |

## 読み込みルールの適用

[読み込みルール]() は、サイト上のどのページにこのタグのインスタンスを読み込むかを決定します。すべてのページに読み込むルールがデフォルトの読み込みルールです。このタグを特定のページに読み込むためには、関連するルール条件を作成してタグに適用してください。

ベストプラクティス：ビデオが提供されるページにこのタグを読み込むためのカスタムルールを作成して適用してください。

## データマッピング

マッピングは、[データレイヤー変数]() からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/) を参照してください。

次のセクションでは、利用可能な各カテゴリについて詳細な表を提供します。
### 標準

標準カテゴリは[タグの構成フィールド](#tag_configs)に対応しています。これらの目的地に値をマッピングできます。空白のままのタグフィールドに動的に値を送信するか、現在の値を上書きします。

|目的地名| 説明|
|---| ---|
|`tracking_server`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat トラッキングサーバー。&lt;/li&gt;&lt;li&gt;すべてのハートビートトラッキングコールが送信されるサーバーのURL。&lt;/li&gt;&lt;/ul&gt; |
|`publisher`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat パブリッシャー。&lt;/li&gt;&lt;li&gt;Adobe担当者によって割り当てられたパブリッシャー名。&lt;/li&gt;&lt;/ul&gt; |
|`ssl`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat SSLフラグ。&lt;/li&gt;&lt;li&gt;ハートビートコールをHTTPSで送信するかどうかを決定するブール値フラグ。&lt;/li&gt;&lt;li&gt;マッピングする変数が `true` または `false` のブール値であることを確認してください。&lt;/li&gt;&lt;li&gt;マッピングは現在のドロップダウン選択を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`syndication_channel`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat チャンネル。&lt;/li&gt;&lt;li&gt;チャンネルのシンジケーション名。&lt;/li&gt;&lt;/ul&gt; |
|`online_video_platform_name`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat ビデオプラットフォーム名。&lt;/li&gt;&lt;li&gt;ビデオコンテンツをレンダリングするオンラインプラットフォームの名前。&lt;/li&gt;&lt;/ul&gt; |
|`player_sdk`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat プレイヤーSDK。&lt;/li&gt;&lt;li&gt;ビデオプレイヤーアプリ/SDKのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|`debug_logging`|  &lt;ul&gt;&lt;li&gt;Adobe Heartbeat デバッグログフラグ。&lt;/li&gt;&lt;li&gt;Heartbeatプラグイン内の各コンポーネントのログを有効/無効にするブール値フラグ。&lt;/li&gt;&lt;li&gt;Adobeは、アクティブなログがパフォーマンスに影響を与えるため、プレイヤーの製品版でこのフラグを無効にすることを推奨します。&lt;/li&gt;&lt;/ul&gt; |

次のフィールドは、タグのバージョンを **Adobe Heartbeat 1.6.7 with Nielsen 5.0** に構成した場合にのみ必要です。必要なNielsen値がない場合は、NielsenまたはAdobeの担当者に連絡してください。

|目的地名| 説明|
|---| ---|
|`nielsen_config_key`|  &lt;ul&gt;&lt;li&gt;Adobe Nielsen SDK構成キー。&lt;/li&gt;&lt;li&gt;Adobe Heartbeatと統合するためのNielsen構成キー。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_client_id`|  &lt;ul&gt;&lt;li&gt;NielsenクライアントID。&lt;/li&gt;&lt;li&gt;あなたのNielsenクライアント識別子。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_vcid`|  &lt;ul&gt;&lt;li&gt;Nielsen VCID。&lt;/li&gt;&lt;li&gt;ビデオチャンネル識別子。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_collection_environment`|  &lt;ul&gt;&lt;li&gt;Nielsen収集環境。&lt;/li&gt;&lt;li&gt;Nielsenの収集環境の場所。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_player_id`|  &lt;ul&gt;&lt;li&gt;NielsenプレイヤーID。&lt;/li&gt;&lt;li&gt;ビデオプレイヤーの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_apn`|  &lt;ul&gt;&lt;li&gt;Nielsen APN。&lt;/li&gt;&lt;li&gt;プレイヤー/サイトの説明で、文字列値として表現されます。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_device_id`|  &lt;ul&gt;&lt;li&gt;NielsenデバイスID。&lt;/li&gt;&lt;li&gt;ビデオを追跡したいモバイル/タブレットの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_sdk_debug`|  &lt;ul&gt;&lt;li&gt;Nielsen SDKデバッグフラグ。&lt;/li&gt;&lt;li&gt;Nielsen統合のログを有効/無効にするブール値フラグ。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_opt_out`|  &lt;ul&gt;&lt;li&gt;Nielsenオプトアウトフラグ。&lt;/li&gt;&lt;li&gt;現在の訪問に対してすべてのNielsenトラッキングを無効にします。&lt;/li&gt;&lt;li&gt;`opt-out` イベントのトリガーが必要です。&lt;/li&gt;&lt;/ul&gt; |

### ビデオイベント

ビデオイベントの目的地は、ビデオプレイヤーで特定のアクションまたは変更が発生したときにトリガーされるイベントリスナーです。イベントをトリガーするには、変数をツールボックスのイベントにマッピングし、変数の値をトリガーとして構成する必要があります。提供されたトリガー値がデータレイヤーで見つかると、マッピングされたイベントが発火します。

以下の表は利用可能なイベントの目的地をリストしています：

|目的地名| 説明|
|---| ---|
|`video_load`|  &lt;ul&gt;&lt;li&gt;ビデオロード。&lt;/li&gt;&lt;li&gt;ビデオが再生準備ができていることを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_start`|  &lt;ul&gt;&lt;li&gt;ビデオスタート。&lt;/li&gt;&lt;li&gt;ビデオが再生を開始したことを示します。次の3つのシナリオのいずれかの後に発生する可能性があります：&lt;ul&gt;&lt;li&gt;初期ローディング&lt;/li&gt;&lt;li&gt;バッファリング&lt;/li&gt;&lt;li&gt;広告表示&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`video_playing`|  &lt;ul&gt;&lt;li&gt;ビデオ再生中。&lt;/li&gt;&lt;li&gt;ビデオが現在再生中であることを示します。&lt;/li&gt;&lt;li&gt;QoSデータを更新するために使用します。&lt;/li&gt;&lt;li&gt;広告が再生されているときには呼び出さないでください。&lt;/li&gt;&lt;/ul&gt; |
|`video_pause`|  &lt;ul&gt;&lt;li&gt;ビデオ一時停止。&lt;/li&gt;&lt;li&gt;ビデオが一時停止されたことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_play`|  &lt;ul&gt;&lt;li&gt;ビデオ再生。&lt;/li&gt;&lt;li&gt;ビデオが再生中であることを示します。バッファリングまたはシークが完了した後に発生する可能性があります。&lt;/li&gt;&lt;/ul&gt; |
|`video_stop`|  &lt;ul&gt;&lt;li&gt;ビデオ停止。&lt;/li&gt;&lt;li&gt;ビデオが手動で停止されたことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_resume`|  &lt;ul&gt;&lt;li&gt;ビデオ再開。&lt;/li&gt;&lt;li&gt;視聴者がビデオの一時停止を解除して再生を再開したことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_complete`|  &lt;ul&gt;&lt;li&gt;ビデオ完了。&lt;/li&gt;&lt;li&gt;ビデオが終了したことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_seek`|  &lt;ul&gt;&lt;li&gt;ビデオシーク。&lt;/li&gt;&lt;li&gt;視聴者がビデオのシークを開始したことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_buffer`|  &lt;ul&gt;&lt;li&gt;ビデオバッファ。&lt;/li&gt;&lt;li&gt;ビデオがバッファリングを開始したことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_skip`|  &lt;ul&gt;&lt;li&gt;ビデオスキップ。&lt;/li&gt;&lt;li&gt;視聴者がビデオまたは広告をスキップしたことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`video_error`|  &lt;ul&gt;&lt;li&gt;ビデオエラー。&lt;/li&gt;&lt;li&gt;ビデオがエラーに遭遇したことを示します。&lt;/li&gt;&lt;/ul&gt; |
|`nielsen_opt_out_status_changed`|  &lt;ul&gt;&lt;li&gt;Nielsenオプトアウトステータス変更。&lt;/li&gt;&lt;li&gt;視聴者がオプトインからオプトアウト、またはその逆に切り替えたことを示します。&lt;/li&gt;&lt;/ul&gt; |

### ビデオ

これらの目的地は、[Adobeビデオ測定パラメータ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html)に対応しています。

|目的地名| 説明|
|---| ---|
|`video.id`|  &lt;ul&gt;&lt;li&gt;ビデオID。&lt;/li&gt;&lt;li&gt;ビデオの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|`video.title`|  &lt;ul&gt;&lt;li&gt;ビデオタイトル。&lt;/li&gt;&lt;li&gt;追跡されているビデオの名前。&lt;/li&gt;&lt;/ul&gt; |
|`video.length`|  &lt;ul&gt;&lt;li&gt;ビデオの長さ。&lt;/li&gt;&lt;li&gt;ビデオアセットの期間（秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|`video.current_playhead`|  &lt;ul&gt;&lt;li&gt;ビデオ現在の再生位置。&lt;/li&gt;&lt;li&gt;広告コンテンツを除く、ビデオのプレイヤーの現在の位置（秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|`video.stream_type`|  &lt;ul&gt;&lt;li&gt;ビデオストリームタイプ。&lt;/li&gt;&lt;li&gt;ビデオアセットのタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`video.is_full_episode`|  &lt;ul&gt;&lt;li&gt;ビデオはフルエピソードです。&lt;/li&gt;&lt;li&gt;ビデオコンテンツがフルエピソードであるかどうかを示すブール値フラグ。&lt;ul&gt;&lt;li&gt;`Y` はフルエピソード。&lt;/li&gt;&lt;li&gt;`N` は部分的なクリップ。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`video.original_air_date_nielsen`|  &lt;ul&gt;&lt;li&gt;ニールセン用ビデオのオリジナル放送日。&lt;/li&gt;&lt;li&gt;エピソードのオリジナル放送日、形式。&lt;/li&gt;&lt;li&gt;例：`YYYYMMDDHH24:MI:SS`&lt;/li&gt;&lt;/ul&gt; |
|`video.channel_name`|  &lt;ul&gt;&lt;li&gt;ビデオチャンネル名。&lt;/li&gt;&lt;li&gt;送信されるプログラムまたはフィードの名前。&lt;/li&gt;&lt;/ul&gt; |
|`video.series_name`|  &lt;ul&gt;&lt;li&gt;ビデオシリーズ名。&lt;/li&gt;&lt;li&gt;視聴されているプログラム（シリーズ名）の名前。&lt;/li&gt;&lt;/ul&gt; |
|`video.player_name`|  &lt;ul&gt;&lt;li&gt;ビデオプレイヤー名。&lt;/li&gt;&lt;li&gt;コンテンツを再生しているビデオプレイヤーの名前。&lt;/li&gt;&lt;/ul&gt; |
|`video.is_ad`|  &lt;ul&gt;&lt;li&gt;ビデオは広告です。&lt;/li&gt;&lt;li&gt;ビデオが広告であるかどうかを示すブール値。&lt;/li&gt;&lt;/ul&gt; |
|`video.fps`|  &lt;ul&gt;&lt;li&gt;ビデオFPS。&lt;/li&gt;&lt;li&gt;メディアのフレームレート、フレーム毎秒（FPS）。&lt;/li&gt;&lt;/ul&gt; |
|`video.bit_rate`|  &lt;ul&gt;&lt;li&gt;ビデオビットレート。&lt;/li&gt;&lt;li&gt;ビデオコンテンツのビット毎秒の属性。&lt;/li&gt;&lt;/ul&gt; |
|`video.startup.time`|  &lt;ul&gt;&lt;li&gt;ビデオ起動時間。&lt;/li&gt;&lt;li&gt;ビデオコンテンツの開始時間（秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|`video.dropped_frames`|  &lt;ul&gt;&lt;li&gt;ビデオドロップフレーム。&lt;/li&gt;&lt;li&gt;再生セッション中にドロップされたすべてのフレームの合計。&lt;/li&gt;&lt;/ul&gt; |
|`video.error_id`|  &lt;ul&gt;&lt;li&gt;ビデオエラーID。&lt;/li&gt;&lt;li&gt;再生中に発生したエラーのID。&lt;/li&gt;&lt;/ul&gt; |
|`video.error_is_fatal`|  &lt;ul&gt;&lt;li&gt;ビデオエラーは致命的です。&lt;/li&gt;&lt;li&gt;エラーが再生の続行を防ぐかどうかを示すブール値。&lt;/li&gt;&lt;/ul&gt; |
### チャプター

これらの目的地は [Adobe Video Chapter Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`chapter.name`|  &lt;ul&gt;&lt;li&gt;チャプター名。&lt;/li&gt;&lt;li&gt;個々のチャプターの名前。&lt;/li&gt;&lt;/ul&gt; |
|`chapter.length`|  &lt;ul&gt;&lt;li&gt;チャプターの長さ。&lt;/li&gt;&lt;li&gt;チャプターの総時間（秒）。&lt;/li&gt;&lt;/ul&gt; |
|`chapter.position`|  &lt;ul&gt;&lt;li&gt;チャプターの位置。&lt;/li&gt;&lt;li&gt;ビデオコンテンツ内のチャプターの位置。&lt;/li&gt;&lt;/ul&gt; |
|`chapter.start_time`|  &lt;ul&gt;&lt;li&gt;チャプター開始時間。&lt;/li&gt;&lt;li&gt;メインコンテンツ内でチャプターが始まるオフセット。&lt;/li&gt;&lt;/ul&gt; |
|`chapter_meta_data.custom`|  &lt;ul&gt;&lt;li&gt;チャプターカスタムメタデータ。&lt;/li&gt;&lt;li&gt;チャプターに関連する追加のカスタム値。&lt;/li&gt;&lt;/ul&gt; |

### 広告

これらの目的地は [Adobe Video Ad Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`adbreak.name`|  &lt;ul&gt;&lt;li&gt;広告ブレイク名。&lt;/li&gt;&lt;li&gt;個々の広告ブレイクの名前。&lt;/li&gt;&lt;/ul&gt; |
|`adbreak.position`|  &lt;ul&gt;&lt;li&gt;広告ブレイクの位置。&lt;/li&gt;&lt;li&gt;ビデオコンテンツ内の広告ブレイクの位置（インデックス）。&lt;/li&gt;&lt;li&gt;`video.is_ad` フラグが `True` に構成されている場合に必要です。&lt;/li&gt;&lt;/ul&gt; |
|`dbreak.start_time`|  &lt;ul&gt;&lt;li&gt;広告ブレイク開始時間。&lt;/li&gt;&lt;li&gt;メインコンテンツ内で広告ブレイクが始まるオフセット。&lt;/li&gt;&lt;/ul&gt; |
|`ad.id`|  &lt;ul&gt;&lt;li&gt;広告ID。&lt;/li&gt;&lt;li&gt;表示される広告のユニークな識別子。&lt;/li&gt;&lt;/ul&gt; |
|`ad.title`|  &lt;ul&gt;&lt;li&gt;広告タイトル。&lt;/li&gt;&lt;li&gt;広告の名前。&lt;/li&gt;&lt;/ul&gt; |
|`ad.type`|  &lt;ul&gt;&lt;li&gt;広告タイプ。&lt;/li&gt;&lt;li&gt;広告のタイプまたはカテゴリー。&lt;/li&gt;&lt;/ul&gt; |
|`ad.length`|  &lt;ul&gt;&lt;li&gt;広告の長さ。&lt;/li&gt;&lt;li&gt;広告の総時間（秒）。&lt;/li&gt;&lt;/ul&gt; |
|`ad.position`|  &lt;ul&gt;&lt;li&gt;広告の位置。&lt;/li&gt;&lt;li&gt;ビデオコンテンツ内の広告の位置（インデックス）。&lt;/li&gt;&lt;li&gt;`video.is_ad` フラグが `True` に構成されている場合に必要です。&lt;/li&gt;&lt;/ul&gt; |

### ビデオメタデータ

これらの目的地は [Adobe Standard Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`meta_data.custom`|  &lt;ul&gt;&lt;li&gt;ビデオカスタムメタデータ。&lt;/li&gt;&lt;li&gt;ビデオに関連する追加のカスタム値。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.show`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータショー。&lt;/li&gt;&lt;li&gt;ショーの名前。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.season`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータシーズン。&lt;/li&gt;&lt;li&gt;シーズン番号。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.episode`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータエピソード。&lt;/li&gt;&lt;li&gt;エピソード番号。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.asset`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータアセット。&lt;/li&gt;&lt;li&gt;ビデオアセット識別子、TMS ID（Tribune Media Service）としても知られています。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.genre`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータジャンル。&lt;/li&gt;&lt;li&gt;ビデオコンテンツのジャンル。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.airDate`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータ放送日。&lt;/li&gt;&lt;li&gt;アセットがテレビで初めて放送された日付。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.digitalDate`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータデジタル放送日。&lt;/li&gt;&lt;li&gt;アセットがデジタルで初めて利用可能になった日付。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.rating`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータ評価。&lt;/li&gt;&lt;li&gt;ビデオコンテンツの評価。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.originator`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータ発信者。&lt;/li&gt;&lt;li&gt;ビデオの発信者の名前。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.network`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータネットワーク。&lt;/li&gt;&lt;li&gt;ショーに関連するネットワークの名前。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.type`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータタイプ。&lt;/li&gt;&lt;li&gt;ショーのタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.adLoad`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータ広告ロード。&lt;/li&gt;&lt;li&gt;広告ロードのメタデータ。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.dayPart`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータデイパート。&lt;/li&gt;&lt;li&gt;広告表示が予定されている日の部分。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.feed`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータフィード。&lt;/li&gt;&lt;li&gt;プログラミングフィードのタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`meta_data.format`|  &lt;ul&gt;&lt;li&gt;ビデオメタデータフォーマット。&lt;/li&gt;&lt;li&gt;ビデオのストリームフォーマット。&lt;/li&gt;&lt;/ul&gt; |

### 広告メタデータ

これらの目的地は [Adobe Standard Ad Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/metadata_params.html) に対応しています。

|目的地名| 説明|
|---| ---|
|`ad_meta_data.custom`|  &lt;ul&gt;&lt;li&gt;広告カスタムメタデータ。&lt;/li&gt;&lt;li&gt;表示される広告に関連する追加のカスタム値。&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.advertiser`|  &lt;ul&gt;&lt;li&gt;広告メタデータ広告主。&lt;/li&gt;&lt;li&gt;広告を表示している会社/ブランドの名前。&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.campaign`|  &lt;ul&gt;&lt;li&gt;広告メタデータキャンペーン。&lt;/li&gt;&lt;li&gt;広告キャンペーン識別子。&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.creative`|  &lt;ul&gt;&lt;li&gt;広告メタデータクリエイティブ。&lt;/li&gt;&lt;li&gt;広告をレンダリングするためのクリエイティブアセット。&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.placement`|  &lt;ul&gt;&lt;li&gt;広告メタデータ配置。&lt;/li&gt;&lt;li&gt;ビデオ内の広告の位置に関連するメタデータ。&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.site`|  &lt;ul&gt;&lt;li&gt;広告メタデータサイト。&lt;/li&gt;&lt;li&gt;広告に関連するサイト。&lt;/li&gt;&lt;/ul&gt; |
|`ad_meta_data.creativeURL`|  &lt;ul&gt;&lt;li&gt;広告メタデータクリエイティブURL。&lt;/li&gt;&lt;li&gt;表示される広告のURL。&lt;/li&gt;&lt;/ul&gt; |
## ビルトイン動画データレイヤー変数

データレイヤーがすでにこれらの値を使用している場合、マッピングは必要ありません。Tealiumは通常、データを対応するタグの宛先に送信します。データレイヤーがこの表に記載されている変数名と異なる変数名を使用している場合は、手動でマップする必要があります。

|ビルトイン変数| ツールボックス宛先変数| 説明|
|---| ---| ---|
|`event_name`| [動画イベント宛先](#video_events_mapping)|  `event_name`変数で以下の値を使用している場合、ツールボックスで再度マップする必要はありません。&lt;ul&gt;&lt;li&gt;`load` は `video_load` にマップされます&lt;/il&gt;&lt;li&gt;`start` は `video_start` にマップされます&lt;/il&gt;&lt;li&gt;`playing` は `video_playing` にマップされます&lt;/il&gt;&lt;li&gt;`pause` は `video_pause` にマップされます&lt;/il&gt;&lt;li&gt;`play` は `video_play` にマップされます&lt;/il&gt;&lt;li&gt;`stop` は `video_stop` にマップされます&lt;/il&gt;&lt;li&gt;`resume` は `video_resume` にマップされます&lt;/il&gt;&lt;li&gt;`complete` は `video_complete` にマップされます&lt;/il&gt;&lt;li&gt;`seek` は `video_seek` にマップされます&lt;/il&gt;&lt;li&gt;`buffer` は `video_buffer` にマップされます&lt;/il&gt;&lt;li&gt;`optstatus` は `Nielsen_opt_out_status_changed` にマップされます&lt;/li&gt;&lt;/ul&gt; |
|`video_id`| --|  &lt;ul&gt;&lt;li&gt;動画の一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|`video_name`| `video.title`|  &lt;ul&gt;&lt;li&gt;動画タイトル。&lt;/li&gt;&lt;li&gt;追跡されている動画の名前。&lt;/li&gt;&lt;/ul&gt; |
|`video_length`| `video.length`|  &lt;ul&gt;&lt;li&gt;動画の長さ。&lt;/li&gt;&lt;li&gt;動画アセットの期間（秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|`video_player_name`| `video.player_name`|  &lt;ul&gt;&lt;li&gt;動画プレーヤー名。&lt;/li&gt;&lt;li&gt;コンテンツを再生している動画プレーヤーの名前。&lt;/li&gt;&lt;/ul&gt; |
|`video_current_playhead`| `video.current_playhead`|  &lt;ul&gt;&lt;li&gt;動画の現在の再生位置。&lt;/li&gt;&lt;li&gt;広告コンテンツを除く、動画内のプレーヤーの現在位置（秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|`video_stream_type`| `video.stream_type`|  &lt;ul&gt;&lt;li&gt;動画ストリームタイプ。&lt;/li&gt;&lt;li&gt;動画アセットのタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`video_fps`| `video.fps`|  &lt;ul&gt;&lt;li&gt;動画FPS。&lt;/li&gt;&lt;li&gt;メディアのフレームレート、フレーム毎秒（FPS）。&lt;/li&gt;&lt;/ul&gt; |
|`video_bitrate`| `video.bit_rate`|  &lt;ul&gt;&lt;li&gt;動画ビットレート。&lt;/li&gt;&lt;li&gt;動画コンテンツのビット毎秒の属性。&lt;/li&gt;&lt;/ul&gt; |
|`video_dropped_frames`| `video.dropped_frames`|  &lt;ul&gt;&lt;li&gt;動画ドロップフレーム。&lt;/li&gt;&lt;li&gt;再生セッション中にドロップされたすべてのフレームの合計。&lt;/li&gt;&lt;/ul&gt; |
|`video_is_ad`| `video.is_ad`|  &lt;ul&gt;&lt;li&gt;動画が広告かどうか。&lt;/li&gt;&lt;li&gt;動画が広告であるかどうかを示すブール値。&lt;/li&gt;&lt;/ul&gt; |
|`video_ad_position` - OR - `video_ad_pod_position`| `ad.position`|  &lt;ul&gt;&lt;li&gt;広告の位置。&lt;/li&gt;&lt;li&gt;動画コンテンツ内の広告の位置（インデックス）。&lt;/li&gt;&lt;li&gt;`video.is_ad`フラグが`true`に構成されている場合に必要です。&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_name`| `chapter.name`|  &lt;ul&gt;&lt;li&gt;チャプター名。&lt;/li&gt;&lt;li&gt;個々のチャプターの名前。&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_length`| `chapter.length`|  &lt;ul&gt;&lt;li&gt;チャプターの長さ。&lt;/li&gt;&lt;li&gt;チャプターの総期間（秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_position`| `chapter.position`|  &lt;ul&gt;&lt;li&gt;チャプターの位置。&lt;/li&gt;&lt;li&gt;動画コンテンツ内のチャプターの位置。&lt;/li&gt;&lt;/ul&gt; |
|`video_chapter_start_time`| `chapter.start_time`|  &lt;ul&gt;&lt;li&gt;チャプター開始時間。&lt;/li&gt;&lt;li&gt;チャプターが開始するメインコンテンツ内のオフセット。&lt;/li&gt;&lt;/ul&gt; |
|`video_ad_pod_name`| `ad.id`|  &lt;ul&gt;&lt;li&gt;広告ID。&lt;/li&gt;&lt;li&gt;表示されている広告の一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|`program`| `video.series_name`|  &lt;ul&gt;&lt;li&gt;動画シリーズ名。&lt;/li&gt;&lt;li&gt;視聴されているプログラム（シリーズ名）の名前。&lt;/li&gt;&lt;/ul&gt; |
|`is_full_episode`| `video.is_full_episode`|  &lt;ul&gt;&lt;li&gt;動画がフルエピソードかどうか。&lt;/li&gt;&lt;li&gt;動画コンテンツがフルエピソードであるかどうかを示すブールフラグ。&lt;ul&gt;&lt;li&gt;`Y` はフルエピソード&lt;/li&gt;&lt;li&gt;`N` は部分的なクリップ&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`original_air_date`| `video.original_air_date_nielsen`|  &lt;ul&gt;&lt;li&gt;ニールセン用の動画のオリジナル放送日。&lt;/li&gt;&lt;li&gt;エピソードのオリジナル放送日、次の形式で: `YYYYMMDDHH24:MI:SS`&lt;/li&gt;&lt;/ul&gt; |

## 検証

Heartbeatタグはイベントベースであり、他のutagコールと区別するために`utag.track(&#34;video&#34;, data)`コールを利用します。このため、[データマッピングツールボックスの動画イベントトリガーを適切に構成することが重要です](#video_events_mapping)。

構成後、タグは毎秒連続して発火し、動画データを最新の状態に保ちます。これは、動画プレーヤーの「playing」イベントハンドラ内で「playing」イベントを発火することによって達成されます。他の動画イベントもそれに対応するAdobe heartbeatイベントを通じて発火するべきです。ネットワークコールは集約され、イベントの変更を含む10秒ごとにAdobeに報告されます。

HeartbeatとNielsenのデバッグフラグを構成する簡単な方法は、動画ページのURLにクエリ文字列パラメータを追加することです。例えば、`adobe_debug=1&amp;Nielsen=1` &lt;br&gt;その後、クエリパラメータ変数をTealium iQのデータレイヤーに追加し、それに応じてマップします。&lt;br&gt;HeartbeatとNielsenのデバッグフラグのマッピング先はStandardカテゴリの下にあります。&#34;Adobe Heartbeat Debug Logging Flag&#34;と&#34;Nielsen SDK Debug Flag&#34;を参照してください。&lt;br&gt;完了したら、ブラウザコンソールで次のTealiumデバッグコマンドを実行できます。&lt;br&gt;
`document.cookie = &#34;utagdb=true&#34;;`

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
