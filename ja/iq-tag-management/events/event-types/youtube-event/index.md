---
title: YouTubeイベント
description: YouTubeイベントは、訪問者がページ上の埋め込みYouTubeビデオと対話するときにトラッキングデータを送信します。訪問者が再生、一時停止、特定の再生マイルストーンに到達する、またはビデオがバッファリングしているときにイベントトリガーを指定できます。
url: https://docs.tealium.com/ja/iq-tag-management/events/event-types/youtube-event/
---
## 必要条件

* YouTube IFrame Player APIスクリプト。
* YouTubeイベントリスナーがビデオのイベントをトラッキングできるようにするには、埋め込みビデオの`enablejsapi`パラメータを`1`に設定する必要があります。また、**iFrame APIを有効にする**チェックボックスを選択すると、**エレメントセレクタ**の基準に一致する埋め込みビデオのパラメータが自動的に設定されます。
* ビデオを個別にトラッキングしたい場合、埋め込みビデオは一意の`id`パラメータを使用する必要があります。


<blockquote>
YouTubeイベントリスナーが含まれるページにYouTube iFrame Player APIスクリプトがすでに含まれていない場合、スクリプトはページ上で自動的に読み込まれます。
</blockquote>


### 埋め込みパラメータ

ビデオID `xWlEk2i9r5Q`のURLは次のURLを使用します：

`https://www.youtube.com/embed/xWlEk2i9r5Q`

このビデオの基本的なiframe埋め込みコードは、`enablejsapi`パラメータを`1`に設定し、一意の`id`パラメータを`video1`に設定し、ビデオIDを使用すると次の形式になります：

```html
<iframe id="video1" type="text/html" width="640" height="360"
 src="https://www.youtube.com/embed/xWlEk2i9r5Q?enablejsapi=1"></iframe>
```

埋め込みYouTubeビデオのパラメータを設定する方法の詳細については、[YouTube Embedded Players and Player Parameters documentation](https://developers.google.com/youtube/player_parameters)を参照してください。

## 動作方法

YouTubeイベントは、訪問者がYouTubeビデオと対話するときにトラッキングします。訪問者がアクションを実行すると、トラッキングコールがトリガーされます。

イベントリスナーを追加する方法の詳細については、[Manage events](https://docs.tealium.com/manage-events/)を参照してください。

## イベントトリガー

イベントトリガーは、イベントリスナーがトラッキングする特定のアクションです。

YouTubeイベントは、次のイベントトリガーをトラッキングできます：

* **再生** – ビデオが再生されたときにイベントリスナーをトリガーします。
* **一時停止** – ビデオが一時停止されたときにイベントリスナーをトリガーします。
* **バッファリング** – ビデオがバッファリングしているときにイベントリスナーをトリガーします。
* **マイルストーン** – ビデオの一部または特定の時間が再生されたときにイベントリスナーをトリガーします。

マイルストーンイベントトリガーでは、次の閾値のいずれかを設定できます：

* **完了のパーセンテージ** – イベントリスナーがトリガーする前に視聴者が視聴する必要があるビデオのパーセンテージ。カンマで区切られたリスト（例：`25, 50, 75`）で複数の値を入力します。
* **視聴時間** – イベントリスナーをトリガーするために必要なビデオの合計視聴時間。

### エレメントセレクタ

エレメントセレクタは、イベントリスナーをトリガーするページ上のどの要素を指定するかを指定します。詳細については、[Event element selector](https://docs.tealium.com/event-element-selector/)を参照してください。

### トリガー頻度

トリガー頻度は、イベントトリガーがトラッキングコールを結果として何回発生させるかを決定します。詳細については、[Event triggers](https://docs.tealium.com/event-triggers/)を参照してください。

## イベントトリガー変数

イベントトリガー変数は、イベントリスナーがトラッキングコールと共に送信する値です。**新規イベント > イベント設定**画面で、**イベントトリガー変数**テーブルに移動し、イベントのトリガー変数を表示または編集するためにトリガータイプをクリックします。

例えば、一時停止トリガーの変数を表示するには、**一時停止**タブをクリックします：

![](https://docs.tealium.com/images/guides/iq/event_trigger_variables.png)

YouTubeイベントには、次のデフォルトのイベントトリガー変数があります：

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`tealium_event`| Tealiumイベント名。| `video_play`| 文字列|
|`video_id`| YouTubeでのビデオID。| `xWlEk2i9r5Q`| 文字列|
|`video_name`| ビデオの名前。| `Tealiumでのビデオトラッキング方法`| 文字列|
|`video_length`| ビデオの合計長さ（秒）。| `300`| 数値|
|`video_platform`| ビデオを提供するプラットフォームの名前。| `youtube`| 文字列|
|`video_playhead`| イベント時のビデオの再生位置（秒）。| `151`| 数値|
|`video_milestone`|  ビデオの再生されたパーセンテージまたは時間。この変数はマイルストーントリガーと共に表示されます。 | `50`| 数値|
|`milestone_type`|  マイルストーンのタイプ、`percent`または`time`。この変数はマイルストーントリガーと共に表示されます。 | `percent`| 数値|
|`iq_event_id` | イベントを送信したイベントリスナーのUID。| `youtube_video_events_1` | 文字列 |

### 再生

|識別子| 説明|
|---| ---|
|`tealium_event="video_play"`| 訪問者がビデオを再生しました。|

**例**

```json
{
   "tealium_event"  : "video_play",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "Tealiumでのビデオトラッキング方法",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "1",
   "iq_event_id:" : "youtube_video_events_1"
}
```

### 一時停止

|識別子| 説明|
|---| ---|
|`tealium_event="video_pause"`| 訪問者が再生中のビデオを一時停止しました。|

**例**

```json
{
   "tealium_event"  : "video_pause",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "Tealiumでのビデオトラッキング方法",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "30",
   "iq_event_id:" : "youtube_video_events_2"
}

```

### バッファリング

|識別子| 説明|
|---| ---|
|`tealium_event="video_buffer"`| 訪問者がビデオのバッファリングを経験しました。|

**例**

```json
{
   "tealium_event"  : "video_buffer",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "Tealiumでのビデオトラッキング方法",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "50",
   "iq_event_id:" : "youtube_video_events_3"
}
```

### マイルストーン

|識別子| 説明|
|---| ---|
|`tealium_event="video_milestone"`| 訪問者がビデオをパーセンテージまたは期間のマイルストーンまで再生しました。|

**例**

```json
{
   "tealium_event"  : "video_milestone",
   "video_milestone" : "50",
   "milestone_type" : "percent",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "Tealiumでのビデオトラッキング方法",
   "video_length" : "300",
   "video_platform" : "youtube",
   "video_playhead" : "151",
   "iq_event_id:" : "youtube_video_events_4"
}
```

