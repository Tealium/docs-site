---
title: APIs and libraries for functions
description: This article provides information on the APIs and libraries available for functions.
url: https://docs.tealium.com/server-side/functions/modules/
---
Functions can use the following APIs and libraries:

* Crypto
* Crypto-ES.js
* TweetNaCl.js
* JavaScript Console API

## Crypto

This feature introduces a high-performance crypto and hashing library for Tealium Functions, implemented in Java. It offers a direct replacement for the existing JavaScript-based Crypto-ES library and provides the same interface.

For more information, see [NPM: Crypto-ES](https://www.npmjs.com/package/crypto-es/v/1.2.7).

### Import library

To import the Tealium crypto library, add the following line to your code:

```js
import C from &#34;tealium/crypto&#34;;
```

### Import modules

The Tealium Crypto library is organized into modules, each providing a separate class with specific cryptographic functionalities. This lets you optimize your function performance by only importing the modules you need.

The list of available modules:

```js
import { SHA384Algo } from &#39;tealium/crypto/lib/sha384.js&#39;;
import { SHA512Algo } from &#39;tealium/crypto/lib/sha512.js&#39;;
import { SHA3Algo } from &#39;tealium/crypto/lib/sha3.js&#39;;
import { RIPEMD160Algo } from &#39;tealium/crypto/lib/ripemd160.js&#39;;
import { PBKDF2Algo } from &#39;tealium/crypto/lib/pbkdf2.js&#39;;
import { EvpKDFAlgo } from &#39;tealium/crypto/lib/evpkdf.js&#39;;
import { AESAlgo } from &#39;tealium/crypto/lib/aes.js&#39;;
import { DESAlgo } from &#39;tealium/crypto/lib/tripledes.js&#39;;
import { TripleDESAlgo } from &#39;tealium/crypto/lib/tripledes.js&#39;;
import { RabbitAlgo } from &#39;tealium/crypto/lib/rabbit.js&#39;;
import { RabbitLegacyAlgo } from &#39;tealium/crypto/lib/rabbit-legacy.js&#39;;
import { RC4Algo } from &#39;tealium/crypto/lib/rc4.js&#39;;
import { RC4DropAlgo } from &#39;tealium/crypto/lib/rc4.js&#39;;
import { CBC } from &#39;tealium/crypto/lib/mode-cbc.js&#39;;
import { CFB } from &#39;tealium/crypto/lib/mode-cfb.js&#39;;
import { CTR } from &#39;tealium/crypto/lib/mode-ctr.js&#39;;
import { ECB } from &#39;tealium/crypto/lib/mode-ecb.js&#39;;
import { OFB } from &#39;tealium/crypto/lib/mode-ofb.js&#39;;
import { GCM } from &#39;tealium/crypto/lib/mode-gcm.js&#39;;
import { AnsiX923 } from &#39;tealium/crypto/lib/pad-ansix923.js&#39;;
import { Iso10126 } from &#39;tealium/crypto/lib/pad-iso10126.js&#39;;
import { Iso97971 } from &#39;tealium/crypto/lib/pad-iso97971.js&#39;;
import { NoPadding } from &#39;tealium/crypto/lib/pad-nopadding.js&#39;;
import { ZeroPadding } from &#39;tealium/crypto/lib/pad-zeropadding.js&#39;;
import { Pkcs7 } from &#39;tealium/crypto/lib/pad-pkcs7.js&#39;;
import { OpenSSLFormatter } from &#34;tealium/crypto/lib/cipher/OpenSSLFormatter.js&#34;;
import { HexFormatter } from &#39;tealium/crypto/lib/format-hex.js&#39;;
import { OpenSSLKdf } from &#34;tealium/crypto/lib/cipher/OpenSSLKdf.js&#34;;
import { MD5 } from &#39;tealium/crypto/lib/md5.js&#39;;
import { HmacMD5 } from &#39;tealium/crypto/lib/md5.js&#39;;
import { SHA1 } from &#39;tealium/crypto/lib/sha1.js&#39;;
import { HmacSHA1 } from &#39;tealium/crypto/lib/sha1.js&#39;;
import { SHA224 } from &#39;tealium/crypto/lib/sha224.js&#39;;
import { HmacSHA224 } from &#39;tealium/crypto/lib/sha224.js&#39;;
import { SHA256 } from &#39;tealium/crypto/lib/sha256.js&#39;;
import { HmacSHA256 } from &#39;tealium/crypto/lib/sha256.js&#39;;
import { SHA384 } from &#39;tealium/crypto/lib/sha384.js&#39;;
import { HmacSHA384 } from &#39;tealium/crypto/lib/sha384.js&#39;;
import { SHA512 } from &#39;tealium/crypto/lib/sha512.js&#39;;
import { HmacSHA512 } from &#39;tealium/crypto/lib/sha512.js&#39;;
import { SHA3 } from &#39;tealium/crypto/lib/sha3.js&#39;;
import { HmacSHA3 } from &#39;tealium/crypto/lib/sha3.js&#39;;
import { RIPEMD160 } from &#39;tealium/crypto/lib/ripemd160.js&#39;;
import { HmacRIPEMD160 } from &#39;tealium/crypto/lib/ripemd160.js&#39;;
import { PBKDF2 } from &#39;tealium/crypto/lib/pbkdf2.js&#39;;
import { EvpKDF } from &#39;tealium/crypto/lib/evpkdf.js&#39;;
import { AES } from &#39;tealium/crypto/lib/aes.js&#39;;
import { DES } from &#39;tealium/crypto/lib/tripledes.js&#39;;
import { TripleDES } from &#39;tealium/crypto/lib/tripledes.js&#39;;
import { Rabbit } from &#39;tealium/crypto/lib/rabbit.js&#39;;
import { RabbitLegacy } from &#39;tealium/crypto/lib/rabbit-legacy.js&#39;;
import { RC4 } from &#39;tealium/crypto/lib/rc4.js&#39;;
import { RC4Drop } from &#39;tealium/crypto/lib/rc4.js&#39;;
import { CRC32 } from &#39;tealium/crypto/lib/crc32.js&#39;;
```

### Examples

#### Hashing and modes

Galois/Counter mode is provided in place of CTRGladman mode. Use `C.mode.GCM` with the AES cipher:

```js
import C from &#34;tealium/crypto&#34;;
const msg = &#34;message&#34;;
const key = C.enc.Hex.parse(
&#34;0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777&#34;);
const iv = C.enc.Hex.parse(&#34;0102030405060708090A0B0C&#34;);
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding });
const decrypted = C.AES.decrypt(encrypted, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding });
```

Additional authentication data and tag length can be passed as parameters:

```js
import C from &#34;tealium/crypto&#34;;
const msg = &#34;message&#34;;
const key = C.enc.Hex.parse(
&#34;0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777&#34;);
const iv = C.enc.Hex.parse(&#34;0102030405060708090A0B0C&#34;);
const aad = C.enc.Utf8.parse(&#34;additional authentication data&#34;);
const tagLength = 128; // bits
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
const decrypted = C.AES.decrypt(encrypted, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
```

The `GCM.mac` method is not provided, but the encrypted output also contains the tag concatenated with the hash:

```js
import C from &#34;tealium/crypto&#34;;
const msg = &#34;message&#34;;
const key = C.enc.Hex.parse(
&#34;0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777&#34;);
const iv = C.enc.Hex.parse(&#34;0102030405060708090A0B0C&#34;);
const tagLength = 128; // bits
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, tagLength });
const sEncrypted = encrypted.ciphertext.toString();
const tag = sEncrypted.slice(sEncrypted.length - tagLength / 8 * 2, sEncrypted.length);
const hash = sEncrypted.slice(0, sEncrypted.length - tag.length);
```

To decrypt the message, the hash and tag must be concatenated:

```js
import C from &#34;tealium/crypto&#34;;
import CryptoES from &#34;crypto-es&#34;;
const msg = &#34;message&#34;;
const key = C.enc.Hex.parse(&#34;0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777&#34;);
const iv = C.enc.Hex.parse(&#34;0102030405060708090A0B0C&#34;);
const aad = C.enc.Utf8.parse(&#34;additional authentication data&#34;);
const tagLength = 120;
// encrypt with third-party
const encrypted = CryptoES.AES.encrypt(msg, key, { iv, mode: CryptoES.mode.GCM, padding: CryptoES.pad.NoPadding });
const tag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, encrypted.iv, aad, encrypted.ciphertext, tagLength / 8);
// decrypt with tealium/crypto
const decrypted = C.AES.decrypt(C.lib.CipherParams.create({ ciphertext: C.enc.Hex.parse(encrypted.ciphertext.toString() &#43; tag) }), key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
```

#### CRC32

CRC32 is added as an extension to `crypto-es` and is available under `index.js` or as a named import:

```js
import C from &#34;tealium/crypto&#34;; // C.CRC32
import { CRC32 } from &#34;tealium/crypto/lib/crc32.js&#34;;
```

In both cases, the function takes an argument representing data:

* `CRC32.buf(byte array)`: Expects a sequence of 8-bit unsigned integers (Uint8Array or array of bytes).
* `CRC32.bstr(binary string)`: Expects a binary string where byte i is the low byte of the UCS-2 char: `str.charCodeAt(i) &amp; 0xFF`
* `CRC32.str(string)`: Expects a standard JavaScript string and calculates the hash of the UTF-8 encoding.
* `CRC32.reset()`: The instance is stateful and requires manual reset after a hash calculation.
* `CRC32.valueOf()`: Returns a 32-bit signed integer representation of the state.

Usage:

```js
import { CRC32 } from &#34;tealium/crypto/lib/crc32.js&#34;;
// single iteration
const hash1 = CRC32.str(&#34;input&#34;).valueOf();
CRC32.reset();
// multiple
const hash2 = CRC32
    .buf([11, 111, 88])
    .str(&#34;try&#34;)
    .bstr(&#34;more&#34;)
    .valueOf();
CRC32.reset();
// convert to unsigned
const uHash1 = hash1 &gt;&gt;&gt; 0;
// convert to hex
const hHash1 = (hash1 &gt;&gt;&gt; 0).toString(16);
```

### Error messages

The Tealium crypto library is stricter about input data than `crypto-es`, so you might experience the following errors in cases of invalid usage:

| Error | Description |
|-------|-------------|
| `Invalid AES key length`| The key size for AES cipher must be 32 bytes. |
| `Wrong key size`| The key size for DES cipher must be 8 bytes, and for TripleDES it must be 16 bytes. |
| `Wrong IV length`| The IV size for some ciphers and modes is strict (DES, TripleDES, OFB) and must be specified correctly. |
| `Input length not multiple of 16 bytes`| `NoPadding` pad is used and the input must be correctly padded. |
| `Parameters missing`| That configuration object is not valid. For example, the `iv` parameter is missing for modes with mandatory IV (OFB, CFB). |
| `No IV set when one expected`| The `iv` parameter is missing in the configuration object for BouncyCastle implemented modes with mandatory IV (CTR). |

### Migrating from Crypto-ES to Tealium crypto library

The `tealium/crypto` library provides the same interface as `crypto-es` and can be used as a direct replacement. To minimize the risk of unexpected behavior in production when migrating, test the migration using one of the following approaches:

* **Use a sandbox environment with the `tealium/crypto` library (recommended)**  
Duplicate the function in a sandbox environment and update the imports to use `tealium/crypto`. Limit invocations to test audiences or feeds to verify that the function behaves as expected without affecting live traffic.

* **Run a `tealium/crypto` version in parallel with the existing function**  
Create a copy of the function and update the imports to use `tealium/crypto`. Route a portion of traffic to it for direct comparison under real-world conditions. This approach enables 1:1 output and performance validation but may increase resource usage and cost. Turn off the duplicate after testing to avoid unnecessary system load.

Avoid using the **Test** tab with test payloads, as it doesn&#39;t simulate production load or provide reliable performance insights.

After validation, you can migrate fully and turn off or delete the previous version using `crypto-es`.

## Crypto-ES.js (legacy)

This is a legacy version of the crypto library. For new use cases, see the [Tealium crypto library](#crypto) library, which offers the same interface with improved performance and modular imports.

Crypto-ES.js is a library of encryption algorithms available that provides hashing, encoding, and cipher algorithms. For more information, see [NPM: Crypto-ES](https://www.npmjs.com/package/crypto-es/v/1.2.7).

The following example shows how to encrypt and decrypt text:

```js
import CryptoES from &#39;crypto-es&#39;;

var encrypted = CryptoES.AES.encrypt(&#34;Message&#34;, &#34;Secret Passphrase&#34;);
console.log(encrypted);
var decrypted = CryptoES.AES.decrypt(encrypted, &#34;Secret Passphrase&#34;);
console.log(CryptoES.enc.Utf8.stringify(decrypted));
```

### GCM mode for AES encryption

The Crypto-ES library supports GCM mode for AES encryption. The following example shows how to encrypt and decrypt text using AES GCM mode:

```js
// import as part of crypto-es lib
import CryptoES from &#34;crypto-es&#34;;
// import as named export to safe computing resources (doesn&#39;t work if whole library is imported as above)
import { GCM } from &#34;crypto-es/lib/mode-gcm.js&#34;;

// Encrypt
const msg = &#34;Original Message&#34;;
const key = CryptoES.enc.Hex.parse(&#34;0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777&#34;);
const iv = CryptoES.enc.Hex.parse(&#34;0102030405060708090A0B0C&#34;);
const authData = CryptoES.enc.Utf8.parse(&#34;Additional authentication data&#34;);
const encrypted = CryptoES.AES.encrypt(msg, key, { iv, mode: CryptoES.mode.GCM });
const authTag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, encrypted.iv,  authData, encrypted.ciphertext, 16);
const enveloped = encrypted.iv.toString() &#43; encrypted.ciphertext.toString() &#43; authTag.toString();
console.log(&#34;encrypted: &#34;, encrypted);
console.log(&#34;authTag: &#34;, authTag);
console.log(&#34;enveloped: &#34;, enveloped);

// Decrypt
const decrypted = CryptoES.AES.decrypt(encrypted, key, { iv, mode: CryptoES.mode.GCM });
console.log(&#34;decrypted: &#34;, decrypted.toString(CryptoES.enc.Utf8));
```

### SHA3 algorithm

The crypto-ES library provides the original SHA3 algorithm. The following example shows how to use the SHA3 algorithm:

```js
import { SHA3 } from &#34;crypto-es/lib/sha3-original.js&#34;;

const hash = SHA3(&#34;Original Message&#34;, { outputLength: 256 });
console.log(&#34;hash: &#34;, hash);
```

### CRC32 algorithm

The crypto-ES library provides the CRC32 algorithm. Each CRC32 function takes an argument representing data and an optional second argument representing the starting seed (for rolling CRC). The return value is a signed 32-bit integer. The supported functions are as follows:

* `CRC32.buf(byte array[, seed])` &amp;ndash; The first argument is a sequence of 8-bit unsigned integers (`Uint8Array` or array of bytes).
* `CRC32.bstr(binary string[, seed])` &amp;ndash; The first argument is a binary string where byte `i` is the low byte of the UCS-2 char: `str.charCodeAt(i) &amp; 0xFF`
* `CRC32.str(string[, seed])` &amp;ndash; The first argument is a standard JS string and calculates the hash of the UTF-8 encoding.

The following example shows how to use the CRC32 algorithm:

```js
import CRC32 from &#34;crypto-es/lib/crc32.js&#34;;

const hash = CRC32.str(&#34;Original Message&#34;);
console.log(&#34;hex value: &#34;, (hash &gt;&gt;&gt; 0).toString(16));
```

## TweetNaCl.js

TweetNaCl is a crypto library that implements secret-key authenticated encryption, public-key authenticated encryption, and hashing and public-key signatures. The TweetNaCl library is available only for event and visitor functions.

Import the TweetNaCl.js module into your event or visitor function as follows:

`import nacl from &#39;tweetnacl&#39;;`

For more information, see [NPM TweetNaCl.js](https://www.npmjs.com/package/tweetnacl).

## JavaScript console API

Use the JavaScript console functions to write messages and errors to the log.

`console.log()` , `console.info(),` and `console.debug()` log messages go to the info output stream. `console.warn()` and `console.error()` log messages go to the error output stream.

The info and error output streams are each limited to 10 Kb of data per function invocation. If log messages exceed this limit, the log file will contain the first 10 Kb of data and end with the following message:&lt;br&gt;
`Output was too large and has been truncated.`

The console object provides other methods that are supported by functions. For more information, refer to any JavaScript [specification](https://developer.mozilla.org/en-US/docs/Web/API/Console &#34;https://developer.mozilla.org/en-US/docs/Web/API/Console&#34;) for the console object. The following additional console methods are supported:

* `assert()`
* `count()`
* `countReset()`
* `group()`
* `groupEnd()`
* `time()`
* `timeEnd()`
* `timeLog()`

### Console API output

The output from most console functions is shown in the **Messages** section of the **Logs** display. For example:

```
Messages:

Function Start
```

Output from `console.warn()` and `console.error()` is shown in the **Errors** section, below the **Messages** output, as follows:

```
Errors:

Warning - page not found
Error - variable not defined
```

### console.assert()

If a function is triggered on EventStream and `console.assert()` is called as follows:

```
console.assert(visitor, &#34;visitor not defined&#34;);
```

The `visitor` object is only defined when the trigger is AudienceStream, so the assertion is false and the output is as follows:

```
Assertion failed: visitor not defined
```

### console.group() and console.groupEnd()

`console.group()` and `console.groupEnd() ` can be used to format related messages in the log. `console.log()` messages that follow `console.group()` are indented in the log. The indentation ends after `console.groupEnd()` is called.

If the function code contains the following:

```js
console.group(&#34;Event info:&#34;);
console.log(&#34;Account: &#34;, event.account);
console.log(&#34;Visitor ID: &#34;, event.visitor_id);
console.groupEnd();
```

The output is as follows:

```
Event info:
  Account:  Acme Mfg
  Visitor ID:  017407a1d9e50019633c3cea732703079011607100bd6
```

### console.time() and console.timeLog()

When a function calls `console.time()`, there is no output. The time that `console.time()` was called with that string is noted. When `console.timeLog()` is called with the same string, `&#34;Current Time: &#34;` in this example, the output is the specified string followed by the time elapsed since `console.time()` was called:

```
Current Time: : 1ms
```

After a function calls `console.timeEnd()`, `console.timeLog()` cannot be called until `console.time()` is called again.

### console.count() and console.countReset()

Each time `console.count()` is called with the same string, the count is incremented. The output of `console.count()` is the string followed by the count. If `console.count(&#34;Current count: &#34;); ` is called twice, the output is as follows:

```
Current count: : 1
Current count: : 2
```

`console.countReset()` resets the count for the specified string to zero.