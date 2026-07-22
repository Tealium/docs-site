---
title: Vimeo イベント
description: Vimeo イベントは、訪問者がページ上の埋め込まれた Vimeo ビデオと対話するときにトラッキングデータを送信します。訪問者が再生、一時停止、特定の再生マイルストーンに到達する、またはビデオがバッファリングしているときにイベントトリガーを指定できます。
url: https://docs.tealium.com/ja/iq-tag-management/events/event-types/vimeo-event/
---
## 要件

* utag v4.38 またはそれ以降。`utag.js` テンプレートの更新についての詳細は、ナレッジベースの記事 [utag.js の最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470) を参照してください。
* Vimeo トラッキング API スクリプト。


<blockquote>
Vimeo イベントリスナーが含まれているページに Vimeo トラッキング API スクリプトがすでに含まれていない場合、スクリプトはページ上で自動的に読み込まれます。
</blockquote>


## 動作方法

Vimeo イベントは、訪問者が Vimeo ビデオと対話するときにトラッキングします。訪問者がアクションを実行すると、トラッキングコールがトリガーされます。

イベントリスナーを追加する方法についての詳細は、[イベントの管理](https://docs.tealium.com/manage-events/)を参照してください。

## イベントトリガー

イベントトリガーは、イベントリスナーがトラッキングする特定のアクションです。

Vimeo イベントは、以下のイベントトリガーをトラッキングできます：

* **再生** – ビデオが再生されたときにイベントリスナーをトリガーします。
* **一時停止** – ビデオが一時停止されたときにイベントリスナーをトリガーします。
* **バッファリング** – ビデオがバッファリングしているときにイベントリスナーをトリガーします。
* **マイルストーン** – ビデオの一部または特定の時間が再生されたときにイベントリスナーをトリガーします。

マイルストーンイベントトリガーでは、以下の閾値のいずれかを設定できます：

* **完了のパーセンテージ** – イベントリスナーがトリガーする前に視聴者が視聴する必要があるビデオのパーセンテージ。カンマで区切られたリストに複数の値を入力します（例：`25, 50, 75`）。
* **視聴時間** – イベントリスナーをトリガーするために必要なビデオの合計視聴時間。

### 要素セレクター

要素セレクターは、イベントリスナーをトリガーするページ上のどの要素を指定するかを指定します。詳細については、[イベント要素セレクター](https://docs.tealium.com/event-element-selector/)を参照してください。

### トリガー頻度

トリガー頻度は、イベントトリガーがトラッキングコールを結果とする回数を決定します。詳細については、[イベントトリガー](https://docs.tealium.com/event-triggers/)を参照してください。

## イベントトリガー変数

イベントトリガー変数は、イベントリスナーがトラッキングコールと共に送信する値です。**新しいイベント > イベント設定**画面で、**イベントトリガー変数**テーブルに移動し、イベントのトリガー変数を表示または編集するためのトリガータイプをクリックします。

例えば、一時停止トリガーの変数を表示するには、**一時停止**タブをクリックします：

![](https://docs.tealium.com/images/guides/iq/event_trigger_variables.png)

Vimeo イベントには、以下のデフォルトのイベントトリガー変数があります：

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`tealium_event`| Tealium イベント名。| `video_play`| 文字列|
|`video_id`| Vimeo でのビデオID。| `xWlEk2i9r5Q`| 文字列|
|`video_name`| ビデオの名前。| `Tealiumでビデオをトラッキングする方法`| 文字列|
|`video_length`| ビデオの合計長さ（秒）。| `300`| 数値|
|`video_platform`| ビデオを提供するプラットフォームの名前。| `vimeo`| 文字列|
|`video_playhead`| イベント時のビデオの再生位置（秒）。| `151`| 数値|
|`video_milestone`|  ビデオの再生されたパーセンテージまたは時間。この変数はマイルストーントリガーと共に表示されます。 | `50`| 数値|
|`milestone_type`|  マイルストーンのタイプ、`percent` または `time`。この変数はマイルストーントリガーと共に表示されます。 | `percent`| 数値|
|`iq_event_id` | イベントを送信したイベントリスナーのUID。|  `vimeo_video_events_1` | 文字列 |

### 再生

|識別子| 説明|
|---| ---|
|`tealium_event="video_play"`| 訪問者がビデオを再生しました。|

**例**

```json
{
   "tealium_event"  : "video_play",
   "video_id" : "xWlEk2i9r5Q",
   "video_name" : "Tealiumでビデオをトラッキングする方法",
   "video_length" : "300",
   "video_platform" : "vimeo",
   "video_playhead" : "1",
   "iq_event_id:" : "vimeo_video_events_1"
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
   "video_name" : "Tealiumでビデオをトラッキングする方法",
   "video_length" : "300",
   "video_platform" : "vimeo",
   "video_playhead" : "30",
   "iq_event_id:" : "vimeo_video_events_2"
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
   "video_name" : "Tealiumでビデオをトラッキングする方法",
   "video_length" : "300",
   "video_platform" : "vimeo",
   "video_playhead" : "50",
   "iq_event_id:" : "vimeo_video_events_3"
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
   "video_name" : "Tealiumでビデオをトラッキングする方法",
   "video_length" : "300",
   "video_platform" : "vimeo",
   "video_playhead" : "151",
   "iq_event_id:" : "vimeo_video_events_4"
}
```

