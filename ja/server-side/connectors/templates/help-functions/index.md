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
|`tally.castIntegers.toJson`| `{&#34;A&#34;:1,&#34;B&#34;:2,&#34;C&#34;:3}`|

## encodeBase64

コンテンツをbase64でエンコードします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#encodeBase64}}`&lt;br&gt; `{{str}}` world&lt;br&gt; `{{/encodeBase64}}`| `wqDCoEhlbGxvIHdvcmxkCg==`|

## encodeUrl

コンテンツをURLエンコードします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#encodeUrl}}https://www.google.com/search?q=tealium{{/encodeUrl}}`| `https%3A%2F%2Fwww.google.com%2Fsearch%3Fq%3Dtealium`|

## escapeHtml

HTMLドキュメントで使用するために値をエスケープします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#escapeHtml}}&lt;hello&gt;&amp;&#34;world{{/escapeHtml}}`| `&amp;lt;hello&amp;gt;&amp;amp;&amp;quot;world`|

## escapeJson

JSONオブジェクト/配列で使用するために値をエスケープします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#escapeJson}}{&#34;foo&#34;:&#34;bar&#34;}{{/escapeJson}}`| `{\&#34;foo\&#34;:\&#34;bar\&#34;}`|

## escapeXml

XMLドキュメントで使用するために値をエスケープします。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#escapeXml}}&lt;hello&gt;&amp;\&#34;world{{/escapeXml}}`| `&amp;lt;hello&amp;gt;&amp;amp;&amp;quot;world`|

## formatDate

指定されたパターンに従って日付変数をフォーマットします。パターン構文はJavaのSimple Dateフォーマットに対応しています。完全な表リストについては、[Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html)を参照してください。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{dat}}`| `2020-09-15T00:00:00.000Z`|
|`{{formatDate dat pattern=&#34;yyyy-MM-dd HH:mm a&#34;}}`| `2020-09-15 00:00 AM`|

## hash

秘密鍵を使用してハッシュベースのメッセージ認証コード（HMAC）を生成します。HMACは、メッセージの性質を認証するのに役立つデータの小さなセットであり、メッセージの完全性と真正性を保護します。

秘密鍵は、HMACを計算するために使用される一意の情報であり、メッセージの送信者と受信者の両方によって知られています。この鍵の長さは使用するアルゴリズムによって異なります。

次の例では、テンプレートのためにマップされた`testKey`、`timestamp`、`ip`、`lang`がテンプレート変数として仮定されています。

**テンプレート変数:**
```js
timestamp = &#34;2020-08-20T08:45:33.412&#34;
ip        = &#34;127.0.0.1&#34;
lang      = &#34;en-US&#34;
testKey   = &#34;w8sZzy8EaPaxFKfaoTqUi6&#34;
```

**テンプレート:**

```json
{{hash algorithm=&#34;HmacSHA256&#34; encodingCharset=&#34;UTF-8&#34; binaryEncoding=&#34;hex&#34; joinOn=&#34;&#34; useSecretKey=&#34;true&#34; testKey timestamp ip lang}}
``` 

**レンダリングされた出力:**

```none
a0afb572e3fc174c2dea112e1a9922fb9903caa65e6aa9e50e47758b8a611542
```

ハッシュ関数の利用可能なオプションを以下の表に示します:

|**オプション**| **必須**| **可能な値**| **説明**|
|---| ---| ---| ---|
|algorithm| はい| 例: `HmacSHA256`| 利用可能なオプションは:&lt;br&gt; - `secretKey=&#34;true&#34;`の場合は[Java Mac Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#Mac)を参照&lt;br&gt; - `secretKey=&#34;false&#34;`の場合は[Java MessageDigest Algorithms](https://docs.oracle.com/javase/7/docs/technotes/guides/security/StandardNames.html#MessageDigest)を参照|
|encodingCharset| いいえ| `UTF-8` (デフォルト), `US-ASCII`|
|binaryEncoding| いいえ| `base64` (デフォルト), `hex`|
|binaryEncodingOptions| いいえ| `lowercase` (デフォルト), `uppercase`| `binaryEncoding=&#34;hex&#34;`の場合のみ適用|
|joinOn| いいえ| 結合セパレータ; 空の値 `&#34;&#34;`が必要な場合は提供|
|useSecretKey| いいえ| `false` (デフォルト) または `true`|
|secretKey| いいえ|
|variables| はい| 最後に指定されたオプションの後にすべての変数を配置します。例えば、`secretKey=&#34;true&#34;`の場合、すべてのオプションが指定された後の最初の変数が`secretKey`として使用され、その他すべてが`joinOn`オプションで結合される変数として使用されます。`secretKey=&#34;false&#34;`を使用する場合、すべての変数が`joinOn`オプションで使用されます。|

## if

変数が存在し、内容がある場合に内容を印刷します。次の例では、テンプレートに`lang`が有効な入力変数として存在すると仮定しています。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#if str}} {{str}} world! {{/if}}`| `Hello world!`|
|`{{#if arrn}} {{arrn.toJson}} {{/if}}`| `[1.0,2.0,3.0]`|
|`{{#if ss}} {{ss.toJson}} {{/if}}`| `[&#34;A&#34;,&#34;B&#34;,&#34;C&#34;]`|

## isEq

値が等しい場合に内容を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#isEq bln true}}Boolean is true{{/isEq}}`| `Boolean is true`|
|`{{#isEq bln false}}Boolean is false{{/isEq}}`|
|`{{#isEq str &#34;Hello&#34;}}String is Hello{{/isEq}}`| `String is Hello`|
|`{{#isEq str &#34;Test&#34;}}String is Test{{/isEq}}`|

## isNotEq

値が等しくない場合に内容を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#isNotEq bln true}}Boolean is false{{/isNotEq}}`|
|`{{#isNotEq bln false}}Boolean is true{{/isNotEq}}`| `Boolean is true`|
|`{{#isNotEq str &#34;Hello&#34;}}Hello world!{{/isNotEq}}`|
|`{{#isNotEq str &#34;Some string&#34;}}Hello there!{{/isNotEq}}`| `Hello there!`|

## join

リストをオプショナルなジョイナーを使用して文字列に変換します。`empty_list`が空のリストであると仮定します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{join ss}}`| `A,B,C`|
|`{{join ss on=&#34; and &#34;}}`| `A and B and C`|
|`{{join ss on=&#34;&#34;}}`| `A B C`|
|`{{join empty_list on=&#34; and &#34;}}`|

## jsonMinify

有効なJSONを含むコンテンツが提供された場合、それを最小化します（すべての空白を削除します）。コンテンツが有効なJSONでない場合、変更なしで元の値が表示されます。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#jsonMinify}}`&lt;br&gt; `{`&lt;br&gt; `&#34;name&#34; : &#34;Bob&#34;,`&lt;br&gt; `&#34;status&#34; : &#34;He is hungry!&#34;,`&lt;br&gt; `}`&lt;br&gt; `{{/jsonMinify}}`| `{&#34;name&#34;:&#34;Bob&#34;,&#34;status&#34;:&#34;He is hungry!&#34;}` |

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
|`{{sequence}}`| &#34;123456789&#34;|
|`{{substring sequence start=&#34;0&#34; end=&#34;5&#34;}}`| &#34;12345&#34;|

## substringAfter

指定されたセパレータ文字列の後の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringAfter screenSize separator=&#34;x&#34;}}`| &#34;480x640&#34;|

## substringAfterLast

指定されたセパレータ文字列の最後の出現後の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringAfterLast screenSize separator=&#34;x&#34;}}`| &#34;640&#34;|

## substringBefore

指定されたセパレータ文字列の前の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringBefore screenSize separator=&#34;x&#34;}}`| &#34;340&#34;|

## substringBeforeLast

指定されたセパレータ文字列の最後の出現前の部分文字列を印刷します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{screensize}}`| &#34;340x480x640&#34;|
|`{{substringBeforeLast screenSize separator=&#34;x&#34;}}`| &#34;340x480&#34;|
## substringBetween

指定された `open` と `close` 文字列の間の部分文字列を出力します。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{animals}}`| &#34;cat dog tiger duck&#34;|
|`{{substringBetween animals open=&#34;cat&#34; close=&#34;duck&#34;}}`| &#34; dog tiger &#34;|

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
|`{{tly.toJson}}`| `{&#34;A&#34;:1.0,&#34;B&#34;:2.0,&#34;C&#34;:3.0}`|

## toList

JSON形式の配列文字列を配列に変換し、追加操作を行います。

`arrn: [&#34;1&#34;,&#34;2&#34;,&#34;2&#34;]`の場合：

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
|`{{unixTimestamp format=&#34;yyyy-MM-dd HH:mm a&#34;}}`| `2020-09-11 21:24 PM`|

## unixTimestampMs

Unixエポック以降のミリ秒数でコネクタの発火時間を出力します。認証ヘッダーに役立ちます。オプションで、指定されたパターンに従って日付変数をフォーマットすることができます。パターンの構文はJavaのSimple Dateフォーマットに対応しています。完全な表のリストについては、[Java Simple Date Format documentation](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html)を参照してください。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{unixTimestampMs}}`| `1599859605838`|
|`{{unixTimestampMs format=&#34;yyyy-MM-dd HH:mm a&#34;}}`| `2020-09-11 21:26 PM`|

## unless

パラメータが存在しないか内容がない場合に内容を出力します。これは `if` の逆です。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{#unless str}}str doesn&#39;t exist or no content{{/unless}}`|
|`{{#unless str2}}str2 doesn&#39;t exist or no content{{/unless}}`| `str2 doesn&#39;t exist or no content`|

## uuid

ランダムに生成されたUUIDを出力します。UUIDは、リソースを識別するためや分散システムでの一意性を保証するために一般的に使用される、全世界で一意の識別子です。

|**テンプレート**| **レンダリングされた値**|
|---| ---|
|`{{uuid}}`| `4d61f298-2a8d-461d-a3bf-b153892a7b49`|