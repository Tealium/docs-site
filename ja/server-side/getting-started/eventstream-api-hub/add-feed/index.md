---
title: イベントフィードを追加する
description: このステップでは、ゼロの結果を含む検索イベントをキャプチャするためのイベントフィードを作成する方法を示します。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/add-feed/
---
## フィードを作成する

イベントフィードを作成するには：

1. **Validate &gt; Live Events**に移動し、**&#43; Add Event Feed**をクリックします。  
1. **Title**、**Notes**、および**Labels**を構成します。  
今のところ**Event Data Storage**は無視してください。この構成は、あなたのアカウントが[DataAccess]()で有効になっていることが必要です。
1. フィードの条件を構成します：
    * ドロップダウンメニューからイベント属性を選択します。
    * 演算子を選択します。
    * 別の属性を選択するか、カスタム値を選択して値を入力します。  
    ![](/images/server-side/getting-started-eventstream-event-feed-condition.png)
    * 追加のAND/OR条件ロジックについては、これを繰り返します。
1. **Save**をクリックします。
1. アカウントを保存して公開します。

## Live Eventsを再訪する

イベント仕様とフィードが構成されたので、より多くのイベントを送信して、それらが**Live Events**でどのように表示されるかを確認するために、インストールを再訪するのが良い時期です。

**Live Events**とフィードに慣れるために試してみること：

* 他の属性なしで`search`イベントを送信します。それらは**Live Events**で赤、緑、または青に表示されますか？
* 必要なすべての属性を持つ`search`イベントを送信します。それらは**Live Events**で有効ですか？
* **Live Events**の**Event Feeds**ドロップダウンで、新しいフィードを選択します。このビューに表示させるために、より多くのイベントをトリガーします。

イベントフィードに慣れたら、次のチュートリアルに進んでコネクタとその動作について学びましょう。
