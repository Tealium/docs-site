---
title: Adobe Analytics 2.0 コネクタ構成ガイド
description: この記事では、Adobe Analytics 2.0 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-analytics-2-connector/
---
## 動作原理

Adobe Analytics 2.0 コネクタは、ウェブページやモバイルアプリ上のJavaScriptビーコンを使用する代わりに、[Adobe Bulk Data Insertion API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/endpoints/bulk-data-insertion/)を利用してアナリティクスデータを送信します。これにより、クライアント側から送信されるデータ量が削減され、オーディエンスや訪問データをAdobe Analyticsに渡すことが可能になるという利点があります。

## Adobe Analytics 2.0 コネクタの違い

Adobe Bulk Data Insertion APIは、リアルタイムまたはほぼリアルタイムのコネクタアクションをサポートしないレート制限があります。このため、**Send Analytics Event** アクションはAdobe Analytics 2.0 コネクタで非推奨となりました。リアルタイムのコネクタアクションが必要ない場合は、**Send Analytics Event (Batch)** アクションに移行してください。リアルタイムのコネクタアクションが必要な場合は、[Adobe Analytics 1.4 コネクタ](https://docs.tealium.com/adobe-analytics-connector/)を使用してください。

以下のAdobe Analytics 1.4 コネクタの機能は、Adobe Analytics 2.0 コネクタでは利用できません：

* カスタムフィールドマッピング（高度）
* モバイルデータソースのライフサイクルイベント属性の自動マッピングを有効にする

以下の表に示すように、Adobe Analytics 1.4 の一部のパラメーターはAdobe Analytics 2.0 コネクタでは利用できません。**Adobe Analytics 2.0 パラメーター**列に✗がある場合、そのパラメーターは2.0コネクタでは利用できません。

| Adobe Analytics 1.4 パラメーター | Adobe Analytics 2.0 パラメーター |
| ----- | ----- |
| a4t | tnta |
| architecture | hints.architecture |
| bitness | hints.bitness |
| browserHeight | browserHeight |
| browserWidth | browserWidth |
| campaign | campaign |
| channel | channel |
| connectionType | connectionType |
| cookiesEnabled | cookiesEnabled |
| currencyCode | currencyCode |
| customerPerspective | ✗ |
| fallbackVisitorID | ✗ |
| homePage | ✗ |
| imsregion | ✗ |
| ipaddress | ipaddress |
| javaEnabled | javaEnabled |
| javaScriptVersion | ✗ |
| language | language |
| linkName | linkName |
| linkType | linkType |
| linkURL | linkURL |
| marketingCloudOrgID | ✗ |
| marketingCloudVisitorID | marketingCloudVisitorID |
| mobile | hints.mobile |
| pageName | pageName |
| pageType | pageType |
| pageURL | pageURL |
| platform | hints.platform |
| platformVersion | hints.platformversion |
| plugins | ✗ |
| purchaseID | purchaseID |
| referrer | referrer |
| reportSuiteID | reportSuiteID |
| resolution | resolution |
| server | server |
| state | ✗ |
| timestamp | timestamp |
| timezone | ✗ |
| transactionID | transactionID |
| userAgent | userAgent |
| visitorID | visitorID |
| wow64 | hints.wow64 |
| zip | zip |

Adobe Analytics 1.4 コネクタからAdobe Analytics 2.0 コネクタへの移行に関する情報は、[Migrator Tool]()を参照してください。

## 構成

Adobe Analytics 2.0 コネクタを構成するには、Adobe Analytics 2.0 APIのクライアントID（APIキー）とクライアントシークレットが必要です。Adobe Developer Consoleでクレデンシャルを作成し、Adobe Analytics 2.0 APIのクライアントIDとクライアントシークレットを取得するには、次の手順に従ってください：

1. Adobe Developer Consoleにアクセスし、Adobe IDでログインします。
1. **新しいプロジェクトを作成**をクリックします。
1. プロジェクトに名前を入力し、**保存**をクリックします。
1. プロジェクトダッシュボードで、**APIを追加**をクリックします。
1. 利用可能なAPIのリストから**Adobe Analytics**を選択します。
1. **認証タイプ**で、**サーバー間認証**を選択します。
1. 統合のタイプとして、**OAuthサーバー間**を選択します。
1. アクセスを提供したい**製品プロファイル**を選択します。
1. クライアントIDとクライアントシークレットを取得するには、プロジェクトの**認証情報**セクションに移動します。
1. クライアントIDとクライアントシークレットを表示してコピーするには、**クライアントシークレットを取得**をクリックします。

クライアントIDとクライアントシークレットを取得した後、インターフェースでAdobe Analyticsコネクタを構成するには、次の手順に従います：

1. **コネクタマーケットプレース**にアクセスし、Adobe Analyticsコネクタを追加します。
一般的なコネクタの追加方法については、[Connector Overview](https://docs.tealium.com/about-connectors/)を参照してください。
1. **オーディエンス**と**トリガー**を選択し、**続行**をクリックします。
1. **コネクタを追加**をクリックします。
1. コネクタの**名前**を入力します。
1. **クライアントID**と**クライアントシークレット**を入力します。
1. （オプション）**接続テスト**をクリックします。
1. **完了**をクリックし、**続行**をクリックします。

次のステップは、[configuring an action]()です。

## アクション

| アクション名      | AudienceStream | EventStream |
|:---------------------|:-------------------|:----------------|
| Send Analytics Event (Batch) | ✓          | ✓               |
| Send Analytics Event (Deprecated) | ✓                  | ✓               |

### Send Analytics Event (Batch)

#### バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：250,000
* 最古のリクエストからの最大時間：30分（1-60分から構成可能）
* リクエストの最大サイズ：300 MB


#### パラメータ

イベントパラメータについては、[一般属性](#general-attributes)を参照してください。

| **グループ**  | **説明** |
|-------------|-----------------|
| コンテキストデータ | <ul><li>ドット形式を使用してキーを指定します。</li><li>例：`my.a`。</li><li>複数のキーバリューペアを指定できます。</li></ul> |
| eVars | <ul><li>属性を番号にマッピングしてイベントeVarsを指定します。</li><li>例：`event_count` を `1` にマッピングして **eVar1**。</li><li>有効範囲は `1` から `100`、プレミアムアカウントの場合は `250` です。</li></ul> |
| 階層 | <ul><li>階層文字列。</li><li>`1` から `5` を選択します。</li></ul> |
| リスト | <ul><li>変数に渡され、報告のために個々の項目として報告される値のリスト。</li><li>`1` から `3` を選択します。</li><li>データレイヤーで配列タイプが必要です。</li><li>Tealiumがデータを正しくフォーマットして渡します。</li></ul> |
| プロパティ | <ul><li>分析プロパティ名。</li><li>属性を番号にマッピングして名前を指定します。</li><li>例：`lifetime_value` を `1` にマッピングして **prop1**。</li></ul> |
| イベント | <ul><li>イベントのリスト、またはカスタム値をコンマ区切りで指定します。</li><li>詳細については、[Adobe Analytics Configure Events Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を参照してください。</li></ul> |
| イベントマッピング | <ul><li>イベント配列に含まれる潜在的な値をAdobe Analyticsカスタムイベント名にマッピングします。</li><li>例：購入を3にマッピングすると、購入はevent3に置き換えられ、元のイベント例の最終出力はevent1,event2,event3,purchaseからevent1,event2,event3,event4に変わります。</li></ul> |
| イベント値 | <ul><li>`Counter`、`Numeric`、`Currency` イベントの値を指定します。</li><li>イベントを指定するには、番号を使用します。</li><li>例えば、9.99を2にマッピングすると、次の出力が得られます：`event1,event2=9.99,event3,event4`。</li></ul> |
| イベントシリアライゼーション | <ul><li>イベントをシリアライズするために使用するイベントIDを指定します。</li><li>詳細については、[Event Serialization](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/events/event-serialization#vars)を参照してください。</li><li>例えば、page_viewを3にマッピングすると、次の出力が得られます：`event1,event2,event3:page_view,event4`。</li></ul> |
| 製品 | <ul><li>製品属性（`Id`、`Category`、`Quantity`、`Price`）を指定します。</li><li>すべての配列は同じサイズで、順序が揃っている必要があります。</li><li>詳細については、[Adobe Analytics Product Implementation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)を参照してください。</li></ul> |
| 製品eVars | <ul><li>製品eVarsの値を指定します。</li><li>すべての配列は**製品**セクションと同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>eVarマッピングを番号で指定します。</li><li>例として、`1` は `eVar1` にマッピングされます。</li></ul> |
| 製品イベント | <ul><li>製品イベントの値を指定します。</li><li>すべての配列は**製品**セクションと同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>イベントマッピングを番号で指定します。</li><li>例として、`1` は `event1` にマッピングされます。</li></ul> |
| ブランド | <ul><li>ブランド属性を指定します。</li><li>利用可能な属性は **brand** と **version** です。</li><li>すべての配列は同じサイズである必要があります。</li></ul> |
| バッチの有効期限 | バッチアクションが送信される頻度を指定するために、有効期限（TTL）を構成します。`1` から `60` 分の間の値を入力します。デフォルト値は `30` 分です。

### Send Analytics Event (非推奨)


<blockquote>
このアクションは非推奨であり、新たに追加することはできません。代わりに [Send Analytics Event (Batch)](#send-analytics-event-batch) を使用してください。
</blockquote>


#### バッチ制限

このアクションはバッチアクションとしてラベル付けされていませんが、リアルタイムでリクエストを送信するわけではありません。次のいずれかの閾値が達成されるか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：250,000
* 最古のリクエストからの最大時間：45秒
* リクエストの最大サイズ：100 MB

## 一般属性

すべての属性の完全なリファレンスについては、各フィールドが何を含むべきかの詳細を含む [Adobe: API documentation](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md) およびこの記事の [Visitor & Experience Cloud IDs](#visitor-and-experience-cloud-ids) セクションを参照してください。

### ユーザーエージェントクライアントヒント

Google ChromeやMicrosoft EdgeなどのChromiumブラウザからのClient Hintsは、デバイス固有の情報を提供します。このデータセットは、デバイス情報の主要な情報源としてユーザーエージェント文字列を置き換えます。

これらのマッピング選択は、**イベントパラメータ**セクションに表示されます。

|マップ元|マップ先|備考|サンプルコネクタ出力|
|----|----|----|----|
| システムアーキテクチャヒントを含むサーバーサイド属性。 | `hints.architecture` | <ul><li>文字列値。</li><li>詳細については、Adobeの [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) を参照してください。</li></ul> | `x64` |
| アプリケーションが使用するビット数を含むサーバーサイド属性。 | `hints.bitness` | <ul><li>文字列値。</li><li>詳細については、Adobeの [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) を参照してください。</li></ul> | `64` |
| カスタムイベントがモバイル接続を通じて発生したかどうかを示すサーバーサイド属性。 | `hints.mobile` | <ul><li>ブール値。</li><li>詳細については、Adobeの [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) を参照してください。</li></ul>  | `true` |
| プラットフォームヒントを含むサーバーサイド属性。 | `hints.platform` | <ul><li>文字列値。</li></ul> | `win` |
| プラットフォームバージョンヒントを含むサーバーサイド属性。 | `hints.platformVersion` | <ul><li>文字列値。</li><li>詳細については、Adobeの [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) を参照してください。</li></ul>  | `10` |
| Windowsが32ビットサブシステムを実行していることを示すサーバーサイド属性。詳細については、[WoW64 at Wikipedia](https://en.wikipedia.org/wiki/WoW64) を参照してください | `hints.wow64` | <ul><li>ブール値。</li><li>詳細については、Adobeの [User agent client hints](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html) を参照してください。</li></ul> | `true` |

### コンテキストデータ

[Context Data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en) は、propsやeVarsに代わるよりユーザーフレンドリーな代替手段として使用できます。任意のイベント属性または訪問属性をAdobe AnalyticsのContext Data変数にマッピングできます。Context Data変数には任意の名前を付けることができますが、すべての変数に一意のキー（たとえば会社名）を接頭辞として付けることがAdobeのベストプラクティスです。一部の変数は予約されており、Lifecycle Metricsなどの予定された機能のみに使用できます。これらの変数は `a.` で接頭辞が付けられます。

| マップ元 | マップ先 | 説明 | 例 | 
|---------------|------------|------------------|---------------|
| リストから任意の属性を選択するか、カスタム値を入力します。 | companyname.someproperty | 定義されたサーバーサイド属性をContext Data属性にマッピングします | マップ：(サーバーサイド属性) キャンペーン名を `tealium.productColor` にマッピング |
### アナリティクス eVars

このフィールドは、サーバーサイドの属性を [eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en) にマッピングするために使用されます。eVarsは、属性を数字にマッピングすることで指定する必要があります。有効な範囲は `1` から `250` です。

| マップ元 | マップ先 | 説明 | 例 |
|---------------|------------|------------------|---------------|
| リストから任意の属性を選択するか、カスタム値を入力します。 | X（Xは1-250の範囲の整数） | サーバーサイドの定義済み属性をアナリティクスレポートのeVarにマッピングします | 例えば、`event_count` を `1` にマッピングして `eVar1` にします。 |

### アナリティクスプロパティ名 (s.props)

このフィールドは、サーバーサイドの属性を [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en) にマッピングするために使用されます。Propsは、`prop` という単語に数字を加えたもの（例：`prop4`）を使用して指定する必要があります。Propsは、属性を数字にマッピングすることで指定する必要があります。有効な範囲は `1` から `75` です。[List props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props) もサポートされていますが、これにはAdobe Analytics Report Suite管理インターフェースで事前に構成が必要です。

| マップ元 | マップ先 | 説明 | 例 | 
|---------------|------------|------------------|---------------|
| リストから任意の属性を選択するか、カスタム値を入力します。 | X（Xは `1` から `75` の範囲の整数） | サーバーサイドの定義済み属性をアナリティクスレポートのpropにマッピングします。 | `lifetime_value` を `1` にマッピングして `prop1` にします。 |

### イベント (s.events)

[イベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en) は、ウェブサイトやアプリで特定のイベントがどれだけ頻繁に発生しているかを測定するために使用されます。イベント変数は、特定のアナリティクスイベントに対してカウントされるべきすべてのイベントをリストするコンマ区切りの文字列です。[事前定義されたイベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en) と [カスタムイベント](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en) は同じ文字列で送信されます。

他の場所（例えば、iQ Tag Managementの拡張機能、エンリッチメント、またはデータレイヤー内で直接）で入力されたイベント名のリストを含む配列値をマッピングします。

| 入力 | サンプルコネクタ出力 |
|------------|----------------------------|
| イベントのリストを表すサーバーサイド属性。 | `event1,event5,event9` |

### イベントマッピング

上記のイベント名をイベントXにリネームする必要がある場合、マッピングによってリネームできます。

例えば、`purchase` を `4` にマッピングすると、`purchase` は `event4` に置き換えられ、[Send Analytics Event (Batch)](#send-analytics-event-batch) セクションのイベントマッピング例に基づいて最終出力は `event1,event2,event3,purchase` から `event1,event2,event3,event4` に変更されます。

| マップ元 | データタイプ | マップ先 | 例の入力 | サンプルコネクタ出力  |
|:---------|:----------|:-------|:--------------|:-------------------------|
| イベント配列内で検索する文字列を含むカスタムテキスト値。 | トリガーするイベントの名前。例えば、`event8`。 | `["newsletter_registration", "homepage_viewed"]` | `newsletter_registration` |

### イベント値

このフィールドでは、イベントに数値を割り当てることができます。

| マップ元 | データタイプ | マップ先 | 例の入力  | サンプルコネクタ出力  |
|:---------|:----------|:-------|:---------------|:-------------------------|
| 数値を表す属性。 | 数値    | X（Xはイベントの番号） | `9` を `event5` にマッピング | `event5=9` |

### イベントシリアライゼーション

イベントIDを含む属性をイベントの番号を指定する数値にマッピングすることでイベントシリアライゼーションを構成します。

| マップ元 | データタイプ | マップ先 | 例の入力 | サンプルコネクタ出力  |
|:---------|:----------|:-------|:--------------|:-------------------------|
| イベントIDを表す属性。 | 文字列    | イベントの番号。 | `ABC123` を `1` にマッピング、<br> `ABC123` を `2` にマッピング | `event1:ABC123,event2:ABC123` |

### 製品

[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数は、特定のページ上の一つまたは複数の製品に関するeコマース情報をキャプチャするために使用されます。

製品変数を入力するためには、配列データタイプを持つサーバーサイド属性のみが使用可能です。すべての配列は長さが等しくなければなりません。例えば、ページ上に5つの製品がある場合、製品ID、数量、価格、カテゴリはすべて5要素の長さでなければなりません。

| マップ元 | データタイプ | マップ先 | 例の入力データ | サンプルコネクタ出力 |
|--------------|--------------|-------------|------------------------|-----------------------|
| 製品カテゴリを表すサーバーサイド属性 | 配列       | 製品カテゴリ | `["Shoes", "Shirts"]`  | `Shoes;;;,Shirts;;;`  |
| 製品IDを表すサーバーサイド属性       | 配列       | 製品ID       | `["ABC123", "EFG234"]` | `;ABC123;;,;EFG234;;` |
| 数量を表すサーバーサイド属性         | 配列       | 製品数量 | `["1", "2"]`           | `;;1;,;;2;;`          |
| 価格を表すサーバーサイド属性            | 配列       | 製品価格    | `["149.99", "79.80"]`  | `;;;149.99,;;;79.80`  |

### 製品イベント

このフィールドでは、[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数の各製品にカスタムのコンバージョンイベントを割り当て、各イベントに数値を割り当てることができます。

単一の変数（単一の値またはカスタムテキスト値）がマッピングされた場合、同じ値がリスト内のすべての製品に適用されます。リスト（配列）値がマッピングされた場合、配列は他の製品配列と同じ長さでなければならず、配列内の各アイテムはその位置に応じて異なる値を持ちます。

これらの例では、次の製品配列がイベント属性として存在していると仮定します：

```
製品カテゴリ: ["Footwear", "Apparel"] 製品ID: ["Running Shoes", "T-Shirt"] 数量: ["1", "1"] 価格: ["99.99", "49.99"]
```

| マップ元  | データタイプ | マップ先  | 例の入力値 | サンプルコネクタ出力 |
|-----------|----------|----------|---------------------|-------------------------|
| 数値を含むカスタムテキスト値。 | 文字列   | トリガーするイベントの名前。例えば、`event8`。 | `9.99` (カスタム値) | `Footwear;RunningShoes;1;99.99;event8=9.99,Apparel;T-Shirt;1;49.99;event8=9.99` |
| 数値配列を表すサーバーサイド属性。 | 配列    | トリガーするイベントの名前。例えば、`event12`。 | `["1.99", "4.99"]`  | `Footwear;RunningShoes;1;99.99;event12=1.99,Apparel;T-Shirt;1;49.99;event12=4.99` |

### 製品 eVars

このフィールドでは、[製品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数の各製品にeVarsを割り当てることができます。

これは上記の **製品イベント** フィールドと同じ方法で動作します。

| マップ元 | データタイプ | マップ先 | 例の入力値 | サンプルコネクタ出力 |
|--------------|---------------|------------|-----------------------|-------------------|
| 数値を含むカスタムテキスト値。 | 文字列 | トリガーするイベントの名前。例えば、`event8`。 | `9.99` (カスタム値) | `Footwear;RunningShoes;1;99.99;event8=9.99,Apparel;T-Shirt;1;49.99;event8=9.99` |
| 数値データの配列を表すサーバーサイド属性。 | 配列 | トリガーするイベントの名前。例えば、`event12`。 | `["1.99", "4.99"]` | `Shoes;1;99.99;event12=1.99,Apparel;T-Shirt;1;49.99;event12=4.99` |

### 階層

ページ [階層](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en) は、サイト/アプリのナビゲーション構造内でページを分類するのに役立ちます。使用可能なスロットは `hier1` から `hier5` までです。
### リストデータ

[リスト変数](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en)は、複数の値を含む区切り文字列であり、しばしば帰属目的で使用されます。各レポートスイートには最大3つのリスト変数が利用可能です。配列変数はコンマ区切りの文字列に変換されます。

| Map From | Data Type | Map To | Description | Example | Sample Connector Output |
|-------------|------------|-------------|---------------|---------------|--------------------|
| リストから任意の配列属性を選択します。 | 配列 | `list1`, `list2`, `list3` (リスト選択) | サーバーサイド属性を配列形式で指定されたAdobe Analyticsのリスト変数にマッピングします。 | Map: (サーバーサイド属性) リファラーリストを `list1` にマッピング | `google.com,yahoo.com` |

### カスタムID値

Adobeは、Adobe Experience Cloud Identity Serviceで使用される識別子を生成するプロセスを簡素化する方法を提供しています。Adobeは、[setCustomerIDs](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/setcustomerids)メソッドの顧客IDの1つを使用して、Adobe Experience Cloud訪問IDを生成することができます。

詳細については、[Adobe Analytics 2.0 APIS](https://github.com/AdobeDocs/analytics-2.0-apis/blob/main/src/pages/guides/endpoints/bulk-data-insertion/mcseed.md)を参照してください。

#### フィールド

* **customerIDType**: 提供する顧客IDのタイプを指定します。例えば、`email`。
* **id**: Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用されるID。customerID.[customerIDType].idにマッピングされます。例えば、customerID.email.id ↔︎ 顧客のメール。
* **isMCSeed**: `customerID.[customerIDType].id`をヒットの識別子として使用することを許可する整数ブール値。`1`を真として、`0`を偽として使用します。
* **authState**: Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用されるauthState。文字列の値は大文字と小文字を区別しません。サポートされる値は以下の通りです：
    * `0`または空文字列：ログインしていない
    * `1`または`AUTHENTICATED`：ログイン済み
    * `2`または`LOGGED_OUT`：ログアウト済み。

#### メソッドパラメータ

| Parameter    | Description |
| ---------------  | --------------- |
| `customerIDType` | 提供する顧客IDのタイプを識別します。例えば、`email`。 |
| `id`             | Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用されるID。customerID.[customerIDType].idにマッピングされます。例えば、customerID.email.id ↔︎ 顧客のメール。 |
| `isMCSeed`       | `customerID.[customerIDType].id`をヒットの識別子として使用することを許可する整数ブール値。`1`を真として、`0`を偽として使用します。 |
| `authState`      | Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用される`authState`。文字列の値は大文字と小文字を区別しません。サポートされる値は以下の通りです：<ul><li>`0`または空文字列 - ログインしていない</li><li>`1`または`AUTHENTICATED` - ログイン済み</li><li>`2`または`LOGGED_OUT` - ログアウト済み</li></ul> |

## 訪問とエクスペリエンスクラウドID

複数のIDが提供された場合の優先順位については、[訪問ID](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en)のAdobe Analyticsドキュメントを参照してください。

### ユースケース1: Adobe Analyticsの実装がこれまでない場合

これが全く新しいAdobe Analyticsの実装である場合、100%サーバーサイドで、独自の一意の訪問IDを使用し、それをコネクタのvisitorID属性に渡すことができます。適切な訪問IDを決定する必要があります。Adobeによって構成された[制約](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=en)の範囲内で。

### ユースケース2: 既存のAdobe AnalyticsクライアントサイドJavaScriptからの移行

JavaScriptベースのAdobe Analyticsタグからサーバーサイドコネクタへ移行する場合、完全に移行するときに「訪問を失う」ことがないように、一貫した訪問IDを維持する必要があります。また、Adobe Analyticsコネクタを二次的な収集メカニズムとして実装している場合（ウェブページやアプリで引き続きJavaScriptタグを主要な収集メカニズムとして使用している場合）、訪問IDを移行する必要があります。

既存のAdobe AnalyticsクライアントサイドJavaScriptからの移行には、次の手順を使用します：

#### ステップ1: Adobe Experience Cloud IDタグを構成する

[これらの指示](https://docs.tealium.com/adobe-experience-cloud-id-service-tag/)に従ってAdobe Experience Cloud IDタグを構成し、iQ Tag Managementでタグを構成します。

#### ステップ2: Adobe訪問IDをファーストパーティクッキーに保存する

Adobe訪問IDをファーストパーティクッキーに保存することで、セッションの期間中、値を再リクエストする必要なく、サーバーサイドプラットフォームに値が送信されるようになります。

1. iQ Tag Managementでデータレイヤータブに移動し、`utag_main_adobe_mcid`および`utag_main_aa_vid`という2つの新しいファーストパーティクッキー変数を作成します。
    
<blockquote>
これらの変数の名前を変更することはできますが、`utag_main`クッキーにスタックしてクッキースペースを節約するために`utag_main_`プレフィックスを保持することを確認してください。変数の名前を変更する場合は、以下のJavaScriptスニペットも更新する必要があります
</blockquote>

1. Adobe Experience Cloud ID ServiceタグにスコープされたJavaScript Code拡張を作成し、次のコードを貼り付けます：
    ```js
    if (typeof vAPI !== "undefined") {
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

    これにより、Adobeのサーバーから訪問IDが正常に取得されたときに呼び出されるAdobe Visitor IDサービスへのコールバックが作成され、訪問IDとExperience Cloud IDがTealiumの独自のファーストパーティクッキー(`utag_main`)に保存されます。クッキーはセッションの終了時に期限切れになります。訪問IDが将来更新される場合を考慮して、クッキーを永続的にする（期限切れにしない）場合は、上記のコードで`sessionExpiry`を`""`に構成します。

1. このセッション中にコードが再度実行されないように、JavaScript拡張に次の条件を追加します。

      
      [
        [
          {
            "input": "utag_main_adobe_mcid",
            "operator": "is not defined"
          },
          {
            "input": "utag_main_aa_vid",
            "operator": "is not defined"
          }
        ]
      ]
      
  
#### ステップ3: AudienceStreamとEventStreamのサーバーサイドを構成する

* **AudienceStream**: AudienceStreamを使用している場合、Adobe Visitor IDとExperience Cloud IDを訪問レベルの文字列属性として保存できます。Visitor ID属性として保存しないでください。オーディエンスイベントによってトリガーされるアクションの場合、コネクタ構成で新しい属性を`visitorID`および`marketingCloudVisitorID`にマッピングできます。
* **EventStream**: EventStreamのみを使用している場合、訪問ID変数を保存する機能がないため、値をクッキーに保存しました。
    * 前のステップのiQタグ管理構成をProdに公開している場合、イベント属性に`utag_main_adobe_mcid`および`utag_main_aa_vid`の値が既に存在していることがわかります。
    * Prodに公開していない場合は、**First Party Cookie**文字列属性タイプを使用してイベント属性を手動で追加できます。これらの属性を定義した後、Adobe Analyticsコネクタでそれらを選択し、それぞれ`marketingCloudVisitorID`および`visitorID`にマッピングできます。

## 一般的な問題のデバッグ

* コネクタをテストするには、[trace](https://docs.tealium.com/about-trace/)の使用をお勧めします。トレースを実行する際には、**HTTP Request Body**フィールドを確認し、バッチコールが実行される際にAdobeに送信されるCSVヘッダーと最初の行のサンプルを確認できます。CSV出力を上記の表の**Sample Connector Output**フィールドと比較して出力を確認してください。
* Adobeから返される応答コードにエラーがないか確認してください。HTTP応答ステータス: 200/成功以外は、リクエストに問題があったことを示します。
    
<blockquote>
コネクタ構成に完全なURL値を入力する必要はありません。TealiumはData Insertion Domain値に基づいてURLを自動生成します。完全なURLはトレースセッションを実行しているときにのみ表示されます。
</blockquote>

* Adobe Analyticsがデータを受信していない場合は、**Admin > Report suites > Edit Settings > General > Timestamp configuration**に移動し、[Timestamps option](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/timestamp-optional)を`Timestamps not allowed`から`Timestamps optional`または`Timestamps required`に変更してください。タイムスタンプが必要な場合は、有効なタイムスタンプをマッピングしてください。
* User AgentまたはClient Hintsにマッピングすることを強くお勧めします。この値をマッピングしないと、AdobeはサーバーのUser Agent（例: `Apache-HttpClient/4.5.5(Java/11.0.17`）を取得し、それがボットトラフィックとして識別される可能性があります。

## マイグレータツール

Adobe Analytics 2.0マイグレータツールを使用すると、既存のAdobe Analytics 1.4コネクタをAdobe Analytics 2.0コネクタに移行できます。Adobe Analytics 1.4コネクタは非推奨ではなく、移行する必要はありません。**Send Analytics Event (Batch)**アクションを使用し、リアルタイムコネクタアクションが必要でない場合にのみ、1.4コネクタアクションを移行してください。

マイグレータツールを使用する前に、次の制限事項に注意してください：

* このツールは、バージョン2.0で利用できない1.4の属性を移行しません。詳細については、[Adobe Analytics 2.0コネクタの違い]()セクションの1.4と2.0の属性の表を参照してください。
* モバイルデータソース属性のライフサイクルイベント属性は2.0 APIでは利用できないため、これらの属性の自動マッピングは移行されません。
* Adobe Analytics 2.0はカスタム属性をサポートしていないため、1.4コネクタのこのセクションの属性は移行されません。

Adobe Analytics 1.4コネクタを移行するには、次の手順に従ってください：

1. **Server-Side**に移動し、Google ChromeのTealium Tools拡張機能を開きます。
1. Tealium Toolsで、**Tool Catalogue**タブをクリックし、**Adobe Analytics 2.0 Migrator**をクリックします。詳細については、[Tealium Tools]()を参照してください。
1. アクションの移行方法を選択します。
    * 移行の一環として既存のAdobe Analytics 1.4アクションを無効にする場合は、**Disable existing action**を選択します。
    * アクティブなアクションのみを移行する場合は、**Migrate only active actions**を選択します。
1. リストから移行の範囲を選択します：
    * すべてのAdobe Analytics 1.4アクション
    * 特定のAdobe Analytics 1.4アクション
    * 特定のAdobe Analytics 1.4コネクタ
1. プロジェクトのAdobe Analytics **Client ID**と**Client secret**を入力します。
1. **Start**をクリックします。
  マイグレータツールは、既存のAdobe Analytics 1.4コネクタを新しいAdobe Analytics 2.0コネクタに自動的に移行します。コネクタの名前は同じで、サフィックスに"2.0 (Migrated)"が付きます。
1. 新しいコネクタ構成とアクションを確認します。
1. プロファイルを保存して公開します。