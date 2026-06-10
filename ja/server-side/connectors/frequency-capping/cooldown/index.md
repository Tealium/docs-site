---
title: クールダウングループ
description: この記事では、頻度制限にクールダウングループを使用する方法について説明します。
url: https://docs.tealium.com/ja/server-side/connectors/frequency-capping/cooldown/
---
## 新しいクールダウングループの追加

新しいクールダウングループを追加すると、そのグループはプロファイル内のすべての頻度制限アクションで利用可能になります。

![](/images/server-side/connectors/frequency-capping/whiteui-tiq-actionfrequencyandcapping-adding-a-new-cooldown-group.png)

新しいクールダウングループを追加するには、次の手順を使用します：

1. サイドバーで、**AudienceStream**に移動します。
1. 管理メニューで、**Manage Cooldown**をクリックします。  
1. **&#43; Add Cooldown Group**をクリックします。
1. **Color**ドロップダウンリストをクリックし、このグループに表示する色を選択します。  
1. **Name**フィールドに、このグループを識別するための一意の名前を入力します。
1. **Duration**ドロップダウンリストで、カスタム数値（時間単位）を入力するか、**6**、**12**、**24**、または**48**時間を選択します。  
時間数は、対象となるアクションをトリガーする間の待ち時間を決定します。
1. **Save**をクリックして確認します。

## デフォルトのクールダウングループの使用

![](/images/server-side/connectors/frequency-capping/whiteui-tiq-actionfrequencycappingandprioritization-default-cooldown-group.png)

デフォルトのクールダウングループは、プロファイルで他のクールダウンが構成されていない場合に頻度制限アクションに適用されます。デフォルトのクールダウングループの色と期間の構成を編集し、選択した頻度制限アクションに適用することができますが、名前は編集できません。

## コネクタアクションにクールダウングループを適用する

このセクションでは、コネクタアクションにクールダウングループを適用する方法について説明します。同じコネクタ内の1つ以上の頻度制限アクションにクールダウングループを適用することができます。

コネクタアクションにクールダウングループを適用するには、次の手順を使用します：

1. サイドバーで、**Connect &gt; Audience Connectors**に移動します。
1. **My Connectors**をクリックします。
1. コネクタをクリックして詳細を展開し、**Edit**をクリックします。  
1. **Actions**タブをクリックし、ドロップダウンリストを使用して頻度制限を適用したいアクションを選択します。
1. **&#43; Create Action**をクリックします。
1. **Frequency Cap**までスクロールダウンし、**On**をクリックします。
1. **Action Priority**の下で、上矢印または下矢印を使用してアクションの優先度として数値を割り当てます。  
      この値をゼロまたは負の数に構成しないでください。優先度は連続した数値ではなく、10の増分で割り当てます。これにより、後で新しいアクションを挿入する際に、他のアクションの優先度値を更新する必要がなくなります。
1. **Action Cooldown Group**の下で、ドロップダウンリストを使用してグループを選択します。  
      ![](/images/server-side/connectors/frequency-capping/whiteui-audiencestream-actionfrequencycappingandprioritization-select-action-cooldown-group-for-connector.png)
1. **Save**をクリックします。
1. プロファイルを保存し、公開します。
