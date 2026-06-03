---
title: コネクター: コネクターの追加
description: このステップでは、コネクターの追加、アクションの構成、データマッピングの使用方法を示します。
url: https://docs.tealium.com/ja/server-side/getting-started/audiencestream-cdp/add-connector/
---
## Googleシートを作成する

この例では、Googleシートのコネクターを使用して、顧客プロファイルデータをスプレッドシートに記録する方法を示しますが、独自のベンダーを使用することもできます。このステップの準備として、&#34;AudienceStream Test&#34;という名前のGoogleシートのスプレッドシートを作成し、最初の2つの列に&#34;email&#34;と&#34;lifetime value&#34;という名前を付けてください。

スプレッドシートは次のようになります：

![](/images/server-side/as-getting-started-sheet-name.jpg)

## Googleシートのコネクターを追加する

Googleシートのコネクターを構成するには、以下の手順を使用します：

1. **AudienceStream &gt; Audience Connectors**に移動します。
1. **&#43; Add Connector**ボタンをクリックします。
1. サイドナビゲーションパネルの**Categories**で**Big Data**をクリックして選択肢を絞ります。
1. **Google Sheets**を選択し、**Continue**をクリックします。
1. **Source**タブで、送信したいデータを選択します
    * **Audience from**
        オーディエンスがドロップダウンリストに表示されない場合、あなたのアカウントはおそらくAudienceStreamが有効になっていません。アカウントマネージャーに連絡してサポートを求めてください。

1. トリガーとして**In Audience at end of visit**を選択します
1. **Frequency Cap** - (On/Off, Default: Off) アクションがトリガーされる頻度を制御します
    * アクションの優先度
    * アクションのクールダウングループ

1. アクションに説明的な名前を付け、例えば`VIP Big Spenders`とし、**Continue**をクリックします。
1. **Configuration**タブで、**Add Connector**をクリックし、接続の名前を入力し、**Establish Connection**をクリックします。  
Googleアカウントの認証ダイアログが表示されます。
1. ユーザーアカウント名を確認し、**Allow**をクリックします。  
コネクターの構成ウィンドウに**Connected**と表示されます。**Done**をクリックし、次に**Continue**をクリックします。
1. **Action**タブで、デフォルトのアクション**Add or Update Row**を選択し、以下のパラメータを構成します：
    * **Row Operation**  
新しい行を追加するだけの**Add Only**、既存の行を検索して更新する**Update Only**、既存の行を検索して見つかった場合は更新し、見つからなかった場合は新しい行を追加する**Add or Update**を選択します。
    * **Spreadsheet Name**  
使用するスプレッドシートファイルの名前を特定します。  
ドロップダウンからスプレッドシートの名前を選択するか、使用するスプレッドシートファイルの名前を入力します（例：&#34;AudienceStream Test&#34;）。 
        ![](/images/server-side/spreadsheet.png)
    * **Worksheet Name**  
使用するスプレッドシート内のワークシートの名前を特定します。  
ドロップダウンからワークシートの名前を選択するか、使用するワークシートの名前を入力します（例：&#34;Sheet1&#34;）。 
        ![](/images/server-side/worksheet.png)
    * **Row ID**  
各イベントの一意の行IDを含む列を特定します。この場合、`Email Address`訪問属性はシートの`email`列名に対応します。  
**Map**リストから属性を選択し、**To**フィールドに対応するスプレッドシートの列名（カスタム値）を入力します。アクションが発火すると、指定された列で属性値を検索し、次のように行います：  
        * 値が存在する場合、行データマッピングによって指定されたように、一致する行が更新されます（次を参照）。
        * 値が存在しない場合、新しい行が**Row ID**の値とRow Dataで指定された属性で作成されます。
    * **Row Data**  
スプレッドシートに追加したい追加の属性をマップします。各属性には、スプレッドシート内に割り当てられた列名が必要です。この場合、`Lifetime Order Value`属性の値を`lifetime value`という名前のスプレッドシートの列に記録しています。  
        ここに入力された名前は、上記の列名と完全に一致していなければなりません。
    * **Exclude empty values when updating**  
スプレッドシートの既存のデータを更新または上書きする際に、空の属性を除外したい場合は、このボックスをチェックします。

1. **Continue**をクリックして**Summary**タブに移動し、**Finish**をクリックして保存します。

アカウントを保存して公開し、次のステップに進んでTraceツールを使用してテストを開始します。
