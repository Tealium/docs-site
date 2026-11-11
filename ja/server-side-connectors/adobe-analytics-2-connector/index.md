---
title: Adobe Analytics 2.0 コネクタ構成ガイド
description: この記事では、Adobe Analytics 2.0 コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-analytics-2-connector/
---
## 仕組み

Adobe Analytics 2.0 コネクタは、Web ページやモバイルアプリで JavaScript ビーコンを使用する代わりに、[Adobe Bulk Data Insertion API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/endpoints/bulk-data-insertion/) を使用して分析データを送信します。これにより、クライアント側から送信されるデータ量を削減できるほか、オーディエンスデータと訪問データを Adobe Analytics に渡せるという利点もあります。

## Adobe Analytics 2.0 コネクタの相違点

Adobe Bulk Data Insertion API には、リアルタイムまたは準リアルタイムのコネクタアクションをサポートしないレート制限があります。このため、Adobe Analytics 2.0 コネクタでは、**分析イベントを送信**アクションが非推奨になっています。ユースケースでリアルタイムのコネクタアクションが不要な場合は、**分析イベントを送信（バッチ）**アクションに移行してください。ユースケースでリアルタイムのコネクタアクションが必要な場合は、[Adobe Analytics 1.4 コネクタ](https://docs.tealium.com/adobe-analytics-connector/)を使用してください。

Adobe Analytics 1.4 コネクタの以下の機能は、Adobe Analytics 2.0 コネクタでは使用できません。

* カスタムフィールドマッピング（詳細）
* モバイルデータソースのライフサイクルイベント属性の自動マッピングを有効化

次の表に示すように、Adobe Analytics 1.4 の一部のパラメータは Adobe Analytics 2.0 コネクタでは使用できません。**Adobe Analytics 2.0 パラメータ**列の ✗ は、そのパラメータが 2.0 コネクタでは使用できないことを示します。

| Adobe Analytics 1.4 パラメータ | Adobe Analytics 2.0 パラメータ |
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

Adobe Analytics 1.4 コネクタから Adobe Analytics 2.0 コネクタへの移行については、[移行ツール]()を参照してください。

## 構成

Adobe Analytics 2.0 コネクタを構成するには、Adobe Analytics 2.0 API のクライアント ID（API キー）とクライアントシークレットが必要です。Adobe Developer Console で認証情報を作成し、Adobe Analytics 2.0 API のクライアント ID とクライアントシークレットを取得するには、次の手順を実行します。

1. Adobe Developer Console に移動し、Adobe ID でログインします。
1. **新しいプロジェクトを作成**をクリックします。
1. プロジェクトの名前を入力し、**保存**をクリックします。
1. プロジェクトダッシュボードで、**API を追加**をクリックします。
1. 使用可能な API の一覧から、**Adobe Analytics** を選択します。
1. **認証タイプ**で、**サーバー間認証**を選択します。
1. 統合タイプとして、**OAuth サーバー間**を選択します。
1. アクセス権を付与する**製品プロファイル**を選択します。
1. クライアント ID とクライアントシークレットを取得するには、プロジェクトの**認証情報**セクションに移動します。
1. クライアント ID とクライアントシークレットを表示してコピーするには、**クライアントシークレットを取得**をクリックします。

クライアント ID とクライアントシークレットを取得したら、インターフェイスで次の手順を実行して Adobe Analytics コネクタを構成します。

1. コネクタマーケットプレイスに移動し、Adobe Analytics コネクタを追加します。  
詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。
1. **オーディエンス**と**トリガー**を選択し、**続行**をクリックします。
1. **コネクタを追加**をクリックします。
1. コネクタの**名前**を入力します。
1. **クライアント ID** と**クライアントシークレット**を入力します。
1. （任意）**接続をテスト**をクリックします。
1. **完了**をクリックしてから、**続行**をクリックします。

次の手順は、[アクションの構成]()です。

## アクション

| アクション名 | 顧客データプラットフォーム（CDP） | イベントストリーミング |
|:---------------------|:-------------------|:----------------|
| 分析イベントを送信（バッチ） | ✓ | ✓ |
| 分析イベントを送信（非推奨） | ✓ | ✓ |

### 分析イベントを送信（バッチ）

#### バッチ制限

このコネクタでは、ベンダーへの大容量データ転送をサポートするために、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：250,000
* 最も古いリクエストからの最大経過時間：30 分（1～60 分の範囲で構成可能）
* リクエストの最大サイズ：300 MB
#### パラメータ

イベントパラメータについては、[一般属性](#general-attributes)を参照してください。

| **グループ** | **説明** |
|-------------|-----------------|
| コンテキストデータ | <ul><li>ドット形式でキーを指定します。</li><li>例：`my.a`。</li><li>複数のキーと値のペアを指定できます。</li></ul> |
| eVar | <ul><li>属性を番号にマッピングして、イベントの eVar を指定します。</li><li>例：**eVar1** の場合、`event_count` を `1` にマッピングします。</li><li>有効な範囲は `1`～`100` です。Premium Accounts の場合は `250` までです。</li></ul> |
| 階層 | <ul><li>階層文字列。</li><li>`1`～`5` から選択します。</li></ul> |
| リスト | <ul><li>変数に渡され、レポートでは個別の明細項目として報告される値のリスト</li><li>`1`～`3` から選択します。</li><li>データレイヤーでは配列型が必要です。</li><li>Tealium は、渡すデータを正しい形式に整形します。</li></ul> |
| プロパティ | <ul><li>Analytics のプロパティ名。</li><li>属性を番号にマッピングして名前を指定します。</li><li>例：**prop1** の場合、`lifetime_value` を `1` にマッピングします。</li></ul> |
| イベント | <ul><li>イベントのリスト、またはカンマ区切りのカスタム値を指定します。</li><li>詳細については、[Adobe Analytics のイベント実装の構成](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を参照してください。</li></ul> |
| イベントマッピング | <ul><li>Events 配列に含まれる可能性のある値を、Adobe Analytics のカスタムイベント名にマッピングします。</li><li>例：purchase を 3 にマッピングすると、purchase が event3 に置き換えられます。そのため、元の Events の例に基づく最終出力は、event1,event2,event3,purchase から event1,event2,event3,event4 に変わります。</li></ul> |
| イベント値 | <ul><li>`Counter`、`Numeric`、`Currency` イベントの値を指定します。</li><li>イベントを指定するには、番号を使用します。</li><li>例：9.99 を 2 にマッピングすると、出力は `event1,event2=9.99,event3,event4` になります。</li></ul> |
| イベントのシリアル化 | <ul><li>イベントのシリアル化に使用するイベント ID を指定します。</li><li>詳細については、[イベントのシリアル化](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/events/event-serialization#vars)を参照してください。</li><li>例：page_view を 3 にマッピングすると、出力は `event1,event2,event3:page_view,event4` になります。</li></ul> |
| 製品 | <ul><li>製品属性（`Id`、`Category`、`Quantity`、`Price`）を指定します。</li><li>すべての配列はサイズが同じで、順序が揃っている必要があります。</li><li>詳細については、[Adobe Analytics の製品実装](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)を参照してください。</li></ul> |
| 製品 eVar | <ul><li>製品 eVar の値を指定します。</li><li>すべての配列は、**製品**セクション内の配列と同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>eVar のマッピングを番号で指定します。</li><li>例として、`1` は `eVar1` にマッピングされます。</li></ul> |
| 製品イベント | <ul><li>製品イベントの値を指定します。</li><li>すべての配列は、**製品**セクション内の配列と同じサイズである必要があります。</li><li>空の値は無視されます。</li><li>イベントのマッピングを番号で指定します。</li><li>例として、`1` は `event1` にマッピングされます。</li></ul> |
| ブランド | <ul><li>ブランド属性を指定します。</li><li>使用可能な属性は **brand** と **version** です。</li><li>すべての配列は同じサイズである必要があります。</li></ul> |
| バッチの有効期間 | バッチアクションを送信する頻度を指定するために、有効期間（TTL）を構成します。`1`～`60` 分の値を入力します。デフォルト値は `30` 分です。 |

### Analytics イベントの送信（非推奨）


<blockquote>
This action is deprecated and can no longer be added. Use [Send Analytics Event (Batch)](#send-analytics-event-batch) instead.
</blockquote>


#### バッチ制限

このアクションにはバッチアクションというラベルが付いていませんが、リクエストはリアルタイムでは送信されません。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：250,000
* 最も古いリクエストからの最大経過時間：45 秒
* リクエストの最大サイズ：100 MB

## 一般属性

各フィールドに含める内容の詳細を含む、すべての属性の完全なリファレンスについては、[Adobe：API ドキュメント](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)およびこの記事の[訪問 ID と Experience Cloud ID](#visitor-and-experience-cloud-ids)セクションを参照してください。

### ユーザーエージェントのクライアントヒント

Google Chrome や Microsoft Edge などの Chromium ブラウザーから提供されるクライアントヒントには、デバイス固有の情報が含まれています。このデータセットは、デバイス情報の主要なソースとしてユーザーエージェント文字列に代わるものです。

これらのマッピングの選択肢は、**イベントパラメータ**セクションに表示されます。

|マッピング元|マッピング先|注記|コネクタ出力の例|
|----|----|----|----|
| システムアーキテクチャのヒントを含むサーバー側属性。 | `hints.architecture` | <ul><li>文字列値。</li><li>詳細については、Adobe の[ユーザーエージェントのクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `x64` |
| 実行中のアプリケーションのビット数を含むサーバー側属性。 | `hints.bitness` | <ul><li>文字列値。</li><li>詳細については、Adobe の[ユーザーエージェントのクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `64` |
| カスタムイベントがモバイル接続経由で発生したかどうかを示すサーバー側属性。 | `hints.mobile` | <ul><li>ブール値。</li><li>詳細については、Adobe の[ユーザーエージェントのクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `true` |
| プラットフォームのヒントを含むサーバー側属性。 | `hints.platform` | <ul><li>文字列値。</li></ul> | `win` |
| プラットフォームバージョンのヒントを含むサーバー側属性。 | `hints.platformVersion` | <ul><li>文字列値。</li><li>詳細については、Adobe の[ユーザーエージェントのクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `10` |
| Windows で 32 ビットサブシステムが実行されていることを示すインジケーターを含むサーバー側属性。詳細については、[Wikipedia の WoW64](https://en.wikipedia.org/wiki/WoW64)を参照してください。 | `hints.wow64` | <ul><li>ブール値。</li><li>詳細については、Adobe の[ユーザーエージェントのクライアントヒント](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/user-agent-client-hints.html)を参照してください。</li></ul> | `true` |

### コンテキストデータ

[コンテキストデータ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en)は、props と eVar に代わる、より使いやすい選択肢として使用できます。任意のイベント属性または訪問属性を、Adobe Analytics のコンテキストデータ変数にマッピングできます。コンテキストデータ変数には任意の名前を付けられますが、会社名などの一意のキーをすべての変数の先頭に付けることが、Adobe のベストプラクティスです。一部の変数は予約されており、ライフサイクル指標など、あらかじめ定められた機能にのみ使用できます。これらの変数には、接頭辞 `a.` が付いています。

| マッピング元 | マッピング先 | 説明 | 例 |
|---------------|------------|------------------|---------------|
| リストから任意の属性を選択するか、カスタム値を入力します。 | companyname.someproperty | 定義済みのサーバー側属性をコンテキストデータ属性にマッピングします。 | マッピング：（サーバー側属性）Campaign Name を `tealium.productColor` にマッピング |
### Analytics eVar

このフィールドは、サーバーサイド属性を [eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=en) にマッピングするために使用します。eVar は、属性を数値にマッピングして指定する必要があります。有効な範囲は `1`～`250` です。

| マッピング元 | マッピング先 | 説明 | 例 |
|---------------|------------|------------------|---------------|
| リストから任意の属性を選択するか、カスタム値を入力します。 | X（X は 1～250 の範囲の整数） | 定義されたサーバーサイド属性を、Analytics レポート内の eVar にマッピングします | たとえば、`eVar1` に使用するため、`event_count` を `1` にマッピングします。 |

### Analytics プロパティ名（s.props）

このフィールドは、サーバーサイド属性を [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en) にマッピングするために使用します。prop は、`prop` という語に prop 番号を加えて指定する必要があります（例：`prop4`）。prop は、属性を数値にマッピングして指定する必要があります。有効な範囲は `1`～`75` です。[リスト prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=en#list-props)もサポートされていますが、Adobe Analytics レポートスイートの管理インターフェイスで事前に構成する必要があります。

| マッピング元 | マッピング先 | 説明 | 例 | 
|---------------|------------|------------------|---------------|
| リストから任意の属性を選択するか、カスタム値を入力します。 | X（X は `1`～`75` の範囲の整数） | 定義されたサーバーサイド属性を、Analytics レポート内の prop にマッピングします。 | `prop1` に使用するため、`lifetime_value` を `1` にマッピングします。 |

### イベント（s.events）

[イベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)を使用すると、特定のイベントが Web サイトまたはアプリで発生する頻度を測定できます。events 変数は、特定の Analytics イベントについてカウントする必要があるすべてのイベントを列挙した、コンマ区切りの文字列です。[定義済みイベント](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=en)と[カスタムイベント](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en)は、同じ文字列で送信されます。

別の場所（たとえば、タグ管理の拡張機能、エンリッチメント、またはデータレイヤー内）で構成されたイベント名のリストを含む配列値をマッピングします。  

| 入力 | コネクタ出力例 |
|------------|----------------------------|
| イベントのリストを表すサーバーサイド属性。 | `event1,event5,event9` |

### イベントのマッピング

上記のイベント名を event X に変更する必要がある場合は、マッピングによって変更できます。

たとえば、`purchase` を `4` にマッピングすると、`purchase` が `event4` に置き換えられます。そのため、[Analytics イベントの送信（バッチ）](#send-analytics-event-batch)セクションのイベントマッピング例に基づく最終出力は、`event1,event2,event3,purchase` から `event1,event2,event3,event4` に変わります。

| マッピング元 | データ型 | マッピング先 | 入力例 | コネクタ出力例 |
|:---------|:----------|:-------|:--------------|:-------------------------|
| Events 配列内で検索する文字列を含むカスタムテキスト値。 | トリガーするイベントの名前（例：`event8`）。 | `["newsletter_registration", "homepage_viewed"]` | `newsletter_registration` |

### イベント値

このフィールドでは、イベントに数値を割り当てることができます。

| マッピング元 | データ型 | マッピング先 | 入力例 | コネクタ出力例 |
|:---------|:----------|:-------|:---------------|:-------------------------|
| 数値を表す属性。 | 数値 | X（X はイベントの番号） | `9` を `event5` にマッピング | `event5=9` |

### イベントのシリアル化

イベント ID を含む属性を、イベントを指定する番号にマッピングして、イベントのシリアル化を構成します。

| マッピング元 | データ型 | マッピング先 | 入力例 | コネクタ出力例 |
|:---------|:----------|:-------|:--------------|:-------------------------|
| イベント ID を表す属性。 | 文字列 | イベント番号。 | `ABC123` を `1` にマッピング、<br> `ABC123` を `2` にマッピング | `event1:ABC123,event2:ABC123` |

### 製品

[Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数は、特定のページ上にある 1 つ以上の製品に関する e コマース情報（カテゴリ、製品 ID、価格、数量）を取得する必要がある場合に使用します。

Products 変数への入力には、配列データ型のサーバーサイド属性のみを使用できます。すべての配列の長さが同じである必要があります。たとえば、ページ上に 5 つの製品がある場合、製品 ID、数量、価格、およびカテゴリは、すべて要素数が 5 である必要があります。

| マッピング元 | データ型 | マッピング先 | 入力データ例 | コネクタ出力例 |
|--------------|--------------|-------------|------------------------|-----------------------|
| 製品カテゴリを表すサーバーサイド属性 | 配列 | 製品カテゴリ | `["Shoes", "Shirts"]` | `Shoes;;;,Shirts;;;` |
| 製品 ID を表すサーバーサイド属性 | 配列 | 製品 ID | `["ABC123", "EFG234"]` | `;ABC123;;,;EFG234;;` |
| 数量を表すサーバーサイド属性 | 配列 | 製品数量 | `["1", "2"]` | `;;1;,;;2;;` |
| 価格を表すサーバーサイド属性 | 配列 | 製品価格 | `["149.99", "79.80"]` | `;;;149.99,;;;79.80` |

### 製品イベント

このフィールドでは、[Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数内の各製品にカスタムコンバージョンイベントを割り当て、各イベントに数値を割り当てることができます。

単純な変数（単一の値またはカスタムテキスト値）をマッピングした場合、リスト内のすべての製品に同じ値が適用されます。リスト（配列）値をマッピングした場合、その配列は他の製品配列と同じ長さである必要があり、配列内の各項目には、配列内の位置に応じて異なる値が構成されます。

以下の例では、次の製品配列がイベント属性として存在するものとします。

```
Product Category: ["Footwear", "Apparel"] Product ID: ["Running Shoes", "T-Shirt"] Quantity: ["1", "1"] Price: ["99.99", "49.99"]
```

| マッピング元 | データ型 | マッピング先 | 入力値の例 | コネクタ出力例 |
|-----------|----------|----------|---------------------|-------------------------|
| 数値を含むカスタムテキスト値。 | 文字列 | トリガーするイベントの名前。例：`event8`。 | `9.99`（カスタム値） | `Footwear;RunningShoes;1;99.99;event8=9.99,Apparel;T-Shirt;1;49.99;event8=9.99` |
| 数値配列を表すサーバーサイド属性。 | 配列 | トリガーするイベントの名前。例：`event12`。 | `["1.99", "4.99"]` | `Footwear;RunningShoes;1;99.99;event12=1.99,Apparel;T-Shirt;1;49.99;event12=4.99` |

### 製品 eVar

このフィールドでは、[Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) 変数内の各製品に eVar を割り当てることができます。

これは、前述の「**製品イベント**」フィールドと同じように機能します。

| マッピング元 | データ型 | マッピング先 | 入力値の例 | コネクタ出力例 |
|--------------|---------------|------------|-----------------------|-------------------|
| 数値を含むカスタムテキスト値。 | 文字列 | トリガーするイベントの名前。例：`event8`。 | `9.99`（カスタム値） | `Footwear;RunningShoes;1;99.99;event8=9.99,Apparel;T-Shirt;1;49.99;event8=9.99` |
| 数値データの配列を表すサーバーサイド属性。 | 配列 | トリガーするイベントの名前。例：`event12`。 | `["1.99", "4.99"]` | `Shoes;1;99.99;event12=1.99,Apparel;T-Shirt;1;49.99;event12=4.99` |

### 階層

ページの[階層](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=en)は、サイトまたはアプリのナビゲーション構造内でページを分類するのに役立ちます。使用可能なスロットは、`hier1`～`hier5` の 5 つです。
### リストデータ

[リスト変数](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=en)は、複数の値を含む区切り文字付き文字列であり、アトリビューションの目的でよく使用されます。各レポートスイートでは、最大3つのリスト変数を使用できます。配列変数はカンマ区切りの文字列に変換されます。

| マッピング元 | データ型 | マッピング先 | 説明 | 例 | コネクタ出力の例 |
|-------------|------------|-------------|---------------|---------------|--------------------|
| リストから任意の配列属性を選択します。 | 配列 | `list1`、`list2`、`list3`（リスト選択） | 配列形式で定義されたサーバーサイド属性を、Adobe Analyticsの指定されたリスト変数にマッピングします。 | マッピング：（サーバーサイド属性）Referrer Listから`list1`へ | `google.com,yahoo.com` |

### カスタムID値

Adobeでは、Adobe Experience Cloud Identity Serviceで使用される識別子の生成プロセスを簡素化する方法を提供しています。Adobeは、[setCustomerIDs](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/setcustomerids)メソッドの顧客IDのいずれかをシードとして使用し、Adobe Experience Cloud訪問IDを生成できます。

詳細については、[Adobe Analytics 2.0 API](https://github.com/AdobeDocs/analytics-2.0-apis/blob/main/src/pages/guides/endpoints/bulk-data-insertion/mcseed.md)を参照してください。

#### フィールド

* **customerIDType**：値を指定する顧客IDのタイプを指定します。例：`email`。
* **id**：Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用されるIDです。customerID.[customerIDType].idにマッピングされます。例：customerID.email.id ↔︎ 顧客のメールアドレス。
* **isMCSeed**：`customerID.[customerIDType].id`をヒットの識別子として使用できるようにする整数のブール値です。trueの場合は`1`、falseの場合は`0`を使用します。
* **authState**：Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用されるauthStateです。文字列値では大文字と小文字が区別されません。サポートされている値は次のとおりです。
    * `0`または空の文字列：未ログイン
    * `1`または`AUTHENTICATED`：ログイン済み
    * `2`または`LOGGED_OUT`：ログアウト済み
    
#### メソッドのパラメーター

| パラメーター | 説明 |
| ---------------  | --------------- |
| `customerIDType` | 値を指定する顧客IDのタイプを識別します。例：`email`。 |
| `id`             | Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用されるIDです。`customerID.[customerIDType].id`にマッピングされます。例：`customerID.email.id` ↔︎ 顧客のメールアドレス。 |
| `isMCSeed`       | `customerID.[customerIDType].id`をヒットの識別子として使用できるようにする整数のブール値です。trueの場合は`1`、falseの場合は`0`を使用します。 |
| `authState`      | Experience Cloud Identity Serviceの`setCustomerIDs`メソッドで使用される`authState`です。文字列値では大文字と小文字が区別されません。サポートされている値は次のとおりです。<ul><li>`0`または空の文字列 - 未ログイン</li><li>`1`または`AUTHENTICATED` - ログイン済み</li><li>`2`または`LOGGED_OUT` - ログアウト済み</li></ul> |

## 訪問IDとExperience Cloud ID

[訪問ID](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en)、および複数のIDが指定された場合の優先順位については、Adobe Analyticsのドキュメントを参照してください。

### ユースケース1：既存のAdobe Analytics実装がない場合

これが完全に新規の100%サーバーサイドのAdobe Analytics実装である場合は、独自の一意な訪問IDを使用し、コネクタのvisitorID属性に渡すことができます。Adobeが定めた[制約](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=en)の範囲内で、何を適切な訪問IDとするかを決定する必要があります。

### ユースケース2：既存のAdobe AnalyticsクライアントサイドJavaScriptからの移行

JavaScriptベースのAdobe Analyticsタグからサーバーサイドコネクタへ移行する場合、完全移行時に訪問を「失う」ことがないよう、一貫した訪問IDを維持する必要があります。また、Adobe Analyticsコネクタを二次的なデータ収集メカニズムとして実装する場合（引き続きWebページやアプリでJavaScriptタグを主要なデータ収集メカニズムとして使用する場合）にも、訪問IDを移行する必要があります。

既存のAdobe AnalyticsクライアントサイドJavaScriptから移行するには、次の手順を実行します。

#### 手順1：Adobe Experience Cloud IDタグを構成する

に従ってAdobe Experience Cloud IDタグを構成し、Tag Managementでタグをセットアップします。

#### 手順2：Adobe訪問IDをファーストパーティCookieに保存する

Adobe訪問IDをファーストパーティCookieに保存すると、セッション中に値を再リクエストすることなく、各ヒットで値がサーバーサイドプラットフォームに送信されます。

1. Tag Managementで「Data Layer」タブに移動し、`utag_main_adobe_mcid`と`utag_main_aa_vid`という2つの新しいファーストパーティCookie変数を作成します。  
    
<blockquote>
You may rename these variables if you want to, but be sure to retain the `utag_main_` prefix, which will save cookie space by stacking into the `utag_main` cookie. If you rename the variables, you will need to also update the JavaScript snippet below
</blockquote>

1. Adobe Experience Cloud ID ServiceタグをスコープとするJavaScript Code拡張機能を作成し、次のコードを貼り付けます。  
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

    これにより、Adobeのサーバーから訪問IDが正常に取得されたときに呼び出されるAdobe Visitor IDサービスへのコールバックが作成され、訪問IDとExperience Cloud IDがTealium独自のファーストパーティCookie（`utag_main`）に保存されます。訪問IDが今後更新される可能性を考慮し、Cookieはセッション終了時に期限切れになります。Cookieを永続化（無期限化）するには、上記のコードで`sessionExpiry`を`""`に構成します。

1. このセッション中にコードが再実行されないようにするため、JavaScript拡張機能に次の条件を追加します。  
  
      
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
      
#### ステップ3：CDPおよびEvent Streamingのサーバーサイド構成を行う
 
* **CDP**：CDPを使用している場合、Adobe Visitor IDとExperience Cloud IDを訪問レベルの文字列属性として保存できます。Visitor ID属性として保存しないでください。オーディエンスイベントによってトリガーされるアクションでは、コネクタ構成で新しい属性を`visitorID`および`marketingCloudVisitorID`にマッピングできます。  
* **Event Streaming**：Event Streamingのみを使用している場合、訪問ID変数を保存できないため、値をCookieに保存します。  
    * 前のステップのタグ管理構成をすでにProdにパブリッシュしている場合、新しい`utag_main_adobe_mcid`と`utag_main_aa_vid`の値がイベント属性にすでに存在しています。  
    * Prodにパブリッシュしていない場合は、文字列属性タイプとして**First Party Cookie**を使用し、イベント属性を手動で追加できます。これらの属性を定義した後、Adobe Analyticsコネクタでそれらを選択し、それぞれ`marketingCloudVisitorID`と`visitorID`にマッピングできます。

## 一般的な問題のデバッグ

* コネクタをテストするには、[トレース](https://docs.tealium.com/about-trace/)の使用をお勧めします。トレースの実行中に、**HTTP Request Body**フィールドを確認してください。このフィールドには、バッチ呼び出しの実行時にAdobeへ送信されるCSVヘッダーと最初の行のサンプルが表示されます。CSV出力を上記の表にある**Sample Connector Output**フィールドと比較して、出力を検証できます。
* Adobeから返されるレスポンスコードにエラーがないか確認します。「HTTP Response Status: 200/Successful」以外の場合は、リクエストでエラーが発生したことを示します。
    
<blockquote>
コネクタ構成に完全なURL値を入力する必要はありません。Tealiumは、Data Insertion Domainの値に基づいてURLを自動生成します。完全なURLは、トレースセッションの実行中にのみ表示されます。
</blockquote>

* Adobe Analyticsがデータを受信していない場合は、**Admin > Report suites > Edit Settings > General > Timestamp configuration**に移動し、[Timestampsオプション](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/timestamp-optional)を`Timestamps not allowed`から`Timestamps optional`または`Timestamps required`に変更します。タイムスタンプが必須の場合は、有効なタイムスタンプを必ずマッピングしてください。
* User AgentまたはClient Hintsへのマッピングを強くお勧めします。この値をマッピングしないと、AdobeはサーバーのUser Agent（例：`Apache-HttpClient/4.5.5(Java/11.0.17`）を取得するため、ボットトラフィックとして識別される可能性があります。

## Migratorツール

Adobe Analytics 2.0 Migratorツールを使用すると、既存のAdobe Analytics 1.4コネクタをAdobe Analytics 2.0コネクタに移行できます。Adobe Analytics 1.4コネクタは非推奨ではなく、移行は必須ではありません。**Send Analytics Event (Batch)**アクションを使用する必要があり、ユースケースでリアルタイムのコネクタアクションを必要としない場合にのみ、1.4コネクタのアクションを移行してください。

Migratorツールを使用する前に、次の制限事項に注意してください。

* このツールでは、バージョン2.0で利用できない1.4の属性は移行されません。詳細については、[Adobe Analytics 2.0コネクタの相違点]()セクションにある1.4と2.0の属性の表を参照してください。
* モバイルデータソース属性のLifecycle Event Attributesは2.0 APIでは利用できないため、これらの属性の自動マッピングは移行されません。
* Adobe Analytics 2.0はカスタム属性をサポートしていません。そのため、1.4コネクタのこのセクションにある属性は移行されません。

Adobe Analytics 1.4コネクタを移行するには、次の手順を実行します。

1. **Server-Side**に移動し、Google Chrome用のTealium Tools拡張機能を開きます。
1. Tealium Toolsで**Tool Catalogue**タブをクリックし、**Adobe Analytics 2.0 Migrator**をクリックします。詳細については、[Tealium Tools]()を参照してください。
1. アクションの移行方法を選択します。  
    * 移行の一環として既存のAdobe Analytics 1.4アクションを無効にするには、**Disable existing action**を選択します。
    * アクティブなアクションのみを移行するには、**Migrate only active actions**を選択します。
1. リストから移行範囲を選択します。
    * すべてのAdobe Analytics 1.4アクション
    * 特定のAdobe Analytics 1.4アクション
    * 特定のAdobe Analytics 1.4コネクタ
1. プロジェクトのAdobe Analytics **Client ID**と**Client secret**を入力します。
1. **Start**をクリックします。  
  Migratorツールにより、既存のAdobe Analytics 1.4コネクタが新しいAdobe Analytics 2.0コネクタへ自動的に移行されます。コネクタ名は元の名前と同じで、末尾に「2.0 (Migrated)」が追加されます。
1. 新しいコネクタの構成とアクションを確認します。
1. プロファイルを保存してパブリッシュします。