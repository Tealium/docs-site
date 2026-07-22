---
title: Hosted data layer API endpoints
description: Manage your hosted data layer using a hosted data layer object or JSON file.
url: https://docs.tealium.com/api/v2/hosted-data-layer/endpoints/
---
## POST (Upload) a Hosted Data Layer object or JSON file

Use the following POST command to upload a hosted data layer object:

```bash
POST /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

Use the following POST command to upload a JSON file:

```bash
POST /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### Example cURL request

Use the following cURL command to execute this task:

```bash
curl -X POST https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id}} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d '{ "key1" : "value1", "key2" : "value2" }'
```


<blockquote>
When passing files to the `-d` parameter using the cURL command, the file name must be prefixed with the `@` character.
</blockquote>


### Example response

The following example shows a typical response generated from the cURL command. Request rates vary up to a maximum of 100 requests per second, depending on network traffic. It may take up to one hour for changes to be reflected by Tealium's servers.

`Status 200 OK`

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 400 Bad request |``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  This error occurs when one of the following is true: The JSON key contains a period; The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The request body is empty; Bad or invalid JSON; JSON data exceeds 1MB; Or the file-type parameter contains a value other than "json" or "javascript".  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" }  ```|  This error occurs when the user lacks the appropriate permissions or there is a typographical error in the account/profile name.  |

## PUT (Update) a Hosted Data Layer object or JSON file

Use the following PUT command to update a hosted data layer object:

```bash
PUT /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

Use the following PUT command to update a JSON file:

```bash
PUT /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### Example cURL request

Use the following cURL command to execute this task:

```bash
curl -X PUT https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d '{ "key1" : "value1", "key2" : "value2" }'
```

### Example response

The following example shows a typical response generated from the cURL command:

`Status 200 OK`


<blockquote>
It may take up to one hour for changes to be reflected by Tealium's servers.
</blockquote>


### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---| ---| ---|
|400 Bad request| ``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```| This error occurs when one of the following is true: The JSON key contains a period; The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The request body is empty; Bad or invalid JSON; JSON data exceeds 1MB; The file-type parameter contains a value other than "json" or "javascript".  |

## DELETE a Hosted Data Layer object or JSON file

Use the following command to delete a hosted data layer object:

```bash
DELETE /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

Use the following command to delete a JSON file:

```bash
DELETE /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### Example cURL request

Use the following cURL command to execute this task:

```bash
curl -X DELETE https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### Example response

The following example shows a typical response generated from the cURL command. Request rates vary up to a maximum of 100 requests per second, depending on network traffic. It may take up to one hour for changes to be reflected by Tealium's servers.

`Status 200 OK`

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|--- | ---|
| 400 Bad request | ``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  This error occurs when one of the following is true: The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The file-type parameter contains a value other than "json" or "javascript".  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |

## GET file metadata

Once a file has been uploaded, you can retrieve metadata about the file using this GET method.

* A 200 response with a return object validates that your file was uploaded successfully.
* If you receive a 404 response for a file after several attempts, use the `failed-uploads` call to look for the file in the returned list.
* A failed upload indicates a possible issue in the file transfer process.
* Attempt the upload again.

Use the following GET command retrieve the file information for a hosted data layer object:

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

Use the following GET command retrieve the information for a JSON file:

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### Example cURL request

Use the following cURL command to execute this task:

```bash
curl -X GET https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### Example response

The following example shows a typical response generated from the cURL command:

```json
{
  "file": "dle/tealium/main/datalayer1.js",
  "lastModified": "2017-04-07T02:41:24+0000",
  "size": 70
}
```

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 404 Not Found | ``` {   "returnCode" : 1404,   "message" : "Could not locate data layer identified by {datalayer_id}" } ```| This error occurs when the supplied `datalayer_id` does not exist.  |
| 400 Bad request | ``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```| This error occurs when one of the following is true: The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The file-type parameter contains a value other than "json" or "javascript".  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |

## GET a list of Data Layer objects and JSON files

Use one of the following commands to return a list of up to 1,000 hosted data layer objects and JSON files. If a continuation token is received in the response, the continuation token query parameter can be used for lists greater than 1,000.

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers
```

### Example cURL requests with or without continuation tokens

Use one of the following cURL commands to execute this task:

#### Example cURL request (No continuation token)

```bash
curl -X GET 'https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers' \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

#### Example cURL request (With continuation token)

```bash
curl -X GET 'https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers?continuationToken={continuation_token}' \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### Example responses

The following examples show typical responses generated from the cURL command:

#### Example response (No continuation token)

```json
{
  "isTruncated": false,
  "fileStatuses": [
    {
      "file": "dle/tealium/main/datalayer1.js",
      "lastModified": "2017-04-07T02:41:24+0000",
      "size": 70
    },
    {
      "file": "dle/tealium/main/datalayer2.js",
      "lastModified": "2017-04-06T23:37:17+0000",
      "size": 69
    },
    {
      "file": "dle/tealium/main/datalayer3.json",
      "lastModified": "2017-04-07T02:40:30+0000",
      "size": 86
    },
    ...
  ]
}
```

#### Example response (With continuation token)

```json
{
 "isTruncated": true,
 "continuationToken":"1bQZQPYomjLBOQxhZhMazJVoPcrW9iEtOcPhcRQVlMZWx9IssfpisOKt0Kb85bVlRDbkR7NR%2BZd3eUgB0vnx5eomAoz5KX0K2qgcNMOwiJXdbN5CtD4A%2B%2FLK%2B%2Fj0AJ1eYXEu2l%2F9Z%2FGk%3D",
 "fileStatuses": [
   {
     "file": "dle/tealium/main/datalayer1.js",
     "lastModified": "2017-04-07T02:41:24+0000",
     "size": 70
   },
   {
     "file": "dle/tealium/main/datalayer2.js",
     "lastModified": "2017-04-06T23:37:17+0000",
     "size": 69
   },
   {
     "file": "dle/tealium/main/datalayer3.json",
     "lastModified": "2017-04-07T02:40:30+0000",
     "size": 86
   },
   ...
 ]
}
```

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 400 Bad request | ``` {   "returnCode" : 1400,   "message" : "Invalid request submission. Please check supplied parameters or request body." } ```| This error occurs due to a typographical error in the account/profile name.  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |

## GET failed uploads

Use the following command to query for failed uploads:

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/failed-uploads?start-date={start_date}&amp;end-date={end_date}
```

* The results returned contain a maximum of 5,000 records and are not paginated.
* A failed upload indicates a possible issue in the file transfer process.
* Attempt the upload again.

Results can be filtered using the following date range parameters with an expected date format of `YYYY-MM-DDTHH:MM:SSTZ`. Example: `2017-03-31T13:45:33-0700`

* **start-date**
    * (Optional) Only failed uploads with a date equal to or later than this value is returned.
* **end-date**
    * (Optional) Only failed uploads with a date equal to or earlier than this value is returned.

### Example cURL request

Use the following cURL command to execute this task:

```bash
curl -X GET 'https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/failed-uploads?start-date={YYYY-MM-DDThh:mm:ssZ}&amp;end-date={YYYY-MM-DDThh:mm:ssZ}' \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### Example response

The following example shows a typical response generated from the cURL command:

```json
Status 200 OK
{
  "account": "your_account",
  "profile": "main",
  "count": 2,
  "failedUploads": [
    {
      "file": "/dle/your_account/main/forremoval2.js",
      "date": "2017-05-20T17:22:00+0000"
    },
    {
      "file": "/dle/your_account/main/forremoval.js",
      "date": "2017-05-20T17:22:00+0000"
    }
  ]
}
```

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 400 Bad request | ``` {   "returnCode" : 1400,   "message" : "Invalid request submission. Please check supplied parameters or request body." } ```| This error occurs when there is a typographical error in the account/profile name.  |
| 401 Unauthorized | ``` {   "returnCode" : 1469,   "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |
