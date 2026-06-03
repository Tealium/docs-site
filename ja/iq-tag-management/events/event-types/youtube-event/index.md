---
title: YouTubeイベント
description: YouTubeイベントは、訪問者がページ上の埋め込みYouTubeビデオと対話するときにトラッキングデータを送信します。訪問者が再生、一時停止、特定の再生マイルストーンに到達する、またはビデオがバッファリングしているときにイベントトリガーを指定できます。
url: https://docs.tealium.com/ja/iq-tag-management/events/event-types/youtube-event/
---
## 必要条件

* YouTube IFrame Player APIスクリプト。
* YouTubeイベントリスナーがビデオのイベントをトラッキングできるようにするには、埋め込みビデオの`enablejsapi`パラメータを`1`に設定する必要があります。また、**iFrame APIを有効にする**チェックボックスを選択すると、**エレメントセレクタ**の基準に一致する埋め込みビデオのパラメータが自動的に設定されます。
* ビデオを個別にトラッキングしたい場合、埋め込みビデオは一意の`id`パラメータを使用する必要があります。

YouTubeイベントリスナーが含まれるページにYouTube iFrame Player APIスクリプトがすでに含まれていない場合、スクリプトはページ上で自動的に読み込まれます。

### 埋め込みパラメータ

ビデオID `xWlEk2i9r5Q`のURLは次のURLを使用します：

`https://www.youtube.com/embed/xWlEk2i9r5Q`

このビデオの基本的なiframe埋め込みコードは、`enablejsapi`パラメータを`1`に設定し、一意の`id`パラメータを`video1`に設定し、ビデオIDを使用すると次の形式になります：

```html
&lt;iframe id=&#34;video1&#34; type=&#34;text/html&#34; width=&#34;640&#34; height=&#34;360&#34;
 src=&#34;https://www.youtube.com/embed/xWlEk2i9r5Q?enablejsapi=1&#34;&gt;&lt;/iframe&gt;
```

埋め込みYouTubeビデオのパラメータを設定する方法の詳細については、[YouTube Embedded Players and Player Parameters documentation](https://developers.google.com/youtube/player_parameters)を参照してください。

## 動作方法

YouTubeイベントは、訪問者がYouTubeビデオと対話するときにトラッキングします。訪問者がアクションを実行すると、トラッキングコールがトリガーされます。

イベントリスナーを追加する方法の詳細については、[Manage events]()を参照してください。

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

エレメントセレクタは、イベントリスナーをトリガーするページ上のどの要素を指定するかを指定します。詳細については、[Event element selector]()を参照してください。

### トリガー頻度

トリガー頻度は、イベントトリガーがトラッキングコールを結果として何回発生させるかを決定します。詳細については、[Event triggers]()を参照してください。

## イベントトリガー変数

イベントトリガー変数は、イベントリスナーがトラッキングコールと共に送信する値です。**新規イベント &gt; イベント設定**画面で、**イベントトリガー変数**テーブルに移動し、イベントのトリガー変数を表示または編集するためにトリガータイプをクリックします。

例えば、一時停止トリガーの変数を表示するには、**一時停止**タブをクリックします：

![](/images/guides/iq/event_trigger_variables.png)

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
|`tealium_event=&#34;video_play&#34;`| 訪問者がビデオを再生しました。|

**例**

```json
{
   &#34;tealium_event&#34;  : &#34;video_play&#34;,
   &#34;video_id&#34; : &#34;xWlEk2i9r5Q&#34;,
   &#34;video_name&#34; : &#34;Tealiumでのビデオトラッキング方法&#34;,
   &#34;video_length&#34; : &#34;300&#34;,
   &#34;video_platform&#34; : &#34;youtube&#34;,
   &#34;video_playhead&#34; : &#34;1&#34;,
   &#34;iq_event_id:&#34; : &#34;youtube_video_events_1&#34;
}
```

### 一時停止

|識別子| 説明|
|---| ---|
|`tealium_event=&#34;video_pause&#34;`| 訪問者が再生中のビデオを一時停止しました。|

**例**

```json
{
   &#34;tealium_event&#34;  : &#34;video_pause&#34;,
   &#34;video_id&#34; : &#34;xWlEk2i9r5Q&#34;,
   &#34;video_name&#34; : &#34;Tealiumでのビデオトラッキング方法&#34;,
   &#34;video_length&#34; : &#34;300&#34;,
   &#34;video_platform&#34; : &#34;youtube&#34;,
   &#34;video_playhead&#34; : &#34;30&#34;,
   &#34;iq_event_id:&#34; : &#34;youtube_video_events_2&#34;
}

```

### バッファリング

|識別子| 説明|
|---| ---|
|`tealium_event=&#34;video_buffer&#34;`| 訪問者がビデオのバッファリングを経験しました。|

**例**

```json
{
   &#34;tealium_event&#34;  : &#34;video_buffer&#34;,
   &#34;video_id&#34; : &#34;xWlEk2i9r5Q&#34;,
   &#34;video_name&#34; : &#34;Tealiumでのビデオトラッキング方法&#34;,
   &#34;video_length&#34; : &#34;300&#34;,
   &#34;video_platform&#34; : &#34;youtube&#34;,
   &#34;video_playhead&#34; : &#34;50&#34;,
   &#34;iq_event_id:&#34; : &#34;youtube_video_events_3&#34;
}
```

### マイルストーン

|識別子| 説明|
|---| ---|
|`tealium_event=&#34;video_milestone&#34;`| 訪問者がビデオをパーセンテージまたは期間のマイルストーンまで再生しました。|

**例**

```json
{
   &#34;tealium_event&#34;  : &#34;video_milestone&#34;,
   &#34;video_milestone&#34; : &#34;50&#34;,
   &#34;milestone_type&#34; : &#34;percent&#34;,
   &#34;video_id&#34; : &#34;xWlEk2i9r5Q&#34;,
   &#34;video_name&#34; : &#34;Tealiumでのビデオトラッキング方法&#34;,
   &#34;video_length&#34; : &#34;300&#34;,
   &#34;video_platform&#34; : &#34;youtube&#34;,
   &#34;video_playhead&#34; : &#34;151&#34;,
   &#34;iq_event_id:&#34; : &#34;youtube_video_events_4&#34;
}
```

