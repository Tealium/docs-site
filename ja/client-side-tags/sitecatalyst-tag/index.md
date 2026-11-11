---
title: SiteCatalystタグ構成ガイド
description: SiteCatalystは、訪問によるサイトの利用状況を追跡するWeb解析機能を提供する、AdobeのSaaS（Software as a Service）アプリケーションです。
url: https://docs.tealium.com/ja/client-side-tags/sitecatalyst-tag/
---
## タグの仕様と要件

### 仕様

**名前**：SiteCatalyst

**ベンダー**：Adobe

**タイプ**：解析

### 必須要件

**サービス**：SiteCatalystアカウント

**構成**：

* S-Codeのバージョン
* レポートスイート
* サーバー
* セキュアサーバー
* 名前空間
* 内部リンクフィルター

## タグの構成

### 1. タグを追加する

タグ管理のタグマーケットプレイスでは、さまざまなタグを提供しています。詳細については、[こちら](https://docs.tealium.com/about-tag-marketplace/)を参照してください。

### 2. タグを構成する

SiteCatalystタグの構成項目は次のとおりです。各構成値は、SiteCatalystから提供された`s_code`ファイルで確認できます。

![](https://docs.tealium.com/images/client-side-tags/no-title-1081i487822e9a007e208.png)

![](https://docs.tealium.com/images/client-side-tags/no-title-1080if5f98fdd321f2089.png)

1. **タイトル**：（必須）タグを識別するための分かりやすいタイトルを入力します。
1. **S-Codeのバージョン**：（必須）使用するSiteCatalystのバージョンを選択します。H20からH27までのバージョンがサポートされています。
1. **レポートスイート**：（必須）SiteCatalystレポートスイートの名前を入力します。この値は、`s_code.js`ファイル内の`s.account`として確認できます。
1. **サーバー**：（必須）データ収集サーバーの情報を入力します。この値は、`s_code.js`ファイル内の`s.trackingServer`として確認できます。
1. **セキュアサーバー**：（必須）セキュアな（`https`）データ収集サーバーの情報を入力します。この値は、`s_code.js`ファイル内の`s.trackingServerSecure`として確認できます。
1. **名前空間**：（必須）この値は、`s_code.js`ファイル内の`s.namespace`として確認できます。
1. **自動リンクトラッキング**：（任意）デフォルトの選択は`Yes`であり、これを選択することを推奨します。`No`に構成した場合は、Tealiumの[リンクトラッキング拡張機能](https://docs.tealium.com/jquery-onhandler-extension/)を使用して、すべての自動リンクトラッキングを再現する必要があります。
`Yes`を選択した場合でも、カスタムトラッキングにTealiumのリンクトラッキング拡張機能を使用できます。

1. **ダウンロードタイプ**：（任意）ダウンロードリンクとして追跡するファイルの拡張子を、このフィールドに列挙します。たとえば、`zip`、`exe`、`wav`、`mp3`、`mov`、`mpg`、`avi`、`wmv`、`pdf`、`doc`、`docx`、`xls`、`xlsx`、`ppt`、`pptx`を入力できます。
1. **内部リンクフィルター**：（任意）ここには値を入力する必要があります。入力しない場合、すべてのリンククリックがSiteCatalystレポートで離脱リンクとして報告されます。モーダルの表示など、JavaScriptの処理を実行するリンククリックを適切に追跡するには、フィールドに`javascript`が含まれていることを確認してください。これらの値は、`s_code.js`ファイル内の`s.linkInternalFilters`として確認できます。
1. **通貨コード**：（任意）収益データで使用する通貨の3文字の通貨コードを入力します。デフォルト値は`USD`です。これは、SiteCatalystがレポートスイート内の収益データを解釈する際に使用するデフォルト通貨です。サイト上で別の通貨による取引が発生した場合、SiteCatalystで通貨換算を行えます。この値は、`s_code.js`ファイル内の`s.currencyCode`で確認できます。
1. **動的アカウントを使用**：（任意）ドメインに基づいて異なるレポートスイートにデータを送信する場合は、`Yes`に構成します。
1. **動的アカウントリスト**：（任意）ドメインに基づいてレポートスイートを動的に構成するため、レポートスイートと対応するドメインのリストを入力します。例：`testreportsuite=testing.example.com,qa.example.com;prodreportsuite=www.example.com`
1. **Sオブジェクト名**：（必須）このタグを完全に独立した別の実装と並行して実行する予定がない限り、デフォルトの`s`のままにします。
1. **変数をクリア**：（任意）各トラッキングリクエストの後に、グローバル`s`オブジェクトに構成されたprops、eVars、イベントをクリアするには、`Yes`に構成します。
1. **パートナー**：（任意）パートナーIDを入力します。これはAdobe AudienceManagerを使用する場合にのみ必要です。Adobe AudienceManagerを使用しない場合は空白のままにしてください。パートナーIDの値は、`DIL.create`呼び出し内で確認できます。

**ヒント**：タグが可能な限り早く読み込まれるように、［タグ］タブのリスト上部付近にこのタグを配置してください。タグの読み込みが早いほど、訪問のアクティビティを早く取得できます。

### 3. 読み込みルールを適用する

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトの読み込みルールは、**すべてのページに表示**です。特定のページでこのタグを読み込むには、該当する条件を構成した新しい読み込みルールを作成します。

**注**：SiteCatalystは解析タグであるため、サイト全体で読み込む必要があります。そのため、デフォルトの**すべてのページで読み込む**という選択をそのまま使用することを推奨します。

### 4. マッピングを構成する

[マッピング](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信するプロセスです。

Products Stringを適切にフォーマットし、SiteCatalystレポートスイートに収益データを送信するには、タグ管理プロファイルに[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を追加して構成する必要があります。


<blockquote>
最新のテンプレート更新以降、linkTrackVarsとlinkTrackEventsは自動的に構成されます。この機能を利用するには、テンプレートを最新バージョンに更新する必要がある場合があります。
</blockquote>


### 標準マッピング

* **pageName**
* **channel**
* **server**
* **hier1からhier3**
* **VisitorID**
* **s\_account**：アカウント構成を動的に指定するには、この宛先にマッピングします。

### イベント

マッピングを使用して、次のイベントをトリガーできます。

* **prodView**
* **scOpen**
* **scAdd**
* **scRemove**
* **scView**
* **scCheckout**
* **purchase**
* **event1からevent100**

タグ管理を介したSiteCatalystのイベントトラッキングの詳細については、[こちら](https://docs.tealium.com/sitecatalyst-firing-multiple-events-and-event-serialization/)をクリックしてください。

#### 製品レベルのイベント

ここでマッピングすると、Products Stringに次のイベントが追加されます。

* `PRODUCTS_event1`から`PRODUCTS_event100`

#### Props

データソースを次の宛先にマッピングし、propsとしてSiteCatalystに送信します。

* `prop1`から`prop75`

#### eVars

データソースを次の宛先にマッピングし、eVarsとしてSiteCatalystに送信します。

* `eVar1`から`eVar75`

#### マーチャンダイジングeVars

データソースを次の宛先にマッピングし、マーチャンダイジングeVarsとしてSiteCatalystに送信します。

* `PRODUCTS_eVar1`から`PRODUCTS_eVAr75`

#### コマース

データソースを次の宛先にマッピングし、コマースデータをSiteCatalystに送信します。このデータの多くは、Eコマース拡張機能によって自動的に送信されます。

* **purchaseID**
* **transactionID**
* **state**
* **zip**
* **製品ID（`PRDOCUTS_id`）\{配列\}**
* **製品カテゴリー（`PRODUCTS_category`）\{配列\}**
* **製品数量（`PRODUCTS_quantity`）\{配列\}**
* **製品価格（`PRODUCTS_price`）\{配列\}**

#### その他

リストデータとdoneActionパラメーターを送信するには、データソースを以下の宛先にマッピングします。

* リンクトラッキング - doneActionパラメーター（H25のみ）
* list1からlist3


## ベンダーのドキュメント

* [一般向けWebサイト](http://www.adobe.com/products/sitecatalyst.html)
* [サポートサイト](http://helpx.adobe.com/sitecatalyst.html)