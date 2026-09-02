---
title: イベントヘルスについて
description: この記事では、イベントヘルスとその構成要素について説明し、データ品質の監視と改善に役立つ方法を解説します。
url: https://docs.tealium.com/ja/server-side/event-health/about/
---
## 動作原理

イベントヘルスは、リアルタイムで受信イベントの品質を監視する機能群です。イベントが以下の条件を満たしているかをチェックします：

* 一貫した構造（定義されたスキーマなど）に従っている。
* 必須とマークされた属性を含んでいる。
* ウェブサイト、アプリ、その他のデータソース全体で同じ実装を使用している。

イベントヘルスには以下のコンポーネントが含まれます：

* **[イベント仕様]()**：イベント仕様は、イベントタイプに必要な属性を定義し、インストールのためのコード例を提供します。イベント仕様を作成すると、リアルタイムでイベントのデータ品質を検証し、ライブイベントチャートを使用して検証します。
* **[イベントフィード]()**：イベントフィードは、属性に基づいて特定の条件に一致するイベントをグループ化します。イベント仕様が自動的に生成するものに加えて、カスタムイベントフィードを作成します。フィードをコネクターやデータ保存ソリューション（EventDBやEventStoreなど）に送信します。
* **[ライブイベント]()**：ライブイベントチャートは、リアルタイムですべてのデータソースとすべてのイベントフィードからのデータを表示します。**データソース**と**イベントフィード**のフィルターを使用して、トラフィックのサブセットに表示を絞り込みます。イベント仕様がアクティブな場合、チャートは属性検証に基づいて受信イベントの品質を表示します。

これらのコンポーネントは連携して、データレイヤーの健全性を示します。

### 利点

健全でよく構造化されたデータレイヤーは、正確でリアルタイムのデータ収集と品質に不可欠です。データを最も価値のある資産として扱うことで、ビジネスの意思決定が信頼できる、実行可能な洞察に基づくようになります。イベントヘルスは、以下を提供することでこれを実現します：

* **データの信頼性**：検証されたイベントは、分析と顧客データが信頼できることを保証します。
* **迅速なトラブルシューティング**：明確なエラーシグナルが問題の特定と修正にかかる時間を短縮します。
* **一貫したデータ品質**：下流システム（コネクターやデータストアなど）は、均一で高品質のデータを受け取ります。
* **自信を持った意思決定**：信頼できるデータはビジネスの決定と顧客体験の改善をサポートします。
* **継続的な改善**：検証結果を使用してトラッキングコードとイベント仕様を洗練させ、有効なイベントの割合を増やし、実際のイベントトラッキングに仕様を合わせます。

### イベントの例

以下の例は、各検証ステータスを説明しています。これらは、`video_complete`イベントの以下のイベント仕様に基づいています：

<!-- GAP: replace whiteui-eventspecifications-videocomplete.png with a screenshot of the video_complete spec showing defined types (String, Number) for each attribute, required toggles enabled for the four required attributes, and video_quality as an optional String attribute -->

仕様はその`tealium_event`値（`video_complete`）をリストし、四つの必須属性：`video_id`, `video_length`, `video_name`, `video_platform`を定義します。また、任意の文字列属性として`video_quality`も定義します。各属性には、受信イベントが有効または警告ステータスを受けるために一致しなければならない定義されたデータタイプがあります。

#### 有効なイベントの例

有効なステータスのイベントは、以下の条件を満たしています：

* `tealium_event`値がイベント仕様のいずれかと一致している。
* 正しいデータタイプで必須属性をすべて含んでいる。
* すべてのプラットフォーム（ウェブやモバイルなど）で同じ構造に従っている。

例えば、次のイベントを考えてみましょう：

```json
{
    "tealium_event": "video_complete",
    "video_id": "xWlEk2i9r5Q",
    "video_length": 300,
    "video_name": "How to track videos in Tealium",
    "video_platform": "YouTube",
    "video_quality": "1080p"
}
```

`tealium_event`値は`video_complete`なので、このイベントは`video_complete`仕様に対してチェックされます。このイベントは、必要な属性と任意の属性を正しいデータタイプで含んでいるため、有効とマークされます。

![](https://docs.tealium.com/images/server-side/valid-video-complete-event.png)
<!-- GAP: replace valid-video-complete-event.png with a screenshot of the valid video_complete event details showing the green header and per-attribute spec validation results, with all attributes listed and their validation status visible -->

#### 無効なイベントの例

次のイベントは、先に述べた`video_complete`仕様に対してチェックされますが、一つ以上の必須属性が欠けているか、予期しない値を含んでいます。

```json
{
    "tealium_event": "video_complete",
    "video_id": "xWlEk2i9r5Q",
    "video_length": "300 seconds",
    "video_platform": "YouTube"
}
```

このイベントは無効です。なぜなら、`video_length`属性が仕様が期待する数値ではなく文字列であり、必須の`video_name`属性が欠けているからです。

![](https://docs.tealium.com/images/server-side/invalid-video-complete-event.png)
<!-- GAP: replace invalid-video-complete-event.png with a screenshot of the invalid video_complete event details showing the red header and per-attribute validation results, with failing attributes highlighted and the failure reason (missing or wrong data type) visible -->

属性、データタイプ、および要件のエラーを特定して、問題をトラブルシューティングし、解決します。

#### 警告イベントの例

警告ステータスのイベントは、以下の条件を満たしています：

* `tealium_event`値がイベント仕様のいずれかと一致している。
* 必須属性がすべて正しいデータタイプで存在している。
* 一つ以上の任意属性が欠けているか、間違ったデータタイプを持っている。

例えば、次のイベントを考えてみましょう。ここで`video_quality`は仕様で任意の文字列属性です：

```json
{
    "tealium_event": "video_complete",
    "video_id": "xWlEk2i9r5Q",
    "video_length": 300,
    "video_name": "How to track videos in Tealium",
    "video_platform": "YouTube",
    "video_quality": 1080
}
```

必須属性はすべて存在し、正しいデータタイプを持っているため、このイベントは必須属性の検証を通過します。しかし、`video_quality`は仕様で文字列であり、イベントが数値を送信したため、このイベントは警告とマークされます。

<!-- GAP: add a screenshot of the warn video_complete event details showing the amber/yellow header and the optional attribute that triggered the warn status -->

#### 未知のイベントの例

未知のイベントは、`tealium_event`値がどのイベント仕様とも一致しないか、`tealium_event`属性が欠けている場合です。

次のイベントは`tealium_event`値が欠けています：

```json
{
    "video_id": "xWlEk2i9r5Q",
    "video_length": 300,
    "video_name": "How to track videos in Tealium",
    "video_platform": "YouTube"
}
```

イベントが`tealium_event`属性を欠いているため、どの仕様にも分類できず、未知（`No Spec`）とマークされます。

同様に、次のイベントも`video_search`のイベント仕様がないため、未知のイベントとマークされます：

```json
{
    "tealium_event": "video_search",
    "video_name": "How to track videos in Tealium",
    "video_platform": "YouTube"
}
```

## ワークフロー

生のイベントデータから監視され、検証されたイベントへと進むためのワークフローを使用します。目標は、明確なイベント仕様を確立し、それらの仕様に対してライブトラフィックを検証し、データ品質の問題を迅速に対処することです。
### ステップ1 - イベントと未知の属性を発見する

**すべてのイベント**フィードでライブイベントチャートを見て、流入するトラフィックを調査します：

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventfeed.png)

このビューは、本番環境での現在の実装の動作を示し、まだ特定していない可能性のある属性も含まれています：

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventsandfeeds-add-unknown-attribute.png)

この情報から、イベント仕様を作成するための主要なイベントとその属性のリストを作成します。

詳細については、[ライブイベント]()を参照してください。

### ステップ2 - リアルタイムイベントからイベント仕様を作成する

**ライブイベント**または**イベント仕様**ページから、発見した属性を使用して主要なイベントのイベント仕様を作成します。顧客ジャーニーで最も重要なイベント（`sign_up`、`login`、`add_to_cart`、`purchase`など）から始めます。各属性について、データ型と属性が必須かどうかを構成します。

![](https://docs.tealium.com/images/server-side/whiteui-eventspecifications-videocomplete.png)
<!-- GAP: replace whiteui-eventspecifications-videocomplete.png with a screenshot of the video_complete spec showing defined types (String, Number) for each attribute, required toggles enabled for the four required attributes, and video_quality as an optional String attribute -->

イベント仕様を作成した後、`tealium_event`値が一致するイベントはその仕様に対して検証され、**Valid**、**Warn**、**Invalid**、または**No Spec**としてマークされます。各イベント仕様は、コネクタ、EventDB、またはEventStore用に有効にできる対応するイベントフィードを作成します。

![](https://docs.tealium.com/images/server-side/video-complete-event-feed.png)

重要なイベントは、Tealiumがリアルタイムで検証する文書化された契約を持っています。一致するイベントは、リンクされたフィードを通じてダウンストリームのワークフローで利用可能です。

詳細については、[イベント仕様の管理]()を参照してください。

### ステップ3 - イベントの健康状態を監視し、問題をトリアージする

ライブイベントチャートとイベント仕様の詳細ページを使用して、時間の経過とともにイベントの健康状態を監視します。**Valid**、**Warn**、**Invalid**、および**No Spec**フィルターを使用して特定の健康状態に焦点を当てます。**Data Sources**および**Event Feeds**を使用して、トラフィックのサブセットにチャートを絞り込みます。

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveevents-filter-drop-down-lists.png)
<!-- GAP: replace whiteui-eventstream-liveevents-filter-drop-down-lists.png with a screenshot showing the filter dropdown with the Warn (yellow) segment visible alongside Valid, Invalid, and No Spec -->

継続的な監視により、必要な属性の送信が停止したり、新しい未定義のイベント名が導入されたりする新しいリリースなど、回帰を迅速にキャッチできます。

このビューから、各仕様と全トラフィックにわたってどのイベントが健康で、どのイベントが注意を必要としているかがわかります。

詳細については、[ライブイベント]()および[イベント仕様について]()を参照してください。

トレースIDを使用して、トリガーしたイベント以外のすべての流入イベントをフィルタリングします。トレースIDは、手動でイベントをテストするためにイベントトラッキングコードに挿入する一時的な一意の識別子です。新しいまたは更新されたイベント仕様を検証する際に、テスト中にトリガーしたイベントのみを表示する場合に便利です。

詳細については、[トレースIDの使用](https://docs.tealium.com/about-live-events/#use-a-trace-id)を参照してください。

### ステップ4 - 修正、反復、および回復の確認

監視から得られた洞察を使用して、データ品質の問題を修正します：

* 無効なイベントの場合、イベントサンプルを調査して、どの必須属性が欠落しているか、または不正な形式であるかを確認します。実装を更新するか、必要に応じて仕様を調整します。
* 警告イベントの場合、イベントサンプルを調査して、どのオプション属性が欠落しているか、またはデータ型が間違っているかを確認します。オプション属性が正しいタイプで送信されるように実装を更新します。
* 仕様のないイベントの場合、仕様を作成するか、範囲外のノイズとして扱うかを決定します。ライブイベントチャートの任意のイベントをクリックし、新しいイベント仕様の基礎として使用します。

イベント仕様を作成または更新した後、データを再度テストします。

イベントの健康状態は、検証結果を使用してトラッキングコードと仕様を洗練することで改善されます。時間の経過とともに、有効なイベントの割合が増加し、仕様はビジネスがイベントを追跡する方法に合わせて調整されます。

詳細については、[ライブイベント]()および[イベント仕様の管理]()を参照してください。

### ステップ5 - 成功シグナルとカバレッジを追跡する

イベントの健康状態は、検出から解決への移行を助けます。

ライブイベントチャートで、緑のバー（有効なイベント）と、黄色（警告）、赤（無効）、青（仕様なし）のセグメントの数が減少しているかを確認します。

**イベント仕様**の概要および詳細ページで、選択した期間にわたるイベントごとの**総ボリューム**、**有効なイベント**、**警告イベント**、**無効なイベント**、および**仕様なし**の数を監視します。

![](https://docs.tealium.com/images/server-side/event-health-table.png)
<!-- GAP: replace event-health-table.png with a screenshot of the Event Specifications overview showing the Warn Events metric tile and the Warn Events column in the Defined Events table -->

これらの指標は、データ品質が改善しているかどうか、次に焦点を当てるべき場所を示します：

* 無効なイベントの急増は、実装の変更や新しい属性値を示していることがあります。
* 警告イベントの急増は、オプションの属性が欠落しているか、間違ったデータ型で送信されていることを示しています。
* 仕様のないイベントの増加は、新しいイベントタイプまたは欠落している仕様を示唆しています。
* 未知の属性は、未知のデータ型としてフラグが立てられます。イベントの詳細ビューから直接定義して、イベント仕様やその他の機能で使用できるようにします。
* イベントが欠落している属性や誤った属性のために無効である場合、新しいイベントが仕様に準拠するようにトラッキングコードまたはタグ管理構成を更新します。

## 次のステップ

この記事では、イベントの健康状態とその機能について説明しました。データ品質の監視と改善を開始するには、次のトピックを参照してください：

* [イベント仕様の管理]()：リアルタイムでイベントを検証するためのイベント仕様を作成および管理します。
* [イベントフィード]()：イベント仕様から自動的に作成され、コネクタやデータ保存ソリューションに送信できるイベントフィードについて学びます。
* [ライブイベント]()：リアルタイムで受信するイベントを表示し、イベント仕様に基づいてその健康状態を反映するライブイベントチャートについて学びます。