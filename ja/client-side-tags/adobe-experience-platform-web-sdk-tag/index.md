---
title: Adobe Experience Platform Web SDK タグ構成ガイド
description: この記事では、Adobe Experience Platform Web SDK タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-experience-platform-web-sdk-tag/
---
Adobe Experience Platform Web SDK（Adobe Alloy）は、Adobe Experience Cloudの顧客がAdobe Experience Platform Edge Networkを通じてExperience Cloudのさまざまなサービスと対話できるようにするクライアントサイドJavaScriptライブラリです。

## タグのヒント

* 標準の構成値を上書きし、カスタムパラメータを構成するためにマッピングを使用します。
* 複数のインスタンスを構成する場合、各インスタンスに固有の**Datastream ID**および**Org ID**を提供する必要があります。カンマ区切りリストで複数の値を提供します。

## 動作原理

マッピング先はドット表記で表されます。最終的なAPIペイロードは、タグで表されるドット表記に基づいてネストされたJSONオブジェクトのシリーズで構成されます。

Adobe Experience Platform Web SDKタグには、使用しているAdobeアプリケーションに特有のマッピングが含まれており、XDMおよび非XDMデータマッピングが含まれます。XDMデータは、Adobe Experience Platform内で作成したスキーマに一致する内容と構造を持つオブジェクトです。

* XDMイベントトリガー：特定の`eventType`値でイベントをトリガーするために使用します。
* イベント固有のパラメータ：特定のイベントに対してXDMおよび非XDM属性をマッピングするために使用します。
* アナリティクスXDMデータ：XDMオブジェクトに渡すデータをマッピングするために使用します。
* ターゲットデータ：ターゲットプロファイルを更新するためにデータオブジェクトに渡す非XDM属性をマッピングするために使用します。

AdobeへのXDMおよび非XDMデータの送信についての詳細は、Adobeのドキュメントの[Track Events](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html)を参照してください。

### イベント例

Adobe Experience Platform Web SDKイベントを構成するには、イベントにマッピングする変数を選択し、トリガーを指定します。変数が特定の値に等しい場合にイベントがトリガーされ、選択したイベント名が`eventType`として渡されます。

#### 使用例：XDMイベントトリガーを使用した購入イベント

購入イベントを構成するには：

1. Adobe Experience Platform Web SDKタグ構成の**データマッピング**画面に移動します。
1. 変数ドロップダウンリストから`tealium_event`を選択し、**送信先を選択**をクリックします。
1. **カテゴリ**セクションで**XDMイベントトリガー**を選択します。
1. **マップされた変数が等しい場合**フィールドに**Purchase**を構成します。これは`tealium_event`が購入をトリガーするために等しくなければならない値です。
1. **トリガーイベント**ドロップダウンリストで、**sendEvent: Commerce Events**セクションの下にある**Purchases** `(commerce.purchases)`を選択します。これは`tealium_event`が購入イベントに等しい場合にトリガーされるイベントです。

![](/images/client-side-tags/adobe-experience-web-sdk-mappings-example.png)

#### 使用例：イベント固有のパラメータを使用した購入イベント

既存のE-Commerce拡張マッピングに含まれていないデータを購入イベントで送信する必要がある場合は、**イベント固有のパラメータ**を使用します。リストから属性を選択するか、カスタム送信先を入力します。指定されたイベントと属性に対してドット表記を正確にフォローしてください。

次の例では、購入イベントで`purchaseOrderNumber`をXDMデータとして渡します：

1. Adobe Experience Platform Web SDKタグ構成の**データマッピング**画面に移動します。
1. 変数ドロップダウンリストから`po_number`（または関連するクライアント固有のデータレイヤー要素）を選択し、**送信先を選択**をクリックします。
1. **カテゴリ**セクションで**イベント固有のパラメータ**を選択します。
1. `purchaseOrderNumber`がデフォルトの送信先ではないため、**カスタムパラメータ**を選択する必要があります。**パラメータ**ドロップダウンから**カスタム**を選択し、送信先の完全なドット表記パスを入力します：`commerce.purchases.xdm.commerce.order.purchaseOrderNumber`。
1. **イベントのために**ドロップダウンリストから**Purchases**イベントを選択します。
1. **追加**をクリックしてパラメータを追加します

#### 使用例：非XDMデータ/Adobe Targetデータ

非XDMまたはTargetデータもイベントマッピングを使用して構成できます。この使用例では、Adobe Targetで使用するために`product_brand`も送信します。

1. Adobe Experience Platform Web SDKタグ構成の**データマッピング**画面に移動します。
1. 変数ドロップダウンリストから`product_brand`を選択し、**送信先を選択**をクリックします。
1. **カテゴリ**セクションで**Target Data**を選択します。
1. マッピング先として`entity.brand`を選択します。
1. 送信される購入イベントには、ペイロードに`data.__adobe.target.entity.brand`が含まれるようになります。

次の例は、E-Commerce拡張のいくつかのデフォルトマッピングを含むAdobe Web SDKの呼び出しを示しています。この例では、`commerce.purchases.xdm.commerce.order.purchaseOrderNumber`のAdobeドット表記がネストされたオブジェクトに展開されています。

```javascript
alloy(&#34;sendEvent&#34;,{
  &#34;xdm&#34;:{
    &#34;commerce&#34;:{
      &#34;order&#34;:{
        &#34;purchaseID&#34;:&#34;123456789&#34;,
        &#34;currencyCode&#34;:&#34;USD&#34;,
        &#34;priceTotal&#34;:39.98,
        &#34;purchaseOrderNumer&#34;:&#34;A1234&#34;
      }
    },
    &#34;productListItems&#34;:[
      {
        &#34;SKU&#34;:&#34;HT105&#34;,
        &#34;name&#34;:&#34;The Big Floppy Hat&#34;,
        &#34;priceTotal&#34;:29.99,
        &#34;quantity&#34;:1
      }
    ]
  },
  &#34;data&#34;:{
    __adobe: {
      target: {
        &#34;entity.brand&#34;: &#34;Acme&#34;
      }
    }
  }
});
```

## Adobe Targetでのちらつきの管理

Adobe Experience Platform Web SDKを非同期で読み込むと、以前に読み込まれたコンテンツがAdobe Targetによって更新されるため、コンテンツのちらつきが発生する可能性があります。ちらつきを最小限に抑えるために、Adobeはprehidingスニペットの追加を推奨しています。このスニペットを`utag.sync.js`テンプレートに[JavaScript拡張]()として追加します。

`utag.sync.js`の詳細については、[How `utag.sync.js` works]()を参照してください。

prehidingスニペットについての情報は、[Manage Flicker](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)を参照してください。

### Cookie Management Solutionを使用している場合の空白ページエラー

タグがトリガーされる前にユーザーが異なるクッキーカテゴリに同意するまで待つようにCookie Management Solution（CMS）を使用している場合、prehidingスニペットが読み込まれ、タイムアウトするまで（3-7秒）ページが空白のままになります。この挙動の理由は、ユーザーが同意を受け入れるまでAdobe Experience Platform Web SDKタグを読み込むことができないためです。

この問題の解決策は、同意が与えられたかどうかを確認し、同意に基づいてprehidingスニペットをトリガーするかどうかを決定することです。

Tealium以外のカスタムCMSを使用している場合は、そのCMSプラットフォームを通じて同意のチェックを管理します。

TealiumのJavaScript拡張を使用している場合は、同意クッキーがAEP Web SDKタグに属するクッキーカテゴリ（例えば機能クッキーのカテゴリ）の特定の値を含む場合にのみ関数がトリガーされるようにロジックを更新します。
#### 例

この例では、CMSは`mycms_cookie`というクッキーを構成し、ユーザーが機能クッキーの使用を承諾した場合は`functional:1`、すべてのクッキーの使用を承諾した場合は`all:1`という値を含みます。

以下のコードは、これらの値をチェックして、プリハイディングスニペットをトリガーします。

 この例には、構成に合わせて変更が必要なコード行を特定するコメントが含まれています。 

```javascript
!function(e,a,n,t){
  if (a) return;
  //クッキーが存在するかチェックし、存在する場合はその値を取得します。mycms_cookie部分をCMSのクッキーの実際の名前に更新してください。
  var cms_cookie_value = (document.cookie.match(/^(?:.*;)?\s*mycms_cookie\s*=\s*([^;]&#43;)(?:.*)?$/)||[,null])[1];
  if(cms_cookie_value){
    //受け入れられた値を配列に追加します。以下の例では、クッキーの値にall:1またはfunctional:1が含まれている必要があります。
    var accepted_values = [&#39;all:1&#39;,&#39;functional:1&#39;];
    for(var i=0;i&lt;accepted_values.length;i&#43;&#43;){
      if(cms_cookie_value.includes(accepted_values[i])){
        var x=e.head;
        if(x){
          var o=e.createElement(&#34;style&#34;);
          o.id=&#34;alloy-prehiding&#34;;
          o.innerText=n;
          x.appendChild(o);
          setTimeout(function(){o.parentNode&amp;&amp;o.parentNode.removeChild(o)},t);
          return;
        }
      }
    }
  }
}

(document, document.location.href.indexOf(&#34;adobe_authoring_enabled&#34;) !== -1, &#34;body { opacity: 0 !important }&#34;, 3000);
```

`&#34;body { opacity: 0 !important }&#34;`コードを、特定の`div`などの対象要素に更新してください。それ以外の場合、コードのデフォルト動作はコンテンツの全体を隠すことです。

## Adobe Analytics 移行ガイド

Adobe Analyticsタグは、Adobe Experience Platform Web SDKタグに置き換えられたレガシータグです。Adobe Experience Platform Web SDKタグは、Experience Data Model (XDM) を Adobe Analytics形式に変換してデータを送信します。

Adobe Experience Platform Web SDKタグは、レガシー変数、プロパティ、イベントをサポートしています。

### コード比較

以下の例は、Adobe AnalyticsとAdobe Experience Platform Web SDKの呼び出しの構造的な違いを示しています：

#### Adobe Analytics

```javascript
// AppMeasurementライブラリをロード
var s = new AppMeasurement();
// レポートスイートIDを構成
s.account = &#34;example-rsid&#34;;
// ページ名を構成
s.pageName = &#34;Home Page&#34;;
// 必要に応じて他の変数を構成
s.prop1 = &#34;value1&#34;;
s.eVar1 = &#34;value2&#34;;
s.hellow = &#34;value3&#34;;
// データをAdobe Analyticsサーバーに送信
var s_code = s.t();
if (s_code) document.write(s_code);
```

#### Adobe Experience Platform Web SDK

```javascript
window.alloy(&#34;sendEvent&#34;, {
    // イベントのタイプを構成
    type: &#34;viewStart&#34;,
    // Adobe Analyticsのデータを構成
    xdm: {
      web: {
        webPageDetails: {
          // ページ名を構成
          name: &#34;Home Page&#34;
        }
      },
      _experience: {
        analytics: {
          customDimensions: {
            props: {
              prop1: &#34;value1&#34;
            },
            eVars: {
              eVar1: &#34;value2&#34;
            }
          }
        }
      },
    },
    data: {
      // 必要に応じて他の変数を構成
      hellow: &#34;value3&#34;,
    }
  });
```

### Tealium Toolsを使用してAdobe Analyticsタグを移行する

Adobe Experience Platform Web SDK Migratorツールを使用すると、既存のAdobe Analytics AppMeasurementタグをAdobe Experience Platform Web SDKタグに移行できます。

Migratorツールを使用する前に、以下の制限に注意してください：

* このツールはdoPluginsや拡張機能を移行しません。構成にdoPluginsや拡張機能を使用している場合は、それらを手動で移行する必要があります。これらの要素を移行する方法については、Adobeのドキュメントの[Migrate events globally](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally)セクションを参照してください。
* `link_name`および`link_trackvars`変数はサポートされていません。
* `products`変数は、Adobe Experience Platform Web SDKタグで手動でマッピングできるように異なる属性に分割する必要があります。詳細については、Adobeのドキュメントの[products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en)を参照してください。
* ツールで自動的に移行されないイベントや属性は、空のマッピングになります。これらの空の属性は、[Migrate the Adobe Analytics tag manually](#migrate-the-adobe-analytics-tag-manually)ガイドを使用して手動でマッピングできます。

Adobe AnalyticsタグをTealium Toolsを使用して移行するには、次の手順を完了してください：

1. 次のURLでJSON定義を使用してTealium ToolsにAdobe Experience Platform Web SDK Migratorを追加します：https://solutions.tealium.net/hosted/tealiumTools/aep_migrate/aep_migrate.json。カスタムツールを追加する方法の詳細については、[Manage Custom Tools]()を参照してください。
1. **Tag Management &gt; Tags**に移動し、Adobe Experience Platform Web SDK Migratorツールを起動します。
1. 移行の一環として既存のAdobe Analyticsタグを無効にするには、**Disable existing tag**を選択します。
1. 移行の範囲を選択します：
    * すべてのAppMeasurementタグ
    * すべてのアクティブなAppMeasurementタグ
    * 特定のAppMeasurementタグ（移行したいタグのUIDを追加する必要があります。）
1. **Start**をクリックします。
Migratorツールは、既存のAdobe Analytics AppMeasurementタグを自動的にAdobe Experience Platform Web SDKタグに移行します。
1. プロファイルを保存して公開します。

構成にdoPluginsや拡張機能を使用している場合は、それらを手動で移行する必要があります（下記参照）。
### Adobe Analyticsタグを手動で移行する

Adobe AnalyticsタグからAdobe Experience Platform Web SDKタグへ手動で移行するには、以下の手順を完了してください。

この移行ガイドでは、Adobe Analyticsタグの以下の例示データマッピングを使用します：

![](/images/client-side-tags/adobe-analytics-migration-example1.png)

![](/images/client-side-tags/adobe-analytics-migration-example2.png)

1. タグマーケットプレイスにアクセスして、新しいAdobe Experience Platform Web SDKタグを追加します。詳細については、[タグについて]()を参照してください。
1. Tealiumで以下のタグ構成を構成します：
    * **Org ID**: Adobeに割り当てられたExperience Cloud組織ID。例：`XXX@AdobeOrg`。
    * **Datastream ID**: Adobeに割り当てられたdatastream IDで、SDKを適切なアカウントと構成にリンクします。`edgeConfigId`とも呼ばれます。
1. Adobe Experience Platformで以下の構成を構成します：
    1. **Datastreams**にアクセスし、移行で使用するdatastreamを選択します。
    1. Datastreamの**Configure**画面で、datastreamで使用される**Event Schema**をメモし、**Save**をクリックします。![](/images/client-side-tags/adobe-experience-platform-datastreams.png)
    1. Datastreamの詳細画面で、Adobe Analyticsサービスが有効であることを確認し、サービスを選択します。![](/images/client-side-tags/adobe-experience-platform-service.png)
    1. **Adobe Analyticsサービス**画面で、適切なデータストアを指すAdobe **Report Suite ID**を入力します。![](/images/client-side-tags/adobe-experience-platform-aa-enable.png)
    1. **Data Management &gt; Schemas**にアクセスし、datastreamにリンクされた**Event Schema**を選択します。
    1. **Field Groups**に**Adobe Analytics ExperienceEvent Template**フィールドグループが含まれていることを確認します。![](/images/client-side-tags/adobe-experience-platform-schemas.png)
1. この例では、以下のレガシー属性、プロパティ、イベントをTealiumのAdobe Experience Platform Web SDKタグにマッピングします。詳細については、[データマッピングについて]()を参照してください。
    1. Adobe Experience Platform Web SDKタグで**Data Mappings**にアクセスします。
    1. **sf (js)**変数を選択し、**Analytics eVars &gt; evar181**にマッピングして**Done**をクリックします。
    1. **page_category (js)**変数を選択し、**Analytics Props &gt; prop5**にマッピングして**Done**をクリックします。
    1. **medallia_custom_event(js)**変数と**XDM Event Trigger**を選択します。以下の値を使用してマッピングを構成し、**Done**をクリックします：
        * カスタムデスティネーションとして`MDigital_Invite_Displayed:_experience.analytics.event101to200`を追加します。
        * マッピングされた変数が**MDigital_Invite_Displayed**と等しい場合
        * トリガーイベント：**Experience Analytics Events 101-200 (\_experience.analytics.event101to200)**
        * カスタムイベント名：**200**
    1. **page_category (js)**変数を選択し、以下の値を使用してマッピングを構成し、**Done**をクリックします：
        * カスタムデスティネーションとして`xdm._experience.analytics.customDimension`と`data.channel`を追加します。
        * **Non-XDM/Custom Schema**にアクセスし、**Non-XDM/Custom Schema Path**に**channel**を入力します。
1. **Finish**をクリックします。
1. **Adobe Analyticsタグ**を無効にします。
1. 保存して公開します。

Adobe Experience Platform Datastream、サービス、スキーマの構成についての詳細は、Adobeのドキュメントの以下の記事を参照してください：

* [Datastreamの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UIでスキーマを作成および編集する](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Analyticsの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#analytics)

## タグ構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Tag Version**: 適切なタグバージョンを選択します。デフォルトは最新バージョンです。
* **Instance Name**: SDKの名前空間です。デフォルトは`alloy`です。
* **Org ID**: Adobeに割り当てられたExperience Cloud組織ID。例：`XXX@AdobeOrg`。
* **Edge Domain**: Adobeサービスとのやり取りに使用されるドメインです。最初のパーティドメインの1つをAdobeが提供するドメインにCNAMEを使用してマッピングした場合は、デフォルト構成を更新します。
* **Datastream ID**: Adobeに割り当てられたdatastream IDで、SDKを適切なアカウントと構成にリンクします。`edgeConfigId`とも呼ばれます。
* **Debug Enabled**: ブラウザのJavaScriptコンソールにデバッグメッセージが表示されるようにします。
* **Edge Base Path**: Adobeアカウントで構成されています。デフォルトは`ee`です。
* **Auto Pageview Tracking**: すべてのページビューに対して自動的に`web.webpagedetails.pageViews`イベントを発火します。
* **Auto Purchase Tracking**: 注文IDが存在する場合に自動的に`commerce.purchases`イベントを発火します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグの対応するデスティネーション変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
| --- | --- | --- |
| `library_version`  | 文字列 | タグバージョン。 |
| `context`  | 配列 | コンテキスト。 |
| `debugEnabled`  | ブール値 | デバッグが有効。 |
| `decisionScopes`  | 配列 | 決定スコープ。 |
| `defaultConsent`  | 文字列 | デフォルトの同意。 |
| `downloadLinkQualifier`  | 文字列 | ダウンロードリンク修飾子。 |
| `edgeConfigId`  | 文字列 | datastream ID。 |
| `edgeDomain`  | 文字列 | エッジドメイン。 |
| `edgeBasePath`  | 文字列 | エッジベースパス。 |
| `auto_page_tracking`  | ブール値 | 自動ページトラッキング。 |
| `auto_purchase_tracking`  | ブール値 | 自動購入トラッキング。 |
| `event_type`  | 文字列 | イベントタイプ。 |
| `errorsEnabled`  | ブール値 | エラーが有効。 |
| `hasHidingSnippet`  | ブール値 | Adobe target pre-hidingスニペット。 |
| `instanceName`  | 文字列 | インスタンス名。 |
| `orgId`  | 文字列 | 組織ID。 |
| `renderDecisions`  | ブール値 | 決定をレンダリング。 |
| `documentUnloading`  | ブール値 | ドキュメントアンローディング。 |
| `custom.##` | - | カスタムデータ。  | 
| `commandCallback`  | 関数 | `commandCallback`関数。 |

### データ収集

| 変数 | タイプ | 説明 |
| ---| --- | --- |
| `clickCollectionEnabled`  | ブール値 | クリック収集が有効。 |
| `onBeforeEventSend`  | 関数 | onBeforeEventSend関数。 |
| `onBeforeLinkClickSend`  | 関数 | onBeforeLinkClickSend関数。 |
| `internalLinkEnabled` | ブール値 | 内部リンクが有効。 |
| `downloadLinkEnabled` | ブール値 | ダウンロードリンクが有効。 |
| `externalLinkEnabled` | ブール値 | 外部リンクが有効。 |
| `eventGroupingEnabled` | ブール値 | イベントグルーピングが有効。 |
| `sessionStorageEnabled` | ブール値 | セッション保存が有効。 |
| `filterClickDetails` | 関数 | クリック詳細をフィルタリングする。 |
### ストリーミングメディア

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `channel` | 文字列 | 必須。ストリーミングメディアの収集が行われるチャンネルの名前。例えば、ビデオチャンネル。 |
| `playerName` | 文字列 | 必須。メディアプレーヤーの名前。 |
| `appVersion` | 文字列 | メディアプレーヤーアプリケーションのバージョン。 |
| `mainPingInterval` | 整数 | メインコンテンツのピング頻度（秒）。デフォルト値は10秒。10秒から50秒の範囲で構成可能。値が指定されていない場合、自動追跡セッションを使用する際にデフォルト値が使用されます。詳細は[データ収集：自動追跡メディアセッションの作成](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/createmediasession#automatic)を参照してください。 |
| `adPingInterval` | 整数 | 広告コンテンツのピング頻度（秒）。デフォルト値は10秒。1秒から10秒の範囲で構成可能。値が指定されていない場合、自動追跡セッションを使用する際にデフォルト値が使用されます。詳細は[データ収集：自動追跡メディアセッションの作成](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/createmediasession#automatic)を参照してください。 |

### Eコマース

| 変数 | タイプ | 説明 |
|:---------| --- | :------------|
| `purchaseID` (`_corder`を上書き) | 文字列 | 注文ID。 | 
| `priceTotal` (`_ctotal`を上書き) | 文字列 | 注文合計。 | 
| `currencyCode` (`_ccurrency`を上書き) | 文字列 | 通貨。 | 
| `product.name` (`_cprodname`を上書き) | 配列 | 名前のリスト。 |
| `product.SKU` (`_csku`を上書き) | 配列 | SKUのリスト。 |
| `product.quantity` (`_cquan`を上書き) | 配列 | 数量のリスト。 |
| `product.priceTotal` (`_cprice`を上書き) | 配列 | 価格のリスト。 |
| `product.lineItemId` (`_ccat`を上書き) | 配列 | ラインアイテムIDのリスト。 |
| `payment.transactionID` | 配列 | 支払い取引ID。 |
| `payment.paymentAmount` | 配列 | 支払い金額。 |
| `payment.paymentType` | 配列 | 支払いタイプ。 |
| `payment.currencyCode` | 配列 | 支払い通貨コード。 |

### プライバシーオプション

| 変数 | タイプ | 説明 |
|:---------| ---| :------------|
| `defaultConsent` | 文字列 | デフォルトの同意。 |

### パーソナライゼーションオプション

| 変数 | タイプ | 説明 |
|:---------| --- | :------------|
| `prehidingStyle` | 文字列 | プリハイディングスタイル。 |
| `targetMigrationEnabled` | ブール値 | ターゲット移行が有効。 |

### オーディエンスオプション

| 変数 | タイプ | 説明 |
|:---------| --- | :------------|
| `cookieDestinationsEnabled` | ブール値 | Cookieの送信先が有効。 |
| `urlDestinationsEnabled` | ブール値 | URLの送信先が有効。 |

### アイデンティティオプション

| 変数 | タイプ | 説明 |
|:---------| --- | :------------|
| `idMigrationEnabled` | ブール値 | ID移行が有効。 |
| `thirdPartyCookiesEnabled` | ブール値 | サードパーティのクッキーが有効。 |
| `identityMap` | 文字列 | アイデンティティマップ。 |

### identityMapパラメータ

| 変数 | タイプ | 説明 |
|:---------| ---- | :------------|
| `id_namespace` | [配列, 文字列] | ID名前空間。 |
| `id` | [配列, 文字列] | ID。 |
| `authenticatedState` | [配列, 文字列] | 認証状態。 |
| `primary` | [配列, 文字列] | プライマリ。 |

### Datastreamオーバーライド

| 変数 | タイプ | 説明 |
|:---------| ---- | :------------|
| `edgeConfigOverrides.com_adobe_experience_platform.datasets.event.datasetId` | 文字列 | Experience Platformイベントデータセット。 |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets.profile.datasetId` | 文字列 | Experience Platformプロファイルデータセット。 |
| `edgeConfigOverrides.com_adobe_analytics.reportSuites` | [配列, 文字列] | Adobe Analyticsレポートスイート。 |
| `edgeConfigOverrides.com_adobe_identity.idSyncContainerId` | 数値 | Audience Manager ID同期コンテナ。 |
| `edgeConfigOverrides.com_adobe_target.propertyToken` | 文字列 | Adobe Targetプロパティトークン。 |
| `edgeConfigOverrides.datastreamId` | 文字列 | &lt;ul&gt;&lt;li&gt;データストリームID。&lt;/li&gt;&lt;li&gt;カンマで区切られた複数のデータストリームIDをマッピングできます。&lt;/li&gt;&lt;li&gt;sendEventコールが行われるたびに、この変数に複数のデータストリームIDがあるかどうかをタグが確認します。&lt;/li&gt;&lt;li&gt;複数のデータストリームIDがある場合、各データストリームIDに対して別々のsendEventコールが行われます。&lt;/li&gt;&lt;li&gt;`edgeConfigOverrides.datastreamId`は、構成ステップで構成されたデータストリームIDを上書きする`edgeConfigID`を上書きします。&lt;/li&gt;&lt;/ul&gt; |

### XDMイベントトリガー

| 変数 | 説明 |
|:---------|:------------|
| `advertising.clicks` | クリック |
| `advertising.completes` | 完了 |
| `advertising.conversions` | コンバージョン |
| `advertising.federated` | フェデレーテッド |
| `advertising.firstQuartiles` | 第1四分位数 |
| `advertising.impressions` | インプレッション |
| `advertising.midpoints` | 中間点 |
| `advertising.starts` | 開始 |
| `advertising.thirdQuartiles` | 第3四分位数 |
| `advertising.timePlayed` | 再生時間 |
| `application.close` | 閉じる |
| `application.launch` | 起動 |
| `commerce.checkouts` | チェックアウト |
| `commerce.productListAdds` | 商品リスト追加 |
| `commerce.productListOpens` | 商品リストオープン |
| `commerce.productListRemovals` | 商品リスト削除 |
| `commerce.productListReopens` | 商品リスト再オープン |
| `commerce.productListViews` | 商品リスト表示 |
| `commerce.productViews` | 商品表示 |
| `commerce.purchases` | 購入 |
| `commerce.saveForLaters` | 後で保存 |
| `decisioning.propositionDisplay` | 提案表示 |
| `decisioning.propositionInteract` | 提案インタラクション |
| `delivery.feedback` | フィードバック |
| `directMarketing.emailBounced` | メールバウンス |
| `directMarketing.emailBouncedSoft` | メールソフトバウンス |
| `directMarketing.emailClicked` | メールクリック |
| `directMarketing.emailDelivered` | メール配信完了 |
| `directMarketing.emailOpened` | メール開封 |
| `directMarketing.emailUnsubscribed` | メール購読解除 |
| `inappmessageTracking.dismiss` | 閉じる |
| `inappmessageTracking.display` | 表示 |
| `inappmessageTracking.interact` | インタラクト |
| `leadOperation.callWebhook` | ウェブフック呼び出し |
| `leadOperation.convertLead` | リード変換 |
| `leadOperation.interestingMoment` | 興味深い瞬間 |
| `leadOperation.newLead` | 新規リード |
| `leadOperation.scoreChanged` | スコア変更 |
| `leadOperation.statusInCampaignProgressionChanged ` | キャンペーン進行中のステータス変更 |
| `listOperation.addToList` | リスト追加 |
| `listOperation.removeFromList` | リスト削除 |
| `message.feedback` | フィードバック |
| `message.tracking` | トラッキング |
| `opportunityEvent.addToOpportunity` | 機会追加 |
| `opportunityEvent.opportunityUpdated` | 機会更新 |
| `opportunityEvent.removeFromOpportunity` | 機会削除 |
| `pushTracking.applicationOpened` | アプリケーション開始 |
| `pushTracking.customAction` | カスタムアクション |
| `web.webinteraction.linkClicks` | リンククリック |
| `web.webpagedetails.pageViews` | ページビュー |
| `web.formFilledOut` | フォーム入力完了 |
| `identityMap` | アイデンティティマップ |
| `Custom._experience.analytics.event1to100 ` | エクスペリエンスアナリティクスイベント1-100 |
| `Custom._experience.analytics.event101to200` | エクスペリエンスアナリティクスイベント101-200 |
| `Custom._experience.analytics.event201to300` | エクスペリエンスアナリティクスイベント201-300 |
| `Custom._experience.analytics.event301to400` | エクスペリエンスアナリティクスイベント301-400 |
| `Custom._experience.analytics.event401to500` | エクスペリエンスアナリティクスイベント401-500 |
| `Custom._experience.analytics.event501to600` | エクスペリエンスアナリティクスイベント501-600 |
| `Custom._experience.analytics.event601to700` | エクスペリエンスアナリティクスイベント601-700 |
| `Custom._experience.analytics.event701to800` | エクスペリエンスアナリティクスイベント701-800 |
| `Custom._experience.analytics.event801to900` | エクスペリエンスアナリティクスイベント801-900 |
| `Custom._experience.analytics.event901to1000` | エクスペリエンスアナリティクスイベント901-1000 |
| カスタム | カスタム |
### Analytics XDM データ

| 変数 | タイプ | 説明 |
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
| `xdm.web.webPageDetails.viewName`  | 文字列 | web.webPageDetails.viewName |
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
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator\[N\].iptc4xmpExt:Name|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number`  | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number |
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating\[N\].iptc4xmpExt:RatingValue|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number`  | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier|
| `xdm.media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name`  | 文字列 | media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name|
| `xdm.media.mediaTimed.primaryAssetReference.showType`  | 文字列 | media.mediaTimed.primaryAssetReference.showType|
| `xdm.media.mediaTimed.primaryAssetReference.xmpDM:duration` | 文字列 | media.mediaTimed.primaryAssetReference.xmpDM:duration|
| `xdm.media.mediaTimed.primaryAssetViewDetails.@id`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.@id
| `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastChannel`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.broadcastChannel|
| `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastContentType`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.broadcastContentType|
| `xdm.media.mediaTimed.primaryAssetViewDetails.broadcastNetwork`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork|
| `xdm.media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value |
| `xdm.media.mediaTimed.primaryAssetViewDetails.playerName`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.playerName|
| `xdm.media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version|
| `xdm.media.mediaTimed.primaryAssetViewDetails.sourceFeed`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.sourceFeed|
| `xdm.media.mediaTimed.primaryAssetViewDetails.streamFormat`  | 文字列 | media.mediaTimed.primaryAssetViewDetails.streamFormat|
| `xdm.media.mediaTimed.progress10.value`  | 文字列 | media.mediaTimed.progress10.value|
| `xdm.media.mediaTimed.progress95.value`  | 文字列 | media.mediaTimed.progress95.value|
| `xdm.media.mediaTimed.resumes.value`  | 文字列 | media.mediaTimed.resumes.value|
| `xdm.media.mediaTimed.starts.value`  | 文字列 | media.mediaTimed.starts.value|
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

### ターゲットデータ（非XDM、データオブジェクト）

| 変数 | タイプ | 説明 |
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

### アナリティクス eVars

このコネクタは `eVar1`-`eVar250` に直接マッピングをサポートしています。例えば、マッピング先は `_experience.analytics.customDimensions.eVars.eVar1-250` に展開されます。

### アナリティクス Props

このコネクタは `prop1`-`prop75` に直接マッピングをサポートしています。例えば、マッピング先は `_experience.analytics.customDimensions.props.prop1-75` に展開されます。

### XDM (レガシー)

| 変数 | タイプ| 説明 |
|:---------| --- |:------------|
| `account_name`  | 文字列 |アカウント名 | 
|  `pageName`  | 文字列 |ページ名 |
|  `clientID`  | 文字列 | クライアントID |


### Adobe Audience Manager Config (レガシー)

| 変数 | タイプ | 説明 |
|:---------| ---| :------------|
| `cookieDestinationsEnabled`  | ブール値 | Cookie Destinations Enabled |
|  `urlDestinationsEnabled`  | ブール値 | URL Destinations Enabled|

