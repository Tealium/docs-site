---
title: Hosted data layer API endpoints
description: Manage your hosted data layer using a hosted data layer object or JSON file.
url: https://docs.tealium.com/api-v1/hosted-data-layer/endpoints/
---This is an older version of the [current Tealium Hosted Data Layer API]().

## Upload

Upload a Hosted Data Layer object.

`POST /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

Using PUT instead of POST will result in a 405 Method Not Allowed error.

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} -X POST -H &#34;Content-Type: application/json&#34; \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token} \
  -d @{dl_id}.json
```

When passing files to the `-d` parrameter using the cURL command, the file name must be prefixed with the `@` character.

### Example response

#### Status 201 OK

```
{
   &#34;status&#34;: &#34;pending&#34;
}
```

It may take five to ten minutes for changes to be reflected by Tealium&#39;s servers. Wait for the status to display as completed before attempting to make another call on the same `dl_id`.

### Error messages

#### 405 Method not allowed

This error occurs when you use PUT instead of POST to perform the upload.
 

```
{
   &#34;returnCode&#34; : 1464,
   &#34;message&#34; : &#34;Resource already exists. Updates are not permitted via this type of request.&#34;
}

```

#### 400 Bad request

This error occurs when one of the following is true:

* The JSON key contains a period
* The combination of account, profile, and`dl_id`exceeds 250 characters
* The `dl_id`contains restricted characters
* The user does not have the appropriate permissions
* There is a typographical error in the account/profile name
* The request body is empty
* Bad or invalid JSON
* JSON data exceeds one (1) mebibyte (MiB)  


```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 401 Unauthorized

This error occurs when the user lacks the appropriate permissions or there is a typographical error in the account/profile name.

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}
```

## Update

` PUT /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

Using PUT instead of POST will result in a 405 Method Not Allowed error.

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} -X PUT -H &#34;Content-Type: application/json&#34; \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token} \
  -d @{dl_id}.json
```

### Example response

#### Status 200 OK

```
{
   &#34;status&#34;: &#34;pending&#34;
}

```

It may take up to one (1) hour for changes to be reflected by Tealium&#39;s servers. Wait for the status to display as completed before attempting to make another call on the same `dl_id.`

### Error messages

#### 400 Bad request

This error occurs when one of the following is true:

* The JSON key contains a period
* The combination of account, profile, and `dl_id` exceeds 250 characters
* The `dl_id` contains restricted characters
* The user does not have the appropriate permissions
* There is a typographical error in the account/profile name
* The request body is empty
* Bad or invalid JSON
* JSON data exceeds one (1) mebibyte (MiB)

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 404 Not Found

This error occurs if the supplied `dl_id` does not exist.

```
{
   &#34;returnCode&#34; : 1404,
   &#34;message&#34; : &#34;Could not locate data layer for supplied params ([account]/[profile]/[dl_id]).&#34;
}
```

## Delete

`DELETE/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} -X DELETE -H &#34;Content-Type: application/json&#34; \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}
```

### Example response

#### Status 200 OK

```
{
   &#34;status&#34;: &#34;pending&#34;
}

```

It may take up to one hour for changes to be reflected by Tealium&#39;s servers. Wait for the status to display as completed before attempting to make another call on the same `dl_id.`

### Error messages

#### 404 Not Found

This error occurs if the supplied `dl_id` does not exist.

```
{
   &#34;returnCode&#34; : 1404,
   &#34;message&#34; : &#34;Could not locate data layer for supplied params ([account]/[profile]/[dl_id]).&#34;
}

```

#### 400 Bad request

This error occurs when one of the following is true:

* The combination of account, profile, and `dl_id` exceeds 250 characters
* The `dl_id` contains restricted characters
* The user does not have the appropriate permissions
* There is a typographical error in the account/profile name

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 401 Unauthorized

This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}
```

## Get status

Get the status of upload, update, and delete actions. Statuses are only retained for 30 days.

Expected status values are:

* Pending
* Completed
* Failed

` GET /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
    https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}
```

### Example Response

```
{
   &#34;status&#34;: &#34;completed&#34;
}

```

### Error messages

#### 404 Not Found

This error occurs when the supplied `dl_id` does not exist or the status for the supplied `dl_id`has expired because it extends beyond the 30-day retention period.

```
{
   &#34;returnCode&#34; : 1404,
   &#34;message&#34; : &#34;Status unavailable. Please refer to documentation for request status retention period.&#34;
}
```

#### 400 Bad request

This error occurs when one of the following is true:

* The combination of account, profile, and `dl_id` exceeds 250 characters
* The `dl_id` contains restricted characters
* The user does not have the appropriate permissions
* There is a typographical error in the account/profile name

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 401 Unauthorized

This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}
```

## List

Returns a list of up to 1,000 Hosted Data Layer names.

` GET /v1/dle/accounts/{account}/profiles/{profile}/datalayers?utk={token}`

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers?utk={token}

```

### Example response

#### Status 200 OK

```
{
   [&#34;demo_1&#34;,&#34;demo_2&#34;,&#34;demo_3&#34;]
}
```

### Error messages

#### 400 Bad request

This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}

```

#### 400 Bad Request

More than 1,000 hosted data layers were found for the account/profile.

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Data layer list size exceeds maximum permissible (1000).&#34;
}

```

#### 401 Unauthorized

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}

```
