---
title: ライブイベント
description: ライブイベントチャートはリアルタイムでのデータ受信を検査するために使用されます。この記事では、データ品質を検査し評価する方法を示します。
url: https://docs.tealium.com/ja/server-side/event-health/live-events/
---
## 動作原理

ライブイベントチャートは、すべてのデータソースおよびイベントフィードからリアルタイムで発生するイベントを表示します。チャートの各バーは、検出されたイベントの量を示す高さを持っています。アクティブな[イベント仕様]()がある場合、チャートは色分けされたセグメントで受信データの品質を反映します：緑は有効なイベント、黄色は警告イベント、赤は無効なイベント、青は仕様のないイベントです。

## ライブイベントの使用

**Validate > Live Events**にアクセスしてライブイベントを使用します。

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventfeed.png)
<!-- GAP: replace whiteui-eventstream-liveeventfeed.png with a screenshot of the live events chart showing all four status segments including Warn (yellow) in the Event Specification Filters legend -->

チャートに表示されるイベントを制御するには、**Data Sources** および **Event Feeds** リストを使用します。デフォルトの選択は **All Data Sources** と **All Events** です。これらのメニューを調整すると、チャートが更新され、選択した組み合わせのイベント活動が表示されます。

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveevents-filter-drop-down-lists.png)

特定のイベントフィードのイベントを選択すると、チャートはそのイベントのデータのみを表示します。すべてのイベントデータとイベントフィードを比較するには、**Compare against All Events**をクリックします。たとえば、特定の国や地域のイベントフィードを作成し、その国や地域のイベントフィードをすべてのイベントと比較することができます。

## トレースIDの使用

トレースIDを使用して、トリガーしたイベント以外のすべての受信イベントをフィルタリングします。トレースIDは一時的な一意の識別子であり、特定のイベントのみがライブイベントチャートに表示されるようにイベント追跡コードに挿入されます。詳細については、[トレースについて](https://docs.tealium.com/about-trace/)を参照してください。

トレースを構成するには：

1. **Trace ID** をクリックします。  
トレースオプションのモーダルが表示されます。
1. **Start Trace** をクリックし、指示に従います。
1. 生成されたトレースIDをコピーし、**Continue** をクリックします。
1. テストするページを開いた新しいChromeブラウザウィンドウを開きます。
1. **Tealium Tools > Trace** を開き、トレースIDを入力します。  

ライブイベントチャートは、トレースされたセッション中にトリガーされたイベントのみを表示するようになります。同じ手順に従って新しいトレースを開始するか、既存のトレースに再参加することができます。

## 仕様ステータスによるフィルター

[イベント仕様]()が定義されている場合、ライブイベントは受信データの品質を表示します。チャートの各バーは適用されたイベント仕様のステータスに応じてセグメント化されます。次のフィルターはオンまたはオフに切り替えてチャートの表示を調整することができます：

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventsandfeeds-event-specification-filters.png)
<!-- GAP: replace whiteui-eventstream-liveeventsandfeeds-event-specification-filters.png with a screenshot showing the filter legend with all four statuses: Valid (green), Warn (yellow), Invalid (red), and No Spec (blue) -->

* **Valid Events**  
これらのイベントはアクティブなイベント仕様の要件を満たしています。有効なイベントは、`tealium_event` 属性の既知の値と仕様からのすべての必要な属性を持っています。有効なイベントが多いほど良いです。なぜなら、より多くの有効なイベントが表示されることは、インストールが仕様で期待されるデータを送信していることを示しているからです。
* **Warn Events**  
これらのイベントはイベント仕様に一致し、すべての必要な属性が検証を通過しますが、1つ以上のオプショナル属性が欠けているか、データタイプが間違っているか、構成されたデータ値ルールに一致しません。
* **Invalid Events**  
これらのイベントはイベント仕様に一致しますが、少なくとも1つの必要な属性が欠けているか、データタイプが間違っているか、構成されたデータ値ルールに一致しません。これらの問題は、イベントを送信しているインストールコードを修正することや、場合によってはイベント仕様を調整することで解決できます。
* **No Spec**  
これらのイベントには一致するイベント仕様がありません。No Specイベントは、`tealium_event` 属性がないか、対応するイベント仕様がありません。


<blockquote>
イベント仕様はデータをフィルタリングしません。イベントが無効であっても、システムはイベントを処理します。
</blockquote>


## イベントの詳細を表示

チャートのバーをクリックして、受信データサンプルからのイベントの詳細を表示します。データサンプルはチャートのバーごとに10イベントに制限されています。イベントは主に`tealium_event`属性によって識別されます。この属性の検出された値はイベント詳細の見出しに表示されます。`tealium_event`に対応するイベント仕様がある場合、イベントは仕様の要件に従って有効、警告、または無効として表示されます。見出しにはまた、イベントが発生したデータソースも表示されます。

たとえば、有効な`cart_empty`イベントは次のようになります：

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-live-events-and-feeds-valid-events-details.png)
<!-- GAP: replace whiteui-eventstream-live-events-and-feeds-valid-events-details.png with a screenshot of a valid event's detail view showing the green header and per-attribute spec validation results -->

イベント属性の詳細は、次の属性タイプに整理されています：Universal Variable, JavaScript Page Variable, HTML Metadata, First-party Cookie, Query String Parameter, および Tealium提供。

無効な`cart_empty`イベントは次のようになります：

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-eventspecifications-invalid-event.png)
<!-- GAP: replace whiteui-eventstream-eventspecifications-invalid-event.png with a screenshot of an invalid cart_empty event detail view showing the red header with per-attribute validation results and failure reasons (missing required attribute or wrong data type) highlighted inline -->

詳細ビューは各属性の検証ステータスをインラインで強調表示し、必要な属性が欠けているか、データタイプが間違っているなどの失敗の理由を示します。

## 未知の属性を定義する

未知の属性は、受信イベントで検出されたが、まだアカウントでイベント属性としてデータタイプ（例：文字列、数値、ブール値など）で作成されていない属性です。アカウントで属性を使用する前に、イベント属性として作成する必要があります。

イベント詳細ビューでは、未知の属性は**Data Type**列で`Unknown`と表示されます。

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventsandfeeds-add-unknown-attribute.png)

未知の属性は、次のようにしてこの画面から直接定義することができます：

1. 未知の属性の隣にあるその他のオプションアイコンをクリックし、**Quick Add**をクリックします。
1. データタイプを選択します。
1. **Define**をクリックします。

属性は新しいデータタイプで表示されるようになります。
## イベント仕様の作成

`tealium_event` にカスタム値を持つイベントは、関連するイベント仕様がない場合、イベント詳細ビューで `Unknown` と表示されます。このような場合、イベント詳細ビューから `tealium_event` の検出された値とイベントの属性に基づいてカスタムイベント仕様を直接作成します。


<blockquote>
ライブイベントからイベント仕様を作成する前に、未知の属性を定義することをお勧めします。詳細は[未知の属性を定義する](#define-unknown-attributes)を参照してください。
</blockquote>


詳細については、[イベント仕様の管理](https://docs.tealium.com/manage-event-specifications/#create-an event-specification)を参照してください。