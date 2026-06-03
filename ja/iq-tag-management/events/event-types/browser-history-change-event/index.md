---
title: ブラウザ履歴変更イベント
description: ブラウザ履歴変更イベントは、シングルページアプリケーション（SPA）のナビゲーションの変更を監視するためのブラウザ履歴APIを監視します。
url: https://docs.tealium.com/ja/iq-tag-management/events/event-types/browser-history-change-event/
---
## 必要条件

* utag v4.38以降。`utag.js`テンプレートの更新についての詳細は、当社のナレッジベースの記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)をご覧ください。
* ページまたはアプリがナビゲーションのためにブラウザの履歴APIの`history.pushState()`および`history.replaceState()`関数を使用しています。

## 仕組み

ブラウザ履歴変更イベントリスナーは、ブラウザの履歴APIの`history.pushState()`および`history.replaceState()`関数を監視します。これらの2つの関数は、SPAでフルページのリロードなしにナビゲーションを管理するために使用されます。訪問がアプリ内の新しいページに移動したり、戻ったりすると、トラッキングコールがトリガーされます。

イベントリスナーを追加する方法についての詳細は、[イベントの管理]()をご覧ください。

## イベントトリガー

イベントトリガーは、イベントリスナーが追跡するアクションです。

トリガーの閾値を以下のように構成できます：

* **遅延** - トラッキングコールを遅延させる時間（ミリ秒）。

### 履歴の変更

このイベントは、ブラウザの履歴変更によってトリガーされます。

|識別子| 説明|
|---| ---|
|`tealium_event=&#34;history_change&#34;`| 訪問がアプリ内の新しいページに移動したか、ページを戻しました。|

## イベントトリガー変数

イベントトリガー変数は、イベントがトラッキングコールと共に送信する値です。このイベントには以下のデフォルト変数があります：

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`tealium_event`| Tealiumのイベント名。| `history_change`| 文字列|
|`iq_event_id` | イベントを送信したイベントリスナーのUID。| `history_change_events_1` | 文字列 |

**例**

```json
{
   &#34;tealium_event&#34;  : &#34;history_change&#34;,
   &#34;iq_event_id:&#34; : &#34;history_change_events_1&#34;
}
```