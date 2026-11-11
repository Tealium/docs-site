---
title: Adobe Analytics 1.4 コネクタ構成ガイド
description: この記事では、Adobe Analytics 1.4 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-analytics-connector/
---
## 仕組み

Tealium Customer Data Hub の Adobe Analytics 1.4 コネクタは、Web ページやモバイルアプリで JavaScript ビーコンを使用する代わりに、Adobe の [Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) を使用して、サーバーサイドで分析データを送信します。これにより、クライアントサイドから送信されるデータ量が削減されるほか、Event Streaming または Customer Data Platform（CDP）から Adobe Analytics にオーディエンスデータや訪問データを渡すことができます。


<blockquote>
Adobe Analytics 1.4 API および WSSE 認証は、2026 年 8 月 12 日にサポート終了となりました。このコネクタで使用されている Data Insertion API は、Adobe Analytics 1.4 API のサポート終了による影響を受けず、引き続き利用できます。このサポート終了を理由に Adobe Analytics 2.0 コネクタへ移行する必要はありません。
</blockquote>


## コネクタのアクション

| **アクション名** | **訪問プロファイル** | **イベントデータ** |
|:---------------------|:-------------------|:----------------|
| 分析イベントを送信 | ✓                  | ✓               |
## コネクタの構成

インターフェイスで次の手順を実行して、Adobe Analytics コネクタを構成します。

1. コネクタマーケットプレイスに移動し、Adobe Analytics コネクタを追加します。  
コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

1. **タイトル**フィールドに、コネクタのタイトルを入力します。
1. **データ挿入ドメイン**フィールドに、Adobe Analytics データ収集サーバーのドメインを入力します。例：`namespace.122.2o7.net`
1. **レポートスイート ID**フィールドに、レポートスイート ID を入力します。  
これは、データの送信に使用されるレポートスイートです。複数の送信先にデータを送信するには、レポートスイートをカンマ区切りのリストで指定します。  
    
<blockquote>
この値は、データマッピングを使用して構成することもできます。
</blockquote>

1. **メモ**フィールドに、このコネクタに関するメモを入力します。
1. **次へ**をクリックします。  
**アクション**タブが表示されます。
1. **アクション**ドロップダウンリストから**分析イベントを送信**を選択し、次のパラメータを構成します。

| **グループ** | **説明** |
|:---|:---|
| イベントパラメータ | <ul><li>以下の「一般属性」を参照してください。</li></ul> |
| モバイルデータソース向けライフサイクルイベント属性の自動マッピング | <ul><li>イベントパラメータセクションの値を Adobe データ要素に自動的にマッピングするには、このチェックボックスをオンにします。</li><li>自動マッピングは、モバイルイベントストリーミングアプリのライフサイクルにのみ適用されます。</li><li>詳細については、[Adobe Analytics コネクタのライフサイクルマッピング](https://docs.tealium.com/adobe-analytics-connector/)を参照してください。</li></ul> |
| コンテキストデータ | <ul><li>ドット形式を使用してキーを指定します。</li><li>例：`my.a`</li><li>複数のキーと値のペアを指定できます。</li></ul> |
| eVar | <ul><li>属性を番号にマッピングして、イベントの eVar を指定します。</li><li>例：**eVar1** には `event_count` を `1` にマッピングします。</li><li>有効な範囲は `1`～`100` です。プレミアムアカウントの場合は `250` までです。</li></ul> |
| 階層 | <ul><li>階層文字列です。</li><li>`1`～`5` から選択します。</li></ul> |
| リスト | <ul><li>変数に渡され、レポートでは個別の明細項目として報告される値のリストです。</li><li>`1`～`3` から選択します。</li><li>データレイヤーで配列型を使用する必要があります。</li><li>Tealium は、渡せるようにデータを正しく書式構成します。</li></ul> |
| プロパティ | <ul><li>Analytics プロパティ名です。</li><li>属性を番号にマッピングして名前を指定します。</li><li>例：**prop1** には `lifetime_value` を `1` にマッピングします。</li></ul> |
| イベント | <ul><li>イベントのリスト、またはカンマ区切りのカスタム値を指定します。</li><li>[Adobe Analytics のイベント実装の構成](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を参照してください。</li></ul> |
| イベントマッピング | <ul><li>上で構成したイベント配列に含まれる可能性のある値を、Adobe Analytics のカスタムイベント名にマッピングします。</li><li>たとえば、registration を `event3` にマッピングすると、イベントペイロード内の `registration` が `event3` に置き換えられます。</li></ul> |
| イベント値 | <ul><li>`Counter`、`Numeric`、`Currency` イベントの値を指定します。</li><li>イベントを指定するには番号を使用します。</li><li>たとえば、1 は `event1` として送信されます。</li></ul> |
| 製品 | <ul><li>製品属性（`Id`、`Category`、`Quantity`、`Price`）を指定します。</li><li>すべての配列は同じサイズで、要素の順序が揃っている必要があります。</li><li>詳細については、[Adobe Analytics の製品実装](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)を参照してください。</li></ul> |
| 製品 eVar | <ul><li>製品 eVar の値を指定します。</li><li>すべての配列は、**製品**セクションの配列と同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>eVar のマッピングを番号で指定します。</li><li>たとえば、`1` は `eVar1` にマッピングされます。</li></ul> |
| 製品イベント | <ul><li>製品イベントの値を指定します。</li><li>すべての配列は、**製品**セクションの配列と同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>イベントのマッピングを番号で指定します。</li><li>たとえば、`1` は `event1` にマッピングされます。</li></ul> |
| ブランド                                                    | <ul><li>ブランド属性を指定します。</li><li>使用可能な属性は **brand** と **version** です。</li><li>すべての配列のサイズは同じである必要があります。</li></ul>                                                                                                                                  |

パラメーターの構成が完了したら、**Save** をクリックし、変更を保存して公開します。

## 一般属性

各フィールドに含めるべき正確な内容など、すべての属性の詳細なリファレンスについては、Adobe の [API ドキュメント](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)および本記事の[訪問 ID と Experience Cloud ID](#visitor-and-experience-cloud-ids)セクションを参照してください。
#### レポートスイート ID

* レポートスイート ID を指定すると、コネクタ構成 UI で以前に入力した値が上書きされます。その値を上書きする必要がない場合は、このフィールドを空白のままにできます。データレイヤー変数または**カスタム値**のいずれかを使用できます。複数のレポートスイートにデータを送信する場合は、カンマ区切りのリストを使用できます。
* これにより、「構成」タブで定義された値が上書きされます。
* データの送信先となるレポートスイートを指定します。URL に含まれます。
* データレイヤー属性を指定する場合は、行ごとに単純な属性タイプを使用してください。渡すデータは適切にフォーマットされます。

| マッピング元                                                                                               | マッピング先                    | 注記                                                                                                                                                                                                                                                                                                                                                                                         | コネクタ出力の例                                                                                                                            |
|:-------------------------------------------------------------------------------------------------------|:--------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|
| 永続的な訪問 ID（例：tealium\_visitor\_id）を含む Customer Data Hub 属性      | visitorID\*               | <ul><li>訪問レベルで永続的な値であることを確認してください。</li><li>例：Tealium 訪問 ID</li></ul>                                                                                                                                                                                                                                                                                   | `<visitorID>01619ea9a91a001af7e29b75797104079005c07101008M</visitorID>`                                                                            |
| ページ名／タイトルを含む Customer Data Hub 属性                                               | pageName                  | <ul><li>文字列値</li></ul>                                                                                                                                                                                                                                                                                                                                                                | `<pageName>Homepage</pageName>`                                                                                                                    |
| 現在の URL（例：組み込みの「Current URL」属性）を含む Customer Data Hub 属性 | pageURL                   | <ul><li>文字列値</li></ul>                                                                                                                                                                                                                                                                                                                                                                | `<pageURL>[http://www.tealium.com](http://www.tealium.com%5C)</pageURL>`                                                                           |
| Adobe Experience Cloud ID を含む Customer Data Hub 属性                                   | marketingCloudVisitorID\* | <ul><li>通常は Visitor API JavaScript タグを通じて取得されます。</li><li>タグ管理で実装されます。</li></ul>                                                                                                                                                                                                                                                                             | `<marketingCloudVisitorID></marketingCloudVisitorID>`                                                                                              |
| リンク名を含む Customer Data Hub 属性                                                   | linkName                  | <ul><li>文字列値。</li><li>例：tealium\_event</li></ul>                                                                                                                                                                                                                                                                                                                               | `<linkName>Buy Now</linkName>`                                                                                                                     |
| クリックされたリンクの URL を含む Customer Data Hub 属性                                     | linkURL                   | <ul><li>文字列値</li></ul>                                                                                                                                                                                                                                                                                                                                                                | `<linkURL>[https://www.tealium.com/products/widgets/buynow\](https://www.tealium.com/products/widgets/buynow%5C)</linkURL>`                        |
| 注文 ID を含む Customer Data Hub 属性                                                    | purchaseID                | <ul><li>文字列値。</li><li>E コマース注文 ID</li></ul>                                                                                                                                                                                                                                                                                                                                   | `<purchaseID>ORD12345</purchaseID>`                                                                                                                |
| ドキュメントの参照元を含む Customer Data Hub 属性                                           | referrer                  | <ul><li>組み込みの「Referring URL」属性の使用を推奨します。</li></ul>                                                                                                                                                                                                                                                                                                                         | `<referrer>[https://www.tealium.com/shop\](https://www.tealium.com/shop%5C)</referrer>`                                                            |
| イベント発生時刻のタイムスタンプを含む Customer Data Hub 属性                  | timestamp                 | <ul><li>（任意）Unix エポック秒または ISO 8601 形式。</li><li>レポートスイートがタイムスタンプ付きヒットを受け入れるよう明示的に構成されていない場合は、マッピングしないでください。</li><li>詳細については、[タイムスタンプ実装ガイド](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/timestamp.html?lang=en "タイムスタンプ実装ガイド")を参照してください。</li></ul> | `<timestamp>1519207951063</timestamp>`                                                                                                             |
| 訪問のIPアドレスを含むCustomer Data Hub属性                                   | ipaddress                 | <ul><li>このオプション属性を使用するには、アカウントで訪問IP属性を有効にしておく必要があります。</li><li>この機能が必要な場合は、アカウントマネージャーにお問い合わせください。</li></ul>                                                                                                                                                                                                              | `<ipaddress>127.0.0.1</ipaddress>`                                                                                                                 |
| ブラウザー／デバイスのユーザーエージェントを含むCustomer Data Hub属性                            | userAgent                 | <ul><li>Customer Data Hubに組み込まれているユーザーエージェント属性の使用を推奨します。</li></ul>                                                                                                                                                                                                                                                                                                      | `<userAgent>Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.167 Safari/537.36</userAgent>` |
| カスタムイベントのトランザクションID（注文IDではありません）を含むCustomer Data Hub属性            | transactionID             | <ul><li>これはpurchaseIDとは異なります。</li><li>詳細については、[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/transactionid.html?lang=en)のドキュメントを参照してください。</li></ul>                                                                                                                                                                | `<transactionID>CMPSUMMER18</transactionID>`                                                                                                       |

#### ユーザーエージェント・クライアントヒント

Google ChromeやMicrosoft EdgeなどのChromiumブラウザーが提供するクライアントヒントには、デバイス固有の情報が含まれます。このデータセットは、デバイス情報の主要な取得元としてユーザーエージェント文字列に代わるものです。

これらのマッピング項目は、**イベントパラメーター**セクションに表示されます。

|マッピング元|マッピング先|注記|コネクター出力例|
|----|----|----|----|
| システムアーキテクチャのヒントを含むCustomer Data Hub属性。 | `architecture` | <ul><li>文字列値。</li><li>詳細については、Adobeの[ユーザーエージェント・クライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<architecture>x64</architecture>` |
| 実行中のアプリケーションが使用するビット数を含むCustomer Data Hub属性。 | `bitness` | <ul><li>文字列値。</li><li>詳細については、Adobeの[ユーザーエージェント・クライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<bitness>64</bitness>` |
| ブランドのヒントを含むCustomer Data Hub属性。 | `brands` | <ul><li>オブジェクトの配列として送信します。</li><li>詳細については、Adobeの[ユーザーエージェント・クライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul>  | `<brands><brand><name>Chromium</name><version>100</version></brand></brands>` |
| カスタムイベントがモバイル接続を介して発生したかどうかを示すCustomer Data Hub属性。 | `mobile` | <ul><li>ブール値。</li><li>詳細については、Adobeの[ユーザーエージェント・クライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul>  | `<mobile>true</mobile>` |
| プラットフォームのヒントを含むCustomer Data Hub属性。 | platform | <ul><li>文字列値。</li></ul> | `<platform>win</platform>` |
| プラットフォームバージョンのヒントを含むCustomer Data Hub属性。 | `platformVersion` | <ul><li>文字列値。</li><li>詳細については、Adobeの[ユーザーエージェント・クライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul>  | `<platformVersion>10</platformVersion>` |
| Windowsで32ビットサブシステムが実行されていることを示す値を含むCustomer Data Hub属性。詳細については、[WikipediaのWoW64](https://en.wikipedia.org/wiki/WoW64)を参照してください。 | `wow64` | <ul><li>ブール値。</li><li>詳細については、Adobeの[ユーザーエージェント・クライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<wow64>true</wow64>` |

### リンクタイプ

このフィールドはリンクトラッキングに使用され、[リンクタイプ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/custom-link.html?lang=en)を構成できます。

| マッピング元                                                           | マッピング先                                                                   | 説明                                                                       | 例                            | コネクター出力例  |
|:-------------------------------------------------------------------|:-------------------------------------------------------------------------|:----------------------------------------------------------------------------------|:-----------------------------------|:-------------------------|
| ドロップダウンリストから任意の属性を選択するか、カスタム値を入力します | リンクタイプ：「d」- ダウンロードリンク、「e」- 離脱リンク、「o」- カスタム（その他）リンク | 選択した属性に値がある場合にのみ、リンクタイプをAdobe Analyticsに送信します\* | マッピング：（カスタム値）「true」から「o」 | `<linkType>o</linkType>` |


<blockquote>
選択した属性の値が`null`、`undefined`、または`""`（空文字列）の場合、送信リクエストにリンクタイプは構成されません。
</blockquote>


### コンテキストデータ

[コンテキストデータ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en)は、propsやeVarsの代わりとなる、より使いやすい選択肢として使用できます。任意のイベント属性または訪問属性を、Adobe Analyticsのコンテキストデータ変数にマッピングできます。コンテキストデータ変数には任意の名前を付けられますが、すべての変数に会社名などの一意のキーを接頭辞として付けることがAdobeのベストプラクティスです。一部の変数は予約されており、ライフサイクル指標など、あらかじめ定められた機能にのみ使用できます。これらの変数には`a.`という接頭辞が付いています。

| マッピング元                                                  | マッピング先                   | 説明                                                            | 例                                                                    | コネクター出力例                                                                             |
|:----------------------------------------------------------|:-------------------------|:-----------------------------------------------------------------------|:---------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|
| ドロップダウンから任意の属性を選択するか、カスタム値を入力します | companyname.someproperty | 定義済みのCustomer Data Hub属性をコンテキストデータ属性にマッピングします | マッピング：（Customer Data Hub属性）キャンペーン名から「tealium.productColor」 | `<contextData>&lt;tealium.productColor&gt;Red&lt;/tealium.productColor&gt;`</contextData> |
### Analytics eVar

このフィールドは、Customer Data Hub の属性を[eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en)にマッピングするために使用します。eVar は、大文字と小文字を区別しない「eVar」という語と eVar の番号を組み合わせて指定する必要があります（例：「eVar11」）。有効な範囲は 1～250 です。

| マッピング元 | マッピング先 | 説明 | 例 | コネクタ出力例 |
|:----------------------------------------------------------|:--------------------------------------------------|:--------------------------------------------------------------------------------|:-------------------------------------------------------------|:----------------------------------------|
| ドロップダウンから任意の属性を選択するか、カスタム値を入力 | eVarX（X は 1～250 の範囲の整数） | 定義済みの Customer Data Hub 属性を Analytics レポートの eVar にマッピングします | マッピング：（Customer Data Hub 属性）Campaign Name を「eVar75」へ | `<eVar75>Summer2018`</eVar75> |

### Analytics プロパティ名（s.props）

このフィールドは、Customer Data Hub の属性を[prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en)にマッピングするために使用します。prop は、`prop` という語と prop の番号を組み合わせて指定する必要があります（例：「prop4」）。有効な範囲は 1～75 です。[リスト prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props)もサポートされていますが、Adobe Analytics レポートスイートの管理インターフェイスで事前に構成する必要があります。

| マッピング元 | マッピング先 | 説明 | 例 | コネクタ出力例 |
|:----------------------------------------------------------|:-------------------------------------------------|:--------------------------------------------------------------------------------|:--------------------------------------------------------|:-----------------------------------|
| ドロップダウンから任意の属性を選択するか、カスタム値を入力 | propX（X は 1～75 の範囲の整数） | 定義済みの Customer Data Hub 属性を Analytics レポートの prop にマッピングします | マッピング：（Customer Data Hub 属性）Link Name を「prop4」へ | `<prop4>Buy Now`</prop4> |

### イベント（s.events）

[イベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を使用すると、Web サイトまたはアプリで特定のイベントが発生する頻度を測定できます。events 変数は、特定の Analytics イベントについてカウントする必要があるすべてのイベントを列挙した、カンマ区切りの文字列です。[定義済みイベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)と[カスタムイベント](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en)は、どちらも同じ文字列で送信されます。

Adobe Analytics コネクタでは、次の 2 つの方法でイベントを指定します。

* 別の場所（Tag Management の拡張機能、エンリッチメント、データレイヤー内など）で構成されたイベント名のリストを含む配列値をマッピングします。  

| マッピング元 | データ型 | 入力例 | コネクタ出力例 |
|:----------------------------------------------------------|:----------|:-------------------------------|:--------------------------------------------------|
| イベントのリストを表す Customer Data Hub 属性 | 配列 | ["event1", "event5", "event9"] | `<events>event1,event5,event9</events>` |

* 特定のイベント番号にマッピングする文字列値の配列を指定し、「カスタムイベントマッピング」セクションでイベント番号のマッピングを次のように指定します。  

| マッピング元 | マッピング先 | イベント配列の例 | 入力例 | コネクタ出力例 |
|:---------------------------------------------------------------------|:----------------------------------------------|:-------------------------------------------------|:---------------------------|:-------------------------------------------------------------------------------------------------------------|
| Events 配列内で検索する文字列を含むカスタムテキスト値 | トリガーするイベントの名前（例：event8） | ["newsletter\_registration", "homepage\_viewed"] | "newsletter\_registration" | `<events>event8</events>`（文字列「newsletter\_registration」が events 配列に含まれているため） |

### イベント値のマッピング

このフィールドでは、イベントに数値を割り当てることができます。このフィールドは「カスタムイベントマッピング」フィールドとは連動していません。つまり、「event2」が「カスタムイベントマッピング」で指定され、さらに「値」イベントとしても指定されている場合、イベント変数には 2 回含まれます。一方は値なしで、もう一方は値付きです。

| マッピング元 | データ型 | マッピング先 | 入力例 | コネクタ出力例 |
|:-----------------------------------------|:----------|:-------------------------------------------|:--------------------|:--------------------------------------|
| 数値を表す属性 | 数値 | eventX（X はイベントの番号） | 「9」を「event5」にマッピング | `<events>event5=9</events>` |

### イベントのシリアル化

イベント ID を含む属性を、イベントを指定する番号にマッピングして、イベントのシリアル化を構成します。たとえば、「ABC123」を「2」にマッピングすると、「event2=ABC123」が送信されます。

| マッピング元 | データ型 | マッピング先 | 入力例 | コネクタ出力例 |
|:-----------------------------------|:----------|:-----------------|:---------------------------------------------|:---------------------------------------------------------|
| イベント ID を表す属性 | 文字列 | イベント番号 | 「ABC123」を「1」にマッピング、<br>「ABC123」を「2」にマッピング | `<events>event1=ABC123,event2:ABC123</events>` |
### ライフサイクルイベント

Adobe Analytics では、アプリケーションのライフサイクルイベントをトラッキングできます。Tealium の各モバイルライブラリには、この機能をサポートするオプションモジュールが用意されており、Adobe Analytics に必要なデータが自動的に生成されます。

| Tealium 属性 | Adobe 変数 | 説明 | データ型 | 例 |
| --- | --- | --- | --- | --- |
| lifecycle\_diddetect\_crash | a.CrashEvent | この起動／復帰イベント中にクラッシュが検出されたかどうか。true の場合にのみ値が構成されます。 | ブール値 | true |
| lifecycle\_dayofweek\_local | a.DayOfWeek | 呼び出しが行われた現地の曜日（1＝日曜日、2＝月曜日など） | 数値 | 13 |
| lifecycle\_dayssincelaunch | a.DaysSinceFirstUse | 初回起動からの日数（整数単位） | 数値 | 23 |
| lifecycle\_dayssinceupdate | a.DaysSinceLastUpgrade | 最後に検出されたアプリバージョンの更新からの日数（整数単位） | 数値 | 46 |
| lifecycle\_dayssincelastwake | a.DaysSinceLastUse | 最後に検出された復帰からの日数（整数単位） | 数値 | 1 |
| lifecycle\_firstlaunchdate\_MMDDYYYY | a.InstallDate | MM/DD/YYYY 形式の GMT タイムスタンプ | 文字列 | 01/18/2012 |
| lifecycle\_hourofday\_local | a.HourOfDay | 呼び出しが行われた現地時刻（24 時間形式） | 文字列 | true |
| lifecycle\_isfirstlaunch | a.InstallEvent | 呼び出しが最初の起動／復帰呼び出しである場合にのみ存在します | 文字列 | true |
| lifecycle\_isfirstlaunchupdate | a.UpgradeEvent | 更新が検出された後、呼び出しが最初の起動／復帰である場合にのみ存在します | ブール値 | true |
| lifecycle\_isfirstwakemonth | a.MonthlyEngUserEvent | 呼び出しがその月の最初の起動／復帰である場合にのみ存在します | ブール値 | true |
| lifecycle\_priorsecondsawake | a.PrevSessionLength | 前回の起動以降にアプリがアクティブだった秒数（整数）。それ以前のすべての復帰からの合計を集計します。lifecycle\_type が launch の呼び出しでのみ送信されます。 | 数値 | 126 |
| lifecycle\_totalwakecount | a.Launches | インストール後の起動数と復帰数の合計（アプリを削除した場合にのみリセット） | 数値 | "563" |
| lifecycle\_type | a.LaunchEvent if lifecycle\_type == "launch" | ライフサイクル呼び出しのタイプ | 文字列 | "launch", "wake", "sleep" |
| device (obj-c/android) or model\_name (swift) | a.DeviceName | デバイスモデル | 文字列 | iPhone 7 Plus |
| carrier (obj-c/android) or network\_name (swift) | a.CarrierName | ネットワークキャリア名 | 文字列 | Verizon |
| device\_resolution | a.Resolution | 画面解像度 | 文字列 | 1080x1920 |
| resolution | 画面解像度 | 文字列 | 1080x1920 |
| app\_id | a.AppID | アプリ ID | 文字列 | Digital Velocity 1.0 |
| device\_os\_version (obj-c/android) or os\_version (swift) | a.OSVersion | オペレーティングシステムのバージョン | 文字列 | 11.1 |

詳細については、Adobe Mobile Core の[ライフサイクル指標](https://developer.adobe.com/client-sdks/documentation/mobile-core/lifecycle/metrics/)ドキュメントを参照してください。

### 製品

[Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数は、特定のページ上にある 1 つ以上の製品について、E コマース情報（カテゴリ、製品 ID、価格、数量）を取得する必要がある場合に使用します。

Products 変数への値の構成に使用できるのは、データ型が配列の Customer Data Hub 属性のみです。すべての配列は同じ長さでなければなりません。たとえば、ページ上に 5 つの製品がある場合、製品 ID、数量、価格、カテゴリの各配列には、すべて 5 つの要素が必要です。

| マッピング元 | データ型 | マッピング先 | 入力データの例 | コネクタ出力の例 |
|:----------------------------------------------------------|:----------|:------------------|:---------------------|:-----------------------------------------------------|
| 製品カテゴリを表す Customer Data Hub 属性 | 配列 | Products Category | ["Shoes", "Shirts"]  | `<products>Shoes;;;,Shirts;;;`</products>  |
| 製品 ID を表す Customer Data Hub 属性 | 配列 | Products ID | ["ABC123", "EFG234"] | `<products>;ABC123;;,;EFG234;;`</products> |
| 数量を表す Customer Data Hub 属性 | 配列 | Products Quantity | ["1", "2"]           | `<products>;;1;,;;2;;`</products>          |
| 価格を表す Customer Data Hub 属性 | 配列 | Products Price | ["149.99", "79.80"]  | `<products>;;;149.99,;;;79.80`</products>  |

### 製品イベント値のマッピング

このフィールドでは、[Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数内の各製品にカスタムコンバージョンイベントを割り当て、各イベントに数値を割り当てることができます。

「単純」変数（単一の値またはカスタムテキスト値）をマッピングすると、リスト内のすべての製品に同じ値が適用されます。リスト（配列）値をマッピングする場合、その配列は他の製品配列と同じ長さである必要があり、配列内の各項目には配列内の位置に応じて異なる値が構成されます。

以下の例では、次の製品配列がイベント属性として存在すると仮定します。

```
Product Category: ["Footwear", "Apparel"] Product ID: ["Running Shoes", "T-Shirt"] Quantity: ["1", "1"] Price: ["99.99", "49.99"]
```

| マッピング元 | データ型 | マッピング先 | 入力値の例 | コネクタ出力の例 |
|:-----------------------------------------------------------------|:----------|:-----------------------------------------------|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 数値を含むカスタムテキスト値 | 文字列 | トリガーするイベントの名前（例：event8） | "9.99"（カスタム値） | `<events>event8</events>``<products>Footwear;Running Shoes;1;99.99;**event8=9.99**,Apparel;T-Shirt;1;49.99;**event8=9.99**`</products>   |
| 数値データの配列を表す Customer Data Hub 属性 | 配列 | トリガーするイベントの名前（例：event12） | ["1.99", "4.99"] | `<events>event8</events>``<products>Footwear;Running Shoes;1;99.99;**event12=1.99**,Apparel;T-Shirt;1;49.99;**event12=4.99**`</products> |

### 製品マーチャンダイジング eVar

このフィールドでは、[Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数内の各製品に eVar を割り当てることができます。

これらは、上記で説明した「製品イベント値のマッピング」フィールドと同じように機能します。

| マッピング元 | データ型 | マッピング先 | 入力値の例 | コネクタ出力の例 |
|:-------------------------------------------------------------------------------------------|:----------|:--------------------------------------------|:--------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| eVar 値を含むカスタムテキスト値 | 文字列 | トリガーする eVar の名前（例：eVar4） | "my\_custom\_value" | `<products>Footwear;Running Shoes;1;99.99;event8=9.99;**eVar4=my\_custom\_value**,Apparel;T-Shirt;1;49.99;event8=9.99;**eVar4=my\_custom\_value**`</products> |
| eVar 値の配列（製品の色など）を表す Customer Data Hub 属性 | 配列 | トリガーする eVar の名前（例：eVar6） | ["red", "green"] | `<products>Footwear;Running Shoes;1;99.99;event8=9.99;**eVar6=red**,Apparel;T-Shirt;1;49.99;event8=9.99;**eVar6=green**`</products> |
### 階層データ

ページの[階層](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en)は、サイト／アプリのナビゲーション構造内でページを分類するために役立ちます。利用可能なスロットは、hier1～hier5 の 5 つです。階層変数として使用できる、サポート対象の Customer Data Hub 属性タイプは配列のみです。

| マッピング元                                                  | データタイプ | マッピング先                              | 説明                                                                                                | 例                                                           | コネクタ出力例            |
|:----------------------------------------------------------|:----------|:------------------------------------|:-----------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------|:-----------------------------------|
| ドロップダウンから任意の属性を選択するか、カスタム値を入力 | 配列     | hier1～hier5（ドロップダウンで選択） | 配列形式で定義された Customer Data Hub 属性を、Adobe Analytics の指定された階層変数にマッピングします | マッピング：（Customer Data Hub 属性）ページ分類を「hier1」にマッピング | `<hier1>Article`</hier1> |

### リストデータ

[リスト変数](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en)は、複数の値を含む区切り文字付き文字列で、多くの場合アトリビューションに使用されます。各レポートスイートでは、最大 3 つのリスト変数を使用できます。リスト変数として使用できる、サポート対象の Customer Data Hub 属性タイプは配列のみです。

| マッピング元                                 | データタイプ | マッピング先                                   | 説明                                                                                           | 例                                                     | コネクタ出力例               |
|:-----------------------------------------|:----------|:-----------------------------------------|:------------------------------------------------------------------------------------------------------|:------------------------------------------------------------|:--------------------------------------|
| ドロップダウンから任意の配列属性を選択 | 配列     | list1、list2、list3（ドロップダウンで選択） | 配列形式で定義された Customer Data Hub 属性を、Adobe Analytics の指定されたリスト変数にマッピングします | マッピング：（Customer Data Hub 属性）リファラーリストを「list1」にマッピング | `<list1>google.com`</list1> |

## 訪問 ID と Experience Cloud ID

[訪問 ID](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en)および複数の ID が指定された場合の優先順位については、Adobe Analytics のドキュメントを参照してください。

### ユースケース 1：既存の Adobe Analytics 実装がない場合

完全に新規の 100% サーバーサイド Adobe Analytics 実装である場合は、独自の一意な訪問 ID を使用し、コネクタの `visitorID` 属性に渡すことができます。Adobe が定める[制約](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/visitorid)の範囲内で、適切な訪問 ID の構成を決定する必要があります。

### ユースケース 2：既存の Adobe Analytics クライアントサイド JavaScript から移行する場合

JavaScript ベースの Adobe Analytics タグからサーバーサイドコネクタへ移行する場合、完全移行時に訪問を「失わない」ように、一貫した訪問 ID を維持する必要があります。また、Adobe Analytics Customer Data Hub コネクタを補助的なデータ収集メカニズムとして実装する場合（引き続き Web ページまたはアプリ上の JavaScript タグを主要なデータ収集メカニズムとして使用する場合）も、訪問 ID を移行する必要があります。

このユースケースで説明するように、既存の Adobe Analytics クライアントサイド JavaScript から移行するには、次の手順に従います。

1. [こちらの手順](https://docs.tealium.com/adobe-experience-cloud-id-service-tag/)に従って Adobe Experience Cloud ID タグを構成し、タグ管理でタグをセットアップします。
1. この手順では、Adobe 訪問 ID をファーストパーティ Cookie に保存します。この Cookie により、セッション中に値を再取得することなく、ヒットのたびに Customer Data Hub へ値が送信されます。  
    * タグ管理で「データレイヤー」タブに移動し、`utag_main_adobe_mcid` および `utag_main_aa_vid` という 2 つの新しいファーストパーティ Cookie 変数を作成します。  
        
<blockquote>
必要に応じてこれらの変数名を変更できますが、`utag_main_` プレフィックスは必ず維持してください。これにより、`utag_main` Cookie 内にまとめて格納され、Cookie の容量を節約できます。変数名を変更する場合は、以下の JavaScript スニペットも更新する必要があります。
</blockquote>
  
    * Adobe Experience Cloud ID サービスタグをスコープとする新しい JavaScript コード拡張機能を作成し、次のコードを貼り付けます。  
        ```
        `if (typeof vAPI !== "undefined") {
        vAPI.getInstance(u.data.adobe_org_id,
	      function (visitor) {
	      var mcID = visitor.getMarketingCloudVisitorID(),
	      analyticsID = visitor.getAnalyticsVisitorID(),
	      sessionExpiry = ";exp-session";
	      // store Adobe IDs for the session duration
	      if (!mcID) {
	        // something went wrong - the visitor IDs could not be retrieved
	        utag.DB("MCID could not be returned");
	      } else {
	        utag.loader.SC("utag_main",{"adobe_mcid" : mcID + sessionExpiry, "aa_vid" : analyticsID + sessionExpiry});
	        // optionally, trigger an empty utag.link call to trigger sending the cookie values to UDH
	        // if utag.track call is omitted (default), values will be sent on the next utag.link or utag.view call anyway
	        // utag.track is used to avoid calling other third-party tags; only the collect tag should respond
	        // utag.track("adobe_vid_updated", {});
	      }
        },
        u.clearEmptyKeys(u.data.config), u.data.customer_ids);
        }   
        ```
        この拡張機能は、Adobe のサーバーから訪問 ID が正常に取得されたときに呼び出される Adobe Visitor ID サービスへのコールバックを作成し、訪問 ID と Experience Cloud ID を Tealium 独自のファーストパーティ Cookie（`utag_main`）に保存します。訪問 ID が将来更新される場合に備えて、Cookie はセッション終了時に期限切れになります。Cookie を永続化（無期限化）する場合は、上記のコードで `sessionExpiry` を `""` に構成します。
    * JavaScript 拡張機能に「utag\_main\_adobe\_mcid `is not defined` AND utag\_main\_aa\_vid `is not defined`」という条件を追加します。これにより、このセッション中にコードが再度実行されるのを防ぎます。
1. CDP およびイベントストリーミング用に Customer Data Hub を構成します。   
    * CDP の構成 — CDP を使用している場合は、Adobe 訪問 ID と Experience Cloud ID を訪問レベルの文字列属性として保存できます。訪問 ID 属性としては保存しないでください。オーディエンスイベントによってトリガーされるアクションでは、コネクタ構成で新しい属性を `visitorID` および `marketingCloudVisitorID` にマッピングできます。
    * イベントストリーミングの構成 — イベントストリーミングのみを使用している場合、訪問 ID 変数を保存できないため、値を Cookie に保存しました。前の手順のタグ管理構成をすでに本番環境へパブリッシュしている場合は、新しい `utag_main_adobe_mcid` および `utag_main_aa_vid` の値が[イベント属性](https://docs.tealium.com/add-enrichment/)にすでに存在しています。
    * 本番環境へパブリッシュしていない場合は、**ファーストパーティ Cookie**文字列属性タイプを使用して、イベント属性を手動で追加できます。これらの属性を定義すると、Adobe Analytics コネクタで属性を選択し、それぞれ `marketingCloudVisitorID` および `visitorID` にマッピングできます。
## 一般的な問題のデバッグ

* コネクタをテストするには、[トレース](https://docs.tealium.com/about-trace/)の使用を推奨します。トレースの実行中に「HTTP Request Body」フィールドを確認すると、Adobe に送信された整形済みの XML が表示されます。XML 出力を上記の表にある「Sample Connector Output」フィールドと比較して、出力が正しいことを確認できます。
* Adobe から返されるレスポンスコードにエラーがないか確認してください。「HTTP Response Status: 200/Successful」以外の場合は、リクエストでエラーが発生しています。
* Data Insertion API の完全な URL 構造は、`http://namespace.112.2o7.net/b/ss//6` という形式です。2 つの連続するスラッシュは意図されたものであり、有効です（JavaScript による Adobe Analytics の実装では、この位置にレポートスイート ID が入ります）。`/6` は XML ペイロードが送信されることを示し、reportSuite 値は XML ペイロードの一部として送信されます。これは、[トレース](https://docs.tealium.com/about-trace/)セッションの実行時に表示される値です。  
    
<blockquote>
コネクタ構成に完全な URL 値を入力する必要はありません。Tealium が Data Insertion Domain の値に基づいて URL を自動生成します。完全な URL は、トレースセッションの実行時にのみ表示されます。
</blockquote>

* 実際の実装では、Data Insertion Domain に別の値（例：`sc.omtrdc.net`）を使用する場合があります。ただし、独自のファーストパーティトラッキングドメイン（例：`smetrics.acme.com`）を使用する場合を除き、名前空間は常にドメインの前に置く必要があります（例：`namespace.sc.omtrdc.net`）。
* Adobe Analytics でデータを受信できない場合は、レポートスイートの[**タイムスタンプ（オプション）**](https://experienceleague.adobe.com/docs/analytics/technotes/timestamps-optional.html?lang=en)セクションを確認してください。タイムスタンプがオプションではない場合は、有効なタイムスタンプを必ずマッピングしてください。
* User Agent または Client Hints へのマッピングを強く推奨します。この値をマッピングしない場合、Adobe はサーバーの User Agent（例：`Apache-HttpClient/4.5.5(Java/11.0.17`）を取得するため、ボットトラフィックとして識別される可能性があります。