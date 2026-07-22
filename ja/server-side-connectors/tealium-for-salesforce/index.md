---
title: SalesforceのためのTealium
description: この記事では、SalesforceのためのTealiumソリューションについて説明します。
url: https://docs.tealium.com/ja/server-side-connectors/tealium-for-salesforce/
---
## 要件

* Salesforce管理者アクセス権限
* AudienceStreamまたはEventStreamに対応したTealiumアカウント

## インストール

Tealium for Salesforceソリューションは、Tealium Collectサービス用のApexクラスと、オブジェクトの更新をトリガーするための1つ以上のApexクラスとしてインストールされます。また、Salesforceの構成を更新して、Customer Data Hubからのレコードのリンク付けとSalesforceからTealiumへのHTTPリクエストの送信をサポートする必要があります。

このソリューションのビデオ概要については、次のチャレンジャービデオをご覧ください：

### Customer Data HubからSalesforceへのレコードのリンク付け

Tealium for Salesforceソリューションは、共有識別子属性を指定することで、Customer Data HubからSalesforceへのレコードのリンク付けが可能です。Customer Data Hubでは、この属性は、インジェスシンク（オムニチャネルのアップロードなど）から来るレコードを一意に識別する任意のビジターID属性であることができます。Salesforceでは、オブジェクトに**Tealium ID**という名前のカスタムフィールドを作成する必要があります。

追加の参考資料：[AudienceStreamのSalesforceコネクタセットアップガイド](https://docs.tealium.com/salesforce-connector/)

Leadオブジェクトにこのカスタムフィールドを追加するには、次の手順を実行します：

1. **セットアップ**から**リード > フィールド**に移動します。
![](https://docs.tealium.com/images/server-side-connectors/salesforce-ui-edit-leas-custom-field.png)
1. 次の構成で、テキストタイプの新しいカスタムフィールドを追加します：
      * **フィールドラベル**：Tealium ID
      * **長さ**：100
      * **フィールド名**：`tealium_id_teal`  
    
<blockquote>
`_teal`のサフィックスは、これらの変数をTealiumに名前空間として指定するのに役立ちます。
</blockquote>

1. **保存**をクリックします。

### Apexクラス：TealiumCollect

このTealiumCollect Apexクラスは、Tealium CollectサービスへのHTTPリクエストを生成します。Tealiumの構成とデータレイヤの値を取り、必要なURL形式にフォーマットします。

追加の参考資料：[Apexクイックスタート](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro.htm)

TealiumCollect Apexクラスを追加するには、次の手順を実行します：

1. **開発者コンソール**から、`TealiumCollect`という名前の新しい**クラス**を作成します。
1. 次のコードをコピーして貼り付けます。アカウント、プロファイル、およびデータソースキーを指定することを忘れないでください：
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
        String tealiumVid = tealiumData.get("tealium_vid");
        if(tealiumVid == null || tealiumVid == ""){
            tealiumData.remove("tealium_vid");
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

### Apexトリガー：リード/連絡先の更新

このトリガーは、Salesforceオブジェクトの更新に基づいてアクティブ化されます。トリガーは他の多くのオブジェクトステージでアクティブ化するように変更することができ、特定のシナリオにカスタマイズおよびフィルタリングすることもできます。

追加の参考資料：[Apex - トリガー](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers.htm)

Tealiumトリガーを作成するには、次の手順を実行します：

1. **開発者コンソール**内で、`TealiumLeadUpdate`（またはオブジェクトに基づいて`TealiumContactUpdate`）という名前の新しい**トリガー**を作成します。
1. 以下のコードをコピーして貼り付けます。
1. コードを変更して、トラッキングしているオブジェクトに合わせます（`Contact`または`Lead`）。

#### 連絡先オブジェクトトリガー

```java
trigger tealiumContactUpdate on Contact (after insert, after update) {
    String tealiumEvent = "crm_contact_update";

    /* POPULATE TEALIUM DATA LAYER */
    Map<string,string> tealiumData = new Map<string,string>();
    for (Contact sfdcObj : Trigger.new ){
        /* REQUIRED TEALIUM DATA */
        tealiumData.put("tealium_event", tealiumEvent);
        tealiumData.put("tealium_vid", sfdcObj.tealium_id_teal__c);

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
        /* 追加のカスタムフィールド */
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
        tealiumData.put("tealium_vid", sfdcObj.tealium_id_teal__c);

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
        /* 追加のカスタムフィールド */
        /* tealiumData.put("custom_field", sfdcObj.customField); */

        TealiumCollect.track(tealiumData);
    }
}
```

### リード変換マッピング

リードを連絡先に変換する際に、カスタムフィールド**Tealium ID**を保持するために、**Lead.Tealium ID**を**Contact.Tealium ID**にマッピングする必要があります。

追加の参考資料：Salesforce - [リード変換のためのカスタムリードフィールドのマッピング](https://help.salesforce.com/articleView?id=customize_mapleads.htm&amp;type=0)

カスタムフィールドマッピングを作成するには、次の手順を実行します：

1. **リード > フィールド**に移動します。
1. **フィールドのマッピング**をクリックします。
1. **連絡先**をクリックします。
1. リードの列の`tealium_id`を連絡先の列の**Tealium ID**にマッピングします。  
![](https://docs.tealium.com/images/server-side-connectors/tealium-salesforce-lead-conversion-mapping.png)

1. **保存**をクリックします。

### リモートサイトの有効化

HTTPリクエストを送信するために、Tealium CollectエンドポイントをSalesforceのリモートサイト構成に登録する必要があります。

追加の参考資料：[Apex - リモートサイト構成の追加](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm)

次の構成で新しいリモートサイトを作成します：

* **リモートサイト名**：TealiumCollect
* **リモートサイトURL**：`https://collect.tealiumiq.com`
* **プロトコルセキュリティの無効化**：有効

#### リモートサイトの例

![](https://docs.tealium.com/images/server-side-connectors/screen-shot-2016-10-04-at-2.32.44-pm.png)

### Salesforceイベント属性の追加

Apexトリガーコードで使用されるSalesforce変数は、Tealiumでイベント属性として定義する必要があります。Salesforceからのデータを確認するには、トリガーコードを検査するか、[**ライブイベント**を使用してリアルタイムでデータを確認](https://docs.tealium.com/about-live-events/)できます。

イベント属性を追加するには、次の手順を実行します：

1. **Enrich > Attributes**に移動します。
1. **+ 属性を追加**をクリックします。
1. スコープを選択します：**イベント**。
1. タイプを選択します：**Universal Data Object**。
1. データ型を選択します：**String**。
1. **名前**をトリガーコードで使用される変数名と同じに構成します（例：`crm_lead_status`）。
1. 保存/公開します。
