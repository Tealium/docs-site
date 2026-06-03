---
title: EUIDを生成するための関数の使用
description: この記事では、訪問関数を使用してユーザーのEUIDを生成し、訪問プロファイルに保存する方法について説明します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/euid/
---
European Unified ID (EUID)は、[The Trade Desk](https://euid.eu/docs/intro)によって作成されたオープンソースのIDフレームワークで、サードパーティクッキーの代わりに使用できます。EUIDは、ユーザーの個人識別情報（PII）に基づいた決定論的なユーザー識別子です。現在、EUIDはユーザーのメールアドレスのみを識別子として使用し、ヨーロッパ地域に限定されています。識別子はハッシュ化および暗号化され、EUIDリクエストへの応答で返されるEUIDが作成されます。詳細については、[European Unified ID Overview](https://euid.eu/docs/intro)を参照してください。

EUIDは、[The Trade Desk connector]()およびその他のサポートされているアウトバウンドコネクタで使用できます。

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
![](/images/server-side/euid-function-trigger-example.png)  
詳細については、[Create an audience]()を参照してください。

## EUIDジェネレータ関数

関数を作成する際には、以下を行ってください：

1. トリガーには**Processed Visitor**を選択します。
1. **Audience**には、EUIDが割り当てられていない特定の訪問のために作成したオーディエンスを選択します。**Trigger On**はデフォルト値の`Joined Audience`に構成します。
処理済み訪問関数のデフォルトコードを削除し、[Example code](#example-code)に示されているEUIDを生成するための例コードをコピーして貼り付けます。必要に応じて例コードを変更してください。
### 例示コード

この例示コードは訪問にEUIDを割り当てる関数を構成するためのガイドであり、**修正なしには使用できません**。コード内の`TODO`と記載されたコメントを探し、あなたの構成に必要な行を修正してください。

この例では、ユーザー識別子としてメールアドレスを使用していますが、他のユーザー識別子に適応させることも可能です。属性IDを使用してメール属性の値を取得します。使用している属性の正しい値で属性IDを更新し、適切な場所（`api_key` と `secret`）にあなたのEUID認証情報を配置してください。

```js
import CryptoES from &#39;crypto-es&#39;

activate(async ({ visitor, visit, helper }) =&gt; {  
  
  const genHash = (data) =&gt; {
    return CryptoES.SHA256(data).toString(CryptoES.enc.Base64)
    }
  const validateEmail = (email) =&gt; {
    return String(email)
      .toLowerCase()
      .match(
        /^(([^&lt;&gt;()[\]\\.,;:\s@&#34;]&#43;(\.[^&lt;&gt;()[\]\\.,;:\s@&#34;]&#43;)*)|.(&#34;.&#43;&#34;))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]&#43;\.)&#43;[a-zA-Z]{2,}))$/
      );
    };

  let tealium_config = {
      tealium_account: &#39;CURRENT&#39;,
      tealium_profile: &#39;CURRENT&#39;,
      tealium_datasource: &#39;DATA_SOURCE_KEY&#39;, // TODO: Change DATA_SOURCE_KEY to your Tealium Data Source key.
      email_hashed: false // TODO: If your email is already hashed, set this to true.
    };

  if(tealium_config.tealium_account == &#39;CURRENT&#39;) {
    tealium_config.tealium_account = visitor.properties.account
  }
  if(tealium_config.tealium_profile == &#39;CURRENT&#39;) {
    tealium_config.tealium_profile = visitor.properties.profile
  }
  const email = visitor.getAttributeValueById(&#34;ATTRIBUTE_ID&#34;) // TODO: Change ATTRIBUTE_ID to the attribute ID of the user identifier attribute
  let email_hash = &#39;&#39;;

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
  const api_key = &#39;api_key&#39; // TODO: Change api_key to your assigned EUID API Key
  const secret = &#39;secret&#39; // TODO: Change secret to your assigned EUID secret
  // const url = &#39;https://integ.euid.eu/v2/identity/map&#39; // Testing Environment (separate credentials are used). Only use for TESTING
  const url = &#39;https://prod.euid.eu/v2/identity/map&#39;  // Production Environment
  const key = CryptoES.enc.Base64.parse(secret)
  the hexRef = &#34;0123456789abcdef&#34;
  const randomBytes = (bytes) =&gt; {
    let buf = &#39;&#39;
    for (let i = 0; i &lt; bytes * 2; i&#43;&#43;)
      buf &#43;= hexRef.charAt(Math.floor(Math.random() * hexRef.length))
    return buf
  }

  const writeBigUint64BE = (num, bytes = 8) =&gt; {
    let buf = num.toString(16)
    let padding = &#39;&#39;
    for (let i = 0; i &lt; bytes * 2 - buf.length; i&#43;&#43;)
      padding &#43;= &#39;0&#39;
    return padding &#43; buf
  }

  const encrypt = (data) =&gt; {
    const iv = randomBytes(12)
    const nonce = randomBytes(8)
    const millisec = Date.now()
    const timestamp = writeBigUint64BE(millisec)
    const payload = CryptoES.enc.Utf8.parse(JSON.stringify(data))
    const body = timestamp &#43; nonce &#43; payload 
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
    the enveloped = &#39;01&#39; &#43; iv &#43; ciphertext.toString() &#43; authTag

    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      enveloped: CryptoES.enc.Hex.parse(enveloped).toString(CryptoES.enc.Base64)
    }
  }

  const decrypt = (data) =&gt; {
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
  //console.log(&#39;\nauthTag check:&#39;, tag == tagCheck)

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

  console.log(&#39;\n********** encypted **********&#39;)
  console.log(&#39;timestamp:&#39;, timestamp)
  console.log(&#39;nonce:&#39;, nonce)
  console.log(&#39;enveloped:&#39;, enveloped)

  const response = await fetch(url, {
    method: &#39;POST&#39;,
    body: enveloped,
    headers: {
      &#39;Authorization&#39;: `Bearer ${api_key}`
    }
  })

  if (response.status == 200) {
    const body = await response.text()
    console.log(&#39;\n********** response **********&#39;)
    console.log(body)
    const data = decrypt(body)
    console.log(&#39;\n********** decrypted **********&#39;)
    console.log(&#39;timeStamp:&#39;, data.timestamp)
    console.log(&#39;nonce:&#39;, data.nonce)
    console.log(&#39;response:&#39;, JSON.stringify(data.developed))
    console.log(&#39;\n&#39;)

 let event_data ={
      tealium_event: &#34;euid_event&#34;,
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
          .then(response =&gt; {
              if (!response.ok) {
                  throw new Error(`Network response was not ok. Status code: ${response.status}.`);
              }
              console.log(&#39;Status code:&#39;, response.status);
              return response.text();
          })
          .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
    } 
    else {
      console.error(&#34;Couldn&#39;t generate advertising ID&#34;)
      }
  } 
  else {
    console.log(&#39;\nxxxxx  failed  xxxxx\n&#39;)
    console.log(JSON.stringify(response))
    }
  })
```