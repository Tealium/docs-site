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
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39; \
-H &#39;Content-Type: application/json&#39; \
-d &#39;{ &#34;key1&#34; : &#34;value1&#34;, &#34;key2&#34; : &#34;value2&#34; }&#39;
```

When passing files to the `-d` parameter using the cURL command, the file name must be prefixed with the `@` character.

### Example response

The following example shows a typical response generated from the cURL command. Request rates vary up to a maximum of 100 requests per second, depending on network traffic. It may take up to one hour for changes to be reflected by Tealium&#39;s servers.

`Status 200 OK`

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 400 Bad request |``` {    &#34;returnCode&#34; : 1400,    &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34; } ```|  This error occurs when one of the following is true: The JSON key contains a period; The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The request body is empty; Bad or invalid JSON; JSON data exceeds 1MB; Or the file-type parameter contains a value other than &#34;json&#34; or &#34;javascript&#34;.  |
| 401 Unauthorized | ``` {    &#34;returnCode&#34; : 1469,    &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34; }  ```|  This error occurs when the user lacks the appropriate permissions or there is a typographical error in the account/profile name.  |

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
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39; \
-H &#39;Content-Type: application/json&#39; \
-d &#39;{ &#34;key1&#34; : &#34;value1&#34;, &#34;key2&#34; : &#34;value2&#34; }&#39;
```

### Example response

The following example shows a typical response generated from the cURL command:

`Status 200 OK`

It may take up to one hour for changes to be reflected by Tealium&#39;s servers.

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---| ---| ---|
|400 Bad request| ``` {    &#34;returnCode&#34; : 1400,    &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34; } ```| This error occurs when one of the following is true: The JSON key contains a period; The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The request body is empty; Bad or invalid JSON; JSON data exceeds 1MB; The file-type parameter contains a value other than &#34;json&#34; or &#34;javascript&#34;.  |

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
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39;
```

### Example response

The following example shows a typical response generated from the cURL command. Request rates vary up to a maximum of 100 requests per second, depending on network traffic. It may take up to one hour for changes to be reflected by Tealium&#39;s servers.

`Status 200 OK`

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|--- | ---|
| 400 Bad request | ``` {    &#34;returnCode&#34; : 1400,    &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34; } ```|  This error occurs when one of the following is true: The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The file-type parameter contains a value other than &#34;json&#34; or &#34;javascript&#34;.  |
| 401 Unauthorized | ``` {    &#34;returnCode&#34; : 1469,    &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34; } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |

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
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39;
```

### Example response

The following example shows a typical response generated from the cURL command:

```json
{
  &#34;file&#34;: &#34;dle/tealium/main/datalayer1.js&#34;,
  &#34;lastModified&#34;: &#34;2017-04-07T02:41:24&#43;0000&#34;,
  &#34;size&#34;: 70
}
```

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 404 Not Found | ``` {   &#34;returnCode&#34; : 1404,   &#34;message&#34; : &#34;Could not locate data layer identified by {datalayer_id}&#34; } ```| This error occurs when the supplied `datalayer_id` does not exist.  |
| 400 Bad request | ``` {    &#34;returnCode&#34; : 1400,    &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34; } ```| This error occurs when one of the following is true: The combination of account, profile, and `datalayer_id` exceeds 250 characters; The `datalayer_id` contains restricted characters; There is a typographical error in the account/profile name; The file-type parameter contains a value other than &#34;json&#34; or &#34;javascript&#34;.  |
| 401 Unauthorized | ``` {    &#34;returnCode&#34; : 1469,    &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34; } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |

## GET a list of Data Layer objects and JSON files

Use one of the following commands to return a list of up to 1,000 hosted data layer objects and JSON files. If a continuation token is received in the response, the continuation token query parameter can be used for lists greater than 1,000.

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers
```

### Example cURL requests with or without continuation tokens

Use one of the following cURL commands to execute this task:

#### Example cURL request (No continuation token)

```bash
curl -X GET &#39;https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers&#39; \
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39;
```

#### Example cURL request (With continuation token)

```bash
curl -X GET &#39;https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers?continuationToken={continuation_token}&#39; \
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39;
```

### Example responses

The following examples show typical responses generated from the cURL command:

#### Example response (No continuation token)

```json
{
  &#34;isTruncated&#34;: false,
  &#34;fileStatuses&#34;: [
    {
      &#34;file&#34;: &#34;dle/tealium/main/datalayer1.js&#34;,
      &#34;lastModified&#34;: &#34;2017-04-07T02:41:24&#43;0000&#34;,
      &#34;size&#34;: 70
    },
    {
      &#34;file&#34;: &#34;dle/tealium/main/datalayer2.js&#34;,
      &#34;lastModified&#34;: &#34;2017-04-06T23:37:17&#43;0000&#34;,
      &#34;size&#34;: 69
    },
    {
      &#34;file&#34;: &#34;dle/tealium/main/datalayer3.json&#34;,
      &#34;lastModified&#34;: &#34;2017-04-07T02:40:30&#43;0000&#34;,
      &#34;size&#34;: 86
    },
    ...
  ]
}
```

#### Example response (With continuation token)

```json
{
 &#34;isTruncated&#34;: true,
 &#34;continuationToken&#34;:&#34;1bQZQPYomjLBOQxhZhMazJVoPcrW9iEtOcPhcRQVlMZWx9IssfpisOKt0Kb85bVlRDbkR7NR%2BZd3eUgB0vnx5eomAoz5KX0K2qgcNMOwiJXdbN5CtD4A%2B%2FLK%2B%2Fj0AJ1eYXEu2l%2F9Z%2FGk%3D&#34;,
 &#34;fileStatuses&#34;: [
   {
     &#34;file&#34;: &#34;dle/tealium/main/datalayer1.js&#34;,
     &#34;lastModified&#34;: &#34;2017-04-07T02:41:24&#43;0000&#34;,
     &#34;size&#34;: 70
   },
   {
     &#34;file&#34;: &#34;dle/tealium/main/datalayer2.js&#34;,
     &#34;lastModified&#34;: &#34;2017-04-06T23:37:17&#43;0000&#34;,
     &#34;size&#34;: 69
   },
   {
     &#34;file&#34;: &#34;dle/tealium/main/datalayer3.json&#34;,
     &#34;lastModified&#34;: &#34;2017-04-07T02:40:30&#43;0000&#34;,
     &#34;size&#34;: 86
   },
   ...
 ]
}
```

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 400 Bad request | ``` {   &#34;returnCode&#34; : 1400,   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34; } ```| This error occurs due to a typographical error in the account/profile name.  |
| 401 Unauthorized | ``` {    &#34;returnCode&#34; : 1469,    &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34; } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |

## GET failed uploads

Use the following command to query for failed uploads:

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/failed-uploads?start-date={start_date}&amp;amp;end-date={end_date}
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
curl -X GET &#39;https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/failed-uploads?start-date={YYYY-MM-DDThh:mm:ssZ}&amp;amp;end-date={YYYY-MM-DDThh:mm:ssZ}&#39; \
-H &#39;Authorization: Bearer {token}&#39; \
-H &#39;Accept: application/json&#39;
```

### Example response

The following example shows a typical response generated from the cURL command:

```json
Status 200 OK
{
  &#34;account&#34;: &#34;your_account&#34;,
  &#34;profile&#34;: &#34;main&#34;,
  &#34;count&#34;: 2,
  &#34;failedUploads&#34;: [
    {
      &#34;file&#34;: &#34;/dle/your_account/main/forremoval2.js&#34;,
      &#34;date&#34;: &#34;2017-05-20T17:22:00&#43;0000&#34;
    },
    {
      &#34;file&#34;: &#34;/dle/your_account/main/forremoval.js&#34;,
      &#34;date&#34;: &#34;2017-05-20T17:22:00&#43;0000&#34;
    }
  ]
}
```

### Error messages

The following table describes potential error messages for this task:

|Error Code| Error Message | Description|
|---|---| ---|
| 400 Bad request | ``` {   &#34;returnCode&#34; : 1400,   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34; } ```| This error occurs when there is a typographical error in the account/profile name.  |
| 401 Unauthorized | ``` {   &#34;returnCode&#34; : 1469,   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34; } ```| This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.  |
