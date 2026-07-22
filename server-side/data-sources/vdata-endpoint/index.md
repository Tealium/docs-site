---
title: Import data using Visitor Data Enrichment (/vdata)
description: Send real-time data updates to EventStream from any external system.
url: https://docs.tealium.com/server-side/data-sources/vdata-endpoint/
---## Introduction

You are likely familiar with the following two standard methods of ingesting data into EventStream:

* The [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/) that manages triggering website event data to EventStream. This tag is configured within Tealium iQ.
* [File Import Data Source](https://docs.tealium.com/about-file-import/) manages the process of bulk importing visitor data into EventStream.

Did you know there is a third method for EventStream to receive data? This additional method is called Visitor Data Enrichment and can be used to send real-time data updates to EventStream from any external system. The following sections provide details and examples.

### What is /vdata/i.gif ?

* The `/vdata/` path in the Tealium Collect endpoint is used to receive data typically in a name/value pair format traditional to tracking pixels.  
   ```
   //my.domain.com/my.gif?name1=value1&name2=value2
   ```

* The `/vdata/ `URL has some key-values that are special and required (those that begin with `tealium_`), but everything else is simply used to build the data layer  
   ```
   //collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE&tealium_vid=ID&name1=value1&name2=value2
   ```

* Data collection can be isolated to a specific region.  
For example, use `collect-eu-central-1.tealiumiq.com` for data collection only in Germany

### Potential Use Cases

The following list describes potential uses of Visitor Data Enrichment.

* Send data to vendors through EventStream  
Mobile apps have the ability to trigger data directly from the application to EventStream, skipping the webview, using Tealium `/vdata/i.gif`.
* Use as an endpoint for cookie sync services  
This allows a tag vendor to redirect to the `/vdata/i.gif` location and send their visitor ID to EventStream
* Impression Tracking  
Display advertisements are typically loaded in an iFrame. The Visitor Data Enrichment can help track which ads have been displayed to a visitor.
* A CMS/CRM/BI/etc system can POST a JSON object of data to EventStream  
This method can be used if your system generates sensitive data that you do not want to be fed through the browser, but EventStream needs the data in real-time to take action on the visitor.

### Required Parameters for the Tealium REST Endpoint

The following table describes required parameters for the Tealium REST endpoint:

|Parameter| Description|
|---| ---|
|`tealium_account`| The account name for EventStream/Tealium iQ|
|`tealium_profile`| The profile name where you have EventStream configured|
|`tealium_vid`| The unique Visitor ID or Secondary ID, such as encoded Email Address or Device ID, from which the tracking request originates|
|`tealium_trace_id`| (Optional) Required only for testing with Trace feature|

## Sample GET Request

```
GET //collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE&tealium_vid=ID&ut.event=view&page_name=product_detail&product_id=sku123456
```

#### What this 'Might' Look Like Embedded in an Email

```
<img src="//collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE&tealium_vid=ID&ut.event=view&email_id=december2015&content_type=
```

Using the `/vdata/i.gif` is the most common method for using the Visitor Data Enrichment and we strongly suggest using it. As there may be limitations or requirements around sending the data in a different format directly from a server, we provide options for doing so in the following sections.

### Sample GET Request using JavaScript

The following example shows how to code a display ad to send the impression tracking information to EventStream.

```
//build your object of data
var a={
    "data":{
        "event_name":"ad_tracking",
        "ad_image_id":"%%macro_to_get_ADID%%",
        "ad_advertiser_id":"%%macro_to_get_ADVID%%",
        "ad_campaign_id":"%%macro_to_get_CAMPID%%",
        "ad_user_id":"%%macro_to_get_USERID%%"
    },
    "event":"view"
}

//stringify the object for the GET event
var json_string = JSON.stringify(a);

//send the data to your collect endpoint
var img = new Image();
img.src='//collect.tealiumiq.com/account/profile/2/i.gif?data='+encodeURIComponent(json_string);

```

## Sample POST Request

The POST request examples are similar to GET except that the POST of data is not as limited to the amount of data it can send as compared to GET.

### Sample POST Request using JavaScript

```
//build your object of data
var a={
   "data":{
      "event_name":"myEvent",
      "customer_id":"user1@tealium.com",
      "cp.trace_id":"12345"
   },
   "event":"view" //change this to "link" or "view" depending on the type of event
}

//stringify the object for the POST event
var json_string = JSON.stringify(a);

//POST the data to your collect endpoint
if (json_string!="") {
   var formData = new FormData();
   formData.append("data", json_string);
   function postData(data) {
      var xhr = new XMLHttpRequest();
      xhr.open('post', "//collect.tealiumiq.com/account/profile/2/i.gif", true);
      xhr.withCredentials = true;
      xhr.send(data);
   }
   postData(formData);
}
```

### Sample POST Request using cURL

The following example shows how to POST data to EventStream from a Command Line Interface (CLI) or terminal for Mac. This example would likely only be used for testing.

```
curl -H "Content-Type: application/json" -X POST -d '{"data":{"event_name":"myEvent","customer_id":"user1@tealium.com","cp.trace_id":"12345"},"event":"view"}' https://collect.tealiumiq.com/account/profile/2/i.gif
```

### Sample POST Request using Python

The following example shows how to programmatically code this to run using Python and is based on an example from [python.org](https://docs.python.org/release/2.6/library/httplib.html).

```
import requests, json
body = {'data':{'event_name':'abc_score','cp.trace_id':'04759','abc_score':'0.56','customer_id':'9999999'},'event':'view'}
headers = {"Content-Type": "text/plain","Accept": "image/gif"}
r = requests.post(' https://collect.tealiumiq.com/account/profile/2/i.gif', data = json.dumps(body), headers=headers);
```

This example uses the Python "Requests" module, which can be installed using the following command:

```
pip2 install requests
```

For Python3, use:

```
pip3 install requests
```


<blockquote>
When complete, update and test accordingly.
</blockquote>

