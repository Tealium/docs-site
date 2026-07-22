---
title: Template helper functions
description: Learn how to build complex connector requests using these helper functions.
url: https://docs.tealium.com/server-side/connectors/templates/help-functions/
---
Connector templates are built on Trimou, a Java templating engine based on Mustache.

For more information, see: [Trimou 2.3.0 Documentation](http://trimou.org/doc/2.3.0.Final/trimou-doc.html)

Connector templates support additional and custom functionality through helper functions. They allow for transforming data to make it easier to generate the exact format required by your vendor's API.

## castIntegers

This helper forces the output in collections to be integer values. Can be used with `toJson`.

|**Template**| **Rendered Value**|
|---| ---|
|`tally`| `{A=1.0, B=2.0, C=3.0}`|
|`tally.castIntegers`| `{A=1, B=2, C=3}`|
|`tally.castIntegers.toJson`| `{"A":1,"B":2,"C":3}`|

## encodeBase64

Encode content in base64.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#encodeBase64}}`<br> `{{str}}` world<br> `{{/encodeBase64}}`| `wqDCoEhlbGxvIHdvcmxkCg==`|

## encodeUrl

URL-encode content.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#encodeUrl}}https://www.google.com/search?q=tealium{{/encodeUrl}}`| `https%3A%2F%2Fwww.google.com%2Fsearch%3Fq%3Dtealium`|

## escapeHtml

Escape values for use in HTML documents.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#escapeHtml}}<hello>&"world{{/escapeHtml}}`| `&lt;hello&gt;&amp;&quot;world`|

## escapeJson

Escape values for use in JSON objects/arrays.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#escapeJson}}{"foo":"bar"}{{/escapeJson}}`| `{\"foo\":\"bar\"}`|

## escapeXml

Escape values for use in XML documents.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#escapeXml}}<hello>&\"world{{/escapeXml}}`| `&lt;hello&gt;&amp;&quot;world`|

## formatDate

Format a date variable according to specified pattern. Pattern syntax corresponds to Java’s Simple Date formatting. For full table listing, see the [Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

|**Template**| **Rendered Value**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{formatDate dat pattern="yyyy-MM-dd HH:mm a"}}`| `2020-09-15 00:00 AM`|

## hash

Generate a hash-based message authentication code (HMAC) using a secret key. An HMAC is a small set of data that helps authenticate the nature of message; it protects the integrity and the authenticity of the message.

The secret key is a unique piece of information used to compute the HMAC and is known both by the sender and the receiver of the message. This key varies in length depending on the algorithm you use.

The following example assumes that `testKey`, `timestamp`, `ip`, and `lang` are mapped template variable for the template.

**Template variables:**
```js
timestamp = "2020-08-20T08:45:33.412"
ip        = "127.0.0.1"
lang      = "en-US"
testKey   = "w8sZzy8EaPaxFKfaoTqUi6"
```

**Template:**

```json
{{hash algorithm="HmacSHA256" encodingCharset="UTF-8" binaryEncoding="hex" joinOn="" useSecretKey="true" testKey timestamp ip lang}}
``` 

**Rendered output:**

```none
a0afb572e3fc174c2dea112e1a9922fb9903caa65e6aa9e50e47758b8a611542
```

The following table lists the available options for the hash function:

|**Options**| **Required**| **Possible Values**| **Description**|
|---| ---| ---| ---|
|algorithm| Yes| Example: `HmacSHA256`| Available options are:<br> - when `secretKey="true"` refer to [Java Mac Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#Mac)<br> - when `secretKey="false"` refer to [Java MessageDigest Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#MessageDigest)|
|encodingCharset| No| `UTF-8` (Default), `US-ASCII`|
|binaryEncoding| No| `base64` (Default), `hex`|
|binaryEncodingOptions| No| `lowercase` (Default), `uppercase`| Only applies when `binaryEncoding="hex"`|
|joinOn| No| Concatenation separator; provide empty value `""` if you need to concatenate on empty.|
|useSecretKey| No| `false` (default) or `true`|
|secretKey| No|
|variables| YES| Place all variables after the last option specified. For example, if with `secretKey="true"` the first variable after all options are specified is used as the `secretKey` and all the others as the variables to be joined by `joinOn` option. When using `secretKey="false"`, all variables are used in the `joinOn` option.|

## if

Print the content if the variable exists and has content. The following example assumes that `lang` exist as valid input variables in the template.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#if str}} {{str}} world! {{/if}}`| `Hello world!`|
|`{{#if arrn}} {{arrn.toJson}} {{/if}}`| `[1.0,2.0,3.0]`|
|`{{#if ss}} {{ss.toJson}} {{/if}}`| `["A","B","C"]`|

## isEq

Print the content if the values are equal.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#isEq bln true}}Boolean is true{{/isEq}}`| `Boolean is true`|
|`{{#isEq bln false}}Boolean is false{{/isEq}}`|
|`{{#isEq str "Hello"}}String is Hello{{/isEq}}`| `String is Hello`|
|`{{#isEq str "Test"}}String is Test{{/isEq}}`|

## isNotEq

Print the content if the values are not equal.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#isNotEq bln true}}Boolean is false{{/isNotEq}}`|
|`{{#isNotEq bln false}}Boolean is true{{/isNotEq}}`| `Boolean is true`|
|`{{#isNotEq str "Hello"}}Hello world!{{/isNotEq}}`|
|`{{#isNotEq str "Some string"}}Hello there!{{/isNotEq}}`| `Hello there!`|

## join

Join will convert a list into a string with an optional joiner. Assuming `empty_list` is an empty list, no value is rendered.

|**Template**| **Rendered Value**|
|---| ---|
|`{{join ss}}`| `A,B,C`|
|`{{join ss on=" and "}}`| `A and B and C`|
|`{{join ss on=""}}`| `A B C`|
|`{{join empty_list on=" and "}}`|

## jsonMinify

If provided content that contains valid JSON, minifies it (removes all whitespace). If the content is not valid JSON, the original value is shown with no changes.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#jsonMinify}}`<br> `{`<br> `"name" : "Bob",`<br> `"status" : "He is hungry!",`<br> `}`<br> `{{/jsonMinify}}`| `{"name":"Bob","status":"He is hungry!"}` |

## md5

MD5 hash the content.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#md5}}Hello World!{{/md5}}`| `ed076287532e86365e841e92bfc50d8c`|

## sha1

SHA1 hash the content.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#sha1}}Hello world!{{/sha1}}`| `d3486ae9136e7856bc42212385ea797094475802`|

## sha256

SHA256 hash the content.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#sha256}}Hello World!{{/sha256}}`| `7f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069`|

## substring

Print the substring that begins at the specified `start` index and ends at the specified `end` index - 1.

|**Template**| **Rendered Value**|
|---| ---|
|`{{sequence}}`| "123456789"|
|`{{substring sequence start="0" end="5"}}`| "12345"|

## substringAfter

Print the substring after the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringAfter screenSize separator="x"}}`| "480x640"|

## substringAfterLast

Print the substring after the last occurrence of the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringAfterLast screenSize separator="x"}}`| "640"|

## substringBefore

Print the substring before the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringBefore screenSize separator="x"}}`| "340"|

## substringBeforeLast

Print the substring before the last occurrence of the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringBeforeLast screenSize separator="x"}}`| "340x480"|

## substringBetween

Print the substring between the specified `open` and `close` strings.

|**Template**| **Rendered Value**|
|---| ---|
|`{{animals}}`| "cat dog tiger duck"|
|`{{substringBetween animals open="cat" close="duck"}}`| " dog tiger "|

## sum

Sum the values in a list or tally.

|**Template**| **Rendered Value**|
|---| ---|
|`{{tly.sum}}`| `6.0`|
|`{{arrn.sum}}`| `6.0`|

## toInteger

Convert a variable's value to an integer.

|**Template**| **Rendered Value**|
|---| ---|
|`{{num}}`| `1.0`|
|`{{num.toInteger}}`| `1`|

## toJson

Print the variable in a JSON format.

|**Template**| **Rendered Value**|
|---| ---|
|`{{tly}}`|` {A=1.0, B=2.0, C=3.0}`|
|`{{tly.toJson}}`| `{"A":1.0,"B":2.0,"C":3.0}`|

## toList

Convert a JSON-formatted-array string into an array for additional operations.

For `arrn: ["1","2","2"]`:

|**Template**| **Rendered Value**|
|---| ---|
|`{{arrn.toList.sum}}`| `6.0`|

## toTimestamp
Convert a date variable’s value to the Unix seconds timestamp format.

|**Template**| **Rendered Value**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{dat.toTimestamp}}`| `1600128000`|

## toTimestampMs

Convert a date variable's value to the Unix milliseconds timestamp format.

|**Template**| **Rendered Value**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{dat.toTimestampMs}}`| `1600128000000`|

## unixTimestamp

Print the connector fire time in seconds since Unix epoch. This is useful for authorization headers. Optionally, format the date variable according to a specified pattern. Pattern syntax corresponds to Java’s Simple Date formatting. For full table listing, see the [Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

|**Template**| **Rendered Value**|
|---| ---|
|`{{unixTimestamp}}`| `1599859440`|
|`{{unixTimestamp format="yyyy-MM-dd HH:mm a"}}`| `2020-09-11 21:24 PM`|

## unixTimestampMs

Print the connector fire time in milliseconds since epoch. This is useful for authorization headers. Optionally, format the date variable according to a specified pattern. Pattern syntax corresponds to Java’s Simple Date formatting. For full table listing, see the [Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

|**Template**| **Rendered Value**|
|---| ---|
|`{{unixTimestampMs}}`| `1599859605838`|
|`{{unixTimestampMs format="yyyy-MM-dd HH:mm a"}}`| `2020-09-11 21:26 PM`|

## unless

Print the content if the parameter does not exist or has no content. This is the inverse of `if`.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#unless str}}str doesn't exist or no content{{/unless}}`|
|`{{#unless str2}}str2 doesn't exist or no content{{/unless}}`| `str2 doesn't exist or no content`|

## uuid

Print a randomly generated UUID, which is a universally unique identifier commonly used for identifying resources or ensuring uniqueness in distributed systems.

|**Template**| **Rendered Value**|
|---| ---|
|`{{uuid}}`| `4d61f298-2a8d-461d-a3bf-b153892a7b49`|