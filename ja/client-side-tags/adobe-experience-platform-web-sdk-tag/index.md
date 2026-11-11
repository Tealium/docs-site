---
title: Adobe Experience Platform Web SDKタグ構成ガイド
description: この記事では、Adobe Experience Platform Web SDKタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-experience-platform-web-sdk-tag/
---
Adobe Experience Platform Web SDK（Adobe Alloy）は、Adobe Experience CloudのユーザーがAdobe Experience Platform Edge Networkを介してExperience Cloudの各種サービスと連携できるようにする、クライアント側のJavaScriptライブラリです。

## タグ構成のヒント

* マッピングを使用して標準の構成値を上書きし、カスタムパラメータを構成します。
* 複数のインスタンスを構成する場合は、インスタンスごとに一意の**データストリームID**と**組織ID**を指定する必要があります。複数の値はカンマ区切りのリストで指定します。

## 仕組み

マッピング先はドット表記で表されます。最終的なAPIペイロードは、タグ内のドット表記に基づく一連のネストされたJSONオブジェクトで構成されます。

Adobe Experience Platform Web SDKタグには、使用するAdobeアプリケーションに固有の次のマッピングが含まれており、XDMデータおよび非XDMデータのマッピングに対応しています。XDMデータは、その内容と構造がAdobe Experience Platform内で作成したスキーマと一致するオブジェクトです。

* XDMイベントトリガー：特定の`eventType`値を持つイベントをトリガーするために使用します。
* イベント固有のパラメータ：特定のイベントについて、XDM属性と非XDM属性の両方をマッピングするために使用します。
* Analytics XDMデータ：XDMオブジェクトで渡すデータをマッピングするために使用します。
* Targetデータ：Targetプロファイルの更新やTarget Recommendations属性の送信のために、データオブジェクトで渡す非XDM属性をマッピングするために使用します。

AdobeへのXDMデータおよび非XDMデータの送信について詳しくは、Adobeドキュメントの[イベントのトラッキング](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html)を参照してください。

### イベントの例

イベントにマッピングする変数を選択し、トリガーを指定してAdobe Experience Platform Web SDKイベントを構成します。変数が特定の値と等しくなるとイベントがトリガーされ、選択したイベント名が`eventType`として渡されます。

#### ユースケース：XDMイベントトリガーを使用した購入イベント

購入イベントを構成するには、次の手順を実行します。

1. Adobe Experience Platform Web SDKタグ構成の**データマッピング**画面に移動します。
1. 変数のドロップダウンリストから`tealium_event`を選択し、**マッピング先を選択**をクリックします。
1. **カテゴリ**セクションで、**XDMイベントトリガー**を選択します。
1. **マッピングされた変数が次と等しい場合**フィールドを**購入**に構成します。これは、購入をトリガーするために`tealium_event`と一致する必要がある値です。
1. **イベントをトリガー**ドロップダウンリストで、**sendEvent：コマースイベント**セクションの**購入**`(commerce.purchases)`を選択します。これは、`tealium_event`が購入イベントと等しい場合にトリガーされるイベントです。

![](https://docs.tealium.com/images/client-side-tags/adobe-experience-web-sdk-mappings-example.png)

#### ユースケース：イベント固有のパラメータを使用した購入イベント

既存のE-Commerce拡張機能のマッピングに含まれていないデータを購入イベントとともに送信する必要がある場合は、**イベント固有のパラメータ**を使用します。リストから属性を選択するか、カスタムのマッピング先を入力します。対象のイベントと属性に応じた正しいドット表記を使用してください。

次の例では、購入イベントとともに`purchaseOrderNumber`をXDMデータとして渡します。

1. Adobe Experience Platform Web SDKタグ構成の**データマッピング**画面に移動します。
1. 変数のドロップダウンリストから`po_number`（または該当するクライアント固有のデータレイヤー要素）を選択し、**マッピング先を選択**をクリックします。
1. **カテゴリ**セクションで、**イベント固有のパラメータ**を選択します。
1. `purchaseOrderNumber`はデフォルトのマッピング先に含まれていないため、**カスタムパラメータ**を入力する必要があります。**パラメータ**ドロップダウンから**カスタム**を選択し、マッピング先の完全なドット表記パス`commerce.purchases.xdm.commerce.order.purchaseOrderNumber`を入力します。
1. **対象イベント**ドロップダウンリストで、**購入**イベントを選択します。
1. **追加**をクリックしてパラメータを追加します。

#### ユースケース：非XDMデータ／Adobe Targetデータ

非XDMデータ（Targetデータ）も、イベントマッピングを使用して構成できます。このユースケースでは、Adobe Targetで使用するために`product_brand`も送信します。

1. Adobe Experience Platform Web SDKタグ構成の**データマッピング**画面に移動します。
1. 変数のドロップダウンリストから`product_brand`を選択し、**マッピング先を選択**をクリックします。
1. **カテゴリ**セクションで、**Targetデータ**を選択します。
1. マッピング先として`entity.brand`を選択します。
1. Adobe Web SDKに送信される購入イベントのペイロードに、`data.__adobe.target.entity.brand`が含まれるようになります。

次の例は、E-Commerce拡張機能のデフォルトマッピングの一部を含む、生成されたAdobe Web SDK呼び出しを示しています。また、Adobeのドット表記`commerce.purchases.xdm.commerce.order.purchaseOrderNumber`が、ネストされたオブジェクトに展開される仕組みも示しています。

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "purchaseOrderNumer":"A1234"
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      }
    ]
  },
  "data":{
    __adobe: {
      target: {
        "entity.brand": "Acme"
      }
    }
  }
});
```

## Adobe Targetによるフリッカーの管理

Adobe Experience Platform Web SDKを非同期で読み込むと、すでに読み込まれたコンテンツがAdobe Targetによって更新される可能性があるため、コンテンツのフリッカーが発生することがあります。フリッカーを最小限に抑えるため、Adobeでは事前非表示スニペットの追加を推奨しています。[JavaScript拡張機能](https://docs.tealium.com/javascript-code-extension/)を使用して、このスニペットを`utag.sync.js`テンプレートに追加します。

`utag.sync.js`について詳しくは、[`utag.sync.js`の仕組み](https://docs.tealium.com/utag-sync/)を参照してください。

事前非表示スニペットについては、[フリッカーの管理](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)を参照してください。

### Cookie管理ソリューション使用時の空白ページエラー

ユーザーが各Cookieカテゴリに同意するまでタグがトリガーされないようにCookie管理ソリューション（CMS）を使用している場合、事前非表示スニペットが読み込まれ、タイムアウトするまで（3～7秒間）空白ページが表示されます。この動作が発生するのは、ユーザーが同意するまでAdobe Experience Platform Web SDKタグを読み込めないためです。

この問題を解決するには、同意が得られているかどうかを確認し、その結果に基づいて事前非表示スニペットをトリガーするかどうかを決定します。

Tealium以外のカスタムCMSを使用している場合は、そのCMSプラットフォームを通じて同意の確認を管理します。

Tealium JavaScript拡張機能を使用している場合は、AEP Web SDKタグが属するCookieカテゴリ（たとえば、機能Cookieのカテゴリ）に対するユーザーの同意を表す特定の値が同意Cookieに含まれている場合にのみ関数がトリガーされるように、ロジックを更新します。
#### 例

この例では、CMS は `mycms_cookie` という名前の Cookie を構成します。この Cookie には、ユーザーが機能 Cookie の使用を許可した場合は `functional:1`、すべての Cookie を許可した場合は `all:1` という値が格納されます。

次のコードでは、これらの値を確認してプリハイディングスニペットを実行します。


<blockquote>
この例には、構成に合わせて変更する必要があるコード行を示すコメントが含まれています。
</blockquote>


```javascript
!function(e,a,n,t){
  if (a) return;
  //Check if the cookie exists, and if it does, get its value. Update the mycms_cookie bit with the actual name of your CMS's cookie.
  var cms_cookie_value = (document.cookie.match(https://docs.tealium.com/^(?:.*;)?\s*mycms_cookie\s*=\s*([^;]+)(?:.*)?$/)||[,null])[1];
  if(cms_cookie_value){
    //Add the accepted values to an array. In the example below, the cookie value must contain either all:1 or functional:1 to trigger the prehidding snippet.     
    var accepted_values = ['all:1','functional:1'];
    for(var i=0;i<accepted_values.length;i++){
      if(cms_cookie_value.includes(accepted_values[i])){
        var x=e.head;
        if(x){
          var o=e.createElement("style");
          o.id="alloy-prehiding";
          o.innerText=n;
          x.appendChild(o);
          setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t);
          return;
        }
      }
    }
  }
}

(document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
```

`"body { opacity: 0 !important }"` のコードを、特定の `div` など、対象とする要素に置き換えます。置き換えない場合、コードのデフォルトの動作ではコンテンツの body 全体が非表示になります。

## Adobe Analytics 移行ガイド

Adobe Analytics タグは、Adobe Experience Platform Web SDK タグに置き換えられたレガシータグです。Adobe Experience Platform Web SDK タグは、エクスペリエンスデータモデル（XDM）を Adobe Analytics 形式に変換して、Adobe Analytics にデータを送信します。

Adobe Experience Platform Web SDK タグは、レガシーの変数、プロパティ、イベントをサポートしています。

### コードの比較

次の例は、Adobe Analytics と Adobe Experience Platform Web SDK の呼び出しにおける構造上の違いを示しています。

#### Adobe Analytics

```javascript
// Load the AppMeasurement library
var s = new AppMeasurement();
// Set the report suite ID
s.account = "example-rsid";
// Set the page name
s.pageName = "Home Page";
// Set other variables as needed
s.prop1 = "value1";
s.eVar1 = "value2";
s.hellow = "value3";
// Send the data to Adobe Analytics servers
var s_code = s.t();
if (s_code) document.write(s_code);
```

#### Adobe Experience Platform Web SDK

```javascript
window.alloy("sendEvent", {
    // Set the type of event
    type: "viewStart",
    // Set the data for Adobe Analytics
    xdm: {
      web: {
        webPageDetails: {
          // Set the page name
          name: "Home Page"
        }
      },
      _experience: {
        analytics: {
          customDimensions: {
            props: {
              prop1: "value1"
            },
            eVars: {
              eVar1: "value2"
            }
          }
        }
      },
    },
    data: {
      // Set other variables as needed
      hellow: "value3",
    }
  });
```

### Tealium Tools を使用した Adobe Analytics タグの移行

Adobe Experience Platform Web SDK Migrator ツールを使用すると、既存の Adobe Analytics AppMeasurement タグを Adobe Experience Platform Web SDK タグに移行できます。

Migrator ツールを使用する前に、次の制限事項に注意してください。

* このツールでは、doPlugins または拡張機能は移行されません。構成で doPlugins または拡張機能を使用している場合は、手動で移行する必要があります。これらの要素を移行する手順については、Adobe ドキュメントの「[イベントをグローバルに移行](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally)」セクションを参照してください）。
* `link_name` 変数と `link_trackvars` 変数はサポートされていません。
* Adobe Experience Platform Web SDK タグで Adobe の仕様に従って手動でマッピングするには、事前に `products` 変数を複数の属性に分割する必要があります。詳細については、Adobe ドキュメントの「[products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)」を参照してください。
* ツールで自動的に移行されないイベントや属性のマッピングは空になります。「[Adobe Analytics タグを手動で移行する](#migrate-the-adobe-analytics-tag-manually)」ガイドを使用して、これらの空の属性を手動でマッピングできます。

Tealium Tools を使用して Adobe Analytics タグを移行するには、次の手順を実行します。

1. 次の URL にある JSON 定義を使用して、Adobe Experience Platform Web SDK Migrator を Tealium Tools に追加します：https://solutions.tealium.net/hosted/tealiumTools/aep_migrate/aep_migrate.json。カスタムツールの追加について詳しくは、「[カスタムツールの管理](https://docs.tealium.com/tealium-tools-browser-extension/#add-a-custom-tool)」を参照してください。
1. **タグ管理／タグ**に移動し、Adobe Experience Platform Web SDK Migrator ツールを起動します。
1. 移行の一環として既存の Adobe Analytics タグを無効にするには、**既存のタグを無効にする**を選択します。
1. 移行の範囲を選択します。
    * すべての AppMeasurement タグ
    * すべてのアクティブな AppMeasurement タグ
    * 特定の AppMeasurement タグ（移行するタグのタグ UID を追加する必要があります。）
1. **開始**をクリックします。  
Migrator ツールによって、既存の Adobe Analytics AppMeasurement タグが Adobe Experience Platform Web SDK タグに自動的に移行されます。
1. プロファイルを保存してパブリッシュします。

構成で doPlugins または拡張機能を使用している場合は、手動で移行する必要があります（以下を参照）。
### Adobe Analyticsタグを手動で移行する

Adobe AnalyticsタグからAdobe Experience Platform Web SDKタグへ手動で移行するには、次の手順を実行します。

この移行ガイドでは、Adobe Analyticsタグで次のデータマッピング例を使用します。

![](https://docs.tealium.com/images/client-side-tags/adobe-analytics-migration-example1.png)

![](https://docs.tealium.com/images/client-side-tags/adobe-analytics-migration-example2.png)

1. タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。
1. Tealiumで次のタグ構成を構成します。
    * **Org ID**：Adobeから割り当てられたExperience Cloud組織ID。例：`XXX@AdobeOrg`。
    * **Datastream ID**：SDKを適切なアカウントおよび構成にリンクする、Adobeから割り当てられたデータストリームID。`edgeConfigId`とも呼ばれます。
1. Adobe Experience Platformで次の構成を構成します。
    1. **Datastreams**に移動し、移行で使用するデータストリームを選択します。
    1. データストリームの**Configure**画面で、そのデータストリームに使用されている**Event Schema**を確認し、**Save**をクリックします。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-datastreams.png)
    1. データストリームの詳細画面で、Adobe Analyticsサービスが有効になっていることを確認し、そのサービスを選択します。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-service.png)
    1. **Adobe Analytics service**画面で、適切なデータストアを参照するAdobeの**Report Suite ID**を入力します。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-aa-enable.png)
    1. **Data Management > Schemas**に移動し、データストリームにリンクされている**Event Schema**を選択します。
    1. **Field Groups**に**Adobe Analytics ExperienceEvent Template**フィールドグループが含まれていることを確認します。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-schemas.png)
1. この例では、次の従来の属性、プロパティ、イベントをTealiumのAdobe Experience Platform Web SDKタグにマッピングします。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。
    1. Adobe Experience Platform Web SDKタグで、**Data Mappings**に移動します。
    1. **sf (js)**変数を選択して**Analytics eVars > evar181**にマッピングし、**Done**をクリックします。
    1. **page_category (js)**変数を選択して**Analytics Props > prop5**にマッピングし、**Done**をクリックします。
    1. **medallia_custom_event(js)**変数と**XDM Event Trigger**を選択します。次の値を使用してマッピングを構成し、**Done**をクリックします。
        * カスタム宛先として`MDigital_Invite_Displayed:_experience.analytics.event101to200`を追加します。
        * マッピングされた変数が次と等しい場合：**MDigital_Invite_Displayed**
        * トリガーイベント：**Experience Analytics Events 101-200 (\_experience.analytics.event101to200)**
        * カスタムイベント名：**200**
    1. **page_category (js)**変数を選択し、次の値を使用してマッピングを構成してから、**Done**をクリックします。
        * カスタム宛先として`xdm._experience.analytics.customDimension`と`data.channel`を追加します。
        * **Non-XDM/Custom Schema**に移動し、**Non-XDM/Custom Schema Path**に**channel**と入力します。
1. **Finish**をクリックします。
1. **Adobe Analyticsタグ**を無効にします。
1. 保存してパブリッシュします。

Adobe Experience Platformのデータストリーム、サービス、スキーマの構成について詳しくは、Adobeドキュメントの次の記事を参照してください。

* [データストリームの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UIでのスキーマの作成と編集](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Analyticsの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#analytics)

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を構成します。

* **Tag Version**：適切なタグバージョンを選択します。デフォルトは最新バージョンです。
* **Instance Name**：SDKの名前空間。デフォルトは`alloy`です。
* **Org ID**：Adobeから割り当てられたExperience Cloud組織ID。例：`XXX@AdobeOrg`。
* **Edge Domain**：Adobeサービスとの通信に使用するドメイン。ファーストパーティドメインのいずれかをAdobeがプロビジョニングしたドメインに（CNAMEを使用して）マッピングしている場合は、デフォルト構成を更新します。
* **Datastream ID**：SDKを適切なアカウントおよび構成にリンクする、Adobeから割り当てられたデータストリームID。`edgeConfigId`とも呼ばれます。
* **Debug Enabled**：ブラウザーのJavaScriptコンソールにデバッグメッセージを表示できるようにします。
* **Edge Base Path**：Adobeアカウントで構成されます。デフォルトは`ee`です。
* **Auto Pageview Tracking**：ページビューごとに`web.webpagedetails.pageViews`イベントを自動的に発生させます。
* **Auto Purchase Tracking**：注文IDが存在する場合に`commerce.purchases`イベントを自動的に発生させます。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
| --- | --- | --- |
| `library_version`  | 文字列 | タグのバージョン。 |
| `context`  | 配列 | コンテキスト。 |
| `debugEnabled`  | ブール値 | デバッグが有効。 |
| `decisionScopes`  | 配列 | 決定スコープ。 |
| `defaultConsent`  | 文字列 | デフォルトの同意構成。 |
| `downloadLinkQualifier`  | 文字列 | ダウンロードリンク修飾子。 |
| `edgeConfigId`  | 文字列 | データストリームID。 |
| `edgeDomain`  | 文字列 | エッジドメイン。 |
| `edgeBasePath`  | 文字列 | エッジのベースパス。 |
| `auto_page_tracking`  | ブール値 | 自動ページトラッキング。 |
| `auto_purchase_tracking`  | ブール値 | 自動購入トラッキング。 |
| `event_type`  | 文字列 | イベントタイプ。 |
| `errorsEnabled`  | ブール値 | エラーが有効。 |
| `hasHidingSnippet`  | ブール値 | Adobe Targetの事前非表示スニペット。 |
| `instanceName`  | 文字列 | インスタンス名。 |
| `orgId`  | 文字列 | 組織ID。 |
| `renderDecisions`  | ブール値 | 決定をレンダリング。|
| `documentUnloading`  | ブール値 | ドキュメントのアンロード。 |
| `custom.##` | - | カスタムデータ。 | 
| `commandCallback`  | 関数 | `commandCallback`関数。 |

### データ収集

| 変数 | 型 | 説明 |
| ---| --- | --- |
| `clickCollectionEnabled`  | ブール値 | クリック収集が有効。 |
| `onBeforeEventSend`  | 関数 | onBeforeEventSend関数。 |
| `onBeforeLinkClickSend`  | 関数 | onBeforeLinkClickSend関数。 |
| `internalLinkEnabled` | ブール値 | 内部リンクが有効。 |
| `downloadLinkEnabled` | ブール値 | ダウンロードリンクが有効。 |
| `externalLinkEnabled` | ブール値 | 外部リンクが有効。 |
| `eventGroupingEnabled` | ブール値 | イベントのグループ化が有効。 |
| `sessionStorageEnabled` | ブール値 | セッション保存が有効。 |
| `filterClickDetails` | 関数 | クリックの詳細をフィルタリング。 |
### ストリーミングメディア

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `channel` | String | （必須）ストリーミングメディアの収集が行われるチャネルの名前。例：ビデオチャネル。 |
| `playerName` | String | （必須）メディアプレーヤーの名前。 |
| `appVersion` | String | メディアプレーヤーアプリケーションのバージョン。 |
| `mainPingInterval` | Integer | メインコンテンツの ping の頻度（秒単位）。デフォルト値は 10 です。値は 10～50 秒の範囲で指定できます。値を指定しない場合、自動追跡セッションを使用するとデフォルト値が使用されます。詳しくは、[データ収集：自動追跡メディアセッションの作成](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/createmediasession#automatic)を参照してください。 |
| `adPingInterval` | Integer | 広告コンテンツの ping の頻度（秒単位）。デフォルト値は 10 です。値は 1～10 秒の範囲で指定できます。値を指定しない場合、自動追跡セッションを使用するとデフォルト値が使用されます。詳しくは、[データ収集：自動追跡メディアセッションの作成](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/createmediasession#automatic)を参照してください。 |

### E コマース

| 変数 | 型 | 説明 |
|:---------| --- | :------------|
| `purchaseID`（`_corder` を上書き） | String | 注文 ID。 | 
| `priceTotal`（`_ctotal` を上書き） | String | 注文合計。 | 
| `currencyCode`（`_ccurrency` を上書き） | String | 通貨。 | 
| `product.name`（`_cprodname` を上書き） | Array | 名前のリスト。 |
| `product.SKU`（`_csku` を上書き） | Array | SKU のリスト。 |
| `product.quantity`（`_cquan` を上書き） | Array | 数量のリスト。 |
| `product.priceTotal`（`_cprice` を上書き） | Array | 価格のリスト。 |
| `product.lineItemId`（`_ccat` を上書き） | Array | 明細項目 ID のリスト。 |
| `payment.transactionID` | Array | 支払いトランザクション ID。 |
| `payment.paymentAmount` | Array | 支払い金額。 |
| `payment.paymentType` | Array | 支払いタイプ。 |
| `payment.currencyCode` | Array | 支払い通貨コード。 |

### プライバシーオプション

| 変数 | 型 | 説明 |
|:---------| ---| :------------|
| `defaultConsent` | String | デフォルトの同意。 |


### パーソナライゼーションオプション

| 変数 | 型 | 説明 |
|:---------| --- | :------------|
| `prehidingStyle` | String | 事前非表示スタイル。 |
|`targetMigrationEnabled` | Boolean | Target の移行が有効。 |


### オーディエンスオプション

| 変数 | 型 | 説明 |
|:---------| --- | :------------|
| `cookieDestinationsEnabled` | Boolean | Cookie 宛先が有効。 |
| `urlDestinationsEnabled` | Boolean | URL 宛先が有効。 |


### ID オプション

| 変数 | 型 | 説明 |
|:---------| --- | :------------|
| `idMigrationEnabled` | Boolean | ID の移行が有効。 |
| `thirdPartyCookiesEnabled` | Boolean | サードパーティ Cookie が有効。 |
| `identityMap` | String | ID マップ。 |

### identityMap パラメーター

| 変数 | 型 | 説明 |
|:---------| ---- | :------------|
| `id_namespace` | [Array, String] | ID 名前空間。 |
| `id` | [Array, String] | ID。 |
| `authenticatedState` | [Array, String] | 認証状態。 |
| `primary` | [Array, String] | プライマリ。 |

### データストリームの上書き

| 変数 | 型 | 説明 |
|:---------| ---- | :------------|
| `edgeConfigOverrides.com_adobe_experience_platform.datasets.event.datasetId` | String | Experience Platform イベントデータセット。 |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets.profile.datasetId` | String | Experience Platform プロファイルデータセット。 |
| `edgeConfigOverrides.com_adobe_analytics.reportSuites` | [Array, String] | Adobe Analytics レポートスイート。 |
| `edgeConfigOverrides.com_adobe_identity.idSyncContainerId` | Number | Audience Manager ID 同期コンテナ。 |
| `edgeConfigOverrides.com_adobe_target.propertyToken` | String | Adobe Target プロパティトークン。 |
| `edgeConfigOverrides.datastreamId` | String | <ul><li>データストリーム ID。</li><li>複数のデータストリーム ID をコンマで区切ってマッピングできます。</li><li>sendEvent 呼び出しが行われるたびに、タグはこの変数に複数のデータストリーム ID があるかどうかを確認します。</li><li>複数のデータストリーム ID がある場合、データストリーム ID ごとに個別の sendEvent 呼び出しが行われます。</li><li>`edgeConfigOverrides.datastreamId` は `edgeConfigID` を上書きし、さらに `edgeConfigID` は構成手順で構成されたデータストリーム ID を上書きすることに注意してください。</li></l> |

### XDM イベントトリガー

| 変数 | 説明 |
|:---------|:------------|
| `advertising.clicks` | クリック |
| `advertising.completes` | 完了 |
| `advertising.conversions` | コンバージョン |
| `advertising.federated` | フェデレーション |
| `advertising.firstQuartiles` | 第 1 四分位点 |
| `advertising.impressions` | インプレッション |
| `advertising.midpoints` | 中間点 |
| `advertising.starts` | 開始 |
| `advertising.thirdQuartiles` | 第 3 四分位点 |
| `advertising.timePlayed` | 再生時間 |
| `application.close` | 終了 |
| `application.launch` | 起動 |
| `commerce.checkouts` | チェックアウト |
| `commerce.productListAdds` | 製品リストへの追加 |
| `commerce.productListOpens` | 製品リストを開く |
| `commerce.productListRemovals` | 製品リストからの削除 |
| `commerce.productListReopens` | 製品リストを再度開く |
| `commerce.productListViews` | 製品リストの表示 |
| `commerce.productViews` | 製品の表示 |
| `commerce.purchases` | 購入 |
| `commerce.saveForLaters` | 後で購入するために保存 |
| `decisioning.propositionDisplay` | 提案の表示 |
| `decisioning.propositionInteract` | 提案の操作 |
| `delivery.feedback` | フィードバック |
| `directMarketing.emailBounced` | メールのバウンス |
| `directMarketing.emailBouncedSoft` | メールのソフトバウンス |
| `directMarketing.emailClicked` | メールのクリック |
| `directMarketing.emailDelivered` | メールの配信 |
| `directMarketing.emailOpened` | メールの開封 |
| `directMarketing.emailUnsubscribed` | メールの購読解除 |
| `inappmessageTracking.dismiss` | 閉じる |
| `inappmessageTracking.display` | 表示 |
| `inappmessageTracking.interact` | 操作 |
| `leadOperation.callWebhook` | Webhook の呼び出し |
| `leadOperation.convertLead` | リードのコンバージョン |
| `leadOperation.interestingMoment` | 注目すべき瞬間 |
| `leadOperation.newLead` | 新規リード |
| `leadOperation.scoreChanged` | スコアの変更 |
| `leadOperation.statusInCampaignProgressionChanged ` | キャンペーン進行状況におけるステータスの変更 |
| `listOperation.addToList` | リストに追加 |
| `listOperation.removeFromList` | リストから削除 |
| `message.feedback` | フィードバック |
| `message.tracking` | トラッキング |
| `opportunityEvent.addToOpportunity` | 商談に追加 |
| `opportunityEvent.opportunityUpdated` | 商談の更新 |
| `opportunityEvent.removeFromOpportunity` | 商談から削除 |
| `pushTracking.applicationOpened` | アプリケーションを開く |
| `pushTracking.customAction` | カスタムアクション |
| `web.webinteraction.linkClicks` | リンクのクリック |
| `web.webpagedetails.pageViews` | ページビュー |
| `web.formFilledOut` | フォーム入力完了 |
| `identityMap` | identityMap |
| `Custom._experience.analytics.event1to100 ` | Experience Analytics イベント 1～100 |
| `Custom._experience.analytics.event101to200` | Experience Analytics イベント 101～200 |
| `Custom._experience.analytics.event201to300` | Experience Analytics イベント 201～300 |
| `Custom._experience.analytics.event301to400` | Experience Analytics イベント 301～400 |
| `Custom._experience.analytics.event401to500` | Experience Analytics イベント 401～500 |
| `Custom._experience.analytics.event501to600` | Experience Analytics イベント 501～600 |
| `Custom._experience.analytics.event601to700` | Experience Analytics イベント 601～700 |
| `Custom._experience.analytics.event701to800` | Experience Analytics イベント 701～800 |
| `Custom._experience.analytics.event801to900` | Experience Analytics イベント 801～900 |
| `Custom._experience.analytics.event901to1000` | Experience Analytics イベント 901～1000 |
| カスタム | カスタム |
### Analytics XDM データ

| 変数 | 型 | 説明 |
|:---------|---|:------------|
| `xdm.timestamp`  | 文字列 | xdm.timestamp |
| `xdm.application.isClose`  | 文字列 | xdm.application.isClose |
| `xdm.application.isInstall`  | 文字列 | xdm.application.isInstall |
| `xdm.application.isLaunch`  | 文字列 | xdm.application.isLaunch |
| `xdm.application.closeType`  | 文字列 | xdm.application.closeType |
| `xdm.application.name`  | 文字列 | xdm.application.name |
| `xdm.application.isUpgrade`  | 文字列 | xdm.application.isUpgrade |
| `xdm.application.version`  | 文字列 | xdm.application.version |
| `xdm.application.sessionLength`  | 文字列 | xdm.application.sessionLength |
| `xdm.web.webInteraction.URL`  | 文字列 | web.webInteraction.URL |
| `xdm.web.webInteraction.name`  | 文字列 | web.webInteraction.name |
| `xdm.web.webInteraction.type`  | 文字列 | web.webInteraction.type |
| `xdm.web.webPageDetails.URL`  | 文字列 | web.webPageDetails.URL |
| `xdm.web.webPageDetails.name`  | 文字列 | web.webPageDetails.name |
| `xdm.web.webPageDetails.isErrorPage`  | 文字列 | web.webPageDetails.isErrorPage |
| `xdm.web.webPageDetails.server`  | 文字列 | web.webPageDetails.server |
| `xdm.web.webPageDetails.siteSection`  | 文字列 | web.webPageDetails.siteSection |
|`xdm.web.webPageDetails.viewName`  | 文字列 |  web.webPageDetails.viewName |
| `xdm.web.webReferrer.URL`  | 文字列 | web.webReferrer.URL |
| `xdm.commerce.checkouts.id`  | 文字列 | xdm.commerce.checkouts.id |
| `xdm.commerce.checkouts.value`  | 文字列 | xdm.commerce.checkouts.value |
| `xdm.commerce.order.currencyCode`  | 文字列 | xdm.commerce.order.currencyCode |
| `xdm.commerce.order.purchaseID`  | 文字列 | xdm.commerce.order.purchaseID |
| `xdm.commerce.order.transactionID`  | 文字列 | xdm.commerce.order.transactionID |
| `xdm.commerce.productListAdds.id`  | 文字列 | xdm.commerce.productListAdds.id |
| `xdm.commerce.productListAdds.value`  | 文字列 | xdm.commerce.productListAdds.value |
| `xdm.commerce.productListOpens.id`  | 文字列 | xdm.commerce.productListOpens.id |
| `xdm.commerce.productListOpens.value`  | 文字列 | xdm.commerce.productListOpens.value |
| `xdm.commerce.productListRemovals.id`  | 文字列 | xdm.commerce.productListRemovals.id |
| `xdm.commerce.productListRemovals.value`  | 文字列 | xdm.commerce.productListRemovals.value |
| `xdm.commerce.productListViews.id`  | 文字列 | xdm.commerce.productListViews.id |
| `xdm.commerce.productListViews.value`  | 文字列 | xdm.commerce.productListViews.value |
| `xdm.commerce.productViews.id`  | 文字列 | xdm.commerce.productViews.id |
| `xdm.commerce.productViews.value`  | 文字列 | xdm.commerce.productViews.value |
| `xdm.commerce.purchases.value`  | 文字列 | xdm.commerce.purchases.value |
| `xdm.device.model`  | 文字列 | device.model |
| `xdm.device.colorDepth`  | 文字列 | device.colorDepth |
| `xdm.device.screenHeight`  | 文字列 | device.screenHeight |
| `xdm.device.screenWidth`  | 文字列 | device.screenWidth |
| `xdm.device.type`  | 文字列 | device.type |
| `xdm.environment.browserDetails.acceptLanguage`  | 文字列 | environment.browserDetails.acceptLanguage |
| `xdm.environment.browserDetails.cookiesEnabled`  | 文字列 | environment.browserDetails.cookiesEnabled |
| `xdm.environment.browserDetails.javaEnabled`  | 文字列 | environment.browserDetails.javaEnabled |
| `xdm.environment.browserDetails.userAgent`  | 文字列 | environment.browserDetails.userAgent |
| `xdm.environment.browserDetails.viewportHeight`  | 文字列 | environment.browserDetails.viewportHeight |
| `xdm.environment.browserDetails.viewportWidth`  | 文字列 | environment.browserDetails.viewportWidth |
| `xdm.environment.carrier`  | 文字列 | environment.carrier |
| `xdm.environment.connectionType`  | 文字列 | environment.connectionType |
| `xdm.environment.ipV4`  | 文字列 | environment.ipV4 |
| `xdm.environment.language`  | 文字列 | environment.language |
| `xdm.environment.operatingSystem`  | 文字列 | environment.operatingSystem |
| `xdm.environment.operatingSystemVersion`  | 文字列 | environment.operatingSystemVersion |
| `xdm.xdm.identityMap.ECID`  | 配列 | identityMap.ECID |
| `xdm.marketing.trackingCode`  | 文字列 | marketing.trackingCode |
| `xdm.media.mediaTimed.completes.value`  | 文字列 | media.mediaTimed.completes.value |
| `xdm.media.mediaTimed.dropBeforeStart.value`  | 文字列 | media.mediaTimed.dropBeforeStart.value |
| `xdm.media.mediaTimed.federated.value`  | 文字列 | media.mediaTimed.federated.value |
| `xdm.media.mediaTimed.firstQuartiles.value`  | 文字列 | media.mediaTimed.firstQuartiles.value |
| `xdm.media.mediaTimed.mediaSegmentView.value`  | 文字列 | media.mediaTimed.mediaSegmentView.value |
| `xdm.media.mediaTimed.midpoints.value`  | 文字列 | media.mediaTimed.midpoints.value |
| `xdm.media.mediaTimed.pauseTime.value`  | 文字列 | media.mediaTimed.pauseTime.value |
| `xdm.media.mediaTimed.pauses.value`  | 文字列 | media.mediaTimed.pauses.value |
| `xdm.media.mediaTimed.primaryAssetReference.@id`  | 文字列 | media.mediaTimed.primaryAssetReference.@id |
| `xdm.media.mediaTimed.primaryAssetReference.dc:title`  | 文字列 | media.mediaTimed.primaryAssetReference.dc:title |
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator\[N\].iptc4xmpExt:Name|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number`  | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number |
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating| N.iptc4xmpExt:RatingValue|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number`  | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier|
|  `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name`  | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name|
|  `xdm.media.mediaTimed.primaryAssetReference.showType`  | 文字列 | media.mediaTimed.primaryAssetReference.showType|
|  `xdm.media.mediaTimed.primaryAssetReference.xmpDM:duration` | 文字列 | media.mediaTimed.primaryAssetReference.xmpDM:duration|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.@id`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.@id
|  `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastChannel`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.broadcastChannel|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastContentType`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.broadcastContentType|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastNetwork`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork|
| `xdm.media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value |
|  `xdm.media.mediaTimed.primaryAssetViewDetails.playerName`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.playerName|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version|
|  `xdm.media.mediaTimed.primaryAssetViewDetails.sourceFeed`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.sourceFeed|
| `xdm.media.mediaTimed.primaryAssetViewDetails.streamFormat`  | 文字列 |  media.mediaTimed.primaryAssetViewDetails.streamFormat|
|  `xdm.media.mediaTimedxdm..progress10.value`  | 文字列 | media.mediaTimed.progress10.value|
|  `xdm.media.mediaTimed.progress95.value`  | 文字列 | media.mediaTimed.progress95.value|
|  `xdm.media.mediaTimed.resumes.value`  | 文字列 | media.mediaTimed.resumes.value|
|  `xdm.media.mediaTimed.starts.value`  | 文字列 | media.mediaTimed.starts.value|
|  `xdm.media.mediaTimed.thirdQuartiles.value`  | 文字列 | media.mediaTimed.thirdQuartiles.value|
|  `xdm.media.mediaTimed.timePlayed.value`  | 文字列 | media.mediaTimed.timePlayed.value|
|  `xdm.media.mediaTimed.totalTimePlayed.value`  | 文字列 | media.mediaTimed.totalTimePlayed.value|
|  `xdm.placeContext.geo.latitude`  | 文字列 |placeContext.geo.latitude|
| `xdm.placeContext.geo.longitude`  | 文字列 | placeContext.geo.longitude|
|  `xdm.placeContext.geo.postalCode`  | 文字列 | placeContext.geo.postalCode|
|  `xdm.placeContext.geo.stateProvince`  | 文字列 | placeContext.geo.stateProvince|
|  `xdm.placeContext.localTime`  | 文字列 | placeContext.localTime|
| `xdm.productListItems.lineItemId`  | 配列 | productListItems.lineItemId |
|  `xdm.productListItems.name`  | 配列 | productListItems.name|
|  `xdm.productListItems.priceTotal`  | 配列 | productListItems.priceTotal|
| `xdm.productListItems.quantity`  | 配列 | productListItems.quantity |
| `xdm.productListItems.SKU`  | 配列 | productListItems.SKU |
|  `xdm._experience.analytics.customDimensions.hierarchies.hier1` | 文字列 |  _experience.analytics.customDimensions.hierarchies.hier1|
|   `xdm._experience.analytics.customDimensions.hierarchies.hier2` | 文字列 | _experience.analytics.customDimensions.hierarchies.hier2|
|   `xdm._experience.analytics.customDimensions.hierarchies.hier3`  | 文字列 | _experience.analytics.customDimensions.hierarchies.hier3|
|   `xdm._experience.analytics.customDimensions.hierarchies.hier4` | 文字列 | _experience.analytics.customDimensions.hierarchies.hier4|
|  `xdm._experience.analytics.customDimensions.hierarchies.hier5` | 文字列 |_experience.analytics.customDimensions.hierarchies.hier5|
|   `xdm._experience.analytics.customDimensions.listProps.prop1.delimiter` | 文字列 | _experience.analytics.customDimensions.listProps.prop1.delimiter|
|   `xdm._experience.analytics.customDimensions.listProps.prop1.values` | 配列 | _experience.analytics.customDimensions.listProps.prop1.values|
|   `xdm._experience.analytics.customDimensions.lists.list1.list` | 配列 | _experience.analytics.customDimensions.lists.list1.list|
|   `xdm._experience.analytics.customDimensions.lists.list2.list` | 配列 | _experience.analytics.customDimensions.lists.list2.list|
|  `xdm._experience.analytics.customDimensions.lists.list3.list` | 配列 | _experience.analytics.customDimensions.lists.list3.list  |
|  `xdm._experience.analytics.event1to100.event1.id` | 文字列 |  _experience.analytics.event1to100.event1.id|
|  `xdm._experience.analytics.event1to100.event1.value` | 文字列 | _experience.analytics.event1to100.event1.value |

### Targetデータ（非XDM、データオブジェクト）

| 変数 | 型 | 説明 |
|:---------| --- | :------------|
| `data.__adobe.target.entity.id`  | 文字列 | entity.id |
| `data.__adobe.target.entity.name`  | 文字列 | entity.name |
| `data.__adobe.target.entity.categoryId`  | 文字列 | entity.categoryId |
| `data.__adobe.target.entity.pageUrl`  | 文字列 | entity.pageUrl |
| `data.__adobe.target.entity.thumbnailUrl`  | 文字列 | entity.thumbnailUrl |
| `data.__adobe.target.entity.message`  | 文字列 | entity.message |
| `data.__adobe.target.entity.value`  | 文字列 | entity.value |
| `data.__adobe.target.entity.inventory`  | 文字列 | entity.inventory |
| `data.__adobe.target.entity.brand`  | 文字列 | entity.brand |
| `data.__adobe.target.entity.margin`  | 文字列 | entity.margin |
| `data.__adobe.target.entity.event.detailsOnly`  | 文字列 | entity.event.detailsOnly |
| `data.__adobe.target.entity.yourCustomAttributeName`  | 文字列 | entity.yourCustomAttributeName |
| `data.__adobe.target.excludedIds`  | 文字列 | entity.excludedIds |
| `data.__adobe.target.cartIds`  | 文字列 | entity.cartIds  |
| `data.__adobe.target.productPurchasedId`  | 文字列 | entity.productPurchasedId |
| `data.__adobe.target.user.categoryId`  | 文字列 | entity.user.categoryId |
| `data.__adobe.target.profile.age`  | 文字列 | entity.profile.age |
| `data.__adobe.target.profile.gender`  | 文字列 | entity.profile.gender |

### Analytics eVar

このコネクタは、`eVar1`～`eVar250`の直接マッピングをサポートしています。たとえば、マッピング先は`_experience.analytics.customDimensions.eVars.eVar1-250`に展開されます。

### Analytics Prop

このコネクタは、`prop1`～`prop75`の直接マッピングをサポートしています。たとえば、マッピング先は`_experience.analytics.customDimensions.props.prop1-75`に展開されます。

### XDM（レガシー）

| 変数 | 型 | 説明 |
|:---------| --- |:------------|
| `account_name`  | 文字列 |アカウント名 | 
|  `pageName`  | 文字列 |ページ名 |
|  `clientID`  | 文字列 | クライアントID |


### Adobe Audience Manager構成（レガシー）

| 変数 | 型 | 説明 |
|:---------| ---| :------------|
| `cookieDestinationsEnabled`  | ブール値 | Cookie宛先が有効 |
|  `urlDestinationsEnabled`  | ブール値 | URL宛先が有効|