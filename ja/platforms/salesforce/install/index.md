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

詳細については、[Salesforce Connector Setup Guide for AudienceStream]()を参照してください。

リードオブジェクトにこのカスタムフィールドを追加するには：

1. **構成**から**リード &gt; フィールド**へ進みます。  
![](/images/server-side-connectors/salesforce-ui-edit-leas-custom-field.png)
1. 次の構成でテキストタイプの新しいカスタムフィールドを追加します：
      * **フィールドラベル**: Tealium ID.
      * **長さ**: 100.
      * **フィールド名**: `tealium_id_teal`.
    `_teal`接尾辞は、これらの変数がTealiumに特有であることを示します。
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
    private static String tealiumAccount       = &#34;YOUR_ACCOUNT&#34;;
    private static String tealiumProfile       = &#34;YOUR_PROFILE&#34;;
    private static String tealiumDataSourceKey = &#34;YOUR_DATASOURCE_KEY&#34;;
    private static String tealiumEventType     = &#34;derived&#34;;
    private static String tealiumEndpoint      = &#34;https://collect.tealiumiq.com/event&#34;;
    @future(callout=true)
    public static void track(Map&lt;String, String&gt; tealiumData){
        List&lt;String&gt; tealiumParams = New List&lt;String&gt;();
        tealiumParams.add(&#34;tealium_account&#34;    &#43; &#34;=&#34; &#43; tealiumAccount);
        tealiumParams.add(&#34;tealium_profile&#34;    &#43; &#34;=&#34; &#43; tealiumProfile);
        tealiumParams.add(&#34;tealium_datasource&#34; &#43; &#34;=&#34; &#43; tealiumDataSourceKey);
        tealiumParams.add(&#34;tealium_event_type&#34; &#43; &#34;=&#34; &#43; tealiumEventType);
        tealiumParams.add(&#34;tealium_event&#34;      &#43; &#34;=&#34; &#43;
            EncodingUtil.urlEncode(tealiumData.get(&#34;tealium_event&#34;), &#34;UTF-8&#34;));
        String tealiumVid = tealiumData.get(&#34;tealium_visitor_id&#34;);
        if(tealiumVid == null || tealiumVid == &#34;&#34;){
            tealiumData.remove(&#34;tealium_visitor_id&#34;);
        }
        for(String key : tealiumData.keySet()){
            try{
                String value = tealiumData.get(key);
                Boolean valueTest = (value != null);
                tealiumParams.add(key &#43; &#34;=&#34; &#43; (valueTest ? EncodingUtil.urlEncode(value, &#34;UTF-8&#34;) : &#34;&#34;));
            }catch(Exception e){}
        }
        HttpRequest req = new HttpRequest();
        String tealCollect = tealiumEndpoint &#43; &#34;?&#34; &#43; String.join(tealiumParams, &#34;&amp;&#34;);
        req.setEndpoint(tealCollect);
        if(debug){
            System.debug(tealCollect);
        }
        req.setMethod(&#34;GET&#34;);
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
    String tealiumEvent = &#34;crm_contact_update&#34;;

    /* POPULATE TEALIUM DATA LAYER */
    Map&lt;string,string&gt; tealiumData = new Map&lt;string,string&gt;();
    for (Contact sfdcObj : Trigger.new ){
        /* REQUIRED TEALIUM DATA */
        tealiumData.put(&#34;tealium_event&#34;, tealiumEvent);
        tealiumData.put(&#34;tealium_visitor_id&#34;, sfdcObj.tealium_id_teal__c);

        /* SFDC DATA */
        tealiumData.put(&#34;customer_email&#34;,      sfdcObj.Email);
        tealiumData.put(&#34;crm_lead_source&#34;,     sfdcObj.LeadSource);
        tealiumData.put(&#34;has_opted_out_email&#34;, String.valueOf(sfdcObj.HasOptedOutOfEmail));
        tealiumData.put(&#34;has_opted_out_phone&#34;, String.valueOf(sfdcObj.DoNotCall));
        tealiumData.put(&#34;mobile_phone_number&#34;, String.valueOf(sfdcObj.MobilePhone));
        tealiumData.put(&#34;home_phone_number&#34;,   String.valueOf(sfdcObj.Phone));
        tealiumData.put(&#34;customer_first_name&#34;, sfdcObj.FirstName);
        tealiumData.put(&#34;customer_last_name&#34;,  sfdcObj.LastName);
        tealiumData.put(&#34;customer_title&#34;,      sfdcObj.Title);
        tealiumData.put(&#34;crm_account&#34;,         String.valueOf(sfdcObj.Account));
        /* Addition Custom Fields */
        /* tealiumData.put(&#34;custom_field&#34;, sfdcObj.customField); */

        TealiumCollect.track(tealiumData);
    }
}
```

#### リードオブジェクトトリガー

```java
trigger tealiumLeadUpdate on Lead (after insert, after update) {
    String tealiumEvent = &#34;crm_lead_update&#34;;

    /* POPULATE TEALIUM DATA LAYER */
    Map&lt;string,string&gt; tealiumData = new Map&lt;string,string&gt;();
    for (Lead sfdcObj : Trigger.new ){
        /* REQUIRED TEALIUM DATA */
        tealiumData.put(&#34;tealium_event&#34;, tealiumEvent);
        tealiumData.put(&#34;tealium_visitor_id&#34;, sfdcObj.tealium_id_teal__c);

        /* SFDC DATA */
        tealiumData.put(&#34;customer_email&#34;,      sfdcObj.Email);
        tealiumData.put(&#34;crm_lead_status&#34;,     sfdcObj.Status);
        tealiumData.put(&#34;crm_lead_source&#34;,     sfdcObj.LeadSource);
        tealiumData.put(&#34;crm_lead_rating&#34;,     sfdcObj.Rating);
        tealiumData.put(&#34;crm_lead_industry&#34;,   sfdcObj.Industry);
        tealiumData.put(&#34;crm_lead_company&#34;,    sfdcObj.Company);
        tealiumData.put(&#34;has_opted_out_email&#34;, String.valueOf(sfdcObj.HasOptedOutOfEmail));
        tealiumData.put(&#34;has_opted_out_phone&#34;, String.valueOf(sfdcObj.DoNotCall));
        tealiumData.put(&#34;mobile_phone_number&#34;, String.valueOf(sfdcObj.MobilePhone));
        tealiumData.put(&#34;home_phone_number&#34;,   String.valueOf(sfdcObj.Phone));
        tealiumData.put(&#34;customer_first_name&#34;, sfdcObj.FirstName);
        tealiumData.put(&#34;customer_last_name&#34;,  sfdcObj.LastName);
        /* Addition Custom Fields */
        /* tealiumData.put(&#34;custom_field&#34;, sfdcObj.customField); */

        TealiumCollect.track(tealiumData);
    }
}
```
### リード変換マッピング

カスタムフィールド **Tealium ID** をリードからコンタクトへの変換時に保持するためには、**Lead.Tealium ID** を **Contact.Tealium ID** にマッピングする必要があります。

詳細については、[Salesforce Sales Cloud Basics: Map Custom Lead Fields for Lead Conversion](https://help.salesforce.com/s/articleView?id=sales.customize_mapleads.htm&amp;type=5)を参照してください。

カスタムフィールドマッピングを作成するには、以下の手順に従ってください：

1. **Lead &gt; Fields** に移動します。
1. **Map Fields** をクリックします。
1. **Contact** をクリックします。
1. Lead列の `tealium_id` をContact列の **Tealium ID** にマッピングします。

    ![](/images/server-side-connectors/tealium-salesforce-lead-conversion-mapping.png)

1. **Save** をクリックします。

### リモートサイト構成の有効化

Tealium Collectエンドポイントは、HTTPリクエストを送信するためにSalesforceのリモートサイト構成に登録する必要があります。

詳細については、[Apex Developer Guide: Adding Remote Site Settings](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm)を参照してください。

以下の構成でリモートサイトを作成します：

* **リモートサイト名**: TealiumCollect
* **リモートサイトURL**: `https://collect.tealiumiq.com`
* **プロトコルセキュリティの無効化**: 有効

#### リモートサイトの例

![](/images/server-side-connectors/screen-shot-2016-10-04-at-2.32.44-pm.png)

### Salesforceイベント属性の追加

Apexトリガーコードで使用されるSalesforce変数は、Tealiumのイベント属性として定義する必要があります。Salesforceからどのようなデータが来ているかを確認するには、トリガーコードを調べるか、[Live Events]()を使用してリアルタイムでデータを確認してください。

イベント属性を追加するには、以下の手順に従ってください：

1. **Enrich &gt; Attributes** に移動します。
1. **&#43; Add Attribute** をクリックします。
1. スコープを選択：**Event**。
1. タイプを選択：**Universal Data Object**。
1. データタイプを選択：**String**。
1. トリガーコードで使用されている変数名と同じ **Name** を構成します。例えば `crm_lead_status` など。
1. 保存して公開します。