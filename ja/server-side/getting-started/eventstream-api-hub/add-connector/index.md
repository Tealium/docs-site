---
title: コネクタ: コネクタを追加する
description: このステップでは、コネクタを追加し、アクションを構成し、データマッピングを使用する方法を示します。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/add-connector/
---
この例では、Google Sheetsコネクタを使用してスプレッドシートにイベントをログする方法を示しますが、独自のベンダーを使用することもできます。このステップを準備するために、`EventStream Test`という名前のGoogle Sheetsスプレッドシートを作成し、最初の3つの列に`Timestamp`、`Search Term`、`Search Results`という名前を付けます。

スプレッドシートは次のようになります:

![](https://docs.tealium.com/images/server-side/es-getting-started-connector-google-sheet-spreadsheet.jpg)

## Google Sheetsコネクタを追加する

Google Sheetsコネクタを構成するには、次の手順を使用します:

1. **Connect > Event Connectors**に移動します。
1. **+ Add Connector**をクリックします。
1. サイドナビゲーションパネルの**Categories**の下で、**Big Data**をクリックしてリストをフィルタリングします。
1. **Google Sheets**を選択し、**Continue**をクリックします。
    ![](https://docs.tealium.com/images/server-side/connectors-select-source.png)
1. **Source**タブで、送信したいデータに対応するデータソースとイベントフィードを選択し、このアクションの名前を入力します。
1. **Configuration**タブで、**Add Connector**をクリックし、接続の名前を入力し、**Establish Connection**をクリックします。Googleアカウントの認証ダイアログが表示されます。
1. ユーザーアカウント名を確認し、**Allow**をクリックします。コネクタの構成ウィンドウには`Connected`というメッセージが表示されます。**Done**をクリックします。
1. **Action**タブで、デフォルトのアクション**Add or Update Row**を選択し、次のパラメータを構成します:
    * **Row Operation**  
  新しい行を検索せずに追加するには**Add Only**を選択し、既存の行を検索して更新するには**Update Only**を選択し、既存の行を検索して見つかった場合は更新し、見つからなかった場合は新しい行を追加するには**Add or Update**を選択します。
    * **Spreadsheet Name**  
  使用するスプレッドシートファイルの名前を特定します。  
  ドロップダウンからスプレッドシートの名前を選択するか、使用するスプレッドシートファイルの名前を入力します（例：`EventStream Test`）。
    * **Worksheet Name**  
  使用するスプレッドシート内のワークシートの名前を特定します。  
  ドロップダウンからワークシートの名前を選択するか、使用するワークシートの名前を入力します（例：`Sheet1`）。
    * **Row ID**  
  各イベントの一意の行IDを含む列を特定します。この列は通常、イベントのタイムスタンプ属性です。マッピングで使用するために、この列の名前を`Timestamp`としました。  
        ![](https://docs.tealium.com/images/server-side/screen-shot-2020-05-27-at-2.52.47-pm.png)  
        **Map**リストから属性を選択し、**To**フィールドに対応するスプレッドシートの列名（カスタム値）を入力します。アクションが発火すると、指定された列で属性値を検索し、次のようにします:  
        * 値が存在する場合、**Row Data**マッピング（次を参照）で指定されたように、一致する行が更新されます。
        * 値が存在しない場合、新しい行が**Row ID**値と**Row Data**で指定された属性で作成されます。
    * **Row Data**  
    スプレッドシートに追加したい追加の属性をマップします。各属性には、スプレッドシート内に割り当てられた列名が必要です。この場合、`search_keyword`属性の値を`Search Term`という名前のスプレッドシートの列にログします。  
        ![](https://docs.tealium.com/images/server-side/screen-shot-2020-05-27-at-2.53.25-pm.png)
    * **Exclude empty values when updating**  
    スプレッドシート内の既存のデータを更新または上書きする際に空の属性を除外したい場合は、このボックスをチェックします。

1. **Continue**をクリックして**Summary**タブに移動し、**Finish**をクリックして保存します。

アカウントを保存して公開し、Traceツールを使用してテストを開始するための次のステップに進みます。
