---
title: データコネクトレシピのベストプラクティス
description: この記事では、Data Connectのベストプラクティスについて説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/best-practices/
---
以下のベストプラクティスは、Tealium Eventsアプリを活用してWorkatoレシピを作成し、データをTealiumに送信する際の参考になります。


* **データの清潔さ**   
Tealiumにデータをインポートする前に、送信されるデータの品質と清潔さを確認してください。
* **地域のTealium APIドメイン**   
Tealium Eventsアプリを構成する際は、地域のTealium APIドメインを使用してください。地域のTealium APIドメインは、[Tealium Connectデータソース]()で見つけることができます。
* **アプリごとの接続**  
Workatoアカウント内のアプリごとに1つの接続を使用してください。例えば、Salesforceアプリを使用する必要がある2つのレシピがある場合、最初のレシピでSalesforce接続を作成し、2つ目のレシピでアクティブな接続のリストから既存の接続を選択します。
* **タスクの削減**  
タスクコストを削減し、処理効率を向上させるために、ファイルバッチを最大化し、ビジネス目標を達成するために必要なWorkatoタスクの数を最小限に抑えてください。
  * レシピで使用されるタスクの数を確認するには、**Integrations &gt; Jobs**に移動し、ジョブを選択します。**Job Details**セクションの**Tasks Used**には、その特定のジョブで使用されたタスクの数が表示されます。
  * バッチトリガーを使用する場合、**Batch size**を最大サイズに構成します。
  * Workatoのデフォルト構成では、ソースデータからすべてのフィールドを取得しますが、Tealiumに送信されるフィールドのみを取得するようにします。
    Tealiumに送信する特定のフィールドを選択するには：
    * アプリ構成の**Setup**ステップで、**Show optional fields**をクリックし、**Fields to retrieve**が選択されていることを確認します。
    * **Fields to retrieve**の下で、Tealiumに送信する特定のフィールドを選択します。
* **トリガーのポーリング間隔をカスタマイズする**   
デフォルト値は5分です。このデフォルト間隔は、特に低ボリュームのデータインポートケースには短すぎます。短すぎるポーリング間隔を使用すると、必要以上のタスクを使用することになります。使用ケースが許容できる最長の値にポーリング間隔を構成することを推奨します。  
トリガーのポーリング間隔をカスタマイズするには、以下の手順を完了します：  
  * アプリ構成の**Setup**ステップで、**Show optional fields**をクリックし、**Trigger poll interval**が選択されていることを確認します。
  * **Trigger poll interval**の下で、使用ケースに合わせたカスタムポーリング間隔を選択します。
* **Tealium Visitor ID**  
Data Connectの各レコードについて、`tealium_visitor_id`に使用される値は必ず構成されている必要があります。この値が構成されていない場合、Data ConnectのTealium EventsアプリはIDが欠落しているレコードのインポートに失敗します。同じTealium Connect API呼び出しの他のデータも影響を受けます。  
`tealium_visitor_id`が正しく構成されていることを確認するために、以下の解決策のいずれかを選択します：
  * **WHERE句** - 多くのWorkatoアプリには、ポーリングトリガーに**WHERE句**があり、これによりソースで`tealium_visitor_id`の値がないレコードをフィルタリングすることができます。
  * **カスタムステップ** - WHERE句を使用することができない場合は、WorkatoレシピのJavaScriptまたはRubyステップを使用して、識別子が欠落しているレコードをフィルタリングします。詳細については、Workatoドキュメンテーションの[JavaScriptの記事](https://docs.workato.com/connectors/javascript.html)を参照してください。
