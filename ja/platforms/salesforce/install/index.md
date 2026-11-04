---
title: インストール
description: この記事では、Apex クラスとトリガーを使用してリードと取引先責任者の更新を Tealium Collect で追跡するために、Tealium for Salesforce をインストールして構成する方法について説明します。
url: https://docs.tealium.com/ja/platforms/salesforce/install/
---
## 要件

* Salesforce の管理者アクセス権
* Customer Data Platform（CDP）または Event Streaming が有効になっている Tealium アカウント

## ソリューションのインストール

Tealium for Salesforce ソリューションは、複数の Apex クラスとしてインストールされます。1 つは Tealium Collect サービス用で、残りの 1 つ以上はオブジェクトの更新時にトリガーするためのものです。また、Customer Data Hub からのレコードのリンクをサポートし、Salesforce から Tealium への HTTP リクエスト送信を許可するために、Salesforce の構成を更新する必要があります。

### Customer Data Hub から Salesforce へのレコードのリンク

Tealium for Salesforce ソリューションでは、共通の識別子属性を指定することで、Customer Data Hub から Salesforce にレコードをリンクできます。Customer Data Hub では、この属性として、取り込み同期から取得したレコードを一意に識別する任意の Visitor ID 属性を使用できます。Salesforce では、その Customer Data Hub 属性を取得するために、オブジェクト内に **Tealium ID** という名前のカスタム項目を作成する必要があります。

詳細については、[CDP 向け Salesforce コネクタ構成ガイド](https://docs.tealium.com/salesforce-connector/)を参照してください。

このカスタム項目をリードオブジェクトに追加するには、次の手順を実行します。

1. **構成**から、**リード > 項目**に移動します。  
![](https://docs.tealium.com/images/server-side-connectors/salesforce-ui-edit-leas-custom-field.png)
1. 次の構成で、テキスト型の新しいカスタム項目を追加します。
      * **項目の表示ラベル**：Tealium ID。
      * **文字数**：100。
      * **項目名**：`tealium_id_teal`。
    
<blockquote>
サフィックス `_teal` は、これらの変数が Tealium 固有であることを示します。
</blockquote>

1. **保存**をクリックします。

### `TealiumCollect` Apex クラスの作成

この `TealiumCollect` Apex クラスは、Tealium Collect サービスへの HTTP リクエストを生成します。Tealium の構成とデータレイヤーの値を受け取り、必要な URL 形式に整形します。

詳細については、[Apex 開発者ガイド：Apex の概要](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro.htm)を参照してください。

`TealiumCollect` Apex クラスを追加するには、次の手順を実行します。

1. **開発者コンソール**で、`TealiumCollect` という名前の**クラス**を作成します。
1. 次のコードをコピーして貼り付け、アカウント、プロファイル、データソースキーを必ず指定します。  
```java
public class TealiumCollect {
    private static Boolean debug = true;
    /* TEALIUM CONFIGURATION */
    private static String tealiumAccount       = "YOUR_ACCOUNT";
    private static String tealiumProfile       = "YOUR_PROFILE";
    private static String tealiumDataSourceKey = "YOUR_DATASOURCE_KEY";
    private static String tealiumEventType     = "derived";
    private static String tealiumEndpoint      = "https://collect.tealiumiq.com/event";
    @future(callout=true)
    public static void track(Map<String, String> tealiumData){
        List<String> tealiumParams = New List<String>();
        tealiumParams.add("tealium_account"    + "=" + tealiumAccount);
        tealiumParams.add("tealium_profile"    + "=" + tealiumProfile);
        tealiumParams.add("tealium_datasource" + "=" + tealiumDataSourceKey);
        tealiumParams.add("tealium_event_type" + "=" + tealiumEventType);
        tealiumParams.add("tealium_event"      + "=" +
            EncodingUtil.urlEncode(tealiumData.get("tealium_event"), "UTF-8"));
        String tealiumVid = tealiumData.get("tealium_visitor_id");
        if(tealiumVid == null || tealiumVid == ""){
            tealiumData.remove("tealium_visitor_id");
        }
        for(String key : tealiumData.keySet()){
            try{
                String value = tealiumData.get(key);
                Boolean valueTest = (value != null);
                tealiumParams.add(key + "=" + (valueTest ? EncodingUtil.urlEncode(value, "UTF-8") : ""));
            }catch(Exception e){}
        }
        HttpRequest req = new HttpRequest();
        String tealCollect = tealiumEndpoint + "?" + String.join(tealiumParams, "&");
        req.setEndpoint(tealCollect);
        if(debug){
            System.debug(tealCollect);
        }
        req.setMethod("GET");
        Http http = new Http();
        HTTPResponse res = http.send(req);
    }
}
```

### リードまたは取引先責任者の更新用 Apex トリガーの作成

このトリガーは、Salesforce オブジェクトの更新に基づいて作動します。トリガーは、オブジェクトのさまざまな段階で作動するように変更でき、特定のシナリオに合わせてカスタマイズおよびフィルタリングできます。

詳細については、[Apex 開発者ガイド：トリガー](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers.htm)を参照してください。

次の手順に従って Tealium トリガーを作成します。

1. **開発者コンソール**で、`TealiumLeadUpdate`（オブジェクトに応じて `TealiumContactUpdate`）という名前の**トリガー**を作成します。
1. 以下の取引先責任者オブジェクトまたはリードオブジェクトのトリガーコードをコピーして貼り付けます。
1. 追跡対象のオブジェクト（`Contact` または `Lead`）に合わせてコードを変更します。

#### 取引先責任者オブジェクトのトリガー

```java
trigger tealiumContactUpdate on Contact (after insert, after update) {
    String tealiumEvent = "crm_contact_update";

    /* POPULATE TEALIUM DATA LAYER */
    Map<string,string> tealiumData = new Map<string,string>();
    for (Contact sfdcObj : Trigger.new ){
        /* REQUIRED TEALIUM DATA */
        tealiumData.put("tealium_event", tealiumEvent);
        tealiumData.put("tealium_visitor_id", sfdcObj.tealium_id_teal__c);

        /* SFDC DATA */
        tealiumData.put("customer_email",      sfdcObj.Email);
        tealiumData.put("crm_lead_source",     sfdcObj.LeadSource);
        tealiumData.put("has_opted_out_email", String.valueOf(sfdcObj.HasOptedOutOfEmail));
        tealiumData.put("has_opted_out_phone", String.valueOf(sfdcObj.DoNotCall));
        tealiumData.put("mobile_phone_number", String.valueOf(sfdcObj.MobilePhone));
        tealiumData.put("home_phone_number",   String.valueOf(sfdcObj.Phone));
        tealiumData.put("customer_first_name", sfdcObj.FirstName);
        tealiumData.put("customer_last_name",  sfdcObj.LastName);
        tealiumData.put("customer_title",      sfdcObj.Title);
        tealiumData.put("crm_account",         String.valueOf(sfdcObj.Account));
        /* Addition Custom Fields */
        /* tealiumData.put("custom_field", sfdcObj.customField); */

        TealiumCollect.track(tealiumData);
    }
}
```

#### リードオブジェクトのトリガー

```java
trigger tealiumLeadUpdate on Lead (after insert, after update) {
    String tealiumEvent = "crm_lead_update";

    /* POPULATE TEALIUM DATA LAYER */
    Map<string,string> tealiumData = new Map<string,string>();
    for (Lead sfdcObj : Trigger.new ){
        /* REQUIRED TEALIUM DATA */
        tealiumData.put("tealium_event", tealiumEvent);
        tealiumData.put("tealium_visitor_id", sfdcObj.tealium_id_teal__c);

        /* SFDC DATA */
        tealiumData.put("customer_email",      sfdcObj.Email);
        tealiumData.put("crm_lead_status",     sfdcObj.Status);
        tealiumData.put("crm_lead_source",     sfdcObj.LeadSource);
        tealiumData.put("crm_lead_rating",     sfdcObj.Rating);
        tealiumData.put("crm_lead_industry",   sfdcObj.Industry);
        tealiumData.put("crm_lead_company",    sfdcObj.Company);
        tealiumData.put("has_opted_out_email", String.valueOf(sfdcObj.HasOptedOutOfEmail));
        tealiumData.put("has_opted_out_phone", String.valueOf(sfdcObj.DoNotCall));
        tealiumData.put("mobile_phone_number", String.valueOf(sfdcObj.MobilePhone));
        tealiumData.put("home_phone_number",   String.valueOf(sfdcObj.Phone));
        tealiumData.put("customer_first_name", sfdcObj.FirstName);
        tealiumData.put("customer_last_name",  sfdcObj.LastName);
        /* Addition Custom Fields */
        /* tealiumData.put("custom_field", sfdcObj.customField); */

        TealiumCollect.track(tealiumData);
    }
}
```
### リードコンバージョンのマッピング

リードから取引先責任者への変換時にカスタム項目 **Tealium ID** を保持するには、**Lead.Tealium ID** を **Contact.Tealium ID** にマッピングする必要があります。

詳細については、[Salesforce Sales Cloud の基本：リード変換用のカスタムリード項目のマッピング](https://help.salesforce.com/s/articleView?id=sales.customize_mapleads.htm&type=5)を参照してください。

次の手順でカスタム項目のマッピングを作成します。

1. **Lead > Fields** に移動します。
1. **Map Fields** をクリックします。
1. **Contact** をクリックします。
1. Lead 列の `tealium_id` を Contact 列の **Tealium ID** にマッピングします。  
    
    ![](https://docs.tealium.com/images/server-side-connectors/tealium-salesforce-lead-conversion-mapping.png)

1. **Save** をクリックします。

### リモートサイト構成の有効化

HTTPリクエストを送信するには、Tealium CollectエンドポイントをSalesforceのリモートサイト構成に登録する必要があります。

詳細については、[Apex開発者ガイド：リモートサイト構成の追加](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm)を参照してください。

次の構成でリモートサイトを作成します。

* **Remote Site Name**：TealiumCollect
* **Remote Site URL**：`https://collect.tealiumiq.com`
* **Disable Protocol Security**：有効

#### リモートサイトの例

![](https://docs.tealium.com/images/server-side-connectors/screen-shot-2016-10-04-at-2.32.44-pm.png)

### Salesforceイベント属性の追加

Apexトリガーコードで使用されるSalesforce変数は、Tealiumでイベント属性として定義する必要があります。Salesforceから送信されるデータを確認するには、トリガーコードを調査するか、[Live Events](https://docs.tealium.com/about-live-events/)を使用してリアルタイムでデータを確認します。

次の手順でイベント属性を追加します。

1. **Enrich > Attributes** に移動します。
1. **+ Add Attribute** をクリックします。
1. スコープとして **Event** を選択します。
1. タイプとして **Universal Data Object** を選択します。
1. データ型として **String** を選択します。
1. **Name** を、`crm_lead_status` など、トリガーコードで使用されている変数名と同じ名前に構成します。
1. 保存してパブリッシュします。