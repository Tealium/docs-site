---
title: Template helper functions
description: Learn how to build complex connector requests using these helper functions.
url: https://docs.tealium.com/server-side/connectors/templates/help-functions/
---
Connector templates are built on Trimou, a Java templating engine based on Mustache.

For more information, see: [Trimou 2.3.0 Documentation](http://trimou.org/doc/2.3.0.Final/trimou-doc.html)

Connector templates support additional and custom functionality through helper functions. They allow for transforming data to make it easier to generate the exact format required by your vendor&#39;s API.

## castIntegers

This helper forces the output in collections to be integer values. Can be used with `toJson`.

|**Template**| **Rendered Value**|
|---| ---|
|`tally`| `{A=1.0, B=2.0, C=3.0}`|
|`tally.castIntegers`| `{A=1, B=2, C=3}`|
|`tally.castIntegers.toJson`| `{&#34;A&#34;:1,&#34;B&#34;:2,&#34;C&#34;:3}`|

## encodeBase64

Encode content in base64.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#encodeBase64}}`&lt;br&gt; `{{str}}` world&lt;br&gt; `{{/encodeBase64}}`| `wqDCoEhlbGxvIHdvcmxkCg==`|

## encodeUrl

URL-encode content.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#encodeUrl}}https://www.google.com/search?q=tealium{{/encodeUrl}}`| `https%3A%2F%2Fwww.google.com%2Fsearch%3Fq%3Dtealium`|

## escapeHtml

Escape values for use in HTML documents.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#escapeHtml}}&lt;hello&gt;&amp;&#34;world{{/escapeHtml}}`| `&amp;lt;hello&amp;gt;&amp;amp;&amp;quot;world`|

## escapeJson

Escape values for use in JSON objects/arrays.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#escapeJson}}{&#34;foo&#34;:&#34;bar&#34;}{{/escapeJson}}`| `{\&#34;foo\&#34;:\&#34;bar\&#34;}`|

## escapeXml

Escape values for use in XML documents.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#escapeXml}}&lt;hello&gt;&amp;\&#34;world{{/escapeXml}}`| `&amp;lt;hello&amp;gt;&amp;amp;&amp;quot;world`|

## formatDate

Format a date variable according to specified pattern. Pattern syntax corresponds to Java’s Simple Date formatting. For full table listing, see the [Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

|**Template**| **Rendered Value**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{formatDate dat pattern=&#34;yyyy-MM-dd HH:mm a&#34;}}`| `2020-09-15 00:00 AM`|

## hash

Generate a hash-based message authentication code (HMAC) using a secret key. An HMAC is a small set of data that helps authenticate the nature of message; it protects the integrity and the authenticity of the message.

The secret key is a unique piece of information used to compute the HMAC and is known both by the sender and the receiver of the message. This key varies in length depending on the algorithm you use.

The following example assumes that `testKey`, `timestamp`, `ip`, and `lang` are mapped template variable for the template.

**Template variables:**
```js
timestamp = &#34;2020-08-20T08:45:33.412&#34;
ip        = &#34;127.0.0.1&#34;
lang      = &#34;en-US&#34;
testKey   = &#34;w8sZzy8EaPaxFKfaoTqUi6&#34;
```

**Template:**

```json
{{hash algorithm=&#34;HmacSHA256&#34; encodingCharset=&#34;UTF-8&#34; binaryEncoding=&#34;hex&#34; joinOn=&#34;&#34; useSecretKey=&#34;true&#34; testKey timestamp ip lang}}
``` 

**Rendered output:**

```none
a0afb572e3fc174c2dea112e1a9922fb9903caa65e6aa9e50e47758b8a611542
```

The following table lists the available options for the hash function:

|**Options**| **Required**| **Possible Values**| **Description**|
|---| ---| ---| ---|
|algorithm| Yes| Example: `HmacSHA256`| Available options are:&lt;br&gt; - when `secretKey=&#34;true&#34;` refer to [Java Mac Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#Mac)&lt;br&gt; - when `secretKey=&#34;false&#34;` refer to [Java MessageDigest Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#MessageDigest)|
|encodingCharset| No| `UTF-8` (Default), `US-ASCII`|
|binaryEncoding| No| `base64` (Default), `hex`|
|binaryEncodingOptions| No| `lowercase` (Default), `uppercase`| Only applies when `binaryEncoding=&#34;hex&#34;`|
|joinOn| No| Concatenation separator; provide empty value `&#34;&#34;` if you need to concatenate on empty.|
|useSecretKey| No| `false` (default) or `true`|
|secretKey| No|
|variables| YES| Place all variables after the last option specified. For example, if with `secretKey=&#34;true&#34;` the first variable after all options are specified is used as the `secretKey` and all the others as the variables to be joined by `joinOn` option. When using `secretKey=&#34;false&#34;`, all variables are used in the `joinOn` option.|

## if

Print the content if the variable exists and has content. The following example assumes that `lang` exist as valid input variables in the template.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#if str}} {{str}} world! {{/if}}`| `Hello world!`|
|`{{#if arrn}} {{arrn.toJson}} {{/if}}`| `[1.0,2.0,3.0]`|
|`{{#if ss}} {{ss.toJson}} {{/if}}`| `[&#34;A&#34;,&#34;B&#34;,&#34;C&#34;]`|

## isEq

Print the content if the values are equal.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#isEq bln true}}Boolean is true{{/isEq}}`| `Boolean is true`|
|`{{#isEq bln false}}Boolean is false{{/isEq}}`|
|`{{#isEq str &#34;Hello&#34;}}String is Hello{{/isEq}}`| `String is Hello`|
|`{{#isEq str &#34;Test&#34;}}String is Test{{/isEq}}`|

## isNotEq

Print the content if the values are not equal.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#isNotEq bln true}}Boolean is false{{/isNotEq}}`|
|`{{#isNotEq bln false}}Boolean is true{{/isNotEq}}`| `Boolean is true`|
|`{{#isNotEq str &#34;Hello&#34;}}Hello world!{{/isNotEq}}`|
|`{{#isNotEq str &#34;Some string&#34;}}Hello there!{{/isNotEq}}`| `Hello there!`|

## join

Join will convert a list into a string with an optional joiner. Assuming `empty_list` is an empty list, no value is rendered.

|**Template**| **Rendered Value**|
|---| ---|
|`{{join ss}}`| `A,B,C`|
|`{{join ss on=&#34; and &#34;}}`| `A and B and C`|
|`{{join ss on=&#34;&#34;}}`| `A B C`|
|`{{join empty_list on=&#34; and &#34;}}`|

## jsonMinify

If provided content that contains valid JSON, minifies it (removes all whitespace). If the content is not valid JSON, the original value is shown with no changes.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#jsonMinify}}`&lt;br&gt; `{`&lt;br&gt; `&#34;name&#34; : &#34;Bob&#34;,`&lt;br&gt; `&#34;status&#34; : &#34;He is hungry!&#34;,`&lt;br&gt; `}`&lt;br&gt; `{{/jsonMinify}}`| `{&#34;name&#34;:&#34;Bob&#34;,&#34;status&#34;:&#34;He is hungry!&#34;}` |

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
|`{{sequence}}`| &#34;123456789&#34;|
|`{{substring sequence start=&#34;0&#34; end=&#34;5&#34;}}`| &#34;12345&#34;|

## substringAfter

Print the substring after the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringAfter screenSize separator=&#34;x&#34;}}`| &#34;480x640&#34;|

## substringAfterLast

Print the substring after the last occurrence of the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringAfterLast screenSize separator=&#34;x&#34;}}`| &#34;640&#34;|

## substringBefore

Print the substring before the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringBefore screenSize separator=&#34;x&#34;}}`| &#34;340&#34;|

## substringBeforeLast

Print the substring before the last occurrence of the specified separator string.

|**Template**| **Rendered Value**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringBeforeLast screenSize separator=&#34;x&#34;}}`| &#34;340x480&#34;|

## substringBetween

Print the substring between the specified `open` and `close` strings.

|**Template**| **Rendered Value**|
|---| ---|
|`{{animals}}`| &#34;cat dog tiger duck&#34;|
|`{{substringBetween animals open=&#34;cat&#34; close=&#34;duck&#34;}}`| &#34; dog tiger &#34;|

## sum

Sum the values in a list or tally.

|**Template**| **Rendered Value**|
|---| ---|
|`{{tly.sum}}`| `6.0`|
|`{{arrn.sum}}`| `6.0`|

## toInteger

Convert a variable&#39;s value to an integer.

|**Template**| **Rendered Value**|
|---| ---|
|`{{num}}`| `1.0`|
|`{{num.toInteger}}`| `1`|

## toJson

Print the variable in a JSON format.

|**Template**| **Rendered Value**|
|---| ---|
|`{{tly}}`|` {A=1.0, B=2.0, C=3.0}`|
|`{{tly.toJson}}`| `{&#34;A&#34;:1.0,&#34;B&#34;:2.0,&#34;C&#34;:3.0}`|

## toList

Convert a JSON-formatted-array string into an array for additional operations.

For `arrn: [&#34;1&#34;,&#34;2&#34;,&#34;2&#34;]`:

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

Convert a date variable&#39;s value to the Unix milliseconds timestamp format.

|**Template**| **Rendered Value**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{dat.toTimestampMs}}`| `1600128000000`|

## unixTimestamp

Print the connector fire time in seconds since Unix epoch. This is useful for authorization headers. Optionally, format the date variable according to a specified pattern. Pattern syntax corresponds to Java’s Simple Date formatting. For full table listing, see the [Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

|**Template**| **Rendered Value**|
|---| ---|
|`{{unixTimestamp}}`| `1599859440`|
|`{{unixTimestamp format=&#34;yyyy-MM-dd HH:mm a&#34;}}`| `2020-09-11 21:24 PM`|

## unixTimestampMs

Print the connector fire time in milliseconds since epoch. This is useful for authorization headers. Optionally, format the date variable according to a specified pattern. Pattern syntax corresponds to Java’s Simple Date formatting. For full table listing, see the [Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html).

|**Template**| **Rendered Value**|
|---| ---|
|`{{unixTimestampMs}}`| `1599859605838`|
|`{{unixTimestampMs format=&#34;yyyy-MM-dd HH:mm a&#34;}}`| `2020-09-11 21:26 PM`|

## unless

Print the content if the parameter does not exist or has no content. This is the inverse of `if`.

|**Template**| **Rendered Value**|
|---| ---|
|`{{#unless str}}str doesn&#39;t exist or no content{{/unless}}`|
|`{{#unless str2}}str2 doesn&#39;t exist or no content{{/unless}}`| `str2 doesn&#39;t exist or no content`|

## uuid

Print a randomly generated UUID, which is a universally unique identifier commonly used for identifying resources or ensuring uniqueness in distributed systems.

|**Template**| **Rendered Value**|
|---| ---|
|`{{uuid}}`| `4d61f298-2a8d-461d-a3bf-b153892a7b49`|