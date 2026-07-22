---
title: Tableauへの接続
description: この記事では、Tealium DataAccessにTableauを接続する方法について説明します
url: https://docs.tealium.com/ja/server-side/data-storage/data-viz-tools/connecting-tableau/
---## 前提条件

* Tableauの基本的な知識
* Tableauのウェブサイト [http://www.tableau.com/support/drivers](http://www.tableau.com/support/drivers) から適切なドライバーをインストールしてください。
* インストールするには、**Amazon Redshift**をクリックし、画面上の指示に従ってください。  

<blockquote>
TealiumはTableauとパートナーシップを結んでいますが、リセラーではありません。製品を使用する前に適切なTableauのライセンスを取得してください。支援が必要な場合は、アカウントマネージャーに連絡してサポートを開始し、進行させてください。
</blockquote>


### Redshiftへの接続

このセクションでは、新しいデータソースを追加し、Amazon Redshiftに接続する方法について説明します。

![](https://docs.tealium.com/images/server-side/tableau-data-soure-example.jpg)

Amazon Redshiftに接続するための次の手順を使用します：

1. 新しいデータソースを追加します。
1. Redshiftの認証情報を入力します。  
セキュアソケットレイヤー（SSL）が必要であることを確認します。
1. スキーマを選択します。  
アカウントとプロファイルに最も近いスキーマを選択します。  
例えば、あなたのアカウントが `tealium` で、プロファイルが `dataaccess` の場合、あなたのスキーマは `tealium__dataaccess` になります。
1. 一つまたは複数のテーブルを選択します。  
アカウントのテーブルとビューはテーブルセクションにリストされています。Tableauで分析したいテーブルを選択します。
    * この時点で、関連するフィールドがわかっている場合は、複数のテーブルを結合することができます。
    * このプロセス中に、"左"のテーブルのどのフィールドが"右"のテーブルのフィールドと関連しているか、そして二つのテーブル間で作成したい結合のタイプ（左、右、内部、または全外部）をTableauに伝える必要があります。  
    ![](https://docs.tealium.com/images/server-side/tableau-join2.jpg)
1. データの使用を開始するには、新しいシートを作成するか、既存のシートを選択します。

#### AudienceDBの例

以下の例では、2つのテーブルを結合するために使用されるキーは次のとおりです：

`visits_view."visit - visitor id"` = `visitors_view_normalized."visitor - id"`

![](https://docs.tealium.com/images/server-side/tableau-join.jpg)

### 分析のためのデータの準備

新しいデータソースを使用する場合、レポートを作成する前にフィールドを整理することをお勧めします。以下の提案を参照してください：

* **ディメンションとメジャー**  
デフォルトでは、ほとんど（またはすべて）のフィールドが"ディメンション"、つまりデータをスライスしたいフィールドとしてインポートされます。特定のフィールドを集計できるメトリックとして使用するつもりなら、これらのフィールドを"ディメンション"から"メジャー"に変換します。これには、注文合計、合計単位などのフィールドが含まれます。
* **カスタムメジャー**  
EventDBはイベントレベルのデータであるため、特定のフィールドが特定の値を持つイベント（行またはレコード）が何回発生したかを頻繁にカウントしたいと思うでしょう。例えば、"ユニークビジター"のカスタムメジャーです。これは、次の例に示す計算を使用して新しい計算フィールドを作成することで達成されます。この場合、特定の訪問IDがデータに何回ユニークに現れたかをカウントします：`COUNTD([Event - Visitor Id])`

### カスタム計算の例

以下のリストは、使用したい他のカスタム計算の例を提供します：

* 合計イベント（メジャー）  
`COUNTD([Event - Id])`
* Mac+Chrome Revenue (Measure)  
`IF FIND([Event - User Agent],"Chrome") > 0 AND FIND([Event - User Agent],"Mac") > 0 THEN [Event - Udo - Order Subtotal] END`
* ユニークな注文  
`COUNTD([Event - Udo - Order Id])`
* 高価な注文  
`COUNTD(IF [Event - Udo - Order Subtotal] > 500 THEN [Event - Udo - Order Id] END)`
* EventDBにはいくつかのデフォルトのフィールドがありますが、他のフィールドのほとんどは各顧客データベースに固有であり、Tealium IQで構成されている内容に基づいています。EventDBのデフォルトフィールドやカスタムフィールドの任意の組み合わせを使用してカスタム計算を作成することができます。

## トラブルシューティング

### パスワードの問題でRedShiftに接続できない

パスワードに以下の禁止されている文字が含まれていないか確認してください：

* プラス記号 (`+`)
* アットマーク (`@`)
* 右または左の中括弧 (`{`, ``}`)
* 右括弧 (`)*`)
* セミコロン (`;`)

### Tableau Serverのページに接続しようとするとエラーメッセージが表示される

Tableau serverのゲートウェイポート（デフォルト = 80）が、プロキシやファイアウォールなどのTableau Serverの外部要素によってブロックされている可能性があります。その結果、Tableau serverからの応答がユーザーに届かない。

このメッセージが表示されると、以下のいずれかが発生した可能性があります：

* 接続がリセットされました。
* ページの読み込み中にサーバーへの接続がリセットされました。
* サイトが一時的に利用できないか、あるいは混雑しています。数分後に再試行してください。
* ページを一つも読み込むことができない場合は、コンピュータのネットワーク接続を確認してください。
* コンピュータやネットワークがファイアウォールやプロキシによって保護されている場合は、ブラウザがウェブにアクセスできるように許可されていることを確認してください。

この問題を解決するには、ITチームと協力して、Tableau serverのゲートウェイポートとして使用されるポートを解放します。

## 追加のリソース

* [Tableau Knowledge Base](https://kb.tableau.com/articles/issue/error-the-connection-was-reset-connecting-to-tableau-server)  
よくある質問やベストプラクティスに関する詳細な情報が含まれています。
* [Connecting Tableau to an Amazon RedShift Data Source](https://onlinehelp.tableau.com/current/pro/desktop/en-us/examples_amazonredshift.htm)  
この記事では、Amazon RedshiftデータベースにTableauを接続し、データソースを構成する方法について説明しています。
