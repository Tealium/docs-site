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
curl -i -X GET 'https://{host}/v3/collect/event?tealium_account={account}&tealium_profile={profile}&tealium_event=user_login&email_address=user@example.com'
--header 'Authorization: Bearer eyJ0**'
```

#### Example response

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:08:50 GMT
< content-type: image/gif
< content-length: 43
< x-amzn-requestid: 03bb378a-2619-4440-9d5a-c1e7d0e8d2ae
< x-amzn-remapped-content-length: 43
< x-region: us-east-1
< x-acc: {account}:{profile}:2:event
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: f513ef4b-5870-4fa4-b908-38c5e12bf3e4
< x-amz-apigw-id: VSBy2Fu6oAMFezA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-0182b50695a2297ec
< expires: Fri, 15 Jul 2022 00:08:50 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< x-tid: f513ef4b58704fa4b90838c5e12bf3e4
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:50 GMT
```

## POST method

The POST method supports JSON payloads where the request header must be set to `Content-Type: application/json` and the payload must be formatted as a valid JSON string.

### Examples for `/event`

#### Example cURL request

```bash
curl --location --request POST 'https://{host}/v3/collect/event' --header 'Authorization: Bearer eyJ0eXA***' --header 'Content-Type: application/json' --data-raw '{
"tealium_account": "{account}",
"tealium_datasource": "abc123",
"tealium_profile": "{profile}",
"tealium_event": "page_view",
"page_type": "123",
"page_name": "testName"
}'
```

#### Example response

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:08:03 GMT
< content-type: application/json
< content-length: 0
< x-amzn-requestid: ad5c154f-3053-4991-9a60-45b35745eba7
< x-region: us-east-1
< x-acc: {account}:main:2:event
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: 1d6b9c12-16c3-44a9-95c9-78afeabaf8e0
< x-amz-apigw-id: VSBroH24oAMFXpQ=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-0a95ad51791af67ac
< expires: Fri, 15 Jul 2022 00:08:03 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< x-tid: abc123_071422_1
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:08:03 GMT
```

### Examples for `/bulk-event`

#### Example cURL request

```bash
curl --location --request POST 'https://{host}/v3/collect/bulk-event' \
--header 'Authorization: Bearer eyJ0eXAi***' \
--header 'Content-Type: application/json' \
--data-raw '{
    "shared": {
      "tealium_account": "{account}",
      "tealium_profile": "{profile}",
      "tealium_environment": "prod",
      "tealium_datasource": "{datasource}",
      "tealium_visitor_id": "abc123_071222_1"
    },
    "events": [
      {
        "page_name": "test1",
        "tealium_event": "page_view"
      },
      {
        "page_name": "test2",
        "tealium_event": "page_view"
      }
    ]
}'
```

#### Example response

```bash
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:07:37 GMT
< content-type: application/json
< content-length: 0
< x-amzn-requestid: 11f79456-cdb8-4ccc-8cc7-e8a54db79414
< x-region: us-east-1
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: 7277c009-f9f5-47a2-9fe6-61f05c98e6fd
< x-amz-apigw-id: VSBnlEqkIAMFbFA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-01e68ac980b602444
< expires: Fri, 15 Jul 2022 00:07:37 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:07:37 GMT
```

### Examples for `/integration/event`

#### Example cURL request

```bash
curl --location --request POST 'https://{host}/v3/collect/integration/event/accounts/{account}/profiles/{profile}/datasources/{datasourceId}' --header 'Authorization: Bearer eyJ0***' --header 'Content-Type: application/json' --data-raw '{
  "tealium_event": "page_view",
  "tealium_datasource": "{datasourceId}",
  "page_type": "123",
  "outerObject": {
    "innerobject":"1234"
  },
  "page_name": "kek"
}'
```

#### Example response

```bash
< HTTP/2 204
< date: Fri, 15 Jul 2022 00:05:23 GMT
< x-amzn-requestid: e3b5bc65-8712-40a3-a87c-9d6bb8df68cf
< x-region: us-east-1
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: fadbdf55-dccb-4241-a9ce-81722fc2a8d9
< x-amz-apigw-id: VSBSnF9OIAMFxXA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-058449c0632b25787
< expires: Fri, 15 Jul 2022 00:05:23 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:05:23 GMT
```

## Status codes

The following table summarizes Tealium's HTTP response status codes:

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
< HTTP/2 200
< date: Fri, 15 Jul 2022 00:03:05 GMT
< content-type: image/gif
< content-length: 43
< x-error: Missing required tealium_account or tealium_profile param value
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-region: us-west-2
< x-serverid: uconnect_i-0b80d0d9adfb124a2
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< vary: Origin
< pragma: no-cache
< expires: Fri, 15 Jul 2022 00:03:05 GMT
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-uuid: 1d0dd863-dc31-4eb2-b7a0-5b98e3b7fb5b
```

The following is an example is a `400 Bad Request` response for a POST request to `/v3/collect/bulk-event`:

```bahs
< HTTP/2 400
< date: Fri, 15 Jul 2022 00:01:16 GMT
< content-type: application/json
< content-length: 78
< x-amzn-requestid: 993d950d-cde4-4ee0-9f18-d3e41a3ed5ca
< x-amzn-remapped-content-length: 78
< x-region: us-east-1
< p3p: policyref="/w3c/p3p.xml", CP="NOI DSP COR NID CUR ADM DEV OUR BUS"
< x-amzn-remapped-connection: keep-alive
< x-uuid: 59afeed7-abe2-487c-bac1-a96903f4a449
< x-amz-apigw-id: VSAr9HOloAMFQkA=
< vary: Origin
< cache-control: no-transform,private,no-cache,no-store,max-age=0,s-maxage=0
< x-serverid: uconnect_i-02ccd81bf59828cde
< expires: Fri, 15 Jul 2022 00:01:16 GMT
< x-ulver: e07c919851780ad8793847fdb12df3611bcdbf78-SNAPSHOT
< pragma: no-cache
< x-amzn-remapped-date: Fri, 15 Jul 2022 00:01:16 GMT
<
* Connection #0 to host us-east-1-platform.tealiumapis.com left intact
{ "returnCode" : 1400 , "message" : "Request body must contain 'events' key."}
```
