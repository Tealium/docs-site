---
title: スクロールイベント
description: スクロールイベントは、訪問者が画面をスクロールするときにトラッキングデータを送信します。スクロール量をピクセルまたは画面のパーセンテージで測定するかどうかを指定できます。また、垂直スクロール、水平スクロール、または両方を追跡するかどうかを指定することもできます。
url: https://docs.tealium.com/ja/iq-tag-management/events/event-types/scroll-event/
---
## 必要条件

* utag v4.38以降。`utag.js`テンプレートの更新についての詳細は、ナレッジベースの記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。

## 動作方法

スクロールイベントは、訪問者が画面をスクロールするときに追跡します。訪問者がアクションを実行すると、トラッキングコールがトリガーされます。

イベントリスナーの追加方法についての詳細は、[イベントの管理](https://docs.tealium.com/manage-events/)を参照してください。

## イベントトリガー

イベントトリガーは、イベントリスナーが追跡する特定のアクションです。

このイベントは以下のトリガーを追跡することができます：

* **垂直スクロール深度** – ユーザーが画面を下にスクロールすると発火します。
* **水平スクロール深度** – ユーザーが画面を横にスクロールすると発火します。

以下の閾値を設定して、各イベントをトリガーするタイミングを制御します：

* **パーセント** - スクロール距離を画面のパーセンテージで測定します。
* **ピクセル** - スクロール距離をピクセル数で測定します。


<blockquote>
複数の値をコンマで区切ったリストとして入力して、異なる画面位置でトリガーします。例えば、パーセンテージを測定するには `25, 50, 75, 100`、ピクセルを測定するには `2000, 5000` を入力します。
</blockquote>


### 要素セレクタ

要素セレクタは、イベントリスナーをトリガーするページ上のどの要素を指定するかを指定します。詳細については、[イベント要素セレクタ](https://docs.tealium.com/event-element-selector/)を参照してください。

## イベントトリガー変数

イベントトリガー変数は、イベントリスナーがトラッキングコールと共に送信する値です。スクロールイベントには、以下のデフォルトのイベントトリガー変数があります：

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`tealium_event`| Tealiumのイベント名。| `scroll`| 文字列|
|`scroll_depth`| スクロールの量。| `50`| 数値|
|`scroll_depth_type`| スクロールの測定方法、`percent`または`pixels`。| `percent`| 文字列|
|`scroll_direction`| スクロールの方向、`vertical`または`horizontal`。| `vertical`| 文字列|
|`iq_event_id` | イベントを送信したイベントリスナーのUID。|

### イベントトラッキング

#### 水平スクロール

|識別子| 説明|
|---| ---|
|`tealium_event="scroll"`| 訪問者が指定した方向と量で画面をスクロールしました。|

**例**

```json
{
   "tealium_event"  : "scroll",
   "scroll_depth" : "500",
   "scroll_depth_type" : "pixels",
   "scroll_direction" : "horizontal",
   "iq_event_id:" : "scroll_depth_events_1"
}
```

#### 垂直スクロール

|識別子| 説明|
|---| ---|
|`tealium_event="scroll"`| 訪問者が指定した方向と量で画面をスクロールしました。|

**例**

```json
{
   "tealium_event"  : "scroll",
   "scroll_depth" : "50",
   "scroll_depth_type" : "percent",
   "scroll_direction" : "vertical",
   "iq_event_id:" : "scroll_depth_events_2"
}
```