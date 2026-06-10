---
title: AudienceDBとEventDBの構成
description: この記事では、EventDBとAudienceDBに保存する属性を構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/configure/
---
## 要件

* EventDBにデータを送信するには、イベントフィードを構成し、EventStoreを有効にする必要があります。
* AudienceDBにデータを送信するには、AudienceStoreを有効にする必要があります。

EventDBとAudienceDBをアカウントとプロファイルで有効にするには、アカウントマネージャーに連絡してください。

## 動作方法
 
データストレージは属性レベルで制御されます。イベント属性、訪問属性、訪問属性を作成するときに、属性をEventDBまたはAudienceDBに送信するオプションを選択できます。
![](/images/server-side/data-access/eventdb-attribute-checkbox.png)

### 訪問と訪問の属性

アカウント内のすべてのオーディエンスはデフォルトでAudienceDBに送信されます。**AudienceDB**画面でAudienceDBに送信するオーディエンスと属性を選択できます。詳細については、[AudienceDB属性の構成](#configure-audiencedb-attributes)を参照してください。

### イベント属性

すべてのプリロードされた属性（Tealiumによって定義され、すべてのアカウントで利用可能な属性）はデフォルトでEventDBに送信されます。**EventDB属性**画面でカスタム属性を選択してEventDBに送信できます。

プリロードされた属性は**EventDB属性**画面で変更できません。**DataAccessコンソール**を使用して、EventDBに保存されるプリロードされた属性を調整します。詳細については、[EventDB属性の構成](#configure-eventdb-attributes)を参照してください。

DOM属性（例えば、URL、ドメイン、リファラ、ユーザーエージェント）は常に送信され、EventDBから除外することはできません。また、Tealiumのイベント属性、例えば`tealium_account`、`tealium_profile`、`tealium_event`も常に送信され、除外することはできません。

データ量が非常に大きくなる可能性があるため、必要な特定のイベントフィードのみにEventDBを有効にすることをお勧めします。詳細については、[ライブイベントとフィード]()を参照してください。

属性についての詳細は、[属性の使用]()を参照してください。

## AudienceDB属性の構成

デフォルトでは、すべてのオーディエンスがAudienceDBに選択されています。AudienceDBからオーディエンスを削除するためにオーディエンスの選択を解除できます。また、必要に応じて訪問と訪問の属性を選択または選択解除できます。

AudienceDBに保存される属性とオーディエンスを構成するには、次の手順を使用します：

1. **Store &gt; AudienceDB**に移動します。  
アカウントで利用可能なオーディエンスと属性のリストが表示されます。以下に示すように。  
![](/images/server-side/data-access/audiencedb-screen.png)  
**Scope**、**Type**、または**Data Type**で属性のリストをフィルタリングできます。
1. 必要に応じてオーディエンスの選択を解除して、AudienceDBから削除します。 
1. AudienceDBに追加または削除するために属性を選択または選択解除します。  
1. 保存して公開します。

## EventDB属性の構成

デフォルトでは、イベントストリームにはアカウントで定義されたすべてのイベント属性が含まれています。Tealium Collectタグからデータを収集するストリームでは、イベント中に発火する各タグに対して追加のブール属性が含まれています。例えば、Tealium iQタグ管理アカウントにGoogle AnalyticsとTealium Collectタグがある場合、イベントストリームには、各イベントで発火したかどうかを示すブール属性`Google Analytics`が含まれます。

EventDBに保存される属性を構成するには、次の手順を実行します：

1. **Store &gt; EventDB**に移動します。
1. **Show EventDB Attributes**をクリックします。  
アカウントで利用可能なイベント属性のリストが表示されます。  
      Restricted Dataとマークされた属性はデフォルトで除外されますが、チェックボックスをチェックして含めることができます。
1. 必要に応じてEventDBから属性を追加または削除します。  
すべてのプリロードされたEventDB属性はデフォルトで追加されます。 
      ![](/images/server-side/data-access/eventdb-attr-select.png)
1. **Save**をクリックします。
1. 保存して公開します。

EventDB属性を構成し、変更を公開した後、データがデータベースに表示されるまでに最大1時間かかる場合があります。

## 保存された属性の変更

EventDBまたはAudienceDBの保存に以前に追加された属性を削除し、変更を公開すると、その属性はEventDBまたはAudienceDBから削除されます。

属性を削除し、その後再度追加して変更を公開すると、削除されたEventDBまたはAudienceDBのデータは復元できません。
