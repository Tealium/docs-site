---
title: Adobe Analytics 1.4 コネクタ構成ガイド
description: この記事では、Adobe Analytics 1.4 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-analytics-connector/
---
## 動作原理

Tealium Customer Data HubのAdobe Analytics 1.4コネクタは、Adobeの[Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)を使用して、ウェブページやモバイルアプリのJavaScriptビーコンを使用する代わりに、アナリティクスデータをサーバーサイドから送信します。これにより、クライアントサイドから送信されるデータ量が削減され、さらに、EventStreamやAudienceStreamからAdobe Analyticsへのオーディエンスおよび訪問データを渡すことができる利点があります。

 Adobe Analytics 1.4のサポート終了日は2026年8月12日で、WSSE認証も含まれます。Data Insertion APIはその日付を超えてアクセス可能ですが、更新やアクティブなサポートは受けられません。AdobeはAdobe Analytics 2.0への移行を強く推奨しており、私たちも[Adobe Analytics 2コネクタ]()の使用への移行をお勧めします。

## コネクタアクション

| **アクション名**      | **AudienceStream** | **EventStream** |
|:---------------------|:-------------------|:----------------|
| アナリティクスイベントを送信 | ✓                  | ✓               |
## コネクター構成

Adobe Analytics コネクターを構成するには、インターフェースで以下の手順に従ってください：

1. **コネクターマーケットプレイス**にアクセスし、Adobe Analytics コネクターを追加します。  
[コネクター概要]()の記事を読んで、コネクターを追加する一般的な手順について確認してください。

1. **タイトル**フィールドにコネクターのタイトルを入力します。
1. **データ挿入ドメイン**フィールドに、Adobe Analytics データ収集サーバーのドメインを入力します。例えば、`namespace.122.2o7.net`です。
1. **レポートスイートID**フィールドにレポートスイートIDを入力します。  
これはデータを送信するレポートスイートです。複数の宛先にデータを送信する場合は、レポートスイートのリストをコンマで区切って入力します。  
    この値はデータマッピングでも構成できます。
1. **ノート**フィールドに、このコネクターに関する関連するメモを入力します。
1. **次へ**をクリックします。  
これで**アクション**タブに移動します。
1. **アクション**ドロップダウンリストから**Send Analytics Event**を選択し、以下のパラメーターを構成します：

| **グループ**                                                          | **説明**                                                                                                                                                                                                                                                                                                                                                                                        |
|:-------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| イベントパラメーター                                                   | &lt;ul&gt;&lt;li&gt;以下の「一般属性」を参照してください&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                         |
| モバイルデータソースのライフサイクルイベント属性の自動マッピング | &lt;ul&gt;&lt;li&gt;このチェックボックスをオンにすると、イベントパラメーターセクションからAdobeデータ要素への値が自動的にマッピングされます。&lt;/li&gt;&lt;li&gt;自動マッピングはモバイルイベントストリームアプリライフサイクルにのみ適用されます。&lt;/li&gt;&lt;li&gt;詳細については、[Adobe Analytics Connector Lifecycle Mappings]()を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| コンテキストデータ                                                       | &lt;ul&gt;&lt;li&gt;ドット形式を使用してキーを指定します。&lt;/li&gt;&lt;li&gt;例：`my.a`。&lt;/li&gt;&lt;li&gt;複数のキーバリューペアを指定できます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                  |
| eVars                                                              | &lt;ul&gt;&lt;li&gt;属性を番号にマッピングして、イベントeVarsを指定します。&lt;/li&gt;&lt;li&gt;例：`event_count`を`1`にマッピングして**eVar1**。&lt;/li&gt;&lt;li&gt;有効な範囲は`1`から`100`、プレミアムアカウントの場合は`250`です&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                             |
| 階層                                                              | &lt;ul&gt;&lt;li&gt;階層文字列。&lt;/li&gt;&lt;li&gt;`1`から`5`を選択します。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                   |
| リスト                                                              | &lt;ul&gt;&lt;li&gt;変数に渡され、報告のために個々の項目として報告される値のリストです。&lt;/li&gt;&lt;li&gt;`1`から`3`を選択します。&lt;/li&gt;&lt;li&gt;データレイヤーには配列タイプが必要です。&lt;/li&gt;&lt;li&gt;Tealiumはデータを正しくフォーマットして渡します&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                         |
| プロパティ                                                         | &lt;ul&gt;&lt;li&gt;アナリティクスプロパティ名。&lt;/li&gt;&lt;li&gt;属性を番号にマッピングして名前を指定します。&lt;/li&gt;&lt;li&gt;例：`lifetime_value`を`1`にマッピングして**prop1**。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                             |
| イベント                                                             | &lt;ul&gt;&lt;li&gt;イベントのリスト、またはカンマ区切りのカスタム値を指定します。&lt;/li&gt;&lt;li&gt;[Adobe Analytics Configure Events Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を参照してください&lt;/li&gt;&lt;/ul&gt;                                                                                   |
| イベントマッピング                                                      | &lt;ul&gt;&lt;li&gt;上記で構成したイベント配列に含まれる潜在的な値をAdobe Analyticsカスタムイベント名にマッピングします。&lt;/li&gt;&lt;li&gt;例えば、`registration`を`event3`にマッピングすると、イベントペイロードで`registration`が`event3`に置き換えられます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                      |
| イベント値                                                           | &lt;ul&gt;&lt;li&gt;`Counter`、`Numeric`、`Currency`イベントの値を指定します。&lt;/li&gt;&lt;li&gt;イベントを指定するには、数字を使用します。&lt;/li&gt;&lt;li&gt;例として、1は`event1`として送信されます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                             |
| 製品                                                               | &lt;ul&gt;&lt;li&gt;製品属性（`Id`、`Category`、`Quantity`、`Price`）を指定します。&lt;/li&gt;&lt;li&gt;すべての配列は同じサイズで順序が揃っている必要があります。&lt;/li&gt;&lt;li&gt;詳細については、[Adobe Analytics Product Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)を参照してください&lt;/li&gt;&lt;/ul&gt;                              |
| 製品eVars                                                          | &lt;ul&gt;&lt;li&gt;製品eVarsの値を指定します。&lt;/li&gt;&lt;li&gt;すべての配列は**製品**セクションと同じサイズである必要があります。&lt;/li&gt;&lt;li&gt;空の値は無視されます。&lt;/li&gt;&lt;li&gt;eVarマッピングを数字で指定します。&lt;/li&gt;&lt;li&gt;例として、`1`は`eVar1`にマッピングされます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                       |
| 製品イベント                                                         | &lt;ul&gt;&lt;li&gt;製品イベントの値を指定します。&lt;/li&gt;&lt;li&gt;すべての配列は**製品**セクションと同じサイズである必要があります。&lt;/li&gt;&lt;li&gt;空の値は無視されます。&lt;/li&gt;&lt;li&gt;イベントマッピングを数字で指定します。&lt;/li&gt;&lt;li&gt;例として、`1`は`event1`にマッピングされます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                              |
| ブランド                                                    | &lt;ul&gt;&lt;li&gt;ブランド属性を指定してください。&lt;/li&gt;&lt;li&gt;利用可能な属性は **brand** と **version** です。&lt;/li&gt;&lt;li&gt;すべての配列は同じサイズでなければなりません。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                  |

パラメータの構成が完了したら、**保存**をクリックし、変更を保存して公開してください。

## 一般属性

すべての属性の完全なリファレンスについては、各フィールドに何を含めるべきかの詳細とともに、Adobeの[APIドキュメント](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)およびこの記事の[訪問およびエクスペリエンスクラウドID](#visitor-and-experience-cloud-ids)セクションを参照してください。
#### レポートスイートID

* レポートスイートIDを指定することで、コネクタ構成UIで以前に入力された値を上書きすることができます。その値を上書きする必要がない場合は、このフィールドを空白のままにしておくことができます。データレイヤー変数、または**カスタム値**を使用することができます。複数のレポートスイートにデータを送信する場合は、カンマ区切りリストを使用することができます。
* この構成は構成タブで定義された値を上書きします
* データを送信したいレポートスイートを指定します。URLに含まれています
* データレイヤー属性を指定する場合は、行ごとに単純な属性タイプを使用してください。データを正しくフォーマットして渡すことができます

| Map From                                                                                               | Map To                    | Notes                                                                                                                                                                                                                                                                                                                                                                                         | Sample Connector Output                                                                                                                            |
|:-------------------------------------------------------------------------------------------------------|:--------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|
| 永続的な訪問IDを含むCustomer Data Hub属性、例えば、tealium\_visitor\_id                              | visitorID\*               | &lt;ul&gt;&lt;li&gt;これが訪問レベルの永続的な値であることを確認してください。&lt;/li&gt;&lt;li&gt;例: Tealium Visitor ID&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                   | `&lt;visitorID&gt;01619ea9a91a001af7e29b75797104079005c07101008M&lt;/visitorID&gt;`                                                                            |
| ページ名/タイトルを含むCustomer Data Hub属性                                                            | pageName                  | &lt;ul&gt;&lt;li&gt;文字列値&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                      | `&lt;pageName&gt;Homepage&lt;/pageName&gt;`                                                                                                                    |
| 現在のURLを含むCustomer Data Hub属性（例えば、組み込みの&#34;Current URL&#34;属性）                              | pageURL                   | &lt;ul&gt;&lt;li&gt;文字列値&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                      | `&lt;pageURL&gt;[http://www.tealium.com](http://www.tealium.com%5C)&lt;/pageURL&gt;`                                                                           |
| Adobe Experience Cloud IDを含むCustomer Data Hub属性                                                     | marketingCloudVisitorID\* | &lt;ul&gt;&lt;li&gt;通常、Visitor API JavaScriptタグを介して取得されます。&lt;/li&gt;&lt;li&gt;iQタグ管理で実装されています。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                 | `&lt;marketingCloudVisitorID&gt;&lt;/marketingCloudVisitorID&gt;`                                                                                              |
| リンク名を含むCustomer Data Hub属性                                                                      | linkName                  | &lt;ul&gt;&lt;li&gt;文字列値。&lt;/li&gt;&lt;li&gt;例: tealium\_event&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                         | `&lt;linkName&gt;Buy Now&lt;/linkName&gt;`                                                                                                                     |
| クリックされたリンクのURLを含むCustomer Data Hub属性                                                     | linkURL                   | &lt;ul&gt;&lt;li&gt;文字列値&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                      | `&lt;linkURL&gt;[https://www.tealium.com/products/widgets/buynow\](https://www.tealium.com/products/widgets/buynow%5C)&lt;/linkURL&gt;`                        |
| 注文IDを含むCustomer Data Hub属性                                                                        | purchaseID                | &lt;ul&gt;&lt;li&gt;文字列値。&lt;/li&gt;&lt;li&gt;電子商取引の注文ID&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                         | `&lt;purchaseID&gt;ORD12345&lt;/purchaseID&gt;`                                                                                                                |
| ドキュメントリファラーを含むCustomer Data Hub属性                                                        | referrer                  | &lt;ul&gt;&lt;li&gt;&#34;Referring URL&#34;属性を使用することをお勧めします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                             | `&lt;referrer&gt;[https://www.tealium.com/shop\](https://www.tealium.com/shop%5C)&lt;/referrer&gt;`                                                            |
| イベント発生時のタイムスタンプを含むCustomer Data Hub属性                                                | timestamp                 | &lt;ul&gt;&lt;li&gt;(オプション) Unixエポック秒またはISO 8601形式。&lt;/li&gt;&lt;li&gt;レポートスイートがタイムスタンプ付きヒットを明示的に受け入れるように構成されていない場合はマッピングしないでください。&lt;/li&gt;&lt;li&gt;詳細については、[タイムスタンプ実装ガイド](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/timestamp.html?lang=en &#34;タイムスタンプ実装ガイド&#34;)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;timestamp&gt;1519207951063&lt;/timestamp&gt;`                                                                                                             |
| 顧客データハブ属性に含まれる訪問のIPアドレス | ipaddress | &lt;ul&gt;&lt;li&gt;このオプショナル属性を使用するには、アカウントで訪問IP属性を有効にする必要があります。&lt;/li&gt;&lt;li&gt;この機能が必要な場合は、アカウントマネージャーに連絡してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;ipaddress&gt;127.0.0.1&lt;/ipaddress&gt;` |
| 顧客データハブ属性に含まれるブラウザ/デバイスのユーザーエージェント | userAgent | &lt;ul&gt;&lt;li&gt;顧客データハブの組み込みユーザーエージェント属性の使用を推奨します&lt;/li&gt;&lt;/ul&gt; | `&lt;userAgent&gt;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.167 Safari/537.36&lt;/userAgent&gt;` |
| 顧客データハブ属性に含まれるカスタムイベントのトランザクションID（注文IDではない） | transactionID | &lt;ul&gt;&lt;li&gt;これはpurchaseIDとは異なります。&lt;/li&gt;&lt;li&gt;詳細については、[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/transactionid.html?lang=en)のドキュメントを参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;transactionID&gt;CMPSUMMER18&lt;/transactionID&gt;` |

#### ユーザーエージェントクライアントヒント

Google ChromeやMicrosoft EdgeなどのChromiumブラウザからのクライアントヒントは、デバイス固有の情報を提供します。このデータセットは、デバイス情報の主要な情報源としてユーザーエージェント文字列を置き換えます。

これらのマッピング選択は**イベントパラメーター**セクションに表示されます。

|マップ元|マップ先|備考|サンプルコネクタ出力|
|----|----|----|----|
| 顧客データハブ属性に含まれるシステムアーキテクチャヒント。 | `architecture` | &lt;ul&gt;&lt;li&gt;文字列値。&lt;/li&gt;&lt;li&gt;詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;architecture&gt;x64&lt;/architecture&gt;` |
| 顧客データハブ属性に含まれるアプリケーションが使用するビット数。 | `bitness` | &lt;ul&gt;&lt;li&gt;文字列値。&lt;/li&gt;&lt;li&gt;詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;bitness&gt;64&lt;/bitness&gt;` |
| 顧客データハブ属性に含まれるブランドヒント。 | `brands` | &lt;ul&gt;&lt;li&gt;オブジェクトの配列として送信します。&lt;/li&gt;&lt;li&gt;詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;brands&gt;&lt;brand&gt;&lt;name&gt;Chromium&lt;/name&gt;&lt;version&gt;100&lt;/version&gt;&lt;/brand&gt;&lt;/brands&gt;` |
| 顧客データハブ属性がモバイル接続を通じてカスタムイベントが発生したかどうかを示します。 | `mobile` | &lt;ul&gt;&lt;li&gt;ブール値。&lt;/li&gt;&lt;li&gt;詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;mobile&gt;true&lt;/mobile&gt;` |
| 顧客データハブ属性に含まれるプラットフォームヒント。 | platform | &lt;ul&gt;&lt;li&gt;文字列値。&lt;/li&gt;&lt;/ul&gt; | `&lt;platform&gt;win&lt;/platform&gt;` |
| 顧客データハブ属性に含まれるプラットフォームバージョンヒント。 | `platformVersion` | &lt;ul&gt;&lt;li&gt;文字列値。&lt;/li&gt;&lt;li&gt;詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;platformVersion&gt;10&lt;/platformVersion&gt;` |
| 顧客データハブ属性に含まれる、Windowsが32ビットサブシステムを実行していることを示す指標。詳細については、[WoW64 at Wikipedia](https://en.wikipedia.org/wiki/WoW64)を参照してください。 | `wow64` | &lt;ul&gt;&lt;li&gt;ブール値。&lt;/li&gt;&lt;li&gt;詳細については、Adobeの[ユーザーエージェントクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; | `&lt;wow64&gt;true&lt;/wow64&gt;` |

### リンクタイプ

このフィールドはリンク追跡に使用され、[Link Type](https://experienceleague.adobe.com/docs/analytics/components/dimensions/custom-link.html?lang=en)の構成を可能にします。

| マップ元 | マップ先 | 説明 | 例 | サンプルコネクタ出力 |
|:----|:----|:----|:----|:----|
| ドロップダウンリストから任意の属性を選択するか、カスタム値を入力 | リンクタイプ: &#34;d&#34; - ダウンロードリンク &#34;e&#34; - エグジットリンク &#34;o&#34; - カスタム（その他）リンク | 選択した属性に値がある場合のみ、Adobe Analyticsにリンクタイプを送信します\* | マップ: (カスタム値): &#34;true&#34; to &#34;o&#34; | `&lt;linkType&gt;o&lt;/linkType&gt;` |

選択した属性の値が `null`、`undefined`、または `&#34;&#34;`（空文字列）の場合、リンクタイプは送信されません。

### コンテキストデータ

[Context Data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en)は、propsやeVarsの代わりによりユーザーフレンドリーな代替手段として使用できます。任意のイベント属性または訪問属性をAdobe Analyticsのコンテキストデータ変数にマッピングできます。コンテキストデータ変数には任意の名前を付けることができますが、Adobeのベストプラクティスでは、すべての変数に会社名などの一意のキーを接頭辞として付けることが推奨されています。一部の変数は予め定められた機能のためにのみ使用され、これらの変数は `a.` で接頭辞が付けられます。

| マップ元 | マップ先 | 説明 | 例 | サンプルコネクタ出力 |
|:----|:----|:----|:----|:----|
| ドロップダウンから任意の属性を選択するか、カスタム値を入力 | companyname.someproperty | 定義された顧客データハブ属性をコンテキストデータ属性にマッピング | マップ: (顧客データハブ属性) キャンペーン名を &#34;tealium.productColor&#34; に | `&lt;contextData&gt;&amp;lt;tealium.productColor&amp;gt;Red&amp;lt;/tealium.productColor&amp;gt;`&lt;/contextData&gt; |
### アナリティクス eVars

このフィールドは、Customer Data Hubの属性を[eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en)にマッピングするために使用されます。eVarsは、「eVar」という単語とeVarの番号を使用して指定する必要があります。例えば、「eVar11」です。有効な範囲は1から250です。

| マップ元                                                  | マップ先                                            | 説明                                                                             | 例                                                            | サンプルコネクタ出力                 |
|:----------------------------------------------------------|:--------------------------------------------------|:--------------------------------------------------------------------------------|:-------------------------------------------------------------|:----------------------------------------|
| ドロップダウンから任意の属性を選択、またはカスタム値を入力 | eVarX（Xは1〜250の整数）                           | Customer Data Hubの定義済み属性をアナリティクスレポートのeVarにマッピングします | マップ：(Customer Data Hub属性) キャンペーン名を「eVar75」に | `&lt;eVar75&gt;Summer2018`&lt;/eVar75&gt; |

### アナリティクスプロパティ名 (s.props)

このフィールドは、Customer Data Hubの属性を[props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en)にマッピングするために使用されます。Propsは、`prop`という単語とpropの番号を使用して指定する必要があります。例えば、「prop4」です。有効な範囲は1から75です。[リストprops](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props)もサポートされていますが、これにはAdobe Analytics Report Suite管理インターフェースで事前に構成が必要です。

| マップ元                                                  | マップ先                                           | 説明                                                                             | 例                                                        | サンプルコネクタ出力            |
|:----------------------------------------------------------|:-------------------------------------------------|:--------------------------------------------------------------------------------|:--------------------------------------------------------|:-----------------------------------|
| ドロップダウンから任意の属性を選択、またはカスタム値を入力 | propX（Xは1〜75の整数）                           | Customer Data Hubの定義済み属性をアナリティクスレポートのpropにマッピングします | マップ：(Customer Data Hub属性) リンク名を「prop4」に   | `&lt;prop4&gt;Buy Now`&lt;/prop4&gt; |

### イベント (s.events)

[イベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)は、ウェブサイトやアプリで特定のイベントがどれだけ頻繁に発生しているかを測定するために使用されます。イベント変数は、特定のアナリティクスイベントに対してカウントされるべきすべてのイベントをリストするコンマ区切りの文字列です。[事前定義されたイベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)と[カスタムイベント](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en)は同じ文字列で送信されます。

Adobe Analyticsコネクタでは、イベントを指定するために次の2つの方法が使用されます：

* 他の場所（例えば、Tag Managementの拡張機能、エンリッチメント、またはデータレイヤー内で直接）で入力されたイベント名のリストを含む配列値をマッピングします。

| マップ元                                                  | データタイプ | 例の入力                        | サンプルコネクタ出力                           |
|:----------------------------------------------------------|:----------|:-------------------------------|:--------------------------------------------------|
| イベントのリストを表すCustomer Data Hub属性               | 配列       | [&#34;event1&#34;, &#34;event5&#34;, &#34;event9&#34;] | `&lt;events&gt;event1,event5,event9&lt;/events&gt;` |

* 特定のイベント番号にマッピングされる文字列値の配列を指定し、「カスタムイベントマッピング」セクションでイベント番号のマッピングを指定します：

| マップ元                                                             | マップ先                                        | 例のイベント配列                                | 例の入力                        | サンプルコネクタ出力                                                                                      |
|:---------------------------------------------------------------------|:----------------------------------------------|:-------------------------------------------------|:---------------------------|:-------------------------------------------------------------------------------------------------------------|
| イベント配列で検索する文字列を含むカスタムテキスト値                 | トリガーするイベント名、例えば、event8          | [&#34;newsletter\_registration&#34;, &#34;homepage\_viewed&#34;] | &#34;newsletter\_registration&#34; | `&lt;events&gt;event8&lt;/events&gt;`（文字列&#34;newsletter\_registration&#34;がイベント配列にあったため） |

### イベント値マッピング

このフィールドでは、イベントに数値を割り当てることができます。このフィールドは「カスタムイベントマッピング」フィールドとは関連していません。つまり、「event2」が「カスタムイベントマッピング」で指定されていても、「値」イベントとして指定されている場合、イベント変数には値なしで1回、値ありで1回、合計2回含まれます。

| マップ元                                 | データタイプ | マップ先                                     | 例の入力       | サンプルコネクタ出力               |
|:-----------------------------------------|:----------|:-------------------------------------------|:--------------------|:--------------------------------------|
| 数値を表す属性                           | 数値       | eventX（Xはイベントの番号）                 | 「9」を「event5」にマップ | `&lt;events&gt;event5=9&lt;/events&gt;` |

### イベントシリアライゼーション

イベントIDを含む属性をマッピングして、イベントを指定する番号を構成することでイベントシリアライゼーションを構成します。例えば、「ABC123」を「2」にマッピングすると、「event2=ABC123」と送信されます。

| マップ元                           | データタイプ | マップ先           | 例の入力                                | サンプルコネクタ出力                                  |
|:-----------------------------------|:----------|:-----------------|:---------------------------------------------|:---------------------------------------------------------|
| イベントIDを表す属性               | 文字列     | イベント番号       | 「ABC123」を「1」にマップ、&lt;br&gt;「ABC123」を「2」にマップ | `&lt;events&gt;event1=ABC123,event2:ABC123&lt;/events&gt;` |
### ライフサイクルイベント

Adobe Analyticsは、アプリケーションのライフサイクルイベントを追跡する機能を持っています。Tealiumのモバイルライブラリには、この機能をサポートするためのオプショナルモジュールが用意されており、Adobe Analyticsに必要なデータを自動的に生成します。

| Tealium属性 | Adobe変数 | 説明 | データタイプ | 例 |
| --- | --- | --- | --- | --- |
| lifecycle\_diddetect\_crash | a.CrashEvent | この起動/ウェイクイベント中にクラッシュが検出されたか。真の場合のみ記入。 | Boolean | true |
| lifecycle\_dayofweek\_local | a.DayOfWeek | 呼び出しが行われた地元の曜日（1=日曜日、2=月曜日など） | Number | 13 |
| lifecycle\_dayssincelaunch | a.DaysSinceFirstUse | 初回起動からの日数（整数で増加） | Number | 23 |
| lifecycle\_dayssinceupdate | a.DaysSinceLastUpgrade | 最後に検出されたアプリバージョン更新からの日数（整数で増加） | Number | 46 |
| lifecycle\_dayssincelastwake | a.DaysSinceLastUse | 最後に検出されたウェイクからの日数（整数で増加） | Number | 1 |
| lifecycle\_firstlaunchdate\_MMDDYYYY | a.InstallDate | GMTタイムスタンプがMM/DD/YYYY形式でフォーマットされる | String | 01/18/2012 |
| lifecycle\_hourofday\_local | a.HourOfDay | 呼び出しが行われた地元の時間（24時間表記） | String | true |
| lifecycle\_isfirstlaunch | a.InstallEvent | 呼び出しが最初の起動/ウェイクの場合のみ存在 | String | true |
| lifecycle\_isfirstlaunchupdate | a.UpgradeEvent | 呼び出しが検出された更新後の最初の起動/ウェイクの場合のみ存在 | Boolean | true |
| lifecycle\_isfirstwakemonth | a.MonthlyEngUserEvent | 呼び出しが月の最初の起動/ウェイクの場合のみ存在 | Boolean | true |
| lifecycle\_priorsecondsawake | a.PrevSessionLength | 最後の起動以来アプリが起動していた全秒数。以前のすべてのウェイクからの合計。ライフサイクルタイプ：起動呼び出しのみで送信。 | Number | 126 |
| lifecycle\_totalwakecount | a.Launches | インストール以来の起動&#43;ウェイクの総数（アプリが削除されない限りリセットされない） | Number | &#34;563&#34; |
| lifecycle\_type | a.LaunchEvent if lifecycle\_type == &#34;launch&#34; | ライフサイクル呼び出しのタイプ | String | &#34;launch&#34;, &#34;wake&#34;, &#34;sleep&#34; |
| device (obj-c/android) or model\_name (swift) | a.DeviceName | デバイスモデル | String | iPhone 7 Plus |
| carrier (obj-c/android) or network\_name (swift) | a.CarrierName | ネットワークキャリア名 | String | Verizon |
| device\_resolution | a.Resolution | 画面解像度 | String | 1080x1920 |
| resolution | 画面解像度 | String | 1080x1920 |
| app\_id | a.AppID | アプリID | String | Digital Velocity 1.0 |
| device\_os\_version (obj-c/android) or os\_version (swift) | a.OSVersion | オペレーティングシステムバージョン | String | 11.1 |

詳細については、[Adobe: Lifecycle Metrics](https://marketing.adobe.com/resources/help/en_US/mobile/android/metrics.html)を参照してください。

### 製品

[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)変数は、特定のページ上の1つ以上の製品に関するeコマース情報をキャプチャするために使用されます（カテゴリ、製品ID、価格、数量）。

製品変数を埋めるためには、配列データタイプを持つCustomer Data Hub属性のみが使用可能です。すべての配列は長さが等しくなければなりません。たとえば、ページ上に5つの製品がある場合、製品ID、数量、価格、カテゴリはすべて5要素の長さでなければなりません。

| マップ元 | データタイプ | マップ先 | 入力データ例 | コネクタ出力例 |
|:----------------------------------------------------------|:----------|:------------------|:---------------------|:-----------------------------------------------------|
| 製品カテゴリを表すCustomer Data Hub属性 | 配列 | 製品カテゴリ | [&#34;靴&#34;, &#34;シャツ&#34;] | `&lt;products&gt;靴;;;,シャツ;;;`&lt;/products&gt; |
| 製品IDを表すCustomer Data Hub属性 | 配列 | 製品ID | [&#34;ABC123&#34;, &#34;EFG234&#34;] | `&lt;products&gt;;ABC123;;,;EFG234;;`&lt;/products&gt; |
| 数量を表すCustomer Data Hub属性 | 配列 | 製品数量 | [&#34;1&#34;, &#34;2&#34;] | `&lt;products&gt;;;1;,;;2;;`&lt;/products&gt; |
| 価格を表すCustomer Data Hub属性 | 配列 | 製品価格 | [&#34;149.99&#34;, &#34;79.80&#34;] | `&lt;products&gt;;;;149.99,;;;79.80`&lt;/products&gt; |

### 製品イベント値マッピング

このフィールドでは、[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)変数の各製品にカスタム変換イベントを割り当て、各イベントに数値を割り当てることができます。

「シンプル」変数（単一値またはカスタムテキスト値）がマッピングされる場合、同じ値がリスト内のすべての製品に適用されます。リスト（配列）値がマッピングされる場合、配列は他の製品配列と同じ長さでなければならず、配列内の各アイテムには異なる値が割り当てられます（配列内の位置に応じて）。

これらの例では、次の製品配列がイベント属性として存在すると仮定します：

```
製品カテゴリ: [&#34;フットウェア&#34;, &#34;アパレル&#34;] 製品ID: [&#34;ランニングシューズ&#34;, &#34;Tシャツ&#34;] 数量: [&#34;1&#34;, &#34;1&#34;] 価格: [&#34;99.99&#34;, &#34;49.99&#34;]
```

| マップ元 | データタイプ | マップ先 | 入力値例 | コネクタ出力例 |
|:-----------------------------------------------------------------|:----------|:-----------------------------------------------|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 数値を含むカスタムテキスト値 | 文字列 | トリガーするイベント名、例：event8 | &#34;9.99&#34; (カスタム値) | `&lt;events&gt;event8&lt;/events&gt;``&lt;products&gt;フットウェア;ランニングシューズ;1;99.99;**event8=9.99**,アパレル;Tシャツ;1;49.99;**event8=9.99**`&lt;/products&gt; |
| 数値データの配列を表すCustomer Data Hub属性 | 配列 | トリガーするイベント名、例：event12 | [&#34;1.99&#34;, &#34;4.99&#34;] | `&lt;events&gt;event8&lt;/events&gt;``&lt;products&gt;フットウェア;ランニングシューズ;1;99.99;**event12=1.99**,アパレル;Tシャツ;1;49.99;**event12=4.99**`&lt;/products&gt; |

### 製品マーチャンダイジングeVars

このフィールドでは、[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)変数の各製品にeVarsを割り当てることができます。

これは上記の「製品イベント値マッピング」フィールドと同じ方法で機能します。

| マップ元 | データタイプ | マップ先 | 入力値例 | コネクタ出力例 |
|:-------------------------------------------------------------------------------------------|:----------|:--------------------------------------------|:--------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| eVar値を含むカスタムテキスト値 | 文字列 | トリガーするeVarの名前、例：eVar4 | &#34;my\_custom\_value&#34; | `&lt;products&gt;フットウェア;ランニングシューズ;1;99.99;event8=9.99;**eVar4=my\_custom\_value**,アパレル;Tシャツ;1;49.99;event8=9.99;**eVar4=my\_custom\_value**`&lt;/products&gt; |
| eVar値の配列を表すCustomer Data Hub属性（例：製品カラー） | 配列 | トリガーするeVarの名前、例：eVar6 | [&#34;赤&#34;, &#34;緑&#34;] | `&lt;products&gt;フットウェア;ランニングシューズ;1;99.99;event8=9.99;**eVar6=赤**,アパレル;Tシャツ;1;49.99;event8=9.99;**eVar6=緑**`&lt;/products&gt; |
### 階層データ

ページ[階層](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en)は、サイト/アプリのナビゲーション構造内でページを分類するのに役立ちます。利用可能なスロットは5つ（hier1 - hier5）です。階層変数として使用できる唯一のサポートされているCustomer Data Hub属性タイプは配列です。

| マップ元                                                  | データタイプ | マップ先                              | 説明                                                                                                  | 例                                                               | サンプルコネクタ出力            |
|:----------------------------------------------------------|:------------|:--------------------------------------|:-----------------------------------------------------------------------------------------------------|:----------------------------------------------------------------|:-------------------------------|
| ドロップダウンから任意の属性を選択、またはカスタム値を入力 | 配列        | hier1 - hier5 (ドロップダウン選択)    | Customer Data Hubの配列形式の属性をAdobe Analyticsの指定された階層変数にマッピングします             | マップ：(Customer Data Hub属性) ページ分類を「hier1」にマッピング | `&lt;hier1&gt;Article&lt;/hier1&gt;` |

### リストデータ

[リスト変数](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en)は、複数の値を含む区切り文字列で、しばしば帰属目的で使用されます。各レポートスイートには最大3つのリスト変数が利用可能です。リスト変数として使用できる唯一のサポートされているCustomer Data Hub属性タイプは配列です。

| マップ元                                 | データタイプ | マップ先                                   | 説明                                                                                               | 例                                                         | サンプルコネクタ出力               |
|:-----------------------------------------|:------------|:-------------------------------------------|:--------------------------------------------------------------------------------------------------|:------------------------------------------------------------|:----------------------------------|
| ドロップダウンから任意の配列属性を選択   | 配列        | list1, list2, list3 (ドロップダウン選択)   | Customer Data Hubの配列形式の属性をAdobe Analyticsの指定されたリスト変数にマッピングします         | マップ：(Customer Data Hub属性) リファラーリストを「list1」にマッピング | `&lt;list1&gt;google.com&lt;/list1&gt;` |

## 訪問およびExperience Cloud ID

[訪問ID](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en)に関するAdobe Analyticsのドキュメントと、複数のIDが提供された場合の優先順位を参照してください。

### ユースケース1: Adobe Analyticsの実装が初めての場合

これが完全にサーバーサイドの新しいAdobe Analytics実装である場合、独自の一意の訪問IDを使用し、コネクタのvisitorID属性に渡すことができます。訪問IDに適したものを決定する必要があります。Adobeによって構成された[制約](https://marketing.adobe.com/resources/help/en_US/sc/implement/visitorID.html)の範囲内で。

### ユースケース2: 既存のAdobe AnalyticsクライアントサイドJavaScriptからの移行

JavaScriptベースのAdobe Analyticsタグからサーバーサイドコネクタへ移行する場合、完全に移行する際に「訪問を失う」ことを避けるために一貫した訪問IDを維持する必要があります。また、Adobe Analytics Customer Data Hubコネクタを二次的な収集メカニズムとして実装する場合（ウェブページやアプリで引き続きJavaScriptタグを主要な収集メカニズムとして使用している場合）、訪問IDを移行する必要があります。

このユースケースで説明されているように、既存のAdobe AnalyticsクライアントサイドJavaScriptから移行するための次の手順に従ってください：

1. [これらの指示]()に従ってAdobe Experience Cloud IDタグを構成し、Tag Managementでタグを構成します。
1. このステップでは、Adobe訪問IDをファーストパーティクッキーに保存します。このクッキーは、セッションの期間中、値を再リクエストする必要なく、Customer Data Hubに値が送信されることを保証します。
    * Tag Managementでデータレイヤータブに移動し、`utag_main_adobe_mcid` と `utag_main_aa_vid` という2つの新しいファーストパーティクッキー変数を作成します。
        これらの変数の名前を変更することはできますが、`utag_main_` 接頭辞を保持してください。これにより、`utag_main`クッキーにスタックしてクッキースペースを節約できます。変数の名前を変更する場合は、以下のJavaScriptスニペットも更新する必要があります。
    * Adobe Experience Cloud ID Serviceタグにスコープされた新しいJavaScriptコード拡張を作成し、次のコードを貼り付けます：
        ```
        `if (typeof vAPI !== &#34;undefined&#34;) {
        vAPI.getInstance(u.data.adobe_org_id,
	      function (visitor) {
	      var mcID = visitor.getMarketingCloudVisitorID(),
	      analyticsID = visitor.getAnalyticsVisitorID(),
	      sessionExpiry = &#34;;exp-session&#34;;
	      // store Adobe IDs for the session duration
	      if (!mcID) {
	        // something went wrong - the visitor IDs could not be retrieved
	        utag.DB(&#34;MCID could not be returned&#34;);
	      } else {
	        utag.loader.SC(&#34;utag_main&#34;,{&#34;adobe_mcid&#34; : mcID &#43; sessionExpiry, &#34;aa_vid&#34; : analyticsID &#43; sessionExpiry});
	        // optionally, trigger an empty utag.link call to trigger sending the cookie values to UDH
	        // if utag.track call is omitted (default), values will be sent on the next utag.link or utag.view call anyway
	        // utag.track is used to avoid calling other third-party tags; only the collect tag should respond
	        // utag.track(&#34;adobe_vid_updated&#34;, {});
	      }
        },
        u.clearEmptyKeys(u.data.config), u.data.customer_ids);
        }   
        ```
        この拡張機能は、Adobeのサーバーから訪問IDが正常に取得されたときに呼び出されるAdobe訪問IDサービスへのコールバックを作成し、訪問IDとExperience Cloud IDをTealiumの独自のファーストパーティクッキー(`utag_main`)に保存します。クッキーはセッションの終了時に期限切れになりますが、将来訪問IDが更新される場合に備えています。クッキーを永続的にする（期限切れにしない）場合は、上記のコードで`sessionExpiry`を`&#34;&#34;`に構成します。
    * JavaScript拡張に条件 &#34;utag\_main\_adobe\_mcid `is not defined` AND utag\_main\_aa\_vid `is not defined`&#34; を追加します。これにより、このセッション中にコードが再度実行されるのを防ぎます。
1. Customer Data HubのAudienceStreamとEventStreamを構成します。
    * AudienceStream構成 - AudienceStreamをお持ちの場合、Adobe訪問IDとExperience Cloud IDを訪問レベルの文字列属性として保存できます。訪問ID属性としては保存しないでください。オーディエンスイベントによってトリガーされるアクションの場合、新しい属性をコネクタ構成の`visitorID`および`marketingCloudVisitorID`にマッピングできます。
    * EventStream構成 - EventStreamのみをお持ちの場合、訪問ID変数を保存する機能がないため、値をクッキーに保存しました。前のステップのTag Management構成をProdに公開している場合は、新しい`utag_main_adobe_mcid`および`utag_main_aa_vid`の値がすでに[イベント属性]()に表示されています。
    * Prodに公開していない場合は、手動でイベント属性を追加できます。**ファーストパーティクッキー**文字列属性タイプを使用してこれらの属性を定義します。これらの属性を定義したら、Adobe Analyticsコネクタでそれらを選択し、それぞれ`marketingCloudVisitorID`および`visitorID`にマッピングできます。
## 一般的な問題のデバッグ

* コネクタのテストには、[trace]()の使用をお勧めします。トレースを実行する際には、「HTTP Request Body」フィールドを確認し、Adobeに送信された整形済みのXMLを表示します。上記の表の「Sample Connector Output」フィールドとXML出力を比較して、出力を検証してください。
* Adobeから返されるレスポンスコードにエラーがないかを確認してください。HTTPレスポンスステータス：200/成功以外は、リクエストにエラーがあったことを示します。
* Data Insertion APIの完全なURL構造は、`http://namespace.112.2o7.net/b/ss//6`の形式に従います。ここで、二重スラッシュは意図的で有効です（JavaScriptのAdobe Analytics実装では、ここにレポートスイートIDが存在します）。`/6`はXMLペイロードが送信されていることを示し、reportSuiteの値はXMLペイロードの一部として送信されます。これは、[trace]()セッションを実行するときに表示される値です。
    コネクタ構成に完全なURL値を入力する必要はありません。TealiumはData Insertion Domainの値に基づいてURLを自動生成します。完全なURLはトレースセッションを実行するときにのみ表示されます。
* 特定の実装によっては、Data Insertion Domainの値が異なる場合があります（例：`sc.omtrdc.net`）、しかし、名前空間は常にドメインの前に来るべきです（例：`namespace.sc.omtrdc.net`）、独自のファーストパーティトラッキングドメインを持っている場合を除きます（例：`smetrics.acme.com`）。
* Adobe Analyticsにデータが受信されていない場合は、レポートスイートの[**Timestamps Optional**](https://experienceleague.adobe.com/docs/analytics/technotes/timestamps-optional.html?lang=en)セクションを確認してください。タイムスタンプがオプションでない場合は、有効なタイムスタンプをマッピングすることが重要です。
* User AgentまたはClient Hintsにマッピングすることを強くお勧めします。この値をマッピングしない場合、AdobeはサーバーのUser Agent（例：`Apache-HttpClient/4.5.5(Java/11.0.17`）を取得し、それがボットトラフィックとして識別される可能性があります。
