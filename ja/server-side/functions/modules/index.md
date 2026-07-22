---
title: 関数用のAPIとライブラリ
description: この記事では、関数用のAPIとライブラリについての情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/modules/
---
関数では、以下のAPIとライブラリを使用できます：

* Crypto
* Crypto-ES.js
* TweetNaCl.js
* JavaScript Console API

## Crypto

この機能は、Tealium Functions用の高性能な暗号化およびハッシュライブラリをJavaで実装しています。既存のJavaScriptベースのCrypto-ESライブラリの直接的な代替品として提供され、同じインターフェースを提供します。

詳細については、[NPM: Crypto-ES](https://www.npmjs.com/package/crypto-es/v/1.2.7)を参照してください。

### ライブラリのインポート

Tealiumの暗号ライブラリをインポートするには、コードに次の行を追加します：

```js
import C from "tealium/crypto";
```

### モジュールのインポート

Tealium Cryptoライブラリは、特定の暗号機能を提供する個別のクラスを持つモジュールに組織されています。必要なモジュールのみをインポートすることで、関数のパフォーマンスを最適化できます。

利用可能なモジュールのリスト：

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

#### ハッシュ化とモード

Galois/CounterモードはCTRGladmanモードの代わりに提供されます。AES暗号で`C.mode.GCM`を使用します：

```js
import C from "tealium/crypto";
const msg = "message";
const key = C.enc.Hex.parse(
"0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding });
const decrypted = C.AES.decrypt(encrypted, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding });
```

追加認証データとタグ長はパラメータとして渡すことができます：

```js
import C from "tealium/crypto";
const msg = "message";
const key = C.enc.Hex.parse(
"0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const aad = C.enc.Utf8.parse("additional authentication data");
const tagLength = 128; // ビット
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
const decrypted = C.AES.decrypt(encrypted, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
```

`GCM.mac`メソッドは提供されていませんが、暗号化された出力にはハッシュと連結されたタグも含まれます：

```js
import C from "tealium/crypto";
const msg = "message";
const key = C.enc.Hex.parse(
"0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const tagLength = 128; // ビット
const encrypted = C.AES.encrypt(msg, key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, tagLength });
const sEncrypted = encrypted.ciphertext.toString();
const tag = sEncrypted.slice(sEncrypted.length - tagLength / 8 * 2, sEncrypted.length);
const hash = sEncrypted.slice(0, sEncrypted.length - tag.length);
```

メッセージを復号するには、ハッシュとタグを連結する必要があります：

```js
import C from "tealium/crypto";
import CryptoES from "crypto-es";
const msg = "message";
const key = C.enc.Hex.parse("0123456789ABCDEF11113333555577770123456789ABCDEF1111333355557777");
const iv = C.enc.Hex.parse("0102030405060708090A0B0C");
const aad = C.enc.Utf8.parse("additional authentication data");
const tagLength = 120;
// third-partyで暗号化
const encrypted = CryptoES.AES.encrypt(msg, key, { iv, mode: CryptoES.mode.GCM, padding: CryptoES.pad.NoPadding });
const tag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, encrypted.iv, aad, encrypted.ciphertext, tagLength / 8);
// tealium/cryptoで復号
const decrypted = C.AES.decrypt(C.lib.CipherParams.create({ ciphertext: C.enc.Hex.parse(encrypted.ciphertext.toString() + tag) }), key, { iv, mode: C.mode.GCM, padding: C.pad.NoPadding, aad, tagLength });
```
#### CRC32

CRC32は`crypto-es`の拡張機能として追加され、`index.js`または名前付きインポートで利用可能です：

```js
import C from "tealium/crypto"; // C.CRC32
import { CRC32 } from "tealium/crypto/lib/crc32.js";
```

どちらの場合も、関数はデータを表す引数を取ります：

* `CRC32.buf(byte array)`: 8ビット符号なし整数のシーケンス（Uint8Arrayまたはバイトの配列）を期待します。
* `CRC32.bstr(binary string)`: バイナリ文字列を期待し、バイトiはUCS-2文字の下位バイトです：`str.charCodeAt(i) & 0xFF`
* `CRC32.str(string)`: 標準的なJavaScript文字列を期待し、UTF-8エンコーディングのハッシュを計算します。
* `CRC32.reset()`: インスタンスは状態を持っており、ハッシュ計算後に手動でリセットが必要です。
* `CRC32.valueOf()`: 状態の32ビット符号付き整数表現を返します。

使用法：

```js
import { CRC32 } from "tealium/crypto/lib/crc32.js";
// 単一の反復
const hash1 = CRC32.str("input").valueOf();
CRC32.reset();
// 複数
const hash2 = CRC32
    .buf([11, 111, 88])
    .str("try")
    .bstr("more")
    .valueOf();
CRC32.reset();
// 符号なしに変換
const uHash1 = hash1 >>> 0;
// 16進数に変換
const hHash1 = (hash1 >>> 0).toString(16);
```

### エラーメッセージ

Tealiumの暗号ライブラリは`crypto-es`よりも入力データに対して厳格なため、無効な使用の場合に以下のエラーが発生する可能性があります：

| エラー | 説明 |
|-------|-------------|
| `Invalid AES key length`| AES暗号のキーサイズは32バイトでなければなりません。 |
| `Wrong key size`| DES暗号のキーサイズは8バイト、TripleDESの場合は16バイトでなければなりません。 |
| `Wrong IV length`| 一部の暗号とモードではIVサイズが厳格です（DES、TripleDES、OFB）正しく指定する必要があります。 |
| `Input length not multiple of 16 bytes`| `NoPadding`パッドが使用され、入力は正しくパディングされている必要があります。 |
| `Parameters missing`| その構成オブジェクトは有効ではありません。たとえば、必須IVモード（OFB、CFB）の`iv`パラメータが欠けています。 |
| `No IV set when one expected`| BouncyCastleで実装されたモードで必須のIV（CTR）の構成オブジェクトに`iv`パラメータが欠けています。 |

### Crypto-ESからTealium暗号ライブラリへの移行

`tealium/crypto`ライブラリは`crypto-es`と同じインターフェースを提供し、直接の置き換えとして使用できます。本番環境で予期しない動作のリスクを最小限に抑えるために、以下のアプローチのいずれかを使用して移行をテストしてください：

* **`tealium/crypto`ライブラリを使用したサンドボックス環境（推奨）**  
サンドボックス環境で関数を複製し、インポートを`tealium/crypto`を使用するように更新します。テストオーディエンスまたはフィードに限定して呼び出しを行い、ライブトラフィックに影響を与えることなく関数が期待通りに動作することを確認します。

* **既存の関数と並行して`tealium/crypto`バージョンを実行する**  
関数のコピーを作成し、インポートを`tealium/crypto`を使用するように更新します。トラフィックの一部をそれにルーティングして、実際の条件下での直接比較を行います。このアプローチは1対1の出力とパフォーマンスの検証を可能にしますが、リソース使用とコストが増加する可能性があります。テスト後は不要なシステム負荷を避けるために重複をオフにします。

テストペイロードを使用した**テスト**タブは、本番負荷をシミュレートせず、信頼性のあるパフォーマンスの洞察を提供しないため、使用を避けてください。

検証後、完全に移行し、`crypto-es`の以前のバージョンをオフにするか削除してください。
### コンソールAPIの出力

ほとんどのコンソール関数の出力は、**ログ**表示の**メッセージ**セクションに表示されます。例えば：

```
メッセージ：

関数開始
```

`console.warn()` と `console.error()` の出力は、以下のように **メッセージ** 出力の下にある **エラー** セクションに表示されます：

```
エラー：

警告 - ページが見つかりません
エラー - 変数が定義されていません
```

### console.assert()

EventStreamで関数がトリガーされ、次のように `console.assert()` が呼び出された場合：

```
console.assert(visitor, "visitor not defined");
```

`visitor` オブジェクトはトリガーがAudienceStreamの場合にのみ定義されるため、アサーションは偽となり、出力は次のようになります：

```
Assertion failed: visitor not defined
```

### console.group() と console.groupEnd()

`console.group()` と `console.groupEnd()` は、ログの関連メッセージを整形するために使用できます。`console.group()` の後に続く `console.log()` メッセージはログでインデントされます。インデントは `console.groupEnd()` が呼び出された後に終了します。

関数コードに次のようなものが含まれている場合：

```js
console.group("Event info:");
console.log("Account: ", event.account);
console.log("Visitor ID: ", event.visitor_id);
console.groupEnd();
```

出力は次のようになります：

```
イベント情報：
  アカウント： Acme Mfg
  ビジターID： 017407a1d9e50019633c3cea732703079011607100bd6
```

### console.time() と console.timeLog()

関数が `console.time()` を呼び出すと、出力はありません。その文字列で `console.time()` が呼び出された時間が記録されます。同じ文字列で `console.timeLog()` が呼び出されると、指定された文字列に続いて `console.time()` が呼び出されてからの経過時間が出力されます：

```
現在の時間：：1ms
```

関数が `console.timeEnd()` を呼び出した後、`console.time()` が再び呼び出されるまで `console.timeLog()` を呼び出すことはできません。

### console.count() と console.countReset()

同じ文字列で `console.count()` が呼び出されるたびに、カウントが増加します。`console.count()` の出力は、文字列に続いてカウントです。`console.count("現在のカウント：");` が2回呼び出された場合、出力は次のようになります：

```
現在のカウント：：1
現在のカウント：：2
```

`console.countReset()` は、指定された文字列のカウントをゼロにリセットします。