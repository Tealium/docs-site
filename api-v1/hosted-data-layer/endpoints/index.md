---
title: Hosted data layer API endpoints
description: Manage your hosted data layer using a hosted data layer object or JSON file.
url: https://docs.tealium.com/api-v1/hosted-data-layer/endpoints/
---This is an older version of the [current Tealium Hosted Data Layer API](https://docs.tealium.com/about-hosted-data-layer-api/).

## Upload

Upload a Hosted Data Layer object.

`POST /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`


<blockquote>
Using PUT instead of POST will result in a 405 Method Not Allowed error.
</blockquote>


### cURL request

```bash
cURL -i -b JSESSIONID={session_id} -X POST -H "Content-Type: application/json" \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token} \
  -d @{dl_id}.json
```


<blockquote>
When passing files to the `-d` parrameter using the cURL command, the file name must be prefixed with the `@` character.
</blockquote>


### Example response

#### Status 201 OK

```
{
   "status": "pending"
}
```


<blockquote>
It may take five to ten minutes for changes to be reflected by Tealium's servers. Wait for the status to display as completed before attempting to make another call on the same `dl_id`.
</blockquote>


### Error messages

#### 405 Method not allowed

This error occurs when you use PUT instead of POST to perform the upload.
 

```
{
   "returnCode" : 1464,
   "message" : "Resource already exists. Updates are not permitted via this type of request."
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
   "returnCode" : 1400,
   "message" : "Invalid request submission. Please check supplied parameters or request body."
}
```

#### 401 Unauthorized

This error occurs when the user lacks the appropriate permissions or there is a typographical error in the account/profile name.

```
{
   "returnCode" : 1469,
   "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions"
}
```

## Update

` PUT /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`


<blockquote>
Using PUT instead of POST will result in a 405 Method Not Allowed error.
</blockquote>


### cURL request

```bash
cURL -i -b JSESSIONID={session_id} -X PUT -H "Content-Type: application/json" \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token} \
  -d @{dl_id}.json
```

### Example response

#### Status 200 OK

```
{
   "status": "pending"
}

```


<blockquote>
It may take up to one (1) hour for changes to be reflected by Tealium's servers. Wait for the status to display as completed before attempting to make another call on the same `dl_id.`
</blockquote>


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
   "returnCode" : 1400,
   "message" : "Invalid request submission. Please check supplied parameters or request body."
}
```

#### 404 Not Found

This error occurs if the supplied `dl_id` does not exist.

```
{
   "returnCode" : 1404,
   "message" : "Could not locate data layer for supplied params ([account]/[profile]/[dl_id])."
}
```

## Delete

`DELETE/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} -X DELETE -H "Content-Type: application/json" \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}
```

### Example response

#### Status 200 OK

```
{
   "status": "pending"
}

```


<blockquote>
It may take up to one hour for changes to be reflected by Tealium's servers. Wait for the status to display as completed before attempting to make another call on the same `dl_id.`
</blockquote>


### Error messages

#### 404 Not Found

This error occurs if the supplied `dl_id` does not exist.

```
{
   "returnCode" : 1404,
   "message" : "Could not locate data layer for supplied params ([account]/[profile]/[dl_id])."
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
   "returnCode" : 1400,
   "message" : "Invalid request submission. Please check supplied parameters or request body."
}
```

#### 401 Unauthorized

This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.

```
{
   "returnCode" : 1469,
   "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions"
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
   "status": "completed"
}

```

### Error messages

#### 404 Not Found

This error occurs when the supplied `dl_id` does not exist or the status for the supplied `dl_id`has expired because it extends beyond the 30-day retention period.

```
{
   "returnCode" : 1404,
   "message" : "Status unavailable. Please refer to documentation for request status retention period."
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
   "returnCode" : 1400,
   "message" : "Invalid request submission. Please check supplied parameters or request body."
}
```

#### 401 Unauthorized

This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.

```
{
   "returnCode" : 1469,
   "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions"
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
   ["demo_1","demo_2","demo_3"]
}
```

### Error messages

#### 400 Bad request

This error occurs due to a lack of appropriate permissions or a typographical error in the account/profile name.

```
{
   "returnCode" : 1400,
   "message" : "Invalid request submission. Please check supplied parameters or request body."
}

```

#### 400 Bad Request

More than 1,000 hosted data layers were found for the account/profile.

```
{
   "returnCode" : 1400,
   "message" : "Invalid request submission. Data layer list size exceeds maximum permissible (1000)."
}

```

#### 401 Unauthorized

```
{
   "returnCode" : 1469,
   "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions"
}

```
