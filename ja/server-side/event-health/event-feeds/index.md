---
title: イベントフィード
description: イベントフィードは、受信データの管理と検査に使用されます。この記事では、イベントフィードの管理方法について説明します。
url: https://docs.tealium.com/ja/server-side/event-health/event-feeds/
---
## 動作原理

イベントフィードは、属性に基づいて特定の条件に一致するイベントのグループです。フィードはコネクターやEventDBやEventStoreなどのデータ保存ソリューションに送信されることがあります。デフォルトのイベントフィードは**すべてのイベント**と名付けられ、すべての受信イベントが含まれ、編集や削除はできません。しかし、属性に基づいてイベントのサブセットを特定するための追加のフィードを作成することができます。

## イベントフィードの作成

イベントフィードを作成するには：

1. **Validate &gt; Live Events**に移動します。
1. **&#43; Add Event Feed**をクリックします。  
**Create Event Feed** ダイアログが表示されます。
1. **Title** と **Notes** を構成します。
1. （オプション）**Labels**を追加します。
1. EventStoreまたはEventDBでフィードを有効にします。  
この構成は、アカウントが[DataAccess]()で有効になっている必要があります。
1. フィードの条件を構成します。  
    ![](/images/server-side/whiteui-eventstream-live-events-and-feeds-enable-eventstore-slider.png)
1. フィードに制限データを含めたい場合は、**Send Restricted Data to DataAccess**を選択します。詳細については、[About Restricted Data]()を参照してください。制限データの構成はコネクターには適用されません。制限データとしてマークされた属性は、マッピングを通じて送信される場合でも、訪問プロファイルの一部として送信される場合でも常に含まれます。
1. **Save**をクリックします。
1. アカウントを保存して公開します。

## イベントフィードの詳細を表示

デフォルトでは、イベントフィードはアルファベット順にリストされ、**すべてのイベント**が最上部に表示されます。リストには以下の情報が表示されます：

![](/images/server-side/whiteui-eventstream-liveeventsandfeeds-eventfeeddetails-alpha.png)

* **Total Volume**: 過去30日間にすべてのデータソースから検出されたイベントの総数。
* **Assigned Actions**: フィードにリンクされたコネクターアクションの数。
* **EventStore**: フィードがEventStoreで有効かどうかを示します。
* **EventDB**: フィードがEventDBで有効かどうかを示します。

イベントフィードのリストからフィードをクリックして詳細を表示します：

![](/images/server-side/whiteui-eventstream-liveeventsandfeeds-viewspecdetails.png)

詳細には以下が表示されます：

* **Feed Activity Chart**: 選択した時間範囲におけるすべてのデータソースから検出されたイベントの数。
* **Conditions**: フィード内のイベントを特定するために使用されるロジック。
* **Assigned Actions**: フィードにリンクされたコネクターアクション。

イベント仕様にリンクされたフィードは削除できず、その名前も変更できません。