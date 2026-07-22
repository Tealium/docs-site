---
title: EUIDを生成するための関数の使用
description: この記事では、訪問関数を使用してユーザーのEUIDを生成し、訪問プロファイルに保存する方法について説明します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/euid/
---
European Unified ID (EUID)は、[The Trade Desk](https://euid.eu/docs/intro)によって作成されたオープンソースのIDフレームワークで、サードパーティクッキーの代わりに使用できます。EUIDは、ユーザーの個人識別情報（PII）に基づいた決定論的なユーザー識別子です。現在、EUIDはユーザーのメールアドレスのみを識別子として使用し、ヨーロッパ地域に限定されています。識別子はハッシュ化および暗号化され、EUIDリクエストへの応答で返されるEUIDが作成されます。詳細については、[European Unified ID Overview](https://euid.eu/docs/intro)を参照してください。

EUIDは、[The Trade Desk connector](https://docs.tealium.com/the-trade-desk-first-party-data-connector/)およびその他のサポートされているアウトバウンドコネクタで使用できます。

## 訪問プロファイルのためのEUIDの生成

EUIDを生成するために訪問関数の使用を推奨します。訪問がPIIを持っているがEUIDが割り当てられていない場合に関数をトリガーします。訪問関数についての詳細は、[About event and visitor functions]()を参照してください。

訪問関数は以下を行います：

* 訪問のメールアドレスをキャプチャしてハッシュ化する。
* 訪問にEUIDが割り当てられていない場合、[EUID endpoint](https://euid.eu/docs/endpoints/post-identity-map)を使用してEUIDを生成する。
* EUIDと`tealium_visitor_id`を含むイベントをTealium Collectに送信する。

関数から送信されたイベントによって訪問属性が豊かになります。

### 前提条件

EUIDを生成する訪問関数を作成する前に、以下を行ってください：

* ユーザーの識別子として使用するPII訪問属性を選択します。EUIDは現在、メールアドレス識別子をサポートしています。
* EUIDを保存する訪問属性を作成します。この訪問属性をイベントEUID属性の値でエンリッチするためにエンリッチメントを追加します。詳細については、[Using Attributes]()および[About enrichments]()を参照してください。
* メールアドレスが割り当てられているがEUIDが割り当てられていない訪問を特定するオーディエンスを作成します。例えば：  
![](https://docs.tealium.com/images/server-side/euid-function-trigger-example.png)  
詳細については、[Create an audience](https://docs.tealium.com/manage-audiences/#create-an-audience)を参照してください。

## EUIDジェネレータ関数

関数を作成する際には、以下を行ってください：

1. トリガーには**Processed Visitor**を選択します。
1. **Audience**には、EUIDが割り当てられていない特定の訪問のために作成したオーディエンスを選択します。**Trigger On**はデフォルト値の`Joined Audience`に構成します。
処理済み訪問関数のデフォルトコードを削除し、[Example code](#example-code)に示されているEUIDを生成するための例コードをコピーして貼り付けます。必要に応じて例コードを変更してください。
### 例示コード


<blockquote>
この例示コードは訪問にEUIDを割り当てる関数を構成するためのガイドであり、**修正なしには使用できません**。コード内の`TODO`と記載されたコメントを探し、あなたの構成に必要な行を修正してください。
</blockquote>


この例では、ユーザー識別子としてメールアドレスを使用していますが、他のユーザー識別子に適応させることも可能です。属性IDを使用してメール属性の値を取得します。使用している属性の正しい値で属性IDを更新し、適切な場所（`api_key` と `secret`）にあなたのEUID認証情報を配置してください。

```js
import CryptoES from 'crypto-es'

activate(async ({ visitor, visit, helper }) => {  
  
  const genHash = (data) => {
    return CryptoES.SHA256(data).toString(CryptoES.enc.Base64)
    }
  const validateEmail = (email) => {
    return String(email)
      .toLowerCase()
      .match(
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      );
    };

  let tealium_config = {
      tealium_account: 'CURRENT',
      tealium_profile: 'CURRENT',
      tealium_datasource: 'DATA_SOURCE_KEY', // TODO: Change DATA_SOURCE_KEY to your Tealium Data Source key.
      email_hashed: false // TODO: If your email is already hashed, set this to true.
    };

  if(tealium_config.tealium_account == 'CURRENT') {
    tealium_config.tealium_account = visitor.properties.account
  }
  if(tealium_config.tealium_profile == 'CURRENT') {
    tealium_config.tealium_profile = visitor.properties.profile
  }
  const email = visitor.getAttributeValueById("ATTRIBUTE_ID") // TODO: Change ATTRIBUTE_ID to the attribute ID of the user identifier attribute
  let email_hash = '';

  console.log(email)
  const tealium_vid = visitor.properties.visitor_id

  if(!tealium_config.email_hashed) {
    if(!validateEmail(email)) {
       throw new Error(`Email Attribute is not a valid email`);
      return false
    }
    email_hash = genHash(email)
  } else {
    email_hash = email
  }
  console.log(email_hash)

  //Update the following variables with your TTD EUID credentials
  const api_key = 'api_key' // TODO: Change api_key to your assigned EUID API Key
  const secret = 'secret' // TODO: Change secret to your assigned EUID secret
  // const url = 'https://integ.euid.eu/v2/identity/map' // Testing Environment (separate credentials are used). Only use for TESTING
  const url = 'https://prod.euid.eu/v2/identity/map'  // Production Environment
  const key = CryptoES.enc.Base64.parse(secret)
  the hexRef = "0123456789abcdef"
  const randomBytes = (bytes) => {
    let buf = ''
    for (let i = 0; i < bytes * 2; i++)
      buf += hexRef.charAt(Math.floor(Math.random() * hexRef.length))
    return buf
  }

  const writeBigUint64BE = (num, bytes = 8) => {
    let buf = num.toString(16)
    let padding = ''
    for (let i = 0; i < bytes * 2 - buf.length; i++)
      padding += '0'
    return padding + buf
  }

  const encrypt = (data) => {
    const iv = randomBytes(12)
    const nonce = randomBytes(8)
    const millisec = Date.now()
    const timestamp = writeBigUint64BE(millisec)
    const payload = CryptoES.enc.Utf8.parse(JSON.stringify(data))
    const body = timestamp + nonce + payload 
    const ivBuf = CryptoES.enc.Hex.parse(iv)
    const encryptedBody = CryptoES.AES.encrypt(
      CryptoES.enc.Hex.parse(body),
      key,
      {
        iv: ivBuf,
        mode: CryptoES.mode.GCM,
        padding: CryptoES.pad.NoPadding
      }
    )
    the ciphertext = encryptedBody.ciphertext
    the authTag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, ivBuf, null, ciphertext).toString()
    the enveloped = '01' + iv + ciphertext.toString() + authTag

    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      enveloped: CryptoES.enc.Hex.parse(enveloped).toString(CryptoES.enc.Base64)
    }
  }

  const decrypt = (data) => {
    const buf = CryptoES.enc.Base64.parse(data).toString(CryptoES.enc.Hex)
    const iv = CryptoES.enc.Hex.parse(buf.substring(0, 24))
    const ciphertext = CryptoES.enc.Hex.parse(buf.substring(24, buf.length - 32))
    const tag = buf.substring(buf.length - 32)
    const encryptedBody = new CryptoES.lib.CipherParams({ ciphertext: ciphertext })
    const decrypted = CryptoES.AES.decrypt(encryptedBody,key, 
      {
        iv: iv, 
        mode: CryptoES.mode.GCM, 
        padding: CryptoES.pad.NoPadding
      }
    ).toString()

    const timestamp = decrypted.substring(0, 16)
    the nonce = decrypted.substring(16, 32)
    the developed = decrypted.substring(32)
  //const tagCheck = CryptoES.mode.GCM.mac(CryptoES.AES, key, iv, null, ciphertext).toString()
  //console.log('\nauthTag check:', tag == tagCheck)

    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      developed: JSON.parse(CryptoES.enc.Hex.parse(developed).toString(CryptoES.enc.Utf8))
    }
  }

  const payload = {
    email_hash: [genHash(email)]
    }
  const {timestamp, nonce, enveloped} = encrypt(payload)

  console.log('\n********** encypted **********')
  console.log('timestamp:', timestamp)
  console.log('nonce:', nonce)
  console.log('enveloped:', enveloped)

  const response = await fetch(url, {
    method: 'POST',
    body: enveloped,
    headers: {
      'Authorization': `Bearer ${api_key}`
    }
  })

  if (response.status == 200) {
    const body = await response.text()
    console.log('\n********** response **********')
    console.log(body)
    const data = decrypt(body)
    console.log('\n********** decrypted **********')
    console.log('timeStamp:', data.timestamp)
    console.log('nonce:', data.nonce)
    console.log('response:', JSON.stringify(data.developed))
    console.log('\n')

 let event_data ={
      tealium_event: "euid_event",
      tealium_visitor_id: tealium_vid,
      euid_hashed_email: data.developed.body.mapped[0].identifier,
      euid_bucket_id: data.developed.body.mapped[0].bucket_id,
      euid_raw: data.developed.body.mapped[0].advertising_id,
      euid_timestamp : JSON.stringify(data.timestamp),
      euid_nonce: JSON.stringify(data.nonce)
    };

  console.log(JSON.stringify(event_data))
    if(event_data.euid_raw) {
      track(event_data, tealium_config)
          .then(response => {
              if (!response.ok) {
                  throw new Error(`Network response was not ok. Status code: ${response.status}.`);
              }
              console.log('Status code:', response.status);
              return response.text();
          })
          .catch(error => console.error('Error:', error.message));
    } 
    else {
      console.error("Couldn't generate advertising ID")
      }
  } 
  else {
    console.log('\nxxxxx  failed  xxxxx\n')
    console.log(JSON.stringify(response))
    }
  })
```