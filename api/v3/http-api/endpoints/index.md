---
title: HTTP API endpoints
description: The HTTP API lets you send data to Tealium.
url: https://docs.tealium.com/api/v3/http-api/endpoints/
---
## GET method

The GET method passes data using key-value pairs in the query string of the endpoint. This method returns a 1x1 transparent GIF to make it compatible with HTML-based implementations.

### Examples for `/event`

#### Example cURL request

```bash
curl -i -X GET &#39;https://{host}/v3/collect/event?tealium_account={account}&amp;tealium_profile={profile}&amp;tealium_event=user_login&amp;email_address=user@example.com&#39;
--header &#39;Authorization: Bearer eyJ0**&#39;
```

#### Example response

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:08:50 GMT
&lt; content-type: image/gif
&lt; content-length: 43
&lt; x-amzn-requestid: 03bb378a-2619-4440-9d5a-c1e7d0e8d2ae
&lt; x-amzn-remapped-content-length: 43
&lt; x-region: us-east-1
&lt; x-acc: {account}:{profile}:2:event
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: f513ef4b-5870-4fa4-b908-38c5e12bf3e4
&lt; x-amz-apigw-id: VSBy2Fu6oAMFezA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-0182b50695a2297ec
&lt; expires: Fri, 15 Jul 2022 00:08:50 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; x-tid: f513ef4b58704fa4b90838c5e12bf3e4
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:50 GMT
```

## POST method

The POST method supports JSON payloads where the request header must be set to `Content-Type: application/json` and the payload must be formatted as a valid JSON string.

### Examples for `/event`

#### Example cURL request

```bash
curl --location --request POST &#39;https://{host}/v3/collect/event&#39; --header &#39;Authorization: Bearer eyJ0eXA***&#39; --header &#39;Content-Type: application/json&#39; --data-raw &#39;{
&#34;tealium_account&#34;: &#34;{account}&#34;,
&#34;tealium_datasource&#34;: &#34;abc123&#34;,
&#34;tealium_profile&#34;: &#34;{profile}&#34;,
&#34;tealium_event&#34;: &#34;page_view&#34;,
&#34;page_type&#34;: &#34;123&#34;,
&#34;page_name&#34;: &#34;testName&#34;
}&#39;
```

#### Example response

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:08:03 GMT
&lt; content-type: application/json
&lt; content-length: 0
&lt; x-amzn-requestid: ad5c154f-3053-4991-9a60-45b35745eba7
&lt; x-region: us-east-1
&lt; x-acc: {account}:main:2:event
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: 1d6b9c12-16c3-44a9-95c9-78afeabaf8e0
&lt; x-amz-apigw-id: VSBroH24oAMFXpQ=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-0a95ad51791af67ac
&lt; expires: Fri, 15 Jul 2022 00:08:03 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; x-tid: abc123_071422_1
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:03 GMT
```

### Examples for `/bulk-event`

#### Example cURL request

```bash
curl --location --request POST &#39;https://{host}/v3/collect/bulk-event&#39; \
--header &#39;Authorization: Bearer eyJ0eXAi***&#39; \
--header &#39;Content-Type: application/json&#39; \
--data-raw &#39;{
    &#34;shared&#34;: {
      &#34;tealium_account&#34;: &#34;{account}&#34;,
      &#34;tealium_profile&#34;: &#34;{profile}&#34;,
      &#34;tealium_environment&#34;: &#34;prod&#34;,
      &#34;tealium_datasource&#34;: &#34;{datasource}&#34;,
      &#34;tealium_visitor_id&#34;: &#34;abc123_071222_1&#34;
    },
    &#34;events&#34;: [
      {
        &#34;page_name&#34;: &#34;test1&#34;,
        &#34;tealium_event&#34;: &#34;page_view&#34;
      },
      {
        &#34;page_name&#34;: &#34;test2&#34;,
        &#34;tealium_event&#34;: &#34;page_view&#34;
      }
    ]
}&#39;
```

#### Example response

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:07:37 GMT
&lt; content-type: application/json
&lt; content-length: 0
&lt; x-amzn-requestid: 11f79456-cdb8-4ccc-8cc7-e8a54db79414
&lt; x-region: us-east-1
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: 7277c009-f9f5-47a2-9fe6-61f05c98e6fd
&lt; x-amz-apigw-id: VSBnlEqkIAMFbFA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-01e68ac980b602444
&lt; expires: Fri, 15 Jul 2022 00:07:37 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:07:37 GMT
```

### Examples for `/integration/event`

#### Example cURL request

```bash
curl --location --request POST &#39;https://{host}/v3/collect/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceId}&#39; --header &#39;Authorization: Bearer eyJ0***&#39; --header &#39;Content-Type: application/json&#39; --data-raw &#39;{
  &#34;tealium_event&#34;: &#34;page_view&#34;,
  &#34;tealium_datasource&#34;: &#34;{datasourceId}&#34;,
  &#34;page_type&#34;: &#34;123&#34;,
  &#34;outerObject&#34;: {
    &#34;innerobject&#34;:&#34;1234&#34;
  },
  &#34;page_name&#34;: &#34;kek&#34;
}&#39;
```

#### Example response

```bash
&lt; HTTP/2 204
&lt; date: Fri, 15 Jul 2022 00:05:23 GMT
&lt; x-amzn-requestid: e3b5bc65-8712-40a3-a87c-9d6bb8df68cf
&lt; x-region: us-east-1
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: fadbdf55-dccb-4241-a9ce-81722fc2a8d9
&lt; x-amz-apigw-id: VSBSnF9OIAMFxXA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-058449c0632b25787
&lt; expires: Fri, 15 Jul 2022 00:05:23 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:05:23 GMT
```

## Status codes

The following table summarizes Tealium&#39;s HTTP response status codes:

|Status Code| Description|
|---| ---|
|`200 Status OK`| The request succeeded.|
|`400 Bad Request`| The server does not understand the request.|

The `400 Bad Request` status code occurs when at least of the following is true:

* The JSON key contains a period, is invalid, or exceeds 1 MB in size.
* The file-type parameter contains a value other than JSON or JavaScript.
* The combination of `account`, `profile`, and `datalayer_id` exceeds 250 characters in length, or contains restricted characters.
* `tealium_account` or `tealium_profile` is missing, or contains typographical errors.
* The request body is empty.

The following is an example of a `400 Bad Request` response for a GET request to `/v3/collect/event`, shown in the `X-Error` header, when the required `tealium_account` or `tealium_profile` parameter values are missing:

```bash
&lt; HTTP/2 200
&lt; date: Fri, 15 Jul 2022 00:03:05 GMT
&lt; content-type: image/gif
&lt; content-length: 43
&lt; x-error: Missing required tealium_account or tealium_profile param value
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-region: us-west-2
&lt; x-serverid: uconnect_i-0b80d0d9adfb124a2
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; vary: Origin
&lt; pragma: no-cache
&lt; expires: Fri, 15 Jul 2022 00:03:05 GMT
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-uuid: 1d0dd863-dc31-4eb2-b7a0-5b98e3b7fb5b
```

The following is an example is a `400 Bad Request` response for a POST request to `/v3/collect/bulk-event`:

```bahs
&lt; HTTP/2 400
&lt; date: Fri, 15 Jul 2022 00:01:16 GMT
&lt; content-type: application/json
&lt; content-length: 78
&lt; x-amzn-requestid: 993d950d-cde4-4ee0-9f18-d3e41a3ed5ca
&lt; x-amzn-remapped-content-length: 78
&lt; x-region: us-east-1
&lt; p3p: policyref=&#34;/w3c/p3p.xml&#34;, CP=&#34;NOI DSP COR NID CUR ADM DEV OUR BUS&#34;
&lt; x-amzn-remapped-connection: keep-alive
&lt; x-uuid: 59afeed7-abe2-487c-bac1-a96903f4a449
&lt; x-amz-apigw-id: VSAr9HOloAMFQkA=
&lt; vary: Origin
&lt; cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
&lt; x-serverid: uconnect_i-02ccd81bf59828cde
&lt; expires: Fri, 15 Jul 2022 00:01:16 GMT
&lt; x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
&lt; pragma: no-cache
&lt; x-amzn-remapped-date: Fri, 15 Jul 2022 00:01:16 GMT
&lt;
* Connection #0 to host us-east-1-platform.tealiumapis.com left intact
{ &#34;returnCode&#34; : 1400 , &#34;message&#34; : &#34;Request body must contain &#39;events&#39; key.&#34;}
```
