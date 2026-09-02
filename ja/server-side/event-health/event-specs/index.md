---
title: イベント仕様
description: イベント仕様は、受信データの品質を検証する方法です。
url: https://docs.tealium.com/ja/server-side/event-health/event-specs/
---
## 仕組み

イベント仕様（「イベントスペック」とも呼ばれます）は、イベントのための[データレイヤー](https://docs.tealium.com/an-introduction-to-the-data-layer/)を表します。イベント仕様を使用すると、[ライブイベントチャート](https://docs.tealium.com/about-live-events/)またはイベント仕様の詳細ビューを使用して、リアルタイムでイベントのデータ品質を検証できます。

イベント仕様には、以下の定義セットが含まれています：

* `tealium_event` 属性は、イベントの名前とそれに関連する仕様を表します。例えば、`tealium_event` 属性の値が `video_complete` の場合、システムは `video_complete` という名前のイベント仕様を探して、受信イベントをそれに対して検証します。イベント仕様を使用して、目的と予想されるデータ構造に基づいてイベントを分類および管理します。
* そのイベントに期待されるデータを説明する属性のリスト。属性は `video_id`、`video_length`、`video_platform` などの個々の情報です。これらの属性を定義することで、システムが受け取るべきデータの明確な期待を作り出します。定義された属性は、チームが一貫したデータ構造を維持し、エラーを減らし、トラブルシューティングを簡素化するのに役立ちます。
* 期待されるデータ型、例えば文字列、数値、またはブール値です。データ型を定義することで、各属性が正しい種類の情報を含むことを保証します。定義されたデータ型はエラーを減らし、データの一貫性を向上させ、異なるシステム間でのイベントの検証と処理を容易にします。
* 有効なイベントに必要な属性かどうか。必須属性は、イベントが有効と見なされるためにはイベントに存在しなければなりません。必須属性は、常に重要な情報が含まれることを保証し、正確な分析と意思決定に不可欠です。

検証中、各属性は存在、データ型、および構成されたデータ値ルールについて評価されます。必須属性の失敗は無効なイベントを生成します。オプションの属性の失敗は警告イベントを生成します。データ値ルールの構成については、[属性に検証ルールを追加する](https://docs.tealium.com/manage-event-specifications/#add-a-validation-rule-to-an-attribute)を参照してください。


<blockquote>
検証はイベントごとに100属性に限定されます。必須属性はアルファベット順に最初に評価され、次にオプションの属性がアルファベット順に評価されます。制限を超える属性は検証されず、**Spec limit reached** の理由で警告とマークされます。
</blockquote>


イベント仕様はデータをフィルタリングしません。イベントが無効であっても、システムは引き続きイベントを処理します。

### イベント仕様の例

例えば、`video_complete` イベントは以下の属性とデータを含んでいます：

```json
{
    "tealium_event"  : "video_complete", // イベントと仕様の名前
    "video_id"       : "xWlEk2i9r5Q",
    "video_length"   : 300,
    "video_name"     : "How to track videos in Tealium",
    "video_platform" : "YouTube",
}
```

この `video_complete` イベントのイベント仕様には、以下が含まれます：

![](https://docs.tealium.com/images/server-side/whiteui-eventspecifications-videocomplete.png)
<!-- GAP: replace whiteui-eventspecifications-videocomplete.png with a screenshot of the video_complete spec showing defined types (String, Number) for each attribute, required toggles enabled for the four required attributes, and video_quality as an optional String attribute -->

* `tealium_event` 属性は、イベントを `video_complete` として識別します。
* **定義** テーブルは、イベントに関する文脈情報を提供し、必要な属性、それらの期待されるデータ型、および有効なイベントに必要かどうかを定義します。

### 利点

イベント仕様は、データ管理において二つの主要な利点を提供します：

* すべてのプラットフォームにわたってイベントの実装を標準化するため。
* 受信イベントのデータ品質を評価するため。

## イベント仕様の統計を表示する

![](https://docs.tealium.com/images/server-side/event-health-table.png)
<!-- GAP: replace event-health-table.png with a screenshot of the Event Specifications overview showing the Warn Events metric tile and the Warn Events column in the Defined Events table -->

**イベントヘルス** ウィンドウは、すべてのイベント仕様の総統計を表示します。テーブルは、個々のイベント仕様の統計を示しています。その期間の統計を表示するために、時間枠を選択できます。

表示される統計は次のとおりです：

* **総ボリューム**  
選択した時間枠で受信したイベントの総数です。
* **有効なイベント**  
アクティブなイベント仕様の要件を満たすイベントの数です。有効なイベントは、`tealium_event` 属性と仕様のすべての必須属性に既知の値があります。有効なイベントが多いほど、データ品質が良いことを示します。高いカウントは、インストールが仕様で期待されるデータを送信していることを示します。
* **警告イベント**  
仕様に一致し、すべての必須属性チェックに合格したイベントの数ですが、1つ以上のオプションの属性が欠落している、間違ったデータ型を持っている、または構成されたデータ値ルールに一致していない場合です。警告イベントを修正すると、オプションの属性データの完全性が向上します。
* **無効なイベント**  
イベント仕様に一致するが、少なくとも1つの必須属性が欠落している、間違ったデータ型を持っている、または構成されたデータ値ルールに一致していないイベントの数です。これらの問題は、イベントを送信しているインストールコードを修正するか、イベント仕様を調整することで解決できます。
* **No Spec**  
一致するイベント仕様がないイベントの数です。No Spec イベントは、`tealium_event` 属性がないか、対応するイベント仕様がない場合です。

**定義されたイベント** テーブルは、すべての既存のイベント仕様と、各イベント仕様の **総ボリューム**、**有効なイベント**、**警告イベント**、**無効なイベント**、および **No Spec** の統計をリストします。

## イベント仕様の詳細を表示する

**定義されたイベント** テーブルの任意のイベント仕様をクリックして、その詳細を表示します。

イベント仕様に関する統計がページの上部に表示され、仕様に一致するイベントの総ボリュームと、有効、警告、無効イベントの割合が表示されます。

**定義** テーブルは、イベントに関する文脈情報を提供し、必要な属性、それらの期待されるデータ型、および有効なイベントに必要かどうかを定義します。

### コードサンプル

イベント仕様の詳細ウィンドウから、**コード** をクリックし、このイベント仕様に使用するデータソースを選択して、基本コードと例を表示します。

次のコードサンプルは、データソース `My iOS App` 用の `video_complete` イベントのトラッキングコードを示しています：

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-eventspecifications-viewcode.png)

## ライブイベントでのイベント仕様

イベント仕様が作成され、トラッキングコードが実装されると、ライブイベントチャートを使用してリアルタイムで受信イベントを表示し、そのデータ品質を評価します。

詳細については、[ライブイベント](https://docs.tealium.com/about-live-events/#event-specification-display-filters)を参照してください。