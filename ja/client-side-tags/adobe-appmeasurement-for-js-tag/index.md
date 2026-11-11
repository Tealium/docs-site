---
title: Adobe Analytics AppMeasurement for JS タグ構成ガイド
description: この記事では、タグ管理アカウントで Adobe Analytics AppMeasurement for JS タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-appmeasurement-for-js-tag/
---
## タグに関するヒント

* Adobe Experience Cloud ID Service を使用するには、このタグを追加する前に Adobe Experience Cloud ID Service タグを追加します。
* 従来の H26 のすべての機能が AppMeasurement タグでサポートされているわけではありません。
* サーバー値を正しく入力してください。たとえば、サードパーティサーバーでは `112.2o7.net` または `122.2o7.net` を使用する場合があります。
* モバイル向け AppMeasurement を使用するには、アプリケーションに Tealium Mobile SDK を実装する必要があります。
* サポートされているプラグインの一覧については、[Adobe：AppMeasurement プラグインの概要](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/plugins/impl-plugins)を参照してください。
* 詳細については、[Adobe：JavaScript 用 AppMeasurement を使用した Adobe Analytics の実装](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview)を参照してください。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **コードバージョン**
  * `AppMeasurement.js` ライブラリのバージョン。
* **デバイスタイプ**
  * 実装するプラットフォームに応じて、次のいずれかを選択します。
    * デスクトップWebサイトにインストールする場合は **Standard**。
    * [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/) または [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/) を使用してネイティブモバイルにインストールする場合は **Mobile App**。
* **レポートスイート**
  * （必須）マッピングを使用してレポートスイートを動的に構成する場合でも、デフォルト値を構成します。
  * 使用するデフォルトのレポートスイート。Dynamic Acct List に構成された値に応じて変更される場合があります。
  * AppMeasurement.js リファレンス：`s.account`
* **サーバー**
  * （必須）データ収集サーバー。
  * AppMeasurement.js リファレンス：`s.trackingServer`
  * 例：`metrics.tealium.com` または `tealiumclient.122.2o7.net`
* **セキュアサーバー**
  * （必須）`https` データ収集サーバー。
  * AppMeasurement.js リファレンス：`s.trackingServerSecure`
  * 例：`smetrics.tealium.com` または `tealiumclient.122.2o7.net`
* **イベントシリアル化の自動検出**
  * トリガー文字列内のイベントシリアル化を自動的に検出します。
  * イベントトリガー値にコロン文字（`:`）が含まれている場合は、**No** に構成する必要があります。
* **自動リンクトラッキング**
  * デフォルト値は **Yes** であり、この選択が推奨されます。
  * **No** に構成した場合は、[リンクトラッキング拡張機能](https://docs.tealium.com/link-tracking-extension/)などの別の方法を使用して、自動リンクトラッキングを再現する必要があります。
* **内部リンクフィルター**
  * 内部リンクとして分類するドメインをカンマで区切ったリストです。リンクのクリックが離脱クリックとして Adobe のレポートに記録されないようにするために使用されます。
  * AppMeasurement.js リファレンス：`s.linkInternalFilters`
  * 例：`tealium.com,tealiumiq.com`
* **clearVars の実行**
  * デフォルト値は **No** です。
  * 各トラッキングリクエストの後に、グローバル S オブジェクトに構成された prop、eVar、イベントをクリアします。
  * **データマッピング**画面で `clearVars_in_RPTCallback` パラメータを使用し、`registerPostTrack` コールバック内で `clearVars` アクションが実行されるように割り当てます。
* **S オブジェクト名**
  * （必須）デフォルト名は `s` です。
  * ページ上で Adobe Analytics または AppMeasurement の複数のインスタンスを実行している場合は、別の名前を構成します。
* **名前空間**
  * （任意）訪問の名前空間。
  * Server と Server Secure の末尾が `2o7.net` の場合に、サードパーティCookieにのみ適用されます。
  * AppMeasurement.js リファレンス：`s.visitorNamespace`
* **Experience Cloud ID**
  * （任意）Adobe Experience Cloud ID。
  * バージョン1.3.x以降でサポートされる Visitor API を使用する場合は、ここに Enterprise Cloud ID を入力します。
  * 詳細については、[Adobe：Enterprise Cloud ID Service](https://experienceleague.adobe.com/en/docs/id-service/using/home)を参照してください。
* **Advertising Cloud Viewthrough の実行**
  * バージョン2.17以降でのみ使用できます。
  * Advertising Cloud Viewthrough ファイルを読み込み、ビュースルーデータを送信します。
* **ビュースルー間隔**
  * ビュースルースクリプトの読み込みを試行する間隔をミリ秒単位で構成します。
* **ビュースルー最大試行回数**
  * Analytics のみを実行するようになるまでに、ビュースルーの読み込みを試行する最大回数を構成します。
* **タイムスタンプの送信**
  * 各トラッキング呼び出しでタイムスタンプを送信できるようにします。モバイルデバイスのトラッキングにのみ適用されます。
* **リンクパラメータのデコード**
  * リンクトラッキング変数を1回エンコードするには、`false` に構成します。
  * リンクトラッキング変数を2回エンコードするには、`true` に構成します。
  * デフォルト値は `false` です。
  * 詳細については、[Adobe：`decodeLinkParameters`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/decodelinkparameters)を参照してください。

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)は、サイト上のどこで、いつこのタグのインスタンスを読み込むかを決定します。

推奨される読み込みルール：**すべてのページ**。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明|
|:---------|:------------|
| `adobe_org_id` | <ul><li>Experience Cloud ID</li></ul>|
| `pageName` | <ul><li>ページ名</li><li>ページのURLまたはパス名ではありません。</li><li>代わりに、`Home Page` や `Checkout` など、ビジネスユーザーが認識できる名前にする必要があります。</li></ul>|
| `channel` | <ul><li>サイトのセクション</li></ul>|
| `server` | <ul><li>Webページのドメイン、またはこの宛先に送信されるページをホストするサーバー。</li></ul>|
| `visitorID` | <ul><li>一意の訪問ID。</li><li>最大100文字の英数字。</li><li>ハイフンは使用できません。</li></ul>|
| `s_account` | <ul><li>レポートスイートの上書き。</li><li>この宛先へのマッピングにより、タグ構成で構成されたレポートスイートが上書きされます。</li></ul>|
| `linkTrackVars` | <ul><li>リンク変数の上書き</li></ul>|
| `linkTrackEvents` | <ul><li>リンクイベントの上書き</li></ul>|
| リンク変数の結合 | <ul><li>値は `true` または `false` です。</li></ul>|
| `charSet` | <ul><li>文字セット</li></ul> |
| `collectHighEntropyUserAgentHits`  | <ul><li>ブール値</li><li>高エントロピーのUser-Agent Client Hintsを収集します</li></ul> |
| `contextData.myvar` | <ul><li>カスタムコンテキストデータ。</li><li>コンテキスト変数全般：<ul><li>定義できるコンテキスト変数の数に制限はありません。</li><li>コンテキスト変数に構成できる内容に文字数制限はありません。</li><li>任意の名前を使用できます。</li></ul></li><li>コンテキストデータを使用すると、特定の値を割り当てる変数の名前を定義できます。</li><li>SiteCatalyst が従来送信していた情報に、追加の詳細情報を提供します。</li><li>たとえば異なるサイトのデータを統合する必要がある場合に、実装を標準化しやすくします。</li><li>データの構成は任意です。Tealium を介したマッピングにより、コンテキストデータ変数を定義できます。</li></ul> |
| `contextData.namespace.myvar` | <ul><li>カスタム名前空間を持つカスタムコンテキストデータ。</li><li>変数名の競合を避けるため、名前空間プレフィックスを使用します。</li><li>名前空間 `a` はモバイル実装用に予約されています。</li></ul> |
| `clearVars_in_RPTCallback` | <ul><li>ブール値</li><li>**clearVars の実行**を **Yes** に構成する必要があります。</li><li>`clearVars_in_RPTCallback` が `true` に構成されている場合、`clearVars` アクションは `registerPostTrack`（RPT）コールバック内で実行されます。`false` に構成されている場合、`clearVars` アクションは RPT コールバックの外部で実行されます。</li><li>デフォルトは `false` です。</li></ul> |
### イベント

イベントのマッピングは、ほかの送信先のマッピングとは異なります。

イベントをマッピングするには、次の手順を実行します。

1. **データマッピング**で、**変数**ドロップダウンリストからイベント変数を選択します。
1. **送信先を選択**をクリックし、**イベントトリガー**カテゴリに移動します。
1. **値**フィールドに、マッピングする変数の値を入力します。  
この変数がトリガー文字列になります。
1. **トリガー**ドロップダウンリストから、トリガーするイベントを選択します。  
プラスアイコン（**+**）をクリックすると、値とトリガーの組み合わせを追加できます。

| 送信先名 | 説明 |
|:-----------------|:-------------|
| 値 | <ul><li>割り当てられたイベントをトリガーする、マッピング済み変数の値。</li></ul> |
| トリガー | <ul><li>トリガーするイベント。</li><li>次から選択します。<ul><li>製品表示の場合は **prodView**。</li><li>新しいショッピングカートを開く、または初期化する場合は **scOpen**。</li><li>ショッピングカートに商品を追加する場合は **scAdd**。</li><li>ショッピングカートから商品を削除する場合は **scRemove**。</li><li>ショッピングカートを表示する場合は **scView**。</li><li>チェックアウトを開始する場合は **scCheckout**。</li><li>注文を完了する場合は **purchase**。</li><li>カスタムイベントを構成する場合は **event1**～**event1000**。<br>**注：イベント101～1000は、ライブラリバージョン1.4以降でのみ使用できます。**<ul><li>SiteCatalystでは、成功イベントとも呼ばれる100個のカスタムイベントを使用できます。</li><li>通常、これらのイベントはログインやフォーム表示など、サイト上で発生する特定の事象をカウントし、通常は値を含みません。</li></ul></li></ul></li></ul> |

#### 製品レベルのイベント

SiteCatalystには、製品固有のアクションを送信するための送信先が100個用意されています。

| 送信先名 | 説明 |
|:----------------------------------------------|:-----------------------------|
| `PRODUCTS_event1`～`PRODUCTS_event100` | 割り当てる製品イベント。 |

#### 値イベント

SiteCatalystには、値イベントを送信するための送信先が100個用意されています。

| 送信先名 | 説明 |
|:----------------------------------------|:---------------------------|
| `VALUE_event1`～`VALUE_event100` | 割り当てる値イベント。 |

#### Prop

SiteCatalystでは、トラフィック変数とも呼ばれるカスタムpropを使用できます。

| 送信先名 | 説明 |
|:----------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `PRODUCTS_event1`～`PRODUCTS_event100` | <ul><li>割り当てる製品イベント。</li><li>75を超えるpropは、マッピングツールボックスに組み込まれていません。</li></ul> |

SiteCatalystでは、トラフィック変数とも呼ばれる75個のカスタムpropを使用できます。propには、ページビューを超えて保持することを意図していないデータが格納されます。propを別の変数と関連付ける場合は、両方の変数が同じページで構成されるようにしてください。製品文字列で渡される、またはシリアル化される特定の数値を保持するには、イベントを使用します。

カスタム送信先をマッピングするには、次の手順を実行します。

1. 変数を任意のprop送信先にマッピングします。
1. 上部のテキストボックスに、選択した組み込み送信先の代わりとなるカスタム送信先を入力します。
1. ほかの変数のマッピングを続行するか、**完了**をクリックして終了します。

#### eVar

| 送信先名 | 説明 |
|:-------------------------------|:-------------|
| `eVar0` | <ul><li>キャンペーン。</li><li>キャンペーン／プロモーションのトラッキング用。</li></ul> |
| `eVar1`～<br> `eVar250` | <ul><li>SiteCatalystでは、コンバージョン変数とも呼ばれる250個のeVarを使用できます。</li><li>`evar76`～`evar250`は、ライブラリバージョン1.4以降でのみ使用できます。</li><li>eVarには、単一のページビューを超えて保持することを意図したデータが格納されます。また、Omniture内でのレポート構成に応じて、あるeVarのデータを別の変数と関連付けるために使用できます。</li><li>通常、eVarには内部検索語、A/Bテスト、キャンペーン／プロモーションのトラッキング、マーチャンダイジングカテゴリ、ユーザータイプなどが含まれます。</li></ul> |

#### マーチャンダイジングeVar

マーチャンダイジングeVarを使用すると、製品文字列で指定するカテゴリに加えて、製品を何らかの値に関連付けることができます。

| 送信先名 | 説明 |
|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `eVar0` | <ul><li>キャンペーン。</li><li>キャンペーン／プロモーションのトラッキング用。</li></ul> |
| `PRODUCTS_eVar1`～`PRODUCTS_eVar75` | <ul><li>SiteCatalystでは、コンバージョン変数とも呼ばれる250個のeVarパラメータを使用できます。</li><li>eVarには、単一のページビューを超えて保持することを意図したデータが格納されます。また、Omniture内でのレポート構成に応じて、あるeVarのデータを別の変数と関連付けるために使用できます。</li></ul> 通常、eVarには内部検索語、A/Bテスト、キャンペーン／プロモーションのトラッキング、マーチャンダイジングカテゴリ、ユーザータイプなどが含まれます。 |

#### コマース

AppMeasurementタグではEコマースが有効になっているため、デフォルトの[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)のマッピングが自動的に使用されます。拡張機能のマッピングを上書きする場合、または特定のEコマース変数が拡張機能で提供されていない場合を除き、通常、このカテゴリで手動マッピングを行う必要はありません。

製品文字列を含む複数のSiteCatalyst変数には、Eコマース拡張機能によって値が自動的に入力されます。SiteCatalystは製品文字列を使用して、製品情報、収益、販売数量、および購入に関するその他の情報を取得します。標準的な製品文字列は次のようになります。

![](https://docs.tealium.com/images/client-side-tags/product-string.png)

##### 製品文字列のベストプラクティス：

* セミコロン `;` は、製品文字列内のほとんどの項目に使用される標準の区切り文字です。
* 複数のマーチャンダイジングeVarは、パイプ（`|`）文字で区切ります。
* 複数の製品インスタンスは、コンマ（`,`）で区切ります。
* 合計価格は、単価に数量を掛けた値です。Eコマース拡張機能の合計価格（`_ctotal`）出力は、製品文字列に自動的にはマッピングされません。
* SiteCatalystのベストプラクティスでは、カテゴリを空のままにすることが推奨されます。これは、SiteCatalystで製品のカテゴリを一度構成すると変更できないためです。ただし、後でカテゴリを変更できなくても問題がない場合、Tealiumではコンバージョン時にカテゴリを構成できます。

#### Eコマース送信先

次のEコマース送信先がツールボックスに組み込まれています。

| 送信先名 | 説明 | Eコマース拡張機能の変数 |
|:---------------------------|:--------------------------------------------------------------------|:-----------------------------|
| purchaseID | <ul><li>この送信先の一意の注文識別子。</li></ul> | `_corder` |
| transactionID | <ul><li>オフラインデータをオンライントランザクションに関連付けます。</li></ul> | 該当なし |
| state | <ul><li>コンバージョンで指定された州の名前。</li></ul> | 該当なし |
| zip | <ul><li>コンバージョンで指定された郵便番号。</li></ul> | 該当なし |
| 製品ID（配列） | <ul><li>製品配列内の各製品の一意のID。</li></ul> | `_cprod` |
| 製品カテゴリ（配列） | <ul><li>製品配列内の各カテゴリの名前。</li></ul> | `_ccat` |
| 製品数量（配列） | <ul><li>製品配列内の各製品の数量。</li></ul> | `_cquan` |
| 製品価格（配列） | <ul><li>製品配列内の各製品の単価。</li></ul> | `_cprice` |

#### その他

| 変数 | 説明 |
|:---------------------------------|:------------|
| リンクトラッキング - doneActionパラメータ | （H25のみ） |
| リスト1 | |
| リスト2 | |
| リスト3 | |
#### モバイル

| 変数 | 説明 |
|:---------|:---------------|
| アプリ ID | (`contextData.a.AppID`) |
| デバイス名 | (`contextData.a.DeviceName`) |
| オペレーティングシステム | (`contextData.a.OSEnvironment`) |
| オペレーティングシステムのバージョン | (`contextData.a.OSVersion`) |
| 通信事業者名 | (`contextData.a.CarrierName`) |
| 解像度 | (`contextData.a.Resolution`) |
| インストール日 | (`contextData.a.InstallDate`) |
| 起動回数 | (`contextData.a.Launches`) |
| 初回使用からの日数 | (`contextData.a.DaysSinceFirstUse`) |
| 前回使用からの日数 | (`contextData.a.DaysSinceLastUse`) |
| インストール | (`contextData.a.InstallEvent`) |
| アップグレード | (`contextData.a.UpgradeEvent`) |
| 起動 | (`contextData.a.LaunchEvent`) |
| クラッシュ | (`contextData.a.CrashEvent`) |
| 前回のセッション時間 | (`contextData.a.PrevSessionLength`) |
| 時刻 | (`contextData.a.HourOfDay`) |
| 曜日 | (`contextData.a.DayOfWeek`) |
| 前回のアップグレードからの日数 | (`contextData.a.DaysSinceLastUpgrade`) |
| アップグレード後の起動回数 | (`contextData.a.LaunchesSinceUpgrade`) |
| 1 日あたりのエンゲージユーザー数 | (`contextData.a.DailyEngUserEvent`) |
| 1 か月あたりのエンゲージユーザー数 | (`contextData.a.MonthlyEngUserEvent`) |
| `disable_wake_track` | <ul><li>ウェイクトラッキングを無効化</li><li>値は `true` または `false` です。</li></ul> |
| `disable_sleep_track` | <ul><li>スリープトラッキングを無効化</li><li>値は `true` または `false` です。</li></ul> |
| `send_timestamp` | <ul><li>タイムスタンプ送信の切り替え</li><li>値は `true` または `false` です。</li></ul> |
| `timestamp` | <ul><li>タイムスタンプ</li><li>ISO 8601 形式</li><li>Unix 時間</li></ul> |

#### リンクトラッキング

| 変数 | 説明 |
|:-----------|:------------|
| `linkType` | リンクタイプ |
| `linkName` | リンク名 |

### イベントシリアル化の検出

AppMeasurement タグは、データレイヤーのトリガー値内にある[イベントシリアル化](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/events/event-serialization)を自動的に検出します。タグが発火すると、**Events** タブでマッピングされたトリガー文字列とデータレイヤー内のトリガー値との照合を試み、いずれかのトリガーにコロンが含まれているかどうかを確認します。

* **イベントシリアル化の検出：オン**  
イベントシリアル化の検出をオン（デフォルト構成）にすると、タグはコロンの後ろにあるトリガー値を検出し、残りの文字列をマッピング済みのトリガーと照合します。完全に一致した場合、イベントがシリアル化されます。
* **イベントシリアル化の検出：オフ**  
イベントシリアル化の検出をオフにすると、タグはコロンを検出しません。タグは両方のトリガー値全体の照合を試みます。マッピング済みのトリガー文字列にコロンが含まれる場合は、この構成を強く推奨します。コロンを含む値でイベントを正しくトリガーするには、イベントシリアル化の検出をオフにする必要があります。


<blockquote>
Whether event serialization detection is on or off, serials mapped directly with the **Event Serialization** tab always take precedence (see [scenario 3 example](#scenario3)).
</blockquote>


以下のシナリオは、イベントシリアル化の検出が、コロンを含むトリガー値と含まないトリガー値をどのように解釈するかを理解するのに役立ちます。


<blockquote>
Throughout this section, the term "mapped trigger" refers to the value in the tag's data mapping configuration and the term "data layer trigger" refers to the value found in the data layer of your website.
</blockquote>


#### 例：コロンを含まないマッピング済みトリガー

たとえば、ページに `fireEvt` が含まれている場合に `prodView` イベントをトリガーしてシリアル化するには、次の操作を行います。

1. Event Serialization タブで、UDO 変数 `serial` を `SERIAL_prodView` にマッピングします。
1. Events で、UDO 変数 `trigger` を `prodView` にマッピングします。
1. `fireEvt` を `prodView` のトリガー文字列としてマッピングします。  
![](https://docs.tealium.com/images/client-side-tags/trigger-without-colon.jpeg)

データレイヤーでは、さまざまなシナリオが発生する可能性があります。

#### シナリオ 1：データレイヤーのトリガーが `fireEvt` で、`serial` の値が空の場合

```js
var utag_data = {
  trigger: "fireEvt",
  serial: ""
}

```

* **イベントシリアル化の検出：オン**  
タグは `fireEvt` をマッピング済みのトリガーと照合し、ページ上で `prodView` を正常に発火させます。ただし、シリアル化は行われません。
* **イベントシリアル化の検出：オフ**  
結果は上記と同じです。

正常なネットワーク呼び出しは次のようになります。

![](https://docs.tealium.com/images/client-side-tags/scene-1-network-call-.png)

#### シナリオ 2：データレイヤーのトリガーが `fireEvt:123` で、`serial` の値が空の場合

```
var utag_data = {
  trigger: "fireEvt:123",
  serial: ""
}
```

* **イベントシリアル化の検出：オン**  
タグは `123` をシリアル化した後、`fireEvt` をマッピング済みのトリガーと照合し、ページ上で `prodView` を正常に発火させます。  
![](https://docs.tealium.com/images/client-side-tags/scene-2-network-call.png)

* **イベントシリアル化の検出：オフ**  
タグは `fireEvt:123` をマッピング済みのトリガーと照合できないため、ページ上で `prodView` は発火しません。

#### シナリオ 3：データレイヤーのトリガーが `fireEvt:123` で、serial の値が `456` の場合 {#scenario3}

```
var utag_data = {
  trigger: "fireEvt:123",
  serial: "456"
}
```

* **イベントシリアル化の検出：オン**  
最初に、タグは `123` をシリアル化し、`fireEvt` をマッピング済みのトリガーと照合します。その後、`prodView` が正常に発火し、`123` ではなく `456` でシリアル化されます。  
これは、イベントシリアル化のマッピングで検出されたシリアル値（`456`）が、イベントシリアル化の検出で検出された値（`123`）よりも優先されるためです。  
![](https://docs.tealium.com/images/client-side-tags/scene-3-network-call.png)
* **イベントシリアル化の検出：オフ**  
タグは `fireEvt:123` をマッピング済みのトリガーと照合できません。そのため、ページ上で `prodView` は発火しません。

#### 例：コロンを含むマッピング済みトリガー

この例はシナリオ 2 と同じ流れですが、マッピング済みのトリガーは `fireEvt` ではなく `fireEvt:123` です。

![](https://docs.tealium.com/images/client-side-tags/trigger-with-colon.png)

#### シナリオ：データレイヤーのトリガーが `fireEvt:123` の場合

```js
var utag_data = {
  trigger: "fireEvt:123",
  serial: ""
}
```

* **イベントシリアル化の検出：オン**  
タグは `123` をシリアル化しますが、`fireEvt` をマッピング済みのトリガーと照合できません。そのため、ページ上で `prodView` は発火しません。
* **イベントシリアル化の検出：オフ**  
タグは `fireEvt:123` をマッピング済みのトリガーと正常に照合し、`prodView` が正常に発火します。このため、文字列にコロンが含まれる場合は、イベントシリアル化の検出をオフにすることをお勧めします。

## 高度な構成

### s.events の構成

Tealium では、`s.event` 文字列の構成を支援する `u.addEvent()` という関数を提供しています。このメソッドは `s.events` の末尾に新しい値を追加するため、以前に構成したすべてのイベントを維持しながら、必要に応じて別のイベントを追加できます。このメソッドを使用するには、`sc_events` という名前の変数を構成に追加します。

`u.addEvent` を使用して `s.events` をカスタマイズするには、次の手順を実行します。

1. [Set Data Values](https://docs.tealium.com/set-data-values-extension/) 拡張機能を追加します。
1. **Scope** を Adobe Analytics タグに構成します。
1. **Set** メニューから **sc_events** を選択します。
1. **To** メニューから **JS Code** を選択します。
1. テキストフィールドに `u.addEvent("CUSTOM_EVENT")` と入力します。  
ここで、`CUSTOM_EVENT` は `s.events `文字列に追加するイベント（`event10` など）です。
1. 1 回の手順で複数のイベントを追加するには、次のように配列を `u.addEvent` に渡します。  
`u.addEvent(["event1","event2","scView"]);`

関数に渡す文字列に値を直接追加するには、`u.addEvent(['event500=500', 'event501=' + b.demo_event_value]);` を使用します。

関数に渡す文字列にシリアル化を直接追加するには、`u.addEvent("event78:" + b.booking_reference);` を使用します。
## サポート対象バージョン

以下の AppMeasurement for JavaScript コードバージョンがサポートされています。

* 2.26.0 バンドル最適化版
* 2.26.0
* 2\.25.0
* 2\.24.0
* 2\.23.0
* 2\.22.4
* 2\.22.3
* 2\.22.0
* 2\.21.0
* 2\.20.0
* 2\.18.0
* 2\.17.0
* 2\.15.0
* 2\.14.0
* 2\.12.0
* 2\.9.0
* 2\.8.2
* 2\.7.0
* 2\.6.0
* 2\.4.0
* 2\.3.0
* 2\.1.0
* 1\.8.0
* 1\.6.3
* 1.6.1
* 1.6.0
* 1\.5.3
* 1.5.2
* 1.5.1
* 1\.4.1
* 1\.3.2
* 1\.2.2
* 1.2.1
* 1\.0.1

### リリースノート

##### v2.23.0 リリース日：9月23日、

* 高エントロピーのユーザーエージェント情報のサポートを追加しました。

##### v2.22.3 2021年12月21日リリース

##### v2.20.0 2020年3月5日リリース

* セキュリティ関連の問題を修正するため、JSLint の警告を抑制するように IE の検出処理を更新しました。

##### v2.18.0 2020年2月13日リリース

* `writeSecureCookies` 変数を構成することで、AppMeasurement が Cookie に Secure 属性を強制的に付与できるようになりました。この変数をサポートするには、クライアントの Web サイト全体を HTTPS で安全に配信する必要があります。

##### v2.17.0 2019年8月23日リリース

* Baidu のクエリ文字列並べ替えのサポートを追加しました。
* オプトインを待機している間にキューに追加されたヒットで、古い訪問値が使用される問題を修正しました。

##### v2.15.0 2019年7月15日リリース

* Activity Map 拡張機能に ActivityMap のスクロール到達度トラッキングを追加しました（AN-172949）。

* AppMeasurement に DIL 9.2 を追加しました（AN-182472）。

##### v2.9.0 2018年5月24日リリース


<blockquote>
Experience Cloud ID Service を使用するお客様には、Visitor API 3.0 以降が必要です。Adobe では、at.js や AppMeasurement.js など、関連するコードライブラリを更新する際に、Visitor API も最新バージョンへアップグレードすることを推奨しています。
</blockquote>


* ID のリクエストに更新された Visitor インターフェイスを使用するように AppMeasurement を更新しました。（AN-151483）
* リンクトラッキングをオフにした後もリンクトラッキング Cookie が書き込まれる問題を修正しました。（AN-156332）
* `registerPreTrackCallback` および `registerPostTrackCallback` を複数回呼び出すと、コールバック関数のシグネチャが壊れる問題を修正しました。（AN-158566）

##### v2.8.2 2018年4月12日リリース

* ID のリクエストに更新された Visitor インターフェイスを使用するように AppMeasurement を更新しました。
* リンクトラッキング Cookie に関する問題を修正しました。
* AppMeasurement のデフォルトの Cookie 有効期間を5年から2年に短縮しました。
* Visitor API（別名 Enterprise Cloud ID Service）バージョン 3.1.2 をサポートします。

##### v2.7.0 2018年1月18日リリース

* Internet Explorer（IE）バージョン6～9のサポートを廃止しました。
* DIL v7.00 が含まれています。
* Visitor API（別名 Marketing Cloud ID Service）バージョン 3.0 をサポートします。

##### v2.6.0 2017年11月9日リリース

* `s_gl` が呼び出されたときに、AppMeasurement ライブラリが必ずしも正しいアカウントの組み合わせを構成しない問題を修正しました。（AN-152153）
* `dil.js` 6.12（Audience Manager モジュール）を追加しました。
* Visitor API 2.5.0 をサポートします。

##### v2.3.0 2017年8月22日リリース

* `s.Util.getQueryParam` が `#` を取得していた不具合を修正しました。
* 最新バージョンの `dil.js`（v6.10）を追加しました。
* 複数の AppMeasurement インスタンス化順序をサポートします。
* Visitor API（別名 Marketing Cloud ID Service）バージョン 2.2.0 をサポートします。

##### v2.1.0 2017年5月11日リリース

* AppMeasurement JavaScript 2.1.0 をサポートします。
* Marketing Cloud ID Service バージョン 2.1.0 をサポートします。
* 最新バージョンの `dil.js` を追加しました。
* ページのリファラーを上書きする `adobe_mc_ref` パラメーターのサポートを追加しました。
* `mcorgid` パラメーターを追加しました。
* `cp`（customerPerspective）パラメーターを追加しました。

##### v1.8.0 2017年3月10日リリース

* AppMeasurement JavaScript 1.8.0 をサポートします。
* Marketing Cloud ID Service バージョン 2.0.0 をサポートします。
* 2つの呼び出しフック、[`s.registerPreTrackCallback`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/registerpretrackcallback) および [`s.registerPostTrackCallback`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/registerposttrackcallback) を追加しました。

##### v1.6.3 2016年8月23日リリース

* AppMeasurement がリクエスト接続を途中で終了する問題を修正しました。
* AppMeasurement が Visitor API 内の誤った難読化メソッドを呼び出す問題を修正しました。
* 「Attribute only valid on v:image」という JavaScript エラーが発生する問題を修正しました。
* Marketing Cloud ID のサポート（別名 Visitor API）を、Marketing Cloud ID Service Tag という新しいタグとして分離しました。


<blockquote>
Marketing Cloud ID Service Tag は、プロファイル内の他のすべての Adobe タグ（AppMeasurement を含む）よりも先に読み込む必要があります。そうしないと、訪問トラッキングの整合性が失われます。このタグを最初に読み込むには、All Pages で[バンドル構成](https://docs.tealium.com/tag-advanced-settings/)を有効にし、他の Adobe タグよりも先に読み込んでください。
</blockquote>


[Adobe AppMeasurement の完全なリリースノート](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates)を参照してください。

##### v1.6.1 2016年7月28日リリース

以下の更新は、AppMeasurement のイベント、値イベント、およびイベントのシリアル化に影響します。

* Data Mapping ツールボックスに、新しい Event Serialization マッピングタブを追加しました。
* AppMeasurement Tag の構成に、Event Serialization をオンまたはオフにするための新しいドロップダウンリストを追加しました。

##### v1.6.1 2016年7月14日リリース

* 新しいバージョン 1.6.1 を追加しました。
* Visitor API バージョン 1.5.7 および 1.5.6 をサポートします。
* Firefox でリンククリックのトラッキングを処理するメカニズムを改善しました。

[Adobe AppMeasurement の完全なリリースノート](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates)を参照してください。

## ベンダーのドキュメント

* [Adobe Experience League：AppMeasurement for JavaScript について](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview)
* [Adobe Experience League：AppMeasurement のリリース履歴](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates)
* [Adobe Experience League：Activity Map の有効化](https://experienceleague.adobe.com/en/docs/analytics/analyze/activity-map/getting-started)
* [Adobe Experience League：モバイル指標について](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/overview)
* [Adobe Experience League：モバイル指標リファレンス](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/lifecycle-metrics)