---
title: AudienceDB と EventDB の構成
description: この記事では、EventDB と AudienceDB に保存する属性の構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/configure/
---
## 要件

* EventDB にデータを送信するには、イベントフィードを構成し、EventStore を有効にする必要があります。
* AudienceDB にデータを送信するには、AudienceStore を有効にする必要があります。


<blockquote>
アカウントとプロファイルで EventDB および AudienceDB を有効にするには、アカウントマネージャーにお問い合わせください。
</blockquote>


## 仕組み
 
データ保存は属性レベルで制御されます。イベント属性、訪問属性、または訪問属性を作成する際に、その属性を EventDB または AudienceDB に送信するオプションを選択できます。
![](https://docs.tealium.com/images/server-side/data-access/eventdb-attribute-checkbox.png)

次の図に示す **EventDB/AudienceDB** 画面でも、EventDB と AudienceDB に送信する属性を構成できます。
![](https://docs.tealium.com/images/server-side/data-access/eventdb-audiencedb-config-screen.png)


<blockquote>
すべてのプリロード済み属性（Tealium によって定義され、すべてのアカウントで利用できる属性）は、デフォルトで EventDB と AudienceDB に対して選択されています。この動作は変更できません。
</blockquote>


### 訪問属性と訪問属性

デフォルトでは、アカウント内のすべてのオーディエンスが AudienceDB に送信されます。AudienceDB に送信するオーディエンスと属性は、**EventDB/AudienceDB** 画面の **AudienceDB** タブで選択できます。詳細については、[AudienceDB 属性の構成](#configure-audiencedb-attributes)を参照してください。

### イベント属性

DOM 属性（URL、ドメイン、リファラー、ユーザーエージェントなど）は常に送信され、EventDB から除外することはできません。また、`tealium_account`、`tealium_profile`、`tealium_event` などの Tealium イベント属性も常に送信され、除外することはできません。その他の属性は、**EventDB/AudienceDB** 画面の **EventDB** タブで選択または選択解除できます。詳細については、[EventDB 属性の構成](#configure-eventdb-attributes)を参照してください。


<blockquote>
データ量によっては非常に大量のデータが生成される可能性があるため、必要な特定のイベントフィードに対してのみ EventDB を有効にすることをお勧めします。詳しくは、[ライブイベントとフィード](https://docs.tealium.com/about-event-feeds/)を参照してください。
</blockquote>


#### Tealium Collect タグからのイベントデータ

Tealium Collect タグからデータを収集するフィードには、イベント中に発火した各タグについて、追加のブール属性が含まれます。たとえば、タグ管理アカウントに Tealium Collect タグとともに Google Analytics が構成されている場合、イベントフィードには `Google Analytics` という名前のブール属性が含まれ、各イベントで Google Analytics が発火したかどうかを示します。

属性について詳しくは、[属性の使用](https://docs.tealium.com/about-attributes/)を参照してください。

## AudienceDB 属性の構成

デフォルトでは、すべてのオーディエンスが AudienceDB に対して選択されています。オーディエンスの選択を解除すると、AudienceDB から削除できます。また、必要に応じて訪問属性と訪問属性を選択または選択解除できます。

AudienceDB に保存する属性とオーディエンスを構成するには、次の手順を実行します。

1. **DataAccess** > **EventDB/AudienceDB** に移動します。
1. **AudienceDB** タブをクリックします。  
アカウントで利用できるオーディエンスと属性の一覧が表示されます。  
属性の一覧は、**データ型**、**属性タイプ**（プリロード済みまたはカスタム）、**AudienceDB**（有効または無効）、**タイプ**（オーディエンスまたは属性）でフィルタリングできます。
1. 属性を選択または選択解除して、AudienceDB に追加するか、AudienceDB から削除します。  
    
<blockquote>
Restricted Data としてマークされた属性は常に AudienceDB に送信されます。この動作は変更できません。
</blockquote>

1. 保存してパブリッシュします。

## EventDB 属性の構成

デフォルトでは、イベントフィードにアカウントで定義されているすべてのイベント属性が含まれます。

EventDB に保存する属性を構成するには、次の手順を実行します。

1. **DataAccess** > **EventDB/AudienceDB** に移動します。  
アカウントで利用できるイベント属性の一覧が表示されます。属性の一覧は、**データ型**、**属性タイプ**（プリロード済みまたはカスタム）、**EventDB**（有効または無効）でフィルタリングできます。  
    
<blockquote>
Restricted Data としてマークされた属性は、デフォルトでイベントフィードから除外されます。この動作は、各フィードの構成で変更できます。
</blockquote>

1. 属性を選択または選択解除して、EventDB に追加するか、EventDB から削除します。
1. 保存してパブリッシュします。


<blockquote>
EventDB 属性を構成して変更をパブリッシュした後、データベースへのデータの格納が開始されるまでに最大 1 時間かかることがあります。
</blockquote>


## 保存済み属性の変更

以前に EventDB または AudienceDB の保存に追加した属性を削除して変更をパブリッシュすると、その属性は EventDB または AudienceDB から削除されます。

属性を削除した後、その属性を再度追加して変更をパブリッシュしても、EventDB または AudienceDB から削除されたデータを復元することはできません。