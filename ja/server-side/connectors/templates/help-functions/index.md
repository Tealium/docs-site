---
title: テンプレートヘルパー関数
description: これらのヘルパー関数を使用して複雑なコネクタリクエストを構築する方法を学びます。
url: https://docs.tealium.com/ja/server-side/connectors/templates/help-functions/
---
コネクタテンプレートは、Mustacheに基づいたJavaテンプレートエンジンであるTrimouを使用して構築されています。

詳細については、[Trimou 2.3.0 ドキュメント](http://trimou.org/doc/2.3.0.Final/trimou-doc.html)を参照してください。

コネクタテンプレートは、ヘルパー関数を通じて追加およびカスタム機能をサポートしています。これにより、データを変換して、ベンダーのAPIに必要な正確な形式を生成しやすくなります。

## castIntegers

このヘルパーは、コレクションの出力を整数値に強制します。`toJson`と共に使用できます。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`tally`| `{A=1.0, B=2.0, C=3.0}`|
|`tally.castIntegers`| `{A=1, B=2, C=3}`|
|`tally.castIntegers.toJson`| `{"A":1,"B":2,"C":3}`|

## encodeBase64

コンテンツをbase64でエンコードします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#encodeBase64}}`<br> `{{str}}` world<br> `{{/encodeBase64}}`| `wqDCoEhlbGxvIHdvcmxkCg==`|

## encodeUrl

コンテンツをURLエンコードします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#encodeUrl}}https://www.google.com/search?q=tealium{{/encodeUrl}}`| `https%3A%2F%2Fwww.google.com%2Fsearch%3Fq%3Dtealium`|

## escapeHtml

HTMLドキュメントで使用するために値をエスケープします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#escapeHtml}}<hello>&"world{{/escapeHtml}}`| `&lt;hello&gt;&amp;&quot;world`|

## escapeJson

JSONオブジェクト/配列で使用するために値をエスケープします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#escapeJson}}{"foo":"bar"}{{/escapeJson}}`| `{\"foo\":\"bar\"}`|

## escapeXml

XMLドキュメントで使用するために値をエスケープします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#escapeXml}}<hello>&\"world{{/escapeXml}}`| `&lt;hello&gt;&amp;&quot;world`|

## formatDate

指定されたパターンに従って日付変数をフォーマットします。パターン構文はJavaのSimple Dateフォーマットに対応しています。完全な表リストについては、[Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html)を参照してください。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{formatDate dat pattern="yyyy-MM-dd HH:mm a"}}`| `2020-09-15 00:00 AM`|

## hash

秘密鍵を使用してハッシュベースのメッセージ認証コード（HMAC）を生成します。HMACは、メッセージの性質を認証するのに役立つデータの小さなセットであり、メッセージの完全性と真正性を保護します。

秘密鍵は、HMACを計算するために使用される一意の情報であり、メッセージの送信者と受信者の両方によって知られています。この鍵の長さは使用するアルゴリズムによって異なります。

次の例では、テンプレートのためにマップされた`testKey`、`timestamp`、`ip`、`lang`がテンプレート変数として仮定されています。

**テンプレート変数:**
```js
timestamp = "2020-08-20T08:45:33.412"
ip        = "127.0.0.1"
lang      = "en-US"
testKey   = "w8sZzy8EaPaxFKfaoTqUi6"
```

**テンプレート:**

```json
{{hash algorithm="HmacSHA256" encodingCharset="UTF-8" binaryEncoding="hex" joinOn="" useSecretKey="true" testKey timestamp ip lang}}
``` 

**レンダリングされた出力:**

```none
a0afb572e3fc174c2dea112e1a9922fb9903caa65e6aa9e50e47758b8a611542
```

ハッシュ関数の利用可能なオプションを以下の表に示します:

|**オプション**| **必須**| **可能な値**| **説明**|
|---| ---| ---| ---|
|algorithm| はい| 例: `HmacSHA256`| 利用可能なオプションは:<br> - `secretKey="true"`の場合は[Java Mac Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#Mac)を参照<br> - `secretKey="false"`の場合は[Java MessageDigest Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#MessageDigest)を参照|
|encodingCharset| いいえ| `UTF-8` (デフォルト), `US-ASCII`|
|binaryEncoding| いいえ| `base64` (デフォルト), `hex`|
|binaryEncodingOptions| いいえ| `lowercase` (デフォルト), `uppercase`| `binaryEncoding="hex"`の場合のみ適用|
|joinOn| いいえ| 結合セパレータ; 空の値 `""`が必要な場合は提供|
|useSecretKey| いいえ| `false` (デフォルト) または `true`|
|secretKey| いいえ|
|variables| はい| 最後に指定されたオプションの後にすべての変数を配置します。例えば、`secretKey="true"`の場合、すべてのオプションが指定された後の最初の変数が`secretKey`として使用され、その他すべてが`joinOn`オプションで結合される変数として使用されます。`secretKey="false"`を使用する場合、すべての変数が`joinOn`オプションで使用されます。|

## if

変数が存在し、内容がある場合に内容を印刷します。次の例では、テンプレートに`lang`が有効な入力変数として存在すると仮定しています。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#if str}} {{str}} world! {{/if}}`| `Hello world!`|
|`{{#if arrn}} {{arrn.toJson}} {{/if}}`| `[1.0,2.0,3.0]`|
|`{{#if ss}} {{ss.toJson}} {{/if}}`| `["A","B","C"]`|

## isEq

値が等しい場合に内容を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#isEq bln true}}Boolean is true{{/isEq}}`| `Boolean is true`|
|`{{#isEq bln false}}Boolean is false{{/isEq}}`|
|`{{#isEq str "Hello"}}String is Hello{{/isEq}}`| `String is Hello`|
|`{{#isEq str "Test"}}String is Test{{/isEq}}`|

## isNotEq

値が等しくない場合に内容を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#isNotEq bln true}}Boolean is false{{/isNotEq}}`|
|`{{#isNotEq bln false}}Boolean is true{{/isNotEq}}`| `Boolean is true`|
|`{{#isNotEq str "Hello"}}Hello world!{{/isNotEq}}`|
|`{{#isNotEq str "Some string"}}Hello there!{{/isNotEq}}`| `Hello there!`|

## join

リストをオプショナルなジョイナーを使用して文字列に変換します。`empty_list`が空のリストであると仮定します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{join ss}}`| `A,B,C`|
|`{{join ss on=" and "}}`| `A and B and C`|
|`{{join ss on=""}}`| `A B C`|
|`{{join empty_list on=" and "}}`|

## jsonMinify

有効なJSONを含むコンテンツが提供された場合、それを最小化します（すべての空白を削除します）。コンテンツが有効なJSONでない場合、変更なしで元の値が表示されます。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#jsonMinify}}`<br> `{`<br> `"name" : "Bob",`<br> `"status" : "He is hungry!",`<br> `}`<br> `{{/jsonMinify}}`| `{"name":"Bob","status":"He is hungry!"}` |

## md5

コンテンツをMD5ハッシュします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#md5}}Hello World!{{/md5}}`| `ed076287532e86365e841e92bfc50d8c`|

## sha1

コンテンツをSHA1ハッシュします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#sha1}}Hello world!{{/sha1}}`| `d3486ae9136e7856bc42212385ea797094475802`|

## sha256

コンテンツをSHA256ハッシュします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#sha256}}Hello World!{{/sha256}}`| `7f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069`|

## substring

指定された`start`インデックスで始まり、指定された`end`インデックス-1で終わる部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{sequence}}`| "123456789"|
|`{{substring sequence start="0" end="5"}}`| "12345"|

## substringAfter

指定されたセパレータ文字列の後の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringAfter screenSize separator="x"}}`| "480x640"|

## substringAfterLast

指定されたセパレータ文字列の最後の出現後の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringAfterLast screenSize separator="x"}}`| "640"|

## substringBefore

指定されたセパレータ文字列の前の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringBefore screenSize separator="x"}}`| "340"|

## substringBeforeLast

指定されたセパレータ文字列の最後の出現前の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| "340x480x640"|
|`{{substringBeforeLast screenSize separator="x"}}`| "340x480"|
## substringBetween

指定された `open` と `close` 文字列の間の部分文字列を出力します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{animals}}`| "cat dog tiger duck"|
|`{{substringBetween animals open="cat" close="duck"}}`| " dog tiger "|

## sum

リストまたは集計の値を合計します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{tly.sum}}`| `6.0`|
|`{{arrn.sum}}`| `6.0`|

## toInteger

変数の値を整数に変換します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{num}}`| `1.0`|
|`{{num.toInteger}}`| `1`|

## toJson

変数をJSON形式で出力します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{tly}}`|` {A=1.0, B=2.0, C=3.0}`|
|`{{tly.toJson}}`| `{"A":1.0,"B":2.0,"C":3.0}`|

## toList

JSON形式の配列文字列を配列に変換し、追加操作を行います。

`arrn: ["1","2","2"]`の場合：

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{arrn.toList.sum}}`| `6.0`|

## toTimestamp
日付変数の値をUnix秒タイムスタンプ形式に変換します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{dat.toTimestamp}}`| `1600128000`|

## toTimestampMs

日付変数の値をUnixミリ秒タイムスタンプ形式に変換します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{dat.toTimestampMs}}`| `1600128000000`|

## unixTimestamp

Unixエポック以降の秒数でコネクタの発火時間を出力します。認証ヘッダーに役立ちます。オプションで、指定されたパターンに従って日付変数をフォーマットすることができます。パターンの構文はJavaのSimple Dateフォーマットに対応しています。完全な表のリストについては、[Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html)を参照してください。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{unixTimestamp}}`| `1599859440`|
|`{{unixTimestamp format="yyyy-MM-dd HH:mm a"}}`| `2020-09-11 21:24 PM`|

## unixTimestampMs

Unixエポック以降のミリ秒数でコネクタの発火時間を出力します。認証ヘッダーに役立ちます。オプションで、指定されたパターンに従って日付変数をフォーマットすることができます。パターンの構文はJavaのSimple Dateフォーマットに対応しています。完全な表のリストについては、[Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html)を参照してください。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{unixTimestampMs}}`| `1599859605838`|
|`{{unixTimestampMs format="yyyy-MM-dd HH:mm a"}}`| `2020-09-11 21:26 PM`|

## unless

パラメータが存在しないか内容がない場合に内容を出力します。これは `if` の逆です。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#unless str}}str doesn't exist or no content{{/unless}}`|
|`{{#unless str2}}str2 doesn't exist or no content{{/unless}}`| `str2 doesn't exist or no content`|

## uuid

ランダムに生成されたUUIDを出力します。UUIDは、リソースを識別するためや分散システムでの一意性を保証するために一般的に使用される、全世界で一意の識別子です。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{uuid}}`| `4d61f298-2a8d-461d-a3bf-b153892a7b49`|