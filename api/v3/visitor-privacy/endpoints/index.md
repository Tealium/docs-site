---
title: Visitor Privacy API endpoints
description: The Visitor Privacy API lets you retrieve known data about a specific visitor, delete a visitor record, and check the status of a delete request.
url: https://docs.tealium.com/api/v3/visitor-privacy/endpoints/
---
## GET Visitor

You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication]().

Use the following GET command to retrieve a visitor record:

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;prettyName={prettyName}
```

This command uses the following parameters:

* `attributeId`
  * The numeric ID representing a [Visitor ID attribute]() from your account.
* `attributeValue`
  * The value to look up.
  * Values containing special characters must be URL encoded.
* `prettyName`
  * A Boolean value indicating how attribute keys display in the response:
    * **True** – Attributes display as user-friendly names, such as &#34;Lifetime Order Value&#34;.
    * **False** – Attributes display as numeric ID&#39;s, such as &#34;28471&#34;.

### Permission requirements

* Server-side reader, editor, or publisher legacy permissions, or
* Minimum **View** Visitor Lookup platform permissions

### Example cURL request

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
 -G \
&#39;https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main&#39; \
 --data-urlencode &#39;attributeId=86&#39; \
 --data-urlencode &#39;attributeValue=user@example.com&#39; \
 --data &#39;prettyName=true&#39;
```

### Example response

See the example visitor object for the format of the response.

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|400|  `{ &#34;message&#34;: &#34;You are missing an attribute Id or Attribute Value&#34;}` |
|401|  `{ &#34;message&#34;: &#34;Unauthorized&#34;}` |
| 404 | `Visitor not found in system {  &#34;transactionId&#34;: {transactionId}  }` |
|429| `{ &#34;message&#34;: &#34;Too many requests&#34;}` |
| 500 |`{ &#34;message&#34;: &#34;Internal Server Error&#34;}` |

## DELETE visitor

You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication]().

Consider the following prior to deleting one or more visitor records:

* Requests to delete visitor records result in the deletion of all data associated to the visitor ID value, including stitched visitor records.
* Delete requests are queued for processing and may take up to 30 days to complete.
* If a visitor replaces or has been replaced by another visitor, all visitors that have been stitched are deleted.
* The parameters to the DELETE command must be passed as URL-encoded form fields using the content-type &#34; `application/x-www-form-urlencoded`&#34;, and not as query string parameters.

Use the following DELETE command to delete a visitor record:

```bash
DELETE /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeID={value}&amp;attributeValue={value}
```

This command uses the following parameters:

* `attributeId`  
The numeric ID representing a [Visitor ID attribute]() from your account.
* `attributeValue`  
The value to look up.

### Permission requirements

* Server-side publisher legacy permissions, or
* **View, Edit, &amp; Delete** Visitor Lookup platform permissions

### Example cURL request

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
-X DELETE \
&#39;https://us-east1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main&#39; \
--data-urlencode &#34;attributeId=86&#34;
--data-urlencode &#34;attributeValue=user@example.com&#34;
```

### Example response

The response to a delete request includes a `transaction_id` and a status. The `transaction_id` is used in the GET transactions call to check the status of a previous request. The following status strings are possible: **PENDING**, **SUCCESS**, or **FAILED**.

A successful response displays the 202 Accepted message with a `transactionId` value. If a request with the exact same `account`, `profile`, `attributeId` , and `attributeValue` already exists with a transaction status of **PENDING**, the existing transaction ID is returned, as follows:

```json
{
&#34;transactionId&#34; : &#34;{transactionId1}&#34;
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|400|  `{ &#34;message&#34;: &#34;You are missing an attribute Id or Attribute Value&#34;}` |
|401|  `{ &#34;message&#34;: &#34;Unauthorized&#34;}` |
|404|  `Visitor not found in system {  &#34;transactionId&#34;: {transactionId}  }` |
|429| `{ &#34;message&#34;: &#34;Too many requests&#34;}` |

## GET transaction

You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication]().

A transaction refers to any DELETE visitor request. DELETE visitor requests are queued for later processing, which makes the `transaction_id` the unique record for that request and ID to be used when checking the processing status.

Use the following GET command to check the status of a transaction:

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/transactions/{transaction_id}
```

### Permission requirements

* Server-side reader, editor, or publisher legacy permissions, or
* Minimum **View** Visitor Lookup platform permissions

### Example cURL request

For information about generating a bearer token from the API key, see [Authentication](). The bearer token is used in the API calls, rather than the API key.

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/transactions/0123456789
```

### Example response

The response contains an object with one key-value pair where the key is a `transaction_id` and the value is one of the following status strings: **PENDING**, **SUCCESS**, or **FAILED**.

```json
{
  &#34;0123456789&#34; : &#34;SUCCESS&#34;
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|401|  `{ &#34;message&#34;: &#34;Unauthorized&#34;}` |
|404|  `Visitor not found in system {  &#34;transactionId&#34;: {transactionId}  }` |
|429| `{ &#34;message&#34;: &#34;Too many requests&#34;}` |

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
curl -H &#39;Authorization: Bearer {token}&#39; \
https://platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/ids
```

### Example response

The response for this command is an object of key-value pairs representing the numeric ID and name of the Visitor ID attribute.

```json
{
  &#34;43&#34; : &#34;Email Address&#34;,
  &#34;57&#34; : &#34;Tax ID Number&#34;
}
```

### Error messages

Potential error messages for this task are:

|Error Message| Description|
|---| ---|
|401|  `{ &#34;message&#34;: &#34;Unauthorized&#34;}` |
|404|  `{ &#34;message&#34; : &#34;No Visitor ids were found for the account and profile&#34;}` |
|429| `{ &#34;message&#34;: &#34;Too many requests&#34;}` |
|500|  `{ &#34;message&#34; : &#34;Internal Server Error&#34;}` |
