---
title: 関数向けの API とライブラリ
description: この記事では、関数で利用できる API とライブラリについて説明します。
url: https://docs.tealium.com/ja/server-side/functions/modules/
---
関数では、次の API とライブラリを使用できます。

* Crypto
* Crypto-ES.js
* TweetNaCl.js
* JavaScript Console API

## Crypto

この機能では、Java で実装された、Tealium Functions 向けの高性能な暗号化およびハッシュライブラリが導入されています。既存の JavaScript ベースの Crypto-ES ライブラリを直接置き換えることができ、同じインターフェイスを提供します。

詳しくは、[NPM: Crypto-ES](https://www.npmjs.com/package/crypto-es/v/1.2.7)を参照してください。

### ライブラリのインポート

Tealium 暗号化ライブラリをインポートするには、コードに次の行を追加します。

```js
import C from "tealium/crypto";
```

### モジュールのインポート

Tealium Crypto ライブラリは複数のモジュールで構成されており、各モジュールは特定の暗号化機能を備えた個別のクラスを提供します。必要なモジュールだけをインポートできるため、関数のパフォーマンスを最適化できます。

利用可能なモジュールは次のとおりです。

```js
import { SHA384Algo } from 'tealium/crypto/lib/sha384.js';
import { SHA512Algo } from 'tealium/crypto/lib/sha512.js';
import { SHA3Algo } from 'tealium/crypto/lib/sha3.js';
import { RIPEMD160Algo } from 'tealium/crypto/lib/ripemd160.js';
import { PBKDF2Algo } from 'tealium/crypto/lib/pbkdf2.js';
import { EvpKDFAlgo } from 'tealium/crypto/lib/evpkdf.js';
import { AESAlgo } from 'tealium/crypto/lib/aes.js';
import { DESAlgo } from 'tealium/crypto/lib/tripledes.js';
import { TripleDESAlgo } from 'tealium/crypto/lib/tripledes.js';
import { RabbitAlgo } from 'tealium/crypto/lib/rabbit.js';
import { RabbitLegacyAlgo } from 'tealium/crypto/lib/rabbit-legacy.js';
import { RC4Algo } from 'tealium/crypto/lib/rc4.js';
import { RC4DropAlgo } from 'tealium/crypto/lib/rc4.js';
import { CBC } from 'tealium/crypto/lib/mode-cbc.js';
import { CFB } from 'tealium/crypto/lib/mode-cfb.js';
import { CTR } from 'tealium/crypto/lib/mode-ctr.js';
import { ECB } from 'tealium/crypto/lib/mode-ecb.js';
import { OFB } from 'tealium/crypto/lib/mode-ofb.js';
import { GCM } from 'tealium/crypto/lib/mode-gcm.js';
import { AnsiX923 } from 'tealium/crypto/lib/pad-ansix923.js';
import { Iso10126 } from 'tealium/crypto/lib/pad-iso10126.js';
import { Iso97971 } from 'tealium/crypto/lib/pad-iso97971.js';
import { NoPadding } from 'tealium/crypto/lib/pad-nopadding.js';
import { ZeroPadding } from 'tealium/crypto/lib/pad-zeropadding.js';
import { Pkcs7 } from 'tealium/crypto/lib/pad-pkcs7.js';
import { OpenSSLFormatter } from "tealium/crypto/lib/cipher/OpenSSLFormatter.js";
import { HexFormatter } from 'tealium/crypto/lib/format-hex.js';
import { OpenSSLKdf } from "tealium/crypto/lib/cipher/OpenSSLKdf.js";
import { MD5 } from 'tealium/crypto/lib/md5.js';
import { HmacMD5 } from 'tealium/crypto/lib/md5.js';
import { SHA1 } from 'tealium/crypto/lib/sha1.js';
import { HmacSHA1 } from 'tealium/crypto/lib/sha1.js';
import { SHA224 } from 'tealium/crypto/lib/sha224.js';
import { HmacSHA224 } from 'tealium/crypto/lib/sha224.js';
import { SHA256 } from 'tealium/crypto/lib/sha256.js';
import { HmacSHA256 } from 'tealium/crypto/lib/sha256.js';
import { SHA384 } from 'tealium/crypto/lib/sha384.js';
import { HmacSHA384 } from 'tealium/crypto/lib/sha384.js';
import { SHA512 } from 'tealium/crypto/lib/sha512.js';
import { HmacSHA512 } from 'tealium/crypto/lib/sha512.js';
import { SHA3 } from 'tealium/crypto/lib/sha3.js';
import { HmacSHA3 } from 'tealium/crypto/lib/sha3.js';
import { RIPEMD160 } from 'tealium/crypto/lib/ripemd160.js';
import { HmacRIPEMD160 } from 'tealium/crypto/lib/ripemd160.js';
import { PBKDF2 } from 'tealium/crypto/lib/pbkdf2.js';
import { EvpKDF } from 'tealium/crypto/lib/evpkdf.js';
import { AES } from 'tealium/crypto/lib/aes.js';
import { DES } from 'tealium/crypto/lib/tripledes.js';
import { TripleDES } from 'tealium/crypto/lib/tripledes.js';
import { Rabbit } from 'tealium/crypto/lib/rabbit.js';
import { RabbitLegacy } from 'tealium/crypto/lib/rabbit-legacy.js';
import { RC4 } from 'tealium/crypto/lib/rc4.js';
import { RC4Drop } from 'tealium/crypto/lib/rc4.js';
import { CRC32 } from 'tealium/crypto/lib/crc32.js';
```

### 例

#### ハッシュとモード

CTRGladman モードの代わりに Galois/Counter モードが提供されます。AES 暗号では `C.mode.GCM` を使用します。

```js
import C from "tealium/crypto";
const msg = "message";
const key = C.enc.Hex.parse(
"0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding });
const decrypted = C.AES.decrypt(encrypted, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding });
```

追加認証データとタグの長さをパラメータとして渡すことができます。

```js
import C from "tealium/crypto";
const msg = "message";
const key = C.enc.Hex.parse(
"0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const aad = C.enc.Utf8.parse("additional authentication data");
const tagLength = 128; // bits
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
const decrypted = C.AES.decrypt(encrypted, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
```

`GCM.mac` メソッドは提供されませんが、暗号化された出力には、ハッシュと連結されたタグも含まれます。

```js
import C from "tealium/crypto";
const msg = "message";
const key = C.enc.Hex.parse(
"0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const tagLength = 128; // bits
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, tagLength });
const sEncrypted = encrypted.ciphertext.toString();
const tag = sEncrypted.slice(sEncrypted.length - tagLength / 8 * 2, sEncrypted.length);
const hash = sEncrypted.slice(0, sEncrypted.length - tag.length);
```

メッセージを復号するには、ハッシュとタグを連結する必要があります。

```js
import C from "tealium/crypto";
import CryptoES from "crypto-es";
const msg = "message";
const key = C.enc.Hex.parse("0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const aad = C.enc.Utf8.parse("additional authentication data");
const tagLength = 120;
// encrypt with third-party
const encrypted = CryptoES.AES.encrypt(msg, key, { iv, mode: CryptoES.mode.GCM, padding: CryptoES.pad.NoPadding });
const tag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, encrypted.iv, aad, encrypted.ciphertext, tagLength / 8);
// decrypt with tealium/crypto
const decrypted = C.AES.decrypt(C.lib.CipherParams.create({ ciphertext: C.enc.Hex.parse(encrypted.ciphertext.toString() + tag) }), key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
```
#### CRC32

CRC32 は `crypto-es` の拡張として追加されており、`index.js` または名前付きインポートから利用できます。

```js
import C from "tealium/crypto"; // C.CRC32
import { CRC32 } from "tealium/crypto/lib/crc32.js";
```

どちらの場合も、関数はデータを表す引数を受け取ります。

* `CRC32.buf(byte array)`: 8 ビット符号なし整数のシーケンス（Uint8Array またはバイト配列）を受け取ります。
* `CRC32.bstr(binary string)`: バイト i が UCS-2 文字の下位バイトであるバイナリ文字列を受け取ります：`str.charCodeAt(i) & 0xFF`
* `CRC32.str(string)`: 標準の JavaScript 文字列を受け取り、その UTF-8 エンコーディングのハッシュを計算します。
* `CRC32.reset()`: インスタンスは状態を保持するため、ハッシュ計算後に手動でリセットする必要があります。
* `CRC32.valueOf()`: 状態を表す 32 ビット符号付き整数を返します。

使用方法：

```js
import { CRC32 } from "tealium/crypto/lib/crc32.js";
// single iteration
const hash1 = CRC32.str("input").valueOf();
CRC32.reset();
// multiple
const hash2 = CRC32
    .buf([11, 111, 88])
    .str("try")
    .bstr("more")
    .valueOf();
CRC32.reset();
// convert to unsigned
const uHash1 = hash1 >>> 0;
// convert to hex
const hHash1 = (hash1 >>> 0).toString(16);
```

### エラーメッセージ

Tealium 暗号化ライブラリは、入力データに関して `crypto-es` より厳密であるため、不正な使用方法の場合には次のエラーが発生する可能性があります。

| エラー | 説明 |
|-------|-------------|
| `Invalid AES key length`| AES 暗号のキーサイズは 32 バイトである必要があります。 |
| `Wrong key size`| DES 暗号のキーサイズは 8 バイト、TripleDES のキーサイズは 16 バイトである必要があります。 |
| `Wrong IV length`| 一部の暗号およびモード（DES、TripleDES、OFB）では IV サイズが厳密に定められているため、正しく指定する必要があります。 |
| `Input length not multiple of 16 bytes`| `NoPadding` パディングが使用されているため、入力を正しくパディングする必要があります。 |
| `Parameters missing`| 構成オブジェクトが無効です。たとえば、IV が必須のモード（OFB、CFB）で `iv` パラメータが指定されていません。 |
| `No IV set when one expected`| BouncyCastle で実装された、IV が必須のモード（CTR）の構成オブジェクトに `iv` パラメータがありません。 |

### Crypto-ES から Tealium 暗号化ライブラリへの移行

`tealium/crypto` ライブラリは `crypto-es` と同じインターフェイスを提供しており、直接置き換えて使用できます。移行時に本番環境で予期しない動作が発生するリスクを最小限に抑えるため、次のいずれかの方法で移行をテストしてください。

* **サンドボックス環境で `tealium/crypto` ライブラリを使用する（推奨）**  
サンドボックス環境で関数を複製し、インポートを更新して `tealium/crypto` を使用します。呼び出し対象をテスト用のオーディエンスまたはフィードに限定し、ライブトラフィックに影響を与えずに関数が期待どおりに動作することを確認します。

* **既存の関数と並行して `tealium/crypto` バージョンを実行する**  
関数のコピーを作成し、インポートを更新して `tealium/crypto` を使用します。実環境の条件下で直接比較するために、トラフィックの一部をこの関数にルーティングします。この方法では、出力とパフォーマンスを 1 対 1 で検証できますが、リソース使用量とコストが増加する可能性があります。不要なシステム負荷を避けるため、テスト後は複製した関数を無効にしてください。

テスト用ペイロードを使用する **Test** タブは、本番環境の負荷をシミュレートできず、信頼できるパフォーマンス情報も得られないため、使用しないでください。

検証後、完全に移行し、`crypto-es` を使用している以前のバージョンを無効化または削除できます。

## Crypto-ES.js（レガシー）


<blockquote>
これは暗号化ライブラリのレガシーバージョンです。新しいユースケースには、同じインターフェイスに加えてパフォーマンスの向上とモジュール単位のインポートを提供する [Tealium 暗号化ライブラリ](#crypto)を参照してください。
</blockquote>


Crypto-ES.js は、ハッシュ、エンコーディング、および暗号化アルゴリズムを提供する暗号化アルゴリズムライブラリです。詳細については、[NPM: Crypto-ES](https://www.npmjs.com/package/crypto-es/v/1.2.7)を参照してください。

次の例は、テキストを暗号化および復号する方法を示しています。

```js
import CryptoES from 'crypto-es';

var encrypted = CryptoES.AES.encrypt("Message", "Secret Passphrase");
console.log(encrypted);
var decrypted = CryptoES.AES.decrypt(encrypted, "Secret Passphrase");
console.log(CryptoES.enc.Utf8.stringify(decrypted));
```

### AES 暗号化の GCM モード

Crypto-ES ライブラリは、AES 暗号化の GCM モードをサポートしています。次の例は、AES GCM モードを使用してテキストを暗号化および復号する方法を示しています。

```js
// import as part of crypto-es lib
import CryptoES from "crypto-es";
// import as named export to safe computing resources (doesn't work if whole library is imported as above)
import { GCM } from "crypto-es/lib/mode-gcm.js";

// Encrypt
const msg = "Original Message";
const key = CryptoES.enc.Hex.parse("0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = CryptoES.enc.Hex.parse("0102030405060708090A0B0C");
const authData = CryptoES.enc.Utf8.parse("Additional authentication data");
const encrypted = CryptoES.AES.encrypt(msg, key, { iv, mode: CryptoES.mode.GCM });
const authTag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, encrypted.iv,  authData, encrypted.ciphertext, 16);
const enveloped = encrypted.iv.toString() + encrypted.ciphertext.toString() + authTag.toString();
console.log("encrypted: ", encrypted);
console.log("authTag: ", authTag);
console.log("enveloped: ", enveloped);

// Decrypt
const decrypted = CryptoES.AES.decrypt(encrypted, key, { iv, mode: CryptoES.mode.GCM });
console.log("decrypted: ", decrypted.toString(CryptoES.enc.Utf8));
```

### SHA3 アルゴリズム

Crypto-ES ライブラリは、オリジナルの SHA3 アルゴリズムを提供します。次の例は、SHA3 アルゴリズムの使用方法を示しています。

```js
import { SHA3 } from "crypto-es/lib/sha3-original.js";

const hash = SHA3("Original Message", { outputLength: 256 });
console.log("hash: ", hash);
```

### CRC32 アルゴリズム

Crypto-ES ライブラリは、CRC32 アルゴリズムを提供します。各 CRC32 関数は、データを表す引数と、開始シード（ローリング CRC 用）を表す省略可能な第 2 引数を受け取ります。戻り値は 32 ビット符号付き整数です。サポートされている関数は次のとおりです。

* `CRC32.buf(byte array[, seed])` &ndash; 第 1 引数は、8 ビット符号なし整数のシーケンス（`Uint8Array` またはバイト配列）です。
* `CRC32.bstr(binary string[, seed])` &ndash; 第 1 引数は、バイト `i` が UCS-2 文字の下位バイトであるバイナリ文字列です：`str.charCodeAt(i) & 0xFF`
* `CRC32.str(string[, seed])` &ndash; 第 1 引数は標準の JS 文字列で、その UTF-8 エンコーディングのハッシュを計算します。

次の例は、CRC32 アルゴリズムの使用方法を示しています。

```js
import CRC32 from "crypto-es/lib/crc32.js";

const hash = CRC32.str("Original Message");
console.log("hex value: ", (hash >>> 0).toString(16));
```

## TweetNaCl.js

TweetNaCl は、秘密鍵による認証付き暗号化、公開鍵による認証付き暗号化、ハッシュ、および公開鍵署名を実装する暗号化ライブラリです。TweetNaCl ライブラリは、イベント関数と訪問関数でのみ使用できます。

次のように、TweetNaCl.js モジュールをイベント関数または訪問関数にインポートします。

`import nacl from 'tweetnacl';`

詳細については、[NPM TweetNaCl.js](https://www.npmjs.com/package/tweetnacl)を参照してください。

## JavaScript コンソール API

JavaScript コンソール関数を使用して、メッセージとエラーをログに書き込みます。

`console.log()`、`console.info(),`、および `console.debug()` のログメッセージは、情報出力ストリームに送られます。`console.warn()` および `console.error()` のログメッセージは、エラー出力ストリームに送られます。


<blockquote>
情報出力ストリームとエラー出力ストリームは、それぞれ関数呼び出しごとに 10 KB のデータに制限されています。ログメッセージがこの上限を超える場合、ログファイルには最初の 10 KB のデータが記録され、末尾に次のメッセージが表示されます：<br>
`Output was too large and has been truncated.`
</blockquote>


コンソールオブジェクトには、関数でサポートされるその他のメソッドも用意されています。詳細については、コンソールオブジェクトに関する JavaScript の[仕様](https://developer.mozilla.org/en-US/docs/Web/API/Console "https://developer.mozilla.org/en-US/docs/Web/API/Console")を参照してください。次の追加コンソールメソッドがサポートされています。

* `assert()`
* `count()`
* `countReset()`
* `group()`
* `groupEnd()`
* `time()`
* `timeEnd()`
* `timeLog()`
### Console API の出力

ほとんどのコンソール関数からの出力は、**Logs** 表示の **Messages** セクションに表示されます。例：

```
Messages:

Function Start
```

`console.warn()` および `console.error()` からの出力は、次のように **Messages** の出力の下にある **Errors** セクションに表示されます。

```
Errors:

Warning - page not found
Error - variable not defined
```

### console.assert()

Event Streaming で関数がトリガーされ、次のように `console.assert()` が呼び出された場合：

```
console.assert(visitor, "visitor not defined");
```

`visitor` オブジェクトは、トリガーが Customer Data Platform（CDP）の場合にのみ定義されるため、アサーションは失敗し、出力は次のようになります。

```
Assertion failed: visitor not defined
```

### console.group() と console.groupEnd()

`console.group()` と `console.groupEnd() ` を使用すると、ログ内の関連するメッセージを書式構成できます。`console.group()` の後に続く `console.log()` メッセージは、ログ内でインデントされます。`console.groupEnd()` が呼び出されると、インデントは終了します。

関数コードに次の内容が含まれている場合：

```js
console.group("Event info:");
console.log("Account: ", event.account);
console.log("Visitor ID: ", event.visitor_id);
console.groupEnd();
```

出力は次のようになります。

```
Event info:
  Account:  Acme Mfg
  Visitor ID:  017407a1d9e50019633c3cea732703079011607100bd6
```

### console.time() と console.timeLog()

関数が `console.time()` を呼び出しても、出力はありません。その文字列を指定して `console.time()` が呼び出された時刻が記録されます。同じ文字列（この例では `"Current Time: "`）を指定して `console.timeLog()` が呼び出されると、指定した文字列に続いて、`console.time()` が呼び出されてからの経過時間が出力されます。

```
Current Time: : 1ms
```

関数が `console.timeEnd()` を呼び出した後は、`console.time()` が再度呼び出されるまで `console.timeLog()` を呼び出すことはできません。

### console.count() と console.countReset()

同じ文字列を指定して `console.count()` が呼び出されるたびに、カウントが増加します。`console.count()` の出力は、文字列の後にカウントが続きます。`console.count("Current count: "); ` が2回呼び出された場合、出力は次のようになります。

```
Current count: : 1
Current count: : 2
```

`console.countReset()` は、指定した文字列のカウントをゼロにリセットします。