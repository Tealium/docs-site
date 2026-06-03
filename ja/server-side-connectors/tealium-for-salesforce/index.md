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

追加の参考資料：[AudienceStreamのSalesforceコネクタセットアップガイド]()

Leadオブジェクトにこのカスタムフィールドを追加するには、次の手順を実行します：

1. **セットアップ**から**リード &gt; フィールド**に移動します。
![](/images/server-side-connectors/salesforce-ui-edit-leas-custom-field.png)
1. 次の構成で、テキストタイプの新しいカスタムフィールドを追加します：
      * **フィールドラベル**：Tealium ID
      * **長さ**：100
      * **フィールド名**：`tealium_id_teal`  
    `_teal`のサフィックスは、これらの変数をTealiumに名前空間として指定するのに役立ちます。
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
        String tealiumVid = tealiumData.get(&#34;tealium_vid&#34;);
        if(tealiumVid == null || tealiumVid == &#34;&#34;){
            tealiumData.remove(&#34;tealium_vid&#34;);
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
    String tealiumEvent = &#34;crm_contact_update&#34;;

    /* POPULATE TEALIUM DATA LAYER */
    Map&lt;string,string&gt; tealiumData = new Map&lt;string,string&gt;();
    for (Contact sfdcObj : Trigger.new ){
        /* REQUIRED TEALIUM DATA */
        tealiumData.put(&#34;tealium_event&#34;, tealiumEvent);
        tealiumData.put(&#34;tealium_vid&#34;, sfdcObj.tealium_id_teal__c);

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
        /* 追加のカスタムフィールド */
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
        tealiumData.put(&#34;tealium_vid&#34;, sfdcObj.tealium_id_teal__c);

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
        /* 追加のカスタムフィールド */
        /* tealiumData.put(&#34;custom_field&#34;, sfdcObj.customField); */

        TealiumCollect.track(tealiumData);
    }
}
```

### リード変換マッピング

リードを連絡先に変換する際に、カスタムフィールド**Tealium ID**を保持するために、**Lead.Tealium ID**を**Contact.Tealium ID**にマッピングする必要があります。

追加の参考資料：Salesforce - [リード変換のためのカスタムリードフィールドのマッピング](https://help.salesforce.com/articleView?id=customize_mapleads.htm&amp;amp;type=0)

カスタムフィールドマッピングを作成するには、次の手順を実行します：

1. **リード &gt; フィールド**に移動します。
1. **フィールドのマッピング**をクリックします。
1. **連絡先**をクリックします。
1. リードの列の`tealium_id`を連絡先の列の**Tealium ID**にマッピングします。  
![](/images/server-side-connectors/tealium-salesforce-lead-conversion-mapping.png)

1. **保存**をクリックします。

### リモートサイトの有効化

HTTPリクエストを送信するために、Tealium CollectエンドポイントをSalesforceのリモートサイト構成に登録する必要があります。

追加の参考資料：[Apex - リモートサイト構成の追加](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm)

次の構成で新しいリモートサイトを作成します：

* **リモートサイト名**：TealiumCollect
* **リモートサイトURL**：`https://collect.tealiumiq.com`
* **プロトコルセキュリティの無効化**：有効

#### リモートサイトの例

![](/images/server-side-connectors/screen-shot-2016-10-04-at-2.32.44-pm.png)

### Salesforceイベント属性の追加

Apexトリガーコードで使用されるSalesforce変数は、Tealiumでイベント属性として定義する必要があります。Salesforceからのデータを確認するには、トリガーコードを検査するか、[**ライブイベント**を使用してリアルタイムでデータを確認]()できます。

イベント属性を追加するには、次の手順を実行します：

1. **Enrich &gt; Attributes**に移動します。
1. **&#43; 属性を追加**をクリックします。
1. スコープを選択します：**イベント**。
1. タイプを選択します：**Universal Data Object**。
1. データ型を選択します：**String**。
1. **名前**をトリガーコードで使用される変数名と同じに構成します（例：`crm_lead_status`）。
1. 保存/公開します。
