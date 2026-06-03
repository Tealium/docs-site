---
title: Install
description: This article explains how to install and configure the Tealium for Salesforce using Apex classes and triggers to track Lead and Contact updates with Tealium Collect.
url: https://docs.tealium.com/platforms/salesforce/install/
---
## Requirements

* Salesforce administrator access
* Tealium account enabled for AudienceStream or EventStream

## Install the solution

The Tealium for Salesforce solution is installed as a number of Apex classes: one for the Tealium Collect service and one or more to trigger on object updates. It also requires updates to Salesforce configuration to support linking records from Customer Data Hub and to allow the sending of HTTP requests from Salesforce to Tealium.

### Link records from Customer Data Hub to Salesforce

The Tealium for Salesforce solution can link records from the Customer Data Hub into Salesforce by specifying a shared identifier attribute. In Customer Data Hub this attribute can be any Visitor ID attribute that uniquely identifies records coming from an ingestion sync. In Salesforce you must create a custom field in the Object named **Tealium ID** to capture that Customer Data Hub attribute.

For more information, see the [Salesforce Connector Setup Guide for AudienceStream]().

To add this custom field to the Lead object:

1. From **Setup**, go to **Lead &gt; Fields**.  
![](/images/server-side-connectors/salesforce-ui-edit-leas-custom-field.png)
1. Add a new custom field of type Text with the following settings:
      * **Field Label**: Tealium ID.
      * **Length**: 100.
      * **Field Name**: `tealium_id_teal`.
    The `_teal` suffix indicates that these variables are specific to Tealium.
1. Click **Save**.

### Create the `TealiumCollect` Apex class

This `TealiumCollect` Apex class generates the HTTP request to the Tealium Collect service. It takes the Tealium configuration and data layer values and formats them into the required URL format.

For more information, see [Apex Developer Guide: Introducing Apex](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_intro.htm).

To add the `TealiumCollect` Apex class:

1. From the **Developer Console** create a **Class** named `TealiumCollect`.
1. Copy and paste the following code, making sure to specify your account, profile, and data source key:  
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

### Create the Apex trigger for lead or contact updates

This trigger activates based on an update to a Salesforce object. Triggers can be changed to activate on many other object stages and can be customized and filtered to specific scenarios.

For more information, see [Apex Developer Guide: Triggers](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers.htm).

Use the following steps to create the Tealium trigger:

1. Within the **Developer Console**, create a **Trigger** named `TealiumLeadUpdate` (or `TealiumContactUpdate` based on the object).
1. Copy and paste the Contact object trigger or Lead object trigger code below.
1. Modify the code to match the object you are tracking (`Contact` or `Lead`).

#### Contact object trigger

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

#### Lead object trigger

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

### Lead conversion mapping

To preserve the custom field **Tealium ID** during a Lead conversion to a Contact you must map **Lead.Tealium ID** to **Contact.Tealium ID**.

For more information, see [Salesforce Sales Cloud Basics: Map Custom Lead Fields for Lead Conversion](https://help.salesforce.com/s/articleView?id=sales.customize_mapleads.htm&amp;type=5).

Use the following steps to create a custom field mapping:

1. Go to **Lead &gt; Fields**.
1. Click **Map Fields**.
1. Click **Contact**.
1. Map `tealium_id` in the Lead column to **Tealium ID**&#34;in the Contact column.  
    
    ![](/images/server-side-connectors/tealium-salesforce-lead-conversion-mapping.png)

1. Click **Save**.

### Enable remote site settings

The Tealium Collect endpoint must be registered in the remote site settings of Salesforce to send HTTP requests.

For more information, see [Apex Developer Guide: Adding Remote Site Settings](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm).

Create the remote site with the following settings:

* **Remote Site Name**: TealiumCollect
* **Remote Site URL**: `https://collect.tealiumiq.com`
* **Disable Protocol Security**: Enable

#### Remote site example

![](/images/server-side-connectors/screen-shot-2016-10-04-at-2.32.44-pm.png)

### Add Salesforce event attributes

The Salesforce variables used in the Apex trigger code must be defined in Tealium as event attributes. To see what data is coming from Salesforce, inspect the trigger code or use [Live Events]() to see the data in real-time.

Use the following steps to add event attributes:

1. Go to **Enrich &gt; Attributes**.
1. Click **&#43; Add Attribute**.
1. Select the scope: **Event**.
1. Select the type: **Universal Data Object**.
1. Select the data type: **String**.
1. Set the **Name** to the same variable name used in the trigger code, such as `crm_lead_status`.
1. Save and Publish.
