---
title: インストール
description: この記事では、Apexクラスとトリガーを使用してSalesforceでTealiumをインストールおよび構成し、Tealium Collectでリードとコンタクトの更新を追跡する方法について説明します。
url: https://docs.tealium.com/ja/platforms/salesforce/install/
---
## 要件

* Salesforce管理者アクセス
* AudienceStreamまたはEventStream用に有効化されたTealiumアカウント

## ソリューションのインストール

Tealium for Salesforceソリューションは、Tealium Collectサービス用のApexクラスとオブジェクト更新をトリガーするための1つ以上のクラスとしてインストールされます。また、Customer Data HubからのレコードをSalesforceにリンクし、SalesforceからTealiumへのHTTPリクエストの送信を許可するために、Salesforce構成の更新が必要です。

### Customer Data HubからSalesforceへのレコードリンク

Tealium for Salesforceソリューションは、共有識別子属性を指定することで、Customer Data HubからSalesforceにレコードをリンクできます。Customer Data Hubでは、この属性は摂取同期から来るレコードを一意に識別する任意の訪問ID属性にすることができます。Salesforceでは、そのCustomer Data Hub属性をキャプチャするためにオブジェクトに**Tealium ID**というカスタムフィールドを作成する必要があります。

詳細については、[Salesforce Connector Setup Guide for AudienceStream](https://docs.tealium.com/salesforce-connector/)を参照してください。

リードオブジェクトにこのカスタムフィールドを追加するには：

1. **構成**から**リード > フィールド**へ進みます。  
![](https://docs.tealium.com/images/server-side-connectors/salesforce-ui-edit-leas-custom-field.png)
1. 次の構成でテキストタイプの新しいカスタムフィールドを追加します：
      * **フィールドラベル**: Tealium ID.
      * **長さ**: 100.
      * **フィールド名**: `tealium_id_teal`.
    
<blockquote>
`_teal`接尾辞は、これらの変数がTealiumに特有であることを示します。
</blockquote>

1. **保存**をクリックします。

### `TealiumCollect` Apexクラスの作成

この`TealiumCollect` Apexクラスは、Tealium CollectサービスへのHTTPリクエストを生成します。それはTealium構成とデータレイヤー値を取り、必要なURL形式にフォーマットします。

詳細については、[Apex Developer Guide: Introducing Apex](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro.htm)を参照してください。

`TealiumCollect` Apexクラスを追加するには：

1. **開発者コンソール**で`TealiumCollect`という名前の**クラス**を作成します。
1. 次のコードをコピーして貼り付け、アカウント、プロファイル、データソースキーを指定してください：  
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

### リードまたはコンタクト更新のためのApexトリガーの作成

このトリガーは、Salesforceオブジェクトの更新に基づいてアクティブ化されます。トリガーは多くの他のオブジェクトステージでアクティブ化するように変更でき、特定のシナリオにフィルタリングしてカスタマイズすることができます。

詳細については、[Apex Developer Guide: Triggers](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers.htm)を参照してください。

Tealiumトリガーを作成するための手順は次のとおりです：

1. **開発者コンソール**内で、`TealiumLeadUpdate`（またはオブジェクトに基づいて`TealiumContactUpdate`）という名前の**トリガー**を作成します。
1. 以下のコンタクトオブジェクトトリガーコードまたはリードオブジェクトトリガーコードをコピーして貼り付けます。
1. トラッキングしているオブジェクト（`Contact`または`Lead`）に合わせてコードを変更します。

#### コンタクトオブジェクトトリガー

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

#### リードオブジェクトトリガー

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
### リード変換マッピング

カスタムフィールド **Tealium ID** をリードからコンタクトへの変換時に保持するためには、**Lead.Tealium ID** を **Contact.Tealium ID** にマッピングする必要があります。

詳細については、[Salesforce Sales Cloud Basics: Map Custom Lead Fields for Lead Conversion](https://help.salesforce.com/s/articleView?id=sales.customize_mapleads.htm&type=5)を参照してください。

カスタムフィールドマッピングを作成するには、以下の手順に従ってください：

1. **Lead > Fields** に移動します。
1. **Map Fields** をクリックします。
1. **Contact** をクリックします。
1. Lead列の `tealium_id` をContact列の **Tealium ID** にマッピングします。

    ![](https://docs.tealium.com/images/server-side-connectors/tealium-salesforce-lead-conversion-mapping.png)

1. **Save** をクリックします。

### リモートサイト構成の有効化

Tealium Collectエンドポイントは、HTTPリクエストを送信するためにSalesforceのリモートサイト構成に登録する必要があります。

詳細については、[Apex Developer Guide: Adding Remote Site Settings](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm)を参照してください。

以下の構成でリモートサイトを作成します：

* **リモートサイト名**: TealiumCollect
* **リモートサイトURL**: `https://collect.tealiumiq.com`
* **プロトコルセキュリティの無効化**: 有効

#### リモートサイトの例

![](https://docs.tealium.com/images/server-side-connectors/screen-shot-2016-10-04-at-2.32.44-pm.png)

### Salesforceイベント属性の追加

Apexトリガーコードで使用されるSalesforce変数は、Tealiumのイベント属性として定義する必要があります。Salesforceからどのようなデータが来ているかを確認するには、トリガーコードを調べるか、[Live Events](https://docs.tealium.com/about-live-events/)を使用してリアルタイムでデータを確認してください。

イベント属性を追加するには、以下の手順に従ってください：

1. **Enrich > Attributes** に移動します。
1. **+ Add Attribute** をクリックします。
1. スコープを選択：**Event**。
1. タイプを選択：**Universal Data Object**。
1. データタイプを選択：**String**。
1. トリガーコードで使用されている変数名と同じ **Name** を構成します。例えば `crm_lead_status` など。
1. 保存して公開します。