---
title: Visitor Privacy API endpoints
description: The Visitor Privacy API lets you retrieve known data about a specific visitor, delete a visitor record, and check the status of a delete request.
url: https://docs.tealium.com/api/v3/visitor-privacy/endpoints/
---
## GET Visitor


<blockquote>
You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).
</blockquote>


Use the following GET command to retrieve a visitor record:

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&attributeValue={attributeValue}&prettyName={prettyName}
```

This command uses the following parameters:

* `attributeId`
  * The numeric ID representing a [Visitor ID attribute](https://docs.tealium.com/visitor-id-attribute/) from your account.
* `attributeValue`
  * The value to look up.
  * Values containing special characters must be URL encoded.
* `prettyName`
  * A Boolean value indicating how attribute keys display in the response:
    * **True** – Attributes display as user-friendly names, such as "Lifetime Order Value".
    * **False** – Attributes display as numeric ID's, such as "28471".

### Permission requirements

* Server-side reader, editor, or publisher legacy permissions, or
* Minimum **View** Visitor Lookup platform permissions

### Example cURL request

```bash
curl -H 'Authorization: Bearer {token}' \
 -G \
'https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main' \
 --data-urlencode 'attributeId=86' \
 --data-urlencode 'attributeValue=user@example.com' \
 --data 'prettyName=true'
```

### Example response

See the example visitor object for the format of the response.

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|400|  `{ "message": "You are missing an attribute Id or Attribute Value"}` |
|401|  `{ "message": "Unauthorized"}` |
| 404 | `Visitor not found in system {  "transactionId": {transactionId}  }` |
|429| `{ "message": "Too many requests"}` |
| 500 |`{ "message": "Internal Server Error"}` |

## DELETE visitor


<blockquote>
You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).
</blockquote>


Consider the following prior to deleting one or more visitor records:

* Requests to delete visitor records result in the deletion of all data associated to the visitor ID value, including stitched visitor records.
* Delete requests are queued for processing and may take up to 30 days to complete.
* If a visitor replaces or has been replaced by another visitor, all visitors that have been stitched are deleted.
* The parameters to the DELETE command must be passed as URL-encoded form fields using the content-type " `application/x-www-form-urlencoded`", and not as query string parameters.

Use the following DELETE command to delete a visitor record:

```bash
DELETE /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeID={value}&attributeValue={value}
```

This command uses the following parameters:

* `attributeId`  
The numeric ID representing a [Visitor ID attribute](https://docs.tealium.com/visitor-id-attribute/) from your account.
* `attributeValue`  
The value to look up.

### Permission requirements

* Server-side publisher legacy permissions, or
* **View, Edit, & Delete** Visitor Lookup platform permissions

### Example cURL request

```bash
curl -H 'Authorization: Bearer {token}' \
-X DELETE \
'https://us-east1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main' \
--data-urlencode "attributeId=86"
--data-urlencode "attributeValue=user@example.com"
```

### Example response

The response to a delete request includes a `transaction_id` and a status. The `transaction_id` is used in the GET transactions call to check the status of a previous request. The following status strings are possible: **PENDING**, **SUCCESS**, or **FAILED**.

A successful response displays the 202 Accepted message with a `transactionId` value. If a request with the exact same `account`, `profile`, `attributeId` , and `attributeValue` already exists with a transaction status of **PENDING**, the existing transaction ID is returned, as follows:

```json
{
"transactionId" : "{transactionId1}"
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|400|  `{ "message": "You are missing an attribute Id or Attribute Value"}` |
|401|  `{ "message": "Unauthorized"}` |
|404|  `Visitor not found in system {  "transactionId": {transactionId}  }` |
|429| `{ "message": "Too many requests"}` |

## GET transaction


<blockquote>
You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).
</blockquote>


A transaction refers to any DELETE visitor request. DELETE visitor requests are queued for later processing, which makes the `transaction_id` the unique record for that request and ID to be used when checking the processing status.

Use the following GET command to check the status of a transaction:

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/transactions/{transaction_id}
```

### Permission requirements

* Server-side reader, editor, or publisher legacy permissions, or
* Minimum **View** Visitor Lookup platform permissions

### Example cURL request

For information about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/). The bearer token is used in the API calls, rather than the API key.

```bash
curl -H 'Authorization: Bearer {token}' \
https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/transactions/0123456789
```

### Example response

The response contains an object with one key-value pair where the key is a `transaction_id` and the value is one of the following status strings: **PENDING**, **SUCCESS**, or **FAILED**.

```json
{
  "0123456789" : "SUCCESS"
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|401|  `{ "message": "Unauthorized"}` |
|404|  `Visitor not found in system {  "transactionId": {transactionId}  }` |
|429| `{ "message": "Too many requests"}` |

## GET Visitor ID Attributes

Use the following GET command to retrieve a list of the Visitor ID attributes available in your account:

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/ids
```

### Permission requirements

* Server-side reader, editor, or publisher legacy permissions, or
* Minimum **View** Visitor Lookup platform permissions

### Example cURL request

```bash
curl -H 'Authorization: Bearer {token}' \
https://platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/ids
```

### Example response

The response for this command is an object of key-value pairs representing the numeric ID and name of the Visitor ID attribute.

```json
{
  "43" : "Email Address",
  "57" : "Tax ID Number"
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|401|  `{ "message": "Unauthorized"}` |
|404|  `{ "message" : "No Visitor ids were found for the account and profile"}` |
|429| `{ "message": "Too many requests"}` |
|500|  `{ "message" : "Internal Server Error"}` |
