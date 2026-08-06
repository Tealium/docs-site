---
title: Adobe Analytics 1.4 コネクタ構成ガイド
description: この記事では、Adobe Analytics 1.4 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-analytics-connector/
---
## 動作原理

Tealium Customer Data HubのAdobe Analytics 1.4コネクタは、Adobeの[Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)を使用して、ウェブページやモバイルアプリのJavaScriptビーコンを使用する代わりに、アナリティクスデータをサーバーサイドから送信します。これにより、クライアントサイドから送信されるデータ量が削減され、さらにEventStreamやAudienceStreamからAdobe Analyticsへのオーディエンスデータや訪問データを渡すことができる利点があります。


<blockquote>
Adobe Analytics 1.4のサポート終了日は2026年8月12日で、WSSE認証も含まれます。Data Insertion APIはその日付を超えてもアクセス可能ですが、更新やアクティブなサポートは受けられません。AdobeはAdobe Analytics 2.0への移行を強く推奨しており、私たちも[Adobe Analytics 2コネクタ](https://docs.tealium.com/adobe-analytics-2-connector/)の使用への移行をお勧めします。
</blockquote>


## コネクタのアクション

| **アクション名**      | **AudienceStream** | **EventStream** |
|:---------------------|:-------------------|:----------------|
| アナリティクスイベントを送信 | ✓                  | ✓               |
## コネクター構成

Adobe Analytics コネクターを構成するには、以下の手順に従ってください：

1. **コネクターマーケットプレイス**にアクセスし、Adobe Analytics コネクターを追加します。  
[コネクター概要](https://docs.tealium.com/about-connectors/)の記事を読んで、コネクターを追加する一般的な手順について確認してください。

1. **タイトル**フィールドにコネクターのタイトルを入力します。
1. **データ挿入ドメイン**フィールドに、Adobe Analytics データ収集サーバーのドメインを入力します。例えば、`namespace.122.2o7.net`です。
1. **レポートスイートID**フィールドにレポートスイートIDを入力します。  
これはデータを送信するレポートスイートです。複数の宛先にデータを送信する場合は、レポートスイートのリストをコンマで区切って入力します。  
    
<blockquote>
この値はデータマッピングでも構成できます。
</blockquote>

1. **メモ**フィールドに、このコネクターに関する関連するメモを入力します。
1. **次へ**をクリックします。  
これで**アクション**タブに移動します。
1. **アクション**ドロップダウンリストから**Send Analytics Event**を選択し、以下のパラメーターを構成します：

| **グループ**                                                          | **説明**                                                                                                                                                                                                                                                                                                                                                                                        |
|:-------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| イベントパラメータ                                                   | <ul><li>以下の「一般属性」を参照してください</li></ul>                                                                                                                                                                                                                                                                                                                                                       |
| モバイルデータソースのライフサイクルイベント属性の自動マッピング | <ul><li>イベントパラメータセクションからAdobeデータ要素への値の自動マッピングを有効にするには、このチェックボックスをオンにします。</li><li>自動マッピングはモバイルイベントストリームアプリのライフサイクルにのみ適用されます。</li><li>詳細については、[Adobe Analytics Connector Lifecycle Mappings](https://docs.tealium.com/adobe-analytics-connector/)を参照してください。</li></ul> |
| コンテキストデータ                                                       | <ul><li>ドット形式を使用してキーを指定します。</li><li>例：`my.a`。</li><li>複数のキーと値のペアを指定できます。</li></ul>                                                                                                                                                                                                                                                                    |
| eVars                                                              | <ul><li>属性を番号にマッピングしてイベントeVarsを指定します。</li><li>例：`event_count`を`1`にマッピングして**eVar1**。</li><li>有効な範囲は`1`から`100`、プレミアムアカウントの場合は`250`です</li></ul>                                                                                                                                                                                       |
| 階層                                                          | <ul><li>階層文字列。</li><li>`1`から`5`を選択します。</li></ul>                                                                                                                                                                                                                                                                                                                             |
| リスト                                                               | <ul><li>変数に渡され、報告のために個々の項目として報告される値のリスト。</li><li>`1`から`3`を選択します。</li><li>データレイヤーには配列タイプが必要です。</li><li>Tealiumがデータを正しくフォーマットします。</li></ul>                                                                                                                             |
| プロパティ                                                         | <ul><li>アナリティクスプロパティ名。</li><li>属性を番号にマッピングして名前を指定します。</li><li>例：`lifetime_value`を`1`にマッピングして**prop1**。</li></ul>                                                                                                                                                                                                                               |
| イベント                                                             | <ul><li>イベントのリスト、またはカスタム値をコンマで区切って指定します。</li><li>[Adobe Analytics Configure Events Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を参照してください。</li></ul>                                                                                                                                      |
| イベントマッピング                                                      | <ul><li>上記で構成したイベント配列に含まれる潜在的な値をAdobe Analyticsカスタムイベント名にマッピングします。</li><li>例えば、`registration`を`event3`にマッピングすると、イベントペイロードで`registration`が`event3`に置き換えられます。</li></ul>                                                                                                                                                      |
| イベント値                                                       | <ul><li>`Counter`、`Numeric`、`Currency`イベントの値を指定します。</li><li>イベントを指定するには、数字を使用します。</li><li>例として、`1`は`event1`として送信されます。</li></ul>                                                                                                                                                                                                                   |
| 製品                                                           | <ul><li>製品属性（`Id`、`Category`、`Quantity`、`Price`）を指定します。</li><li>すべての配列は同じサイズで順序が揃っている必要があります。</li><li>詳細については、[Adobe Analytics Product Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)を参照してください。</li></ul>                                                                  |
| 製品eVars                                                      | <ul><li>製品eVarsの値を指定します。</li><li>すべての配列は**製品**セクションと同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>eVarマッピングを数字で指定します。</li><li>例として、`1`は`eVar1`にマッピングされます。</li></ul>                                                                                                                                   |
| 製品イベント                                                     | <ul><li>製品イベントの値を指定します。</li><li>すべての配列は**製品**セクションと同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>イベントマッピングを数字で指定します。</li><li>例として、`1`は`event1`にマッピングされます。</li></ul>                                                                                                                                  |

| ブランド                                                    | <ul><li>ブランド属性を指定してください。</li><li>利用可能な属性は **brand** と **version** です。</li><li>すべての配列は同じサイズでなければなりません。</li></ul>                                                                                                                                  |

パラメータの構成が完了したら、**保存**をクリックし、変更を保存して公開してください。

## 一般属性

すべての属性の完全なリファレンスについては、各フィールドに何を含めるべきかの詳細とともに、Adobeの[APIドキュメント](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)およびこの記事の[訪問およびエクスペリエンスクラウドID](#visitor-and-experience-cloud-ids)セクションを参照してください。
#### レポートスイートID

* レポートスイートIDを指定することで、コネクタ構成UIで以前に入力された値を上書きすることができます。その値を上書きする必要がない場合は、このフィールドを空白のままにしておくことができます。データレイヤー変数、または**カスタム値**を使用することができます。複数のレポートスイートにデータを送信する場合は、カンマ区切りリストを使用することができます。
* この構成は構成タブで定義された値を上書きします
* データを送信したいレポートスイートを指定します。URLに含まれています
* データレイヤー属性を指定する場合は、行ごとに単純な属性タイプを使用します。データを正しくフォーマットして渡すことができます

| Map From                                                                                               | Map To                    | Notes                                                                                                                                                                                                                                                                                                                                                                                         | Sample Connector Output                                                                                                                            |
|:-------------------------------------------------------------------------------------------------------|:--------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|
| 永続的な訪問IDを含むCustomer Data Hub属性、例えば、tealium\_visitor\_id                              | visitorID\*               | <ul><li>これが訪問レベルの永続的な値であることを確認してください。</li><li>例: Tealium Visitor ID</li></ul>                                                                                                                                                                                                                                                                                   | `<visitorID>01619ea9a91a001af7e29b75797104079005c07101008M</visitorID>`                                                                            |
| ページ名/タイトルを含むCustomer Data Hub属性                                                            | pageName                  | <ul><li>文字列値</li></ul>                                                                                                                                                                                                                                                                                                                                                                    | `<pageName>Homepage</pageName>`                                                                                                                    |
| 現在のURLを含むCustomer Data Hub属性（例えば、組み込みの"Current URL"属性）                              | pageURL                   | <ul><li>文字列値</li></ul>                                                                                                                                                                                                                                                                                                                                                                    | `<pageURL>[http://www.tealium.com](http://www.tealium.com%5C)</pageURL>`                                                                           |
| Adobe Experience Cloud IDを含むCustomer Data Hub属性                                                    | marketingCloudVisitorID\* | <ul><li>通常、Visitor API JavaScriptタグを通じて取得されます。</li><li>iQタグ管理で実装されています。</li></ul>                                                                                                                                                                                                                                                                                 | `<marketingCloudVisitorID></marketingCloudVisitorID>`                                                                                              |
| リンク名を含むCustomer Data Hub属性                                                                      | linkName                  | <ul><li>文字列値。</li><li>例: tealium\_event</li></ul>                                                                                                                                                                                                                                                                                                                                       | `<linkName>Buy Now</linkName>`                                                                                                                     |
| クリックされたリンクのURLを含むCustomer Data Hub属性                                                    | linkURL                   | <ul><li>文字列値</li></ul>                                                                                                                                                                                                                                                                                                                                                                    | `<linkURL>[https://www.tealium.com/products/widgets/buynow\](https://www.tealium.com/products/widgets/buynow%5C)</linkURL>`                        |
| 注文IDを含むCustomer Data Hub属性                                                                        | purchaseID                | <ul><li>文字列値。</li><li>電子商取引の注文ID</li></ul>                                                                                                                                                                                                                                                                                                                                       | `<purchaseID>ORD12345</purchaseID>`                                                                                                                |
| ドキュメントリファラーを含むCustomer Data Hub属性                                                        | referrer                  | <ul><li>"Referring URL"属性を使用することをお勧めします。</li></ul>                                                                                                                                                                                                                                                                                                                           | `<referrer>[https://www.tealium.com/shop\](https://www.tealium.com/shop%5C)</referrer>`                                                            |
| イベント発生時のタイムスタンプを含むCustomer Data Hub属性                                                | timestamp                 | <ul><li>(オプション) Unixエポック秒またはISO 8601形式。</li><li>レポートスイートがタイムスタンプ付きヒットを明示的に受け入れるように構成されていない場合はマッピングしないでください。</li><li>詳細については、[タイムスタンプ実装ガイド](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/timestamp.html?lang=en "タイムスタンプ実装ガイド")を参照してください。</li></ul> | `<timestamp>1519207951063</timestamp>`                                                                                                             |


| 顧客データハブ属性で訪問のIPアドレスを含む | ipaddress | <ul><li>このオプション属性を使用するには、アカウントで訪問IP属性を有効にする必要があります。</li><li>この機能が必要な場合は、アカウントマネージャーに連絡してください。</li></ul> | `<ipaddress>127.0.0.1</ipaddress>` |
| 顧客データハブ属性でブラウザ/デバイスのユーザーエージェントを含む | userAgent | <ul><li>顧客データハブの組み込みユーザーエージェント属性の使用を推奨します</li></ul> | `<userAgent>Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.167 Safari/537.36</userAgent>` |
| 顧客データハブ属性でカスタムイベントのトランザクションID（注文IDではない）を含む | transactionID | <ul><li>これはpurchaseIDと同じではありません。</li><li>詳細については、[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/transactionid.html?lang=en)のドキュメントを参照してください。</li></ul> | `<transactionID>CMPSUMMER18</transactionID>` |

#### ユーザーエージェントクライアントヒント

Google ChromeやMicrosoft EdgeなどのChromiumブラウザからのクライアントヒントは、デバイス固有の情報を提供します。このデータセットは、デバイス情報の主要な情報源としてユーザーエージェント文字列を置き換えます。

これらのマッピング選択は**イベントパラメーター**セクションに表示されます。

|マップ元|マップ先|備考|サンプルコネクタ出力|
|----|----|----|----|
| 顧客データハブ属性でシステムアーキテクチャヒントを含む | `architecture` | <ul><li>文字列値。</li><li>詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<architecture>x64</architecture>` |
| 顧客データハブ属性でアプリケーションが使用するビット数を含む | `bitness` | <ul><li>文字列値。</li><li>詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<bitness>64</bitness>` |
| 顧客データハブ属性でブランドヒントを含む | `brands` | <ul><li>オブジェクトの配列として送信します。</li><li>詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<brands><brand><name>Chromium</name><version>100</version></brand></brands>` |
| 顧客データハブ属性でカスタムイベントがモバイル接続を通じて発生したかどうかを示す | `mobile` | <ul><li>ブール値。</li><li>詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<mobile>true</mobile>` |
| 顧客データハブ属性でプラットフォームヒントを含む | platform | <ul><li>文字列値。</li></ul> | `<platform>win</platform>` |
| 顧客データハブ属性でプラットフォームバージョンヒントを含む | `platformVersion` | <ul><li>文字列値。</li><li>詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<platformVersion>10</platformVersion>` |
| 顧客データハブ属性でWindowsが32ビットサブシステムを実行していることを示す。詳細については、[WoW64 at Wikipedia](https://en.wikipedia.org/wiki/WoW64)を参照してください | `wow64` | <ul><li>ブール値。</li><li>詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `<wow64>true</wow64>` |

### リンクタイプ

このフィールドはリンク追跡に使用され、[Link Type](https://experienceleague.adobe.com/docs/analytics/components/dimensions/custom-link.html?lang=en)の構成を可能にします。

| マップ元 | マップ先 | 説明 | 例 | サンプルコネクタ出力 |
|:----|:----|:----|:----|:----|
| ドロップダウンリストから任意の属性を選択するか、カスタム値を入力する | リンクタイプ: "d" - ダウンロードリンク "e" - エグジットリンク "o" - カスタム（その他）リンク | 選択した属性に値がある場合のみ、Adobe Analyticsにリンクタイプを送信します\* | マップ: (カスタム値): "true" to "o" | `<linkType>o</linkType>` |


<blockquote>
選択した属性の値が `null`、`undefined`、または `""`（空文字列）の場合、リンクタイプは送信されません。
</blockquote>


### コンテキストデータ

[Context Data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en)は、propsやeVarsの代わりとしてよりユーザーフレンドリーな代替手段として使用できます。任意のイベント属性または訪問属性をAdobe Analyticsのコンテキストデータ変数にマッピングできます。コンテキストデータ変数には任意の名前を付けることができますが、Adobeのベストプラクティスとして、すべての変数にユニークなキー（例えば会社名）を接頭辞として付けることが推奨されています。いくつかの変数は予め定められた機能のためにのみ使用され、これらの変数は `a.` で接頭辞が付けられます。

| マップ元 | マップ先 | 説明 | 例 | サンプルコネクタ出力 |
|:----|:----|:----|:----|:----|
| ドロップダウンから任意の属性を選択するか、カスタム値を入力する | companyname.someproperty | 定義された顧客データハブ属性をコンテキストデータ属性にマッピングする | マップ: (顧客データハブ属性) キャンペーン名を "tealium.productColor" に | `<contextData>&lt;tealium.productColor&gt;Red&lt;/tealium.productColor&gt;`</contextData> |
### Analytics eVars

このフィールドは、Customer Data Hubの属性を[eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en)にマッピングするために使用されます。eVarsは、「eVar」という単語とeVarの番号を使用して指定する必要があります。例えば、「eVar11」です。有効な範囲は1から250です。

| Map From                                                  | Map To                                            | Description                                                                     | Example                                                      | Sample Connector Output                 |
|:----------------------------------------------------------|:--------------------------------------------------|:--------------------------------------------------------------------------------|:-------------------------------------------------------------|:----------------------------------------|
| ドロップダウンから任意の属性を選択、またはカスタム値を入力 | eVarX（Xは1〜250の整数）                          | Customer Data Hubの定義済み属性を分析レポートのeVarにマッピング                 | Map: (Customer Data Hub Attribute) Campaign Name to "eVar75" | `<eVar75>Summer2018`</eVar75> |

### Analytics Property Name (s.props)

このフィールドは、Customer Data Hubの属性を[props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en)にマッピングするために使用されます。Propsは、「prop」という単語とpropの番号を使用して指定する必要があります。例えば、「prop4」です。有効な範囲は1から75です。[List props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props)もサポートされていますが、これにはAdobe Analytics Report Suite管理インターフェースでの事前構成が必要です。

| Map From                                                  | Map To                                           | Description                                                                     | Example                                                 | Sample Connector Output            |
|:----------------------------------------------------------|:-------------------------------------------------|:--------------------------------------------------------------------------------|:--------------------------------------------------------|:-----------------------------------|
| ドロップダウンから任意の属性を選択、またはカスタム値を入力 | propX（Xは1〜75の整数）                          | Customer Data Hubの定義済み属性を分析レポートのpropにマッピング                 | Map: (Customer Data Hub Attribute) Link Name to "prop4" | `<prop4>Buy Now`</prop4> |

### Events (s.events)

[Events](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)は、ウェブサイトやアプリで特定のイベントがどれだけ頻繁に発生しているかを測定するために使用されます。events変数は、特定の分析イベントに対してカウントされるべきすべてのイベントをリストするコンマ区切りの文字列です。[predefined events](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)と[custom events](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en)は同じ文字列で送信されます。

Adobe Analyticsコネクタでは、以下の2つの方法でイベントを指定します：

* 他の場所（例えば、iQ Tag Managementの拡張、Enrichment、またはデータレイヤー内で直接）で入力されたイベント名のリストを含む配列値をマッピングします。

| Map From                                                  | Data Type | Example Input                  | Sample Connector Output                           |
|:----------------------------------------------------------|:----------|:-------------------------------|:--------------------------------------------------|
| イベントのリストを表すCustomer Data Hub属性               | Array     | ["event1", "event5", "event9"] | `<events>event1,event5,event9</events>` |

* 特定のイベント番号にマッピングされる文字列値の配列を指定し、"Custom Event Mapping"セクションでイベント番号のマッピングを指定します：

| Map From                                                             | Map To                                        | Example Event Array                              | Example Input              | Sample Connector Output                                                                                      |
|:---------------------------------------------------------------------|:----------------------------------------------|:-------------------------------------------------|:---------------------------|:-------------------------------------------------------------------------------------------------------------|
| イベント配列で検索する文字列を含むカスタムテキスト値                 | トリガーするイベントの名前、例えばevent8        | ["newsletter\_registration", "homepage\_viewed"] | "newsletter\_registration" | `<events>event8</events>` (文字列 "newsletter\_registration" がイベント配列に含まれていたため) |

### Event Value Mapping

このフィールドでは、イベントに数値を割り当てることができます。このフィールドは「Custom Event Mapping」フィールドとは関連していません。つまり、「event2」が「Custom Event Mapping」で指定されていても、「Value」イベントとして指定されている場合、イベント変数には値なしで1回、値ありで1回、合計2回含まれます。

| Map From                                 | Data Type | Map To                                     | Example Input       | Sample Connector Output               |
|:-----------------------------------------|:----------|:-------------------------------------------|:--------------------|:--------------------------------------|
| 数値を表す属性                           | Number    | eventX（Xはイベントの番号）                | Map "9" to "event5" | `<events>event5=9</events>` |

### Event Serialization

イベントIDを含む属性をマッピングしてイベントのシリアライズを構成します。例えば、「ABC123」を「2」にマッピングすると、「event2=ABC123」と送信されます。

| Map From                           | Data Type | Map To           | Example Input                                | Sample Connector Output                                  |
|:-----------------------------------|:----------|:-----------------|:---------------------------------------------|:---------------------------------------------------------|
| イベントIDを表す属性               | String    | イベント番号      | Map "ABC123" to "1",<br> Map "ABC123" to "2" | `<events>event1=ABC123,event2:ABC123</events>` |
### ライフサイクルイベント

Adobe Analyticsは、アプリケーションのライフサイクルイベントを追跡する機能を持っています。Tealiumのモバイルライブラリには、この機能をサポートするためのオプションモジュールが用意されており、Adobe Analyticsに必要なデータを自動的に生成します。

| Tealium属性 | Adobe変数 | 説明 | データタイプ | 例 |
| --- | --- | --- | --- | --- |
| lifecycle\_diddetect\_crash | a.CrashEvent | この起動/スリープ解除イベント中にクラッシュが検出されたか。真の場合のみ記入されます。 | Boolean | true |
| lifecycle\_dayofweek\_local | a.DayOfWeek | 呼び出しが行われた地元の曜日（1=日曜日、2=月曜日など） | Number | 13 |
| lifecycle\_dayssincelaunch | a.DaysSinceFirstUse | 最初の起動からの日数（整数で増加） | Number | 23 |
| lifecycle\_dayssinceupdate | a.DaysSinceLastUpgrade | 最後に検出されたアプリバージョンの更新からの日数（整数で増加） | Number | 46 |
| lifecycle\_dayssincelastwake | a.DaysSinceLastUse | 最後に検出されたスリープ解除からの日数（整数で増加） | Number | 1 |
| lifecycle\_firstlaunchdate\_MMDDYYYY | a.InstallDate | GMTタイムスタンプがMM/DD/YYYY形式でフォーマットされます | String | 01/18/2012 |
| lifecycle\_hourofday\_local | a.HourOfDay | 呼び出しが行われた地元の時間（24時間形式） | String | true |
| lifecycle\_isfirstlaunch | a.InstallEvent | 呼び出しが最初の起動/スリープ解除の場合のみ存在します | String | true |
| lifecycle\_isfirstlaunchupdate | a.UpgradeEvent | 呼び出しが検出された更新後の最初の起動/スリープ解除の場合のみ存在します | Boolean | true |
| lifecycle\_isfirstwakemonth | a.MonthlyEngUserEvent | 呼び出しが月の最初の起動/スリープ解除の場合のみ存在します | Boolean | true |
| lifecycle\_priorsecondsawake | a.PrevSessionLength | 最後の起動以来アプリがスリープ解除していた全秒数。以前のすべてのスリープ解除からの合計が送信されます。lifecycle\_type: launch呼び出しのみで送信されます。 | Number | 126 |
| lifecycle\_totalwakecount | a.Launches | インストール以来の起動+スリープ解除の総数（アプリが削除されない限りリセットされません） | Number | "563" |
| lifecycle\_type | a.LaunchEvent if lifecycle\_type == "launch" | ライフサイクル呼び出しのタイプ | String | "launch", "wake", "sleep" |
| device (obj-c/android) or model\_name (swift) | a.DeviceName | デバイスモデル | String | iPhone 7 Plus |
| carrier (obj-c/android) or network\_name (swift) | a.CarrierName | ネットワークキャリア名 | String | Verizon |
| device\_resolution | a.Resolution | 画面解像度 | String | 1080x1920 |
| resolution | 画面解像度 | String | 1080x1920 |
| app\_id | a.AppID | アプリID | String | Digital Velocity 1.0 |
| device\_os\_version (obj-c/android) or os\_version (swift) | a.OSVersion | オペレーティングシステムのバージョン | String | 11.1 |

詳細については、Adobe Mobile Coreの[ライフサイクルメトリクス](https://developer.adobe.com/client-sdks/documentation/mobile-core/lifecycle/metrics/)のドキュメントを参照してください。

### 製品

[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)変数は、特定のページ上の1つ以上の製品に関するeコマース情報をキャプチャするために必要な場合に使用されます（カテゴリ、製品ID、価格、数量）。
### 階層データ

ページ[階層](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en)は、サイト/アプリのナビゲーション構造内でページを分類するのに役立ちます。使用可能なスロットは5つ（hier1 - hier5）です。階層変数として使用できる唯一のサポートされているCustomer Data Hub属性タイプは配列です。

| マップ元                                                  | データタイプ | マップ先                              | 説明                                                                                                  | 例                                                               | サンプルコネクタ出力                 |
|:----------------------------------------------------------|:------------|:--------------------------------------|:-----------------------------------------------------------------------------------------------------|:----------------------------------------------------------------|:-----------------------------------|
| ドロップダウンから任意の属性を選択、またはカスタム値を入力 | 配列        | hier1 - hier5 (ドロップダウン選択)    | Customer Data Hub属性を配列形式でAdobe Analyticsの指定された階層変数にマッピングします              | マップ：(Customer Data Hub属性) ページ分類を「hier1」にマッピング | `<hier1>Article</hier1>`           |

### リストデータ

[リスト変数](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en)は、複数の値を含む区切り文字列で、しばしば帰属目的で使用されます。各レポートスイートには最大3つのリスト変数が利用可能です。リスト変数として使用できる唯一のサポートされているCustomer Data Hub属性タイプは配列です。

| マップ元                                 | データタイプ | マップ先                                   | 説明                                                                                               | 例                                                         | サンプルコネクタ出力                   |
|:-----------------------------------------|:------------|:-------------------------------------------|:--------------------------------------------------------------------------------------------------|:------------------------------------------------------------|:--------------------------------------|
| ドロップダウンから任意の配列属性を選択   | 配列        | list1, list2, list3 (ドロップダウン選択)   | Customer Data Hub属性を配列形式でAdobe Analyticsの指定されたリスト変数にマッピングします          | マップ：(Customer Data Hub属性) リファラーリストを「list1」にマッピング | `<list1>google.com</list1>`           |

## 訪問およびExperience Cloud ID

[訪問ID](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en)に関するAdobe Analyticsのドキュメントと、複数のIDが提供された場合の優先順位を参照してください。

### ユースケース1: Adobe Analyticsの実装が初めての場合

これが完全にサーバーサイドの新しいAdobe Analytics実装になる場合、独自の一意の訪問IDを使用し、コネクタのvisitorID属性に渡すことができます。[制約](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/visitorid)に基づいて適切な訪問IDを決定する必要があります。

### ユースケース2: 既存のAdobe AnalyticsクライアントサイドJavaScriptからの移行

JavaScriptベースのAdobe Analyticsタグからサーバーサイドコネクタへ移行する場合、訪問を「失う」ことがないように一貫した訪問IDを維持する必要があります。また、Adobe Analytics Customer Data Hubコネクタを二次的な収集メカニズムとして実装する場合（ウェブページやアプリで引き続きJavaScriptタグを主要な収集メカニズムとして使用している場合）、訪問IDを移行する必要があります。

このユースケースで説明されているように、既存のAdobe AnalyticsクライアントサイドJavaScriptから移行するための次の手順に従ってください：

1. [これらの指示](https://docs.tealium.com/adobe-experience-cloud-id-service-tag/)に従ってAdobe Experience Cloud IDタグを構成し、iQ Tag Managementでタグを構成します。
1. このステップでは、Adobe訪問IDをファーストパーティクッキーに保存します。このクッキーは、セッションの期間中、値を再リクエストする必要なく、Customer Data Hubに値が送信されることを保証します。
    * iQ Tag Managementでデータレイヤータブに移動し、`utag_main_adobe_mcid`および`utag_main_aa_vid`という2つの新しいファーストパーティクッキー変数を作成します。
        
<blockquote>
これらの変数の名前を変更することはできますが、`utag_main_`プレフィックスを保持してください。これにより、`utag_main`クッキーにスタックしてクッキースペースを節約できます。変数の名前を変更する場合は、以下のJavaScriptスニペットも更新する必要があります。
</blockquote>

    * 新しいJavaScriptコード拡張を作成し、Adobe Experience Cloud IDサービスタグにスコープを構成し、次のコードを貼り付けます：
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
        この拡張機能は、Adobeのサーバーから訪問IDが正常に取得されたときに呼び出されるAdobe Visitor IDサービスへのコールバックを作成し、訪問IDとExperience Cloud IDをTealiumの独自のファーストパーティクッキー(`utag_main`)に保存します。クッキーはセッションの終了時に期限切れになりますが、将来訪問IDが更新される場合に備えています。クッキーを永続的にする（期限切れにしない）場合は、上記のコードで`sessionExpiry`を`""`に構成します。
    * JavaScript拡張に条件を追加します。「utag\_main\_adobe\_mcid `is not defined` AND utag\_main\_aa\_vid `is not defined`」。これにより、このセッション中にコードが再度実行されるのを防ぎます。
1. Customer Data HubのAudienceStreamおよびEventStreamを構成します。
    * AudienceStream構成 - AudienceStreamをお持ちの場合、Adobe訪問IDとExperience Cloud IDを訪問レベルの文字列属性として保存できます。訪問ID属性としては保存しないでください。オーディエンスイベントによってトリガーされるアクションの場合、新しい属性をコネクタ構成の`visitorID`および`marketingCloudVisitorID`にマッピングできます。
    * EventStream構成 - EventStreamのみをお持ちの場合、訪問ID変数を保存する機能がないため、値をクッキーに保存しました。前のステップのiQ Tag Management構成をProdに公開している場合は、新しい`utag_main_adobe_mcid`および`utag_main_aa_vid`の値がすでに[イベント属性](https://docs.tealium.com/add-enrichment/)に表示されています。
    * Prodに公開していない場合は、手動でイベント属性を追加できます。**First Party Cookie**文字列属性タイプを使用してこれらの属性を定義します。これらの属性を定義したら、Adobe Analyticsコネクタでそれらを選択し、それぞれ`marketingCloudVisitorID`および`visitorID`にマッピングできます。
## 一般的な問題のデバッグ

* コネクタのテストには、[trace](https://docs.tealium.com/about-trace/)の使用をお勧めします。トレースを実行する際には、「HTTP Request Body」フィールドを確認し、Adobeに送信された整形済みXMLを表示します。出力を上記の表の「Sample Connector Output」フィールドと比較して、出力を検証してください。
* Adobeから返されるレスポンスコードにエラーがないかを確認してください。HTTPレスポンスステータス：200/成功以外は、リクエストにエラーがあったことを示します。
* Data Insertion APIの完全なURL構造は、`http://namespace.112.2o7.net/b/ss//6`の形式に従います。ここで、二重スラッシュは意図的で有効です（JavaScriptのAdobe Analytics実装では、ここにレポートスイートIDが存在します）。`/6`はXMLペイロードが送信されていることを示し、reportSuite値はXMLペイロードの一部として送信されます。これは、[trace](https://docs.tealium.com/about-trace/)セッションを実行するときに表示される値です。
    
<blockquote>
コネクタ構成に完全なURL値を入力する必要はありません。TealiumはData Insertion Domain値に基づいてURLを自動生成します。完全なURLはトレースセッションを実行しているときにのみ表示されます。
</blockquote>

* 特定の実装によっては、Data Insertion Domainの値が異なる場合があります（例：`sc.omtrdc.net`）、しかし、独自のファーストパーティトラッキングドメインを持っている場合を除き、ドメインの前には常に名前空間が先行します（例：`namespace.sc.omtrdc.net`）。
* Adobe Analyticsにデータが受信されていない場合は、レポートスイートの[**Timestamps Optional**](https://experienceleague.adobe.com/docs/analytics/technotes/timestamps-optional.html?lang=en)セクションを確認してください。タイムスタンプがオプションでない場合は、有効なタイムスタンプをマッピングすることが重要です。
* User AgentまたはClient Hintsにマッピングすることを強くお勧めします。この値をマッピングしない場合、AdobeはサーバーのUser Agent（例：`Apache-HttpClient/4.5.5(Java/11.0.17`）を取得し、それがボットトラフィックとして識別される可能性があります。