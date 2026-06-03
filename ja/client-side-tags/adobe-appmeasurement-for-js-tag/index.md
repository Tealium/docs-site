---
title: Adobe Analytics AppMeasurement for JS タグ構成ガイド
description: この記事では、iQタグ管理アカウントでAdobe Analytics AppMeasurement for JSタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-appmeasurement-for-js-tag/
---
## タグのヒント

* Adobe Experience Cloud IDサービスを使用するには、このタグを追加する前にAdobe Experience Cloud IDサービスタグを追加してください。
* すべての古いH26機能がAppMeasurementタグでサポートされているわけではありません。
* サーバー値を正しく入力してください。例えば、サードパーティのサーバーは `112.2o7.net` や `122.2o7.net` になることがあります。
* モバイル用AppMeasurementを使用する場合、アプリケーションにTealiumモバイルSDKを実装する必要があります。
* サポートされているプラグインのリストについては、[Adobe: AppMeasurementプラグインの概要](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/plugins/impl-plugins)を参照してください。
* 追加情報については、[Adobe: JavaScriptでAdobe Analyticsを実装する](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview)を参照してください。

## タグの構成

タグマーケットプレイスにアクセスして、Adobe Analytics AppMeasurement for JSタグを追加します（[タグの追加方法についてはこちら]()を参照）。

タグを追加した後、以下の構成を構成します：

* **コードバージョン**
  * `AppMeasurement.js` ライブラリのバージョン。
* **デバイスタイプ**
  * 実装のプラットフォームに基づいて以下から選択してください：
    * **標準** デスクトップウェブサイトのインストール用。
    * **モバイルアプリ** [Tealium for iOS](/ja/platforms/ios-swift/) や [Tealium for Android](/ja/platforms/android-kotlin/) でのネイティブモバイルインストール用。
* **レポートスイート**
  * (必須) マッピングを使用して動的にレポートスイートを構成する場合でも、デフォルト値を構成してください。
  * 使用するデフォルトのレポートスイート。Dynamic Acct Listで構成された値に基づいて変更される場合があります。
  * AppMeasurement.jsの参照：`s.account`
* **サーバー**
  * (必須) データ収集サーバー。
  * AppMeasurement.jsの参照：`s.trackingServer`
  * 例：`metrics.tealium.com` や `tealiumclient.122.2o7.net`
* **サーバーセキュア**
  * (必須) `https` データ収集サーバー。
  * AppMeasurement.jsの参照：`s.trackingServerSecure`
  * 例：`smetrics.tealium.com` や `tealiumclient.122.2o7.net`
* **自動イベントシリアライゼーション検出**
  * トリガー文字列内のイベントシリアライゼーションを自動的に検出します。
  * イベントトリガー値にコロン文字(`:`)が含まれている場合は、**いいえ**に構成する必要があります。
* **自動リンクトラッキング**
  * デフォルト値は**はい**で、推奨される選択です。
  * **いいえ**に構成する場合は、[リンクトラッキング拡張]()などの他の方法を使用して自動リンクトラッキングを再現する必要があります。
* **内部リンクフィルター**
  * ドメインをカンマ区切りでリストアップし、内部として分類されることで、リンククリックがAdobeレポートの退出クリックとして報告されないようにします。
  * AppMeasurement.jsの参照：`s.linkInternalFilters`
  * 例：`tealium.com,tealiumiq.com`
* **Run clearVars**
  * デフォルト値は**いいえ**です。
  * 各トラッキングリクエスト後にグローバルS-Objectに構成されたprops、eVars、およびイベントをクリアします。
  * **データマッピング**画面で、`registerPostTrack`コールバック内で`clearVars`アクションが発生するように`clearVars_in_RPTCallback`パラメータを割り当てます。
* **S-Object名**
  * (必須) デフォルト名は`s`です。
  * ページ上でAdobe AnalyticsまたはAppMeasurementの複数のインスタンスを実行している場合は、異なる名前を構成してください。
* **名前空間**
  * (オプション) 訪問の名前空間。
  * サーバーとサーバーセキュアが`2o7.net`で終わる場合にのみ、サードパーティのクッキーに適用されます。
  * AppMeasurement.jsの参照：`s.visitorNamespace`
* **Experience Cloud ID**
  * (オプション) あなたのAdobe Experience Cloud ID。
  * バージョン1.3.x以降でサポートされているVisitor APIを使用する場合は、ここにEnterprise Cloud IDを入力してください。
  * 詳細については、[Adobe: Enterprise Cloud IDサービス](https://experienceleague.adobe.com/en/docs/id-service/using/home)を参照してください。
* **Run Advertising Cloud Viewthrough**
  * バージョン2.17以降でのみ利用可能です。
  * Advertising Cloud Viewthroughファイルをロードし、viewthroughデータを送信します。
* **Viewthrough Interval**
  * viewthroughスクリプトをロードする試みの間隔をミリ秒単位で構成します。
* **Viewthrough Max Tries**
  * viewthroughをロードする最大試行回数を構成します。それを超えると、アナリティクスのみを実行します。
* **Send Timestamp**
  * トラッキングコールごとにタイムスタンプを送信することを許可します。モバイルデバイスのトラッキングにのみ適用されます。
* **Decode Link Parameters**
  * リンクトラッキング変数を一度エンコードするには`false`に構成します。
  * リンクトラッキング変数を二度エンコードするには`true`に構成します。
  * デフォルト値は`false`です。
  * 詳細については、[Adobe: `decodeLinkParameters`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/decodelinkparameters)を参照してください。

## ロードルール

[ロードルール]()は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

推奨されるロードルール：**すべてのページ**。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明|
|:---------|:------------|
| `adobe_org_id` | &lt;ul&gt;&lt;li&gt;Experience Cloud ID&lt;/li&gt;&lt;/ul&gt;|
| `pageName` | &lt;ul&gt;&lt;li&gt;ページ名&lt;/li&gt;&lt;li&gt;これはページのURLやパス名ではありません。&lt;/li&gt;&lt;li&gt;ビジネスユーザーが認識するものであるべきです。例：`ホームページ`や`チェックアウト`。&lt;/li&gt;&lt;/ul&gt;|
| `channel` | &lt;ul&gt;&lt;li&gt;あなたのサイトのセクション&lt;/li&gt;&lt;/ul&gt;|
| `server` | &lt;ul&gt;&lt;li&gt;ウェブページのドメインまたはそのページをホストするサーバー。&lt;/li&gt;&lt;/ul&gt;|
| `visitorID` | &lt;ul&gt;&lt;li&gt;ユニークな訪問ID。&lt;/li&gt;&lt;li&gt;最大100文字の英数字。&lt;/li&gt;&lt;li&gt;ハイフンを含むことはできません。&lt;/li&gt;&lt;/ul&gt;|
| `s_account` | &lt;ul&gt;&lt;li&gt;レポートスイートのオーバーライド。&lt;/li&gt;&lt;li&gt;この宛先へのマッピングは、タグ構成で構成されたレポートスイートをオーバーライドします。&lt;/li&gt;&lt;/ul&gt;|
| `linkTrackVars` | &lt;ul&gt;&lt;li&gt;リンク変数のオーバーライド&lt;/li&gt;&lt;/ul&gt;|
| `linkTrackEvents` | &lt;ul&gt;&lt;li&gt;リンクイベントのオーバーライド&lt;/li&gt;&lt;/ul&gt;|
| リンク変数の結合 | &lt;ul&gt;&lt;li&gt;値は`true`または`false`です。&lt;/li&gt;&lt;/ul&gt;|
| `charSet` | &lt;ul&gt;&lt;li&gt;文字セット&lt;/li&gt;&lt;/ul&gt; |
| `collectHighEntropyUserAgentHits`  | &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;高エントロピーのユーザーエージェントヒントを収集&lt;/li&gt;&lt;/ul&gt; |
| `contextData.myvar` | &lt;ul&gt;&lt;li&gt;カスタムコンテキストデータ。&lt;/li&gt;&lt;li&gt;一般的にコンテキスト変数：&lt;ul&gt;&lt;li&gt;定義できるコンテキスト変数の数に制限はありません。&lt;/li&gt;&lt;li&gt;コンテキスト変数に配置できる文字に制限はありません。&lt;/li&gt;&lt;li&gt;好きな名前を含めることができます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;コンテキストデータを使用すると、特定の値を割り当てる変数の名前を定義できます。&lt;/li&gt;&lt;li&gt;SiteCatalystが従来伝えるものに追加の詳細を提供します。&lt;/li&gt;&lt;li&gt;必要に応じて実装を標準化する能力を簡素化します。例えば、異なるサイトからのデータを組み合わせる場合などです。&lt;/li&gt;&lt;li&gt;データの整理はあなたの裁量に任されています。Tealiumを通じてコンテキストデータ変数を定義することができます。&lt;/li&gt;&lt;/ul&gt; |
| `contextData.namespace.myvar` | &lt;ul&gt;&lt;li&gt;カスタム名前空間を持つカスタムコンテキストデータ。&lt;/li&gt;&lt;li&gt;変数名の競合を避けるために名前空間プレフィックスを使用します。&lt;/li&gt;&lt;li&gt;名前空間`a`はモバイル実装用に予約されています。&lt;/li&gt;&lt;/ul&gt; |
| `clearVars_in_RPTCallback` | &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;**Run clearVars**を**はい**に構成する必要があります。&lt;/li&gt;&lt;li&gt;`clearVars_in_RPTCallback`が`true`に構成されている場合、`clearVars`アクションは`registerPostTrack`（RPT）コールバック内で発生します。`false`に構成されている場合、`clearVars`アクションはRPTコールバックの外で発生します。&lt;/li&gt;&lt;li&gt;デフォルトは`false`です。&lt;/li&gt;&lt;/ul&gt; |


### イベント

イベントのマッピングは他のデスティネーションのマッピングと異なります。

イベントをマッピングするには、以下の手順を使用します：

1. **データマッピング**の下で、**変数**ドロップダウンリストからイベント変数を選択します。
1. **デスティネーションを選択**をクリックし、**イベントトリガー**カテゴリに進みます。
1. **値**フィールドにマッピングされる変数の値を入力します。  
この変数がトリガー文字列になります。
1. **トリガー**ドロップダウンリストからトリガーしたいイベントを選択します。  
プラスアイコン（**&#43;**）をクリックして、追加の値/トリガーの組み合わせを追加できます。

| デスティネーション名 | 説明 |
|:-----------------|:-------------|
| 値 | &lt;ul&gt;&lt;li&gt;割り当てられたイベントをトリガーするマップされた変数の値。&lt;/li&gt;&lt;/ul&gt; |
| トリガー | &lt;ul&gt;&lt;li&gt;トリガーするイベント。&lt;/li&gt;&lt;li&gt;選択:  &lt;ul&gt;&lt;li&gt;**prodView** 製品ビュー用。&lt;/li&gt;&lt;li&gt;**scOpen** 新しいショッピングカートを開く/初期化するため。&lt;/li&gt;&lt;li&gt;**scAdd** ショッピングカートにアイテムを追加するため。&lt;/li&gt;&lt;li&gt;**scRemove** ショッピングカートからアイテムを削除するため。&lt;/li&gt;&lt;li&gt;**scView** ショッピングカートを表示するため。&lt;/li&gt;&lt;li&gt;**scCheckout** チェックアウトを開始するため。&lt;/li&gt;&lt;li&gt;**purchase** 注文を完了するため。&lt;/li&gt;&lt;li&gt;**event1** から **event1000** カスタムイベントを構成するため。 &lt;br&gt;**注: イベント101-1000はライブラリバージョン1.4以降でのみ利用可能です。** &lt;ul&gt;&lt;li&gt;SiteCatalystでは、成功イベントとも呼ばれる100のカスタムイベントを使用できます。&lt;/li&gt;&lt;li&gt;これらのイベントは通常、サイト上で発生する特定の事象を数え、通常は値を含まないものです（例：ログイン、フォームビューなど）。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

#### 製品レベルのイベント

SiteCatalystは製品固有のアクションを送信するための100のデスティネーションを提供します。

| デスティネーション名 | 説明 |
|:----------------------------------------------|:-----------------------------|
| `PRODUCTS_event1` から `PRODUCTS_event100` | 割り当てる製品イベント。 |

#### 値イベント

SiteCatalystは値イベントを送信するための100のデスティネーションを提供します。

| デスティネーション名 | 説明 |
|:----------------------------------------|:---------------------------|
| `VALUE_event1` から `VALUE_event100` | 割り当てる値イベント。 |

#### Props

SiteCatalystでは、カスタムprops（トラフィック変数とも呼ばれます）を使用できます。

| デスティネーション名 | 説明 |
|:----------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `PRODUCTS_event1` から `PRODUCTS_event100` | &lt;ul&gt;&lt;li&gt;割り当てる製品イベント。&lt;/li&gt;&lt;li&gt;75以上のPropsはマッピングツールボックスに組み込まれていません。&lt;/li&gt;&lt;/ul&gt; |

SiteCatalystでは、75のカスタムprops（トラフィック変数とも呼ばれます）を使用できます。Propsはページビューを超えて持続することを意図していないデータを含みます。他の変数とpropを相関させたい場合は、両方の変数が同じページで構成されていることを確認してください。製品文字列で渡されたりシリアライズされたりする特定の数値を保持するためにイベントを使用します。

カスタムデスティネーションをマッピングするには、以下の手順を使用します：

1. 変数を任意のpropデスティネーションにマッピングします。
1. 上部のテキストボックスに、選択した組み込みデスティネーションの代わりにカスタムデスティネーションを入力します。
1. 他の変数のマッピングを続けるか、**完了**をクリックして終了します。

#### eVars

| デスティネーション名 | 説明 |
|:-------------------------------|:-------------|
| `eVar0` | &lt;ul&gt;&lt;li&gt;キャンペーン。&lt;/li&gt;&lt;li&gt;キャンペーン/プロモーション追跡用&lt;/li&gt;&lt;/ul&gt; |
| `eVar1` から &lt;br&gt; `eVar250` | &lt;ul&gt;&lt;li&gt;SiteCatalystでは、250のeVars（変換変数とも呼ばれます）を使用できます。&lt;/li&gt;&lt;li&gt;`evar76` から `evar250` はライブラリバージョン1.4以降でのみ利用可能です。&lt;/li&gt;&lt;li&gt;eVarsはページビューを超えて持続するデータを含み、Omniture内でレポートを構成する方法に応じて他の変数からのデータと相関させることができます。&lt;/li&gt;&lt;li&gt;eVarsは通常、内部検索用語、A/Bテスト、キャンペーン/プロモーション追跡、マーチャンダイジングカテゴリ、ユーザータイプを含みます。&lt;/li&gt;&lt;/ul&gt; |

#### マーチャンダイジングeVars

マーチャンダイジングeVarsは、製品文字列で指定するカテゴリに加えて、製品にいくつかの値を関連付けることを可能にします。

| デスティネーション名 | 説明 |
|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `eVar0` | &lt;ul&gt;&lt;li&gt;キャンペーン。&lt;/li&gt;&lt;li&gt;キャンペーン/プロモーション追跡用&lt;/li&gt;&lt;/ul&gt; |
| `PRODUCTS_eVar1` から `PRODUCTS_eVar75` | &lt;ul&gt;&lt;li&gt;SiteCatalystでは、250のeVarパラメータ（変換変数とも呼ばれます）を使用できます。&lt;/li&gt;&lt;li&gt;eVarsはページビューを超えて持続するデータを含み、Omniture内でレポートを構成する方法に応じて他の変数からのデータと相関させることができます。&lt;/li&gt;&lt;/ul&gt; eVarsは通常、内部検索用語、A/Bテスト、キャンペーン/プロモーション追跡、マーチャンダイジングカテゴリ、ユーザータイプを含みます。 |

#### コマース

AppMeasurementタグはeコマース対応であり、デフォルトで[E-Commerce Extension]()のマッピングを自動的に使用します。拡張マッピングをオーバーライドするか、拡張機能で提供されていない特定のeコマース変数を使用したい場合を除き、このカテゴリでの手動マッピングは通常必要ありません。

いくつかのSiteCatalyst変数、製品文字列を含む、はE-Commerce拡張によって自動的に入力されます。SiteCatalystは製品情報、収益、販売単位、および購入に関連するその他の情報をキャプチャするために製品文字列を使用します。標準的な製品文字列は次のようになります：

![](/images/client-side-tags/product-string.png)

##### 製品文字列のベストプラクティス：

* セミコロン `;` は製品文字列のほとんどの項目の標準セパレータです。
* 複数のマーチャンダイジングeVarsをパイプ (`|`) 文字で区切ります。
* 複数の製品インスタンスをコンマ (`,`) で区切ります。
* 合計価格は単価に数量を掛けたものです。E-Commerce拡張の合計価格 (`_ctotal`) 出力は自動的に製品文字列にマッピングされません。
* SiteCatalystのベストプラクティスでは、カテゴリを空にしておくことが推奨されます。なぜなら、一度SiteCatalystで構成された製品のカテゴリは変更できないからです。ただし、後でカテゴリを変更することが問題ない場合は、変換時にカテゴリを構成することができます。

#### E-Commerceデスティネーション

ツールボックスに組み込まれている以下のeコマースデスティネーション：

| デスティネーション名 | 説明 | Ecommerce拡張変数 |
|:---------------------------|:--------------------------------------------------------------------|:-----------------------------|
| purchaseID | &lt;ul&gt;&lt;li&gt;このデスティネーションへの一意の注文識別子。&lt;/li&gt;&lt;/ul&gt; | `_corder` |
| transactionID | &lt;ul&gt;&lt;li&gt;オフラインデータをオンライントランザクションに関連付けます。&lt;/li&gt;&lt;/ul&gt; | N/A |
| state | &lt;ul&gt;&lt;li&gt;変換で指定された州の名前&lt;/li&gt;&lt;/ul&gt; | N/A |
| zip | &lt;ul&gt;&lt;li&gt;変換で指定された郵便番号&lt;/li&gt;&lt;/ul&gt; | N/A |
| Product IDs (array) | &lt;ul&gt;&lt;li&gt;製品配列内の各製品の一意ID&lt;/li&gt;&lt;/ul&gt; | `_cprod` |
| Product Categories (array) | &lt;ul&gt;&lt;li&gt;製品配列内の各カテゴリの名前&lt;/li&gt;&lt;/ul&gt; | `_ccat` |
| Product Quantities (array) | &lt;ul&gt;&lt;li&gt;製品配列内の各製品の数量&lt;/li&gt;&lt;/ul&gt; | `_cquan` |
| Product Prices (array) | &lt;ul&gt;&lt;li&gt;製品配列内の各製品の単価&lt;/li&gt;&lt;/ul&gt; | `_cprice` |

#### その他

| 変数 | 説明 |
|:---------------------------------|:------------|
| Link Tracking - doneAction param | (H25のみ) |
| List 1 | |
| List 2 | |
| List 3 | |
#### モバイル

| 変数 | 説明 |
|:---------|:---------------|
| アプリID | (`contextData.a.AppID`) |
| デバイス名 | (`contextData.a.DeviceName`) |
| オペレーティングシステム | (`contextData.a.OSEnvironment`) |
| オペレーティングシステムバージョン | (`contextData.a.OSVersion`) |
| キャリア名 | (`contextData.a.CarrierName`) |
| 解像度 | (`contextData.a.Resolution`) |
| インストール日 | (`contextData.a.InstallDate`) |
| 起動回数 | (`contextData.a.Launches`) |
| 初回使用からの日数 | (`contextData.a.DaysSinceFirstUse`) |
| 最終使用からの日数 | (`contextData.a.DaysSinceLastUse`) |
| インストール数 | (`contextData.a.InstallEvent`) |
| アップグレード数 | (`contextData.a.UpgradeEvent`) |
| 起動数 | (`contextData.a.LaunchEvent`) |
| クラッシュ数 | (`contextData.a.CrashEvent`) |
| 前回のセッション時間 | (`contextData.a.PrevSessionLength`) |
| 時間帯 | (`contextData.a.HourOfDay`) |
| 曜日 | (`contextData.a.DayOfWeek`) |
| 最後のアップグレードからの日数 | (`contextData.a.DaysSinceLastUpgrade`) |
| アップグレード後の起動回数 | (`contextData.a.LaunchesSinceUpgrade`) |
| 日間エンゲージメントユーザー | (`contextData.a.DailyEngUserEvent`) |
| 月間エンゲージメントユーザー | (`contextData.a.MonthlyEngUserEvent`) |
| `disable_wake_track` | &lt;ul&gt;&lt;li&gt;ウェイクトラッキングを無効にする&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `disable_sleep_track` | &lt;ul&gt;&lt;li&gt;スリープトラッキングを無効にする&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `send_timestamp` | &lt;ul&gt;&lt;li&gt;タイムスタンプ送信トグル&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `timestamp` | &lt;ul&gt;&lt;li&gt;タイムスタンプ&lt;/li&gt;&lt;li&gt;ISO 8601形式&lt;/li&gt;&lt;li&gt;Unix Time&lt;/li&gt;&lt;/ul&gt; |

#### リンクトラッキング

| 変数 | 説明 |
|:-----------|:------------|
| `linkType` | リンクタイプ |
| `linkName` | リンク名 |

### イベントシリアライゼーション検出

AppMeasurementタグは、データレイヤーのトリガー値内で[イベントシリアライゼーション](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/events/event-serialization)を自動的に検出します。タグが発火すると、**イベント**タブでマップされたトリガー文字列とデータレイヤーのトリガー値を比較し、どちらかにコロンが含まれているかを確認します。

* **イベントシリアライゼーション検出：オン**  
イベントシリアライゼーション検出がオン（デフォルト構成）の場合、タグはコロンの隣のトリガー値を検出し、残りの文字列とマップされたトリガーを一致させようとします。正確な一致がある場合、イベントはシリアライズされます。
* **イベントシリアライゼーション検出：オフ**  
イベントシリアライゼーション検出がオフの場合、タグはコロンを検出しません。タグは両方のトリガー値を完全に一致させようとします。この構成は、マップされたトリガー文字列にコロンが含まれている場合に強く推奨されます。イベントシリアライゼーション検出をオフにすることは、コロンを含む値でイベントを正しくトリガーする唯一の方法です。

イベントシリアライゼーション検出がオンまたはオフの場合でも、**イベントシリアライゼーション**タブを直接マップしたシリアルは常に優先されます（[シナリオ3の例](#scenario3)を参照）。

このセクションでは、コロンの有無に関わらず、イベントシリアライゼーション検出がトリガー値をどのように解釈するかを理解するためのシナリオを説明します。

このセクション全体で、「マップされたトリガー」という用語は、タグのデータマッピング構成の値を指し、「データレイヤートリガー」という用語は、ウェブサイトのデータレイヤーに見つかる値を指します。

#### 例：コロンなしのマップされたトリガー

例えば、ページに`fireEvt`が含まれている場合に`prodView`イベントをトリガーしてシリアライズする場合、以下の手順を実行します：

1. イベントシリアライゼーションタブでUDO変数`serial`を`SERIAL_prodView`にマップします。
1. イベントの下でUDO変数`trigger`を`prodView`にマップします。
1. `prodView`のトリガー文字列として`fireEvt`をマップします。  
![](/images/client-side-tags/trigger-without-colon.jpeg)

データレイヤーで発生する可能性のある多くのシナリオがあります。

#### シナリオ1: データレイヤートリガーは`fireEvt`で、`serial`値は空です

```js
var utag_data = {
  trigger: &#34;fireEvt&#34;,
  serial: &#34;&#34;
}

```

* **イベントシリアライゼーション検出：オン**  
タグは`fireEvt`をマップされたトリガーと一致させ、ページ上で`prodView`を成功裏に発火させますが、シリアライズはありません。
* **イベントシリアライゼーション検出：オフ**  
上記と同じ結果です。

成功したネットワークコールは次のようになります：

![](/images/client-side-tags/scene-1-network-call-.png)

#### シナリオ2: データレイヤートリガーは`fireEvt:123`で、`serial`値は空です

```
var utag_data = {
  trigger: &#34;fireEvt:123&#34;,
  serial: &#34;&#34;
}
```

* **イベントシリアライゼーション検出：オン**  
タグは`123`をシリアライズし、その後`fireEvt`をマップされたトリガーと一致させ、ページ上で`prodView`を成功裏に発火させます。  
![](/images/client-side-tags/scene-2-network-call.png)

* **イベントシリアライゼーション検出：オフ**  
タグは`fireEvt:123`をマップされたトリガーと一致させることができず、その結果、ページ上で`prodView`は発火しません。

#### シナリオ3: データレイヤートリガーは`fireEvt:123`で、シリアル値は`456`です {#scenario3}

```
var utag_data = {
  trigger: &#34;fireEvt:123&#34;,
  serial: &#34;456&#34;
}
```

* **イベントシリアライゼーション検出：オン**  
最初に、タグは`123`をシリアライズし、その後`fireEvt`をマップされたトリガーと一致させます。その後、`prodView`が成功裏に発火し、`123`ではなく`456`でシリアライズされます。  
これは、イベントシリアライゼーション検出によって検出されたシリアル値(`123`)よりも、イベントシリアライゼーションマッピングによって検出されたシリアル値(`456`)が優先されるためです。  
![](/images/client-side-tags/scene-3-network-call.png)
* **イベントシリアライゼーション検出：オフ**  
タグは`fireEvt:123`をマップされたトリガーと一致させることができず、その結果、ページ上で`prodView`は発火しません。

#### 例：コロン付きのマップされたトリガー

この例はシナリオ2と同じパスをたどりますが、マップされたトリガーは`fireEvt`ではなく`fireEvt:123`です。

![](/images/client-side-tags/trigger-with-colon.png)

#### シナリオ: データレイヤートリガーは`fireEvt:123`

```js
var utag_data = {
  trigger: &#34;fireEvt:123&#34;,
  serial: &#34;&#34;
}
```

* **イベントシリアライゼーション検出：オン**  
タグは`123`をシリアライズしますが、マップされたトリガーと`fireEvt`を一致させることができず、その結果、ページ上で`prodView`は発火しません。
* **イベントシリアライゼーション検出：オフ**  
タグは`fireEvt:123`をマップされたトリガーと成功裏に一致させ、`prodView`が成功裏に発火します。このため、文字列にコロンが含まれている場合はイベントシリアライゼーション検出をオフにすることをお勧めします。

## 高度な構成

### s.eventsの構成

Tealiumは`s.event`文字列を構成するのに役立つ`u.addEvent()`という関数を提供しています。この方法は`s.events`の最後に新しい値を追加することができ、必要に応じて別のイベントを追加しながら、以前に構成されたすべてのイベントを保持することができます。この方法を使用するには、構成に`sc_events`という名前の変数を追加します。

`s.events`を`u.addEvent`を使用してカスタマイズするための次の手順を使用します：

1. [データ値の構成]()拡張機能を追加します。
1. **スコープ**をAdobe Analyticsタグに構成します。
1. **Set**メニューから**sc_events**を選択します。
1. **To**メニューから**JS Code**を選択します。
1. テキストフィールドに次のように入力します：`u.addEvent(&#34;CUSTOM_EVENT&#34;)`  
ここで、`CUSTOM_EVENT`は`s.events`文字列に追加したいイベントです、例えば`event10`です。
1. 一度に複数のイベントを追加するには、次のように配列を`u.addEvent`に渡します：  
`u.addEvent([&#34;event1&#34;,&#34;event2&#34;,&#34;scView&#34;]);`

関数に渡される文字列内で直接値を追加するには：`u.addEvent([&#39;event500=500&#39;, &#39;event501=&#39; &#43; b.demo_event_value]);`

関数に渡される文字列内で直接シリアライゼーションを追加するには：`u.addEvent(&#34;event78:&#34; &#43; b.booking_reference);`
## 対応バージョン

以下のAppMeasurement for JavaScriptのコードバージョンがサポートされています：

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

##### v2.23.0 リリース日 2019年9月23日

* 高エントロピーのユーザーエージェント情報のサポートを追加。

##### v2.22.3 2021年12月21日リリース

##### v2.20.0 2020年3月5日リリース

* IE検出の更新により、JSLint警告を抑制し、セキュリティ関連の問題を修正。

##### v2.18.0 2020年2月13日リリース

* `writeSecureCookies`変数を構成することで、AppMeasurementがクッキーにSecure属性を含めるように強制できるようになりました。この変数をサポートするには、クライアントのウェブサイト全体がHTTPSを使用して安全に提供されている必要があります。

##### v2.17.0 2019年8月23日リリース

* Baiduクエリ文字列の並び替えをサポート。
* オプトインを待っている間にキューに入れられたヒットで訪問の値が古くなる問題を修正。

##### v2.15.0 2019年7月15日リリース

* Activity Map拡張機能にActivityMapスクロールリーチトラッキングを追加（AN-172949）

* AppMeasurementにDIL 9.2を追加（AN-182472）

##### v2.9.0 2018年5月24日リリース

Experience Cloud IDサービスを使用する顧客には、Visitor API 3.0以上が必要です。Adobeは、at.js、AppMeasurement.jsなどの関連コードライブラリが更新されたときに、最新のVisitor APIバージョンにアップグレードすることを推奨します。

* 更新されたVisitorインターフェースを使用してIDを要求するようにAppMeasurementを更新しました。（AN-151483）
* リンクトラッキングがオフになった後にリンクトラッキングクッキーが書き込まれる問題を修正。（AN-156332）
* `registerPreTrackCallback`および`registerPostTrackCallback`が複数回呼び出されるとコールバック関数のシグネチャが壊れる問題を修正。（AN-158566）

##### v2.8.2 2018年4月12日リリース

* 更新されたvisitorインターフェースを使用してIDを要求するようにAppMeasurementを更新。
* リンクトラッキングクッキーに関する問題を修正。
* AppMeasurementのデフォルトクッキー寿命を5年から2年に短縮。
* Visitor API（別名Enterprise Cloud IDサービス）、バージョン3.1.2をサポート

##### v2.7.0 2018年1月18日リリース

* Internet Explorer（IE）のバージョン6から9までのサポートを非推奨に。
* DIL v7.00を含む
* Visitor API（別名Marketing Cloud IDサービス）、バージョン3.0をサポート

##### v2.6.0 2017年11月9日リリース

* `s_gl`が呼び出されたときにAppMeasurementライブラリが常に正しいアカウントの組み合わせを構成しない問題を修正。（AN-152153）
* `dil.js` 6.12（Audience Managerモジュール）を含む。
* Visitor API 2.5.0をサポート。

##### v2.3.0 2017年8月22日リリース

* `s.Util.getQueryParam`が`#`をキャプチャしていたバグを修正。
* 最新バージョンの`dil.js`（v6.10）を含む。
* 複数のAppMeasurementインスタンス化順序をサポート。
* Visitor API（別名Marketing Cloud IDサービス）バージョン2.2.0をサポート。

##### v2.1.0 2017年5月11日リリース

* AppMeasurement JavaScript 2.1.0をサポート
* Marketing Cloud IDサービスバージョン2.1.0をサポート
* 最新バージョンの`dil.js`を含む。
* ページリファラーを上書きする`adobe_mc_ref`パラメータをサポート。
* `mcorgid`パラメータを追加。
* `cp`（customerPerspective）パラメータを追加。

##### v1.8.0 2017年3月10日リリース

* AppMeasurement JavaScript 1.8.0をサポート。
* Marketing Cloud IDサービスバージョン2.0.0をサポート。
* 2つのコールフックを追加：[`s.registerPreTrackCallback`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/registerpretrackcallback) および [`s.registerPostTrackCallback`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/registerposttrackcallback).

##### v1.6.3 2016年8月23日リリース

* AppMeasurementがリクエスト接続を早期に終了する問題を修正。
* AppMeasurementがVisitor APIの誤った難読化メソッドを呼び出す問題を修正。
* JavaScriptエラー「Attribute only valid on v:image」の問題を修正。
* Marketing Cloud IDサポート（別名Visitor API）を新しいタグ、Marketing Cloud ID Service Tagに分離。

Marketing Cloud ID Service Tagは、他のAdobeタグ（AppMeasurementを含む）よりも先にプロファイルで読み込む必要があります。そうしないと、訪問トラッキングの整合性が失われます。タグを最初にロードするには、[bundle setting]()をAll Pagesで有効にし、他のAdobeタグよりも先にロードします。

[完全なAdobe AppMeasurementリリースノートを見る](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates).

##### v1.6.1 2016年7月28日リリース

AppMeasurementのイベント、値イベント、およびイベントシリアライゼーションに影響する次の更新：

* データマッピングツールボックスに新しいイベントシリアライゼーションマッピングタブを追加。
* AppMeasurementタグ構成でイベントシリアライゼーションのON/OFFを切り替えるための新しいドロップダウンリストを追加

##### v1.6.1 2016年7月14日リリース

* 新バージョン1.6.1を追加
* Visitor APIバージョン1.5.7および1.5.6をサポート
* Firefoxでのリンククリックトラッキングの取り扱いメカニズムを改善。

[完全なAdobe AppMeasurementリリースノートを見る](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates).

## ベンダー文書

* [Adobe Experience League: JavaScript用AppMeasurementについて](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview)
* [Adobe Experience League: AppMeasurementリリース履歴](https://experienceleague.adobe.com/en/docs/analytics/implementation/appmeasurement-updates)
* [Adobe Experience League: アクティビティマップの有効化](https://experienceleague.adobe.com/en/docs/analytics/analyze/activity-map/getting-started)
* [Adobe Experience League: モバイルメトリックスの理解](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/overview)
* [Adobe Experience League: モバイルメトリックスリファレンス](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/lifecycle-metrics)

