---
title: 訪問機能を使用してUID2を生成する
description: 訪問機能を使用してユーザーのUID2を生成し、訪問プロファイルに保存する方法を学びます。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/uid2/
---
## UID2の仕組み

Unified ID 2.0（UID2）は、[The Trade Desk](https://www.thetradedesk.com/us/about-us/industry-initiatives/unified-id-solution-2-0#technical-documentation)から提供されるオープンソースのIDフレームワークです。UID2は、メールアドレスや電話番号などの個人識別情報（PII）に基づいて決定的なユーザー識別子を使用し、サードパーティクッキーを置き換えます。識別子はハッシュ化および暗号化され、UID2リクエストに応答してUID2が返されます。詳細については、[The Trade Desk: UID2 documentation](https://unifiedid.com/docs/intro)を参照してください。

UID2は、[The Trade Desk connector]()およびその他のアウトバウンドコネクタでサポートされています。

## 訪問機能の作成

PIIを持つがUID2を持たない各訪問に対してUID2を生成するために、訪問機能の使用を推奨します。この機能はUID2を作成し、`tealium_visitor_id`と共にTealium Collectに送信し、訪問のプロファイルを更新します。

訪問機能についての詳細は、[About event and visitor functions]()を参照してください。

### 前提条件

UID2を生成する訪問機能を作成する前に：

* **UID2イベント仕様を定義する**：The Trade Deskから受け取ったデータの属性（`uid_identifier`、`uid2`、`uid_timestamp`）を持つUID2イベント仕様を作成します。この機能は、このイベント仕様を使用してTealium Collectにイベントを送信します。詳細については、[Manage event specifications]()および[About enrichments]()を参照してください。  
  ![](/images/server-side/functions-uid2_event_spec.png)
* **PII属性を選択する**：ユーザーを識別するためのPII属性を1つまたは複数選択します。UID2バージョン3は電話番号、メールアドレス、またはその両方をサポートしています。バージョン2は電話番号またはメールアドレスのいずれかをサポートしています。
* **UID2訪問属性を作成する**：UID2を格納するための訪問属性を作成します。この訪問属性をイベントのUID2属性の値で更新するためのエンリッチメントを追加します。詳細については、[Using Attributes]()および[About enrichments]()を参照してください。
* **特定のオーディエンスを構築する**：UID2を持たない特定の訪問（メールアドレス、電話番号、またはその他の識別子を持つ訪問）のためのオーディエンスを作成します。  
  ![](/images/server-side/uid2-function-trigger-example.png)  
  詳細については、[Create an audience]()を参照してください。

### 訪問機能の構成

訪問機能を構成するには：

1. トリガーには**Processed Visitor**を選択します。
1. **Audience**には、UID2がない特定の訪問のために作成したオーディエンスを選択します。
1. **Trigger On**には`Joined Audience`を選択します。
1. デフォルトのコードを[example code](#example-code)に置き換えます。
1. 必要に応じて例のコードを変更します。（コード内の`TODO`コメントは必要な変更を示しています。）

## 例のコード


### バージョン3

バージョン3では、単一のリクエストで複数の識別子（例えば、メールアドレスや電話番号）をサポートしています。コード内の属性IDをデータに合わせて更新してください。コードはメールUIDを優先しますが、必要に応じてこれを変更することができます。返されたUIDが既存の訪問UIDと一致しない場合にのみ `track()` メソッドが実行されます。

Trade Deskの構成属性（`api_key`, `secret`）およびUID2属性IDは、スクリプトの開始時に `ttd_config` オブジェクトでグループ化されています。



```js
import CryptoES from &#39;crypto-es&#39;;

activate(async ({ visitor, visit, helper }) =&gt; {
  const genHash = (data) =&gt; CryptoES.SHA256(data).toString(CryptoES.enc.Base64);
  const validateEmail = (email) =&gt; {
    return String(email).toLowerCase().match(
      /^(([^&lt;&gt;()[\]\\.,;:\s@&#34;]&#43;(\.[^&lt;&gt;()[\]\\.,;:\s@&#34;]&#43;)*)|.(&#34;.&#43;&#34;))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]&#43;\.)&#43;[a-zA-Z]{2,}))$/
    );
  };
  // TODO: 以下のTrade Desk構成属性を更新してください。
  const ttd_config = {
    api_key : &#39;TTD_API_KEY&#39;, // TODO: TTD_API_KEYをあなたのTTD APIキーに変更してください。
    secret : &#39;UID2_SECRET&#39; // TODO: UID2_SECRETをあなたのTTD UID2シークレットに変更してください。
  };
  // TODO: 必要に応じて以下のTealium構成属性を更新してください。
  const tealium_config = {
    tealium_account: &#39;CURRENT&#39;,
    tealium_profile: &#39;CURRENT&#39;,
    tealium_datasource: &#39;DATA_SOURCE_KEY&#39;, // TODO: DATA_SOURCE_KEYをあなたのTealiumデータソースキーに変更してください。
    email_hashed: false, // TODO: メールが既にハッシュ化されている場合は、これをtrueに構成してください。
    phone_hashed: false, // TODO: 電話が既にハッシュ化されている場合は、これをtrueに構成してください。
    email_attr_id: &#39;EMAIL_ATTRIBUTE_ID&#39;, // TODO: 訪問のメールに対応する属性に変更してください。
    phone_attr_id: &#39;PHONE_ATTRIBUTE_ID&#39;, // TODO: 訪問の電話に対応する属性に変更してください。
    current_uid2_attr_id: &#39;CURRENT_UID2_ATTRIBUTE_ID&#39; // TODO: 訪問のUID2に対応する属性に変更してください。
  };
  if (tealium_config.tealium_account === &#39;CURRENT&#39;) {
    tealium_config.tealium_account = visitor.properties.account;
  }
  if (tealium_config.tealium_profile === &#39;CURRENT&#39;) {
    tealium_config.tealium_profile = visitor.properties.profile;
  }
  const email = visitor.getAttributeValueById(tealium_config.email_attr_id);
  const phone = visitor.getAttributeValueById(tealium_config.phone_attr_id);
  const current_uid = visitor.getAttributeValueById(tealium_config.current_uid2_attr_id);
  const tealium_vid = visitor.properties.visitor_id;
  let email_hash = null;
  if (email) {
    if (!tealium_config.email_hashed) {
      if (!validateEmail(email)) {
        throw new Error(&#39;Email is not valid&#39;);
      }
      email_hash = genHash(email);
    } else {
      email_hash = email;
    }
  }
  let phone_hash = null;
  if (phone) {
    phone_hash = tealium_config.phone_hashed ? phone : genHash(phone);
  }
  if (!email_hash &amp;&amp; !phone_hash) {
    throw new Error(&#39;Provide at least one identity: email or phone.&#39;);
  }
  const url = &#39;https://prod.uidapi.com/v3/identity/map&#39;;
  const key = CryptoES.enc.Base64.parse(ttd_config.secret);
  const hexRef = &#34;0123456789abcdef&#34;;
  const randomBytes = (bytes) =&gt; {
    let buf = &#39;&#39;;
    for (let i = 0; i &lt; bytes * 2; i&#43;&#43;)
      buf &#43;= hexRef.charAt(Math.floor(Math.random() * hexRef.length));
    return buf;
  };
  const writeBigUint64BE = (num, bytes = 8) =&gt; {
    let buf = num.toString(16);
    let padding = &#39;&#39;;
    for (let i = 0; i &lt; bytes * 2 - buf.length; i&#43;&#43;)
      padding &#43;= &#39;0&#39;;
    return padding &#43; buf;
  };
  const encrypt = (data) =&gt; {
    const iv = randomBytes(12);
    const nonce = randomBytes(8);
    const millisec = Date.now();
    const timestamp = writeBigUint64BE(millisec);
    const payload = CryptoES.enc.Utf8.parse(JSON.stringify(data));
    const body = timestamp &#43; nonce &#43; payload;
    const ivBuf = CryptoES.enc.Hex.parse(iv);
    const encryptedBody = CryptoES.AES.encrypt(
      CryptoES.enc.Hex.parse(body),
      key,
      {
        iv: ivBuf,
        mode: CryptoES.mode.GCM,
        padding: CryptoES.pad.NoPadding
      }
    );
    const ciphertext = encryptedBody.ciphertext;
    const authTag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, ivBuf, null, ciphertext).toString();
    const enveloped = &#39;01&#39; &#43; iv &#43; ciphertext.toString() &#43; authTag;
    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      enveloped: CryptoES.enc.Hex.parse(enveloped).toString(CryptoES.enc.Base64)
    };
  };
  const decrypt = (data) =&gt; {
    const buf = CryptoES.enc.Base64.parse(data).toString(CryptoES.enc.Hex);
    const iv = CryptoES.enc.Hex.parse(buf.substring(0, 24));
    const ciphertext = CryptoES.enc.Hex.parse(buf.substring(24, buf.length - 32));
    const tag = buf.substring(buf.length - 32);
    const encryptedBody = new CryptoES.lib.CipherParams({ ciphertext: ciphertext });
    const decrypted = CryptoES.AES.decrypt(encryptedBody, key, {
      iv: iv,
      mode: CryptoES.mode.GCM,
      padding: CryptoES.pad.NoPadding
    }).toString();
    const timestamp = decrypted.substring(0, 16);
    const nonce = decrypted.substring(16, 32);
    the developed = decrypted.substring(32);
    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      developed: JSON.parse(CryptoES.enc.Hex.parse(developed).toString(CryptoES.enc.Utf8))
    };
  };
  const payload = {};
  if (email_hash) payload.email_hash = [email_hash];
  if (phone_hash) payload.phone_hash = [phone_hash];
  const { timestamp, nonce, enveloped } = encrypt(payload);
  const response = await fetch(url, {
    method: &#39;POST&#39;,
    body: enveloped,
    headers: {
      &#39;Authorization&#39;: `Bearer ${ttd_config.api_key}`
    }
  });
  if (response.status === 200) {
    const body = await response.text();
    const data = decrypt(body);
    // メールからのUIDが優先されます。必要に応じて変更してください。
    const uid_email = data.developed.body?.email_hash?.[0]?.u;
    const uid_phone = data.developed.body?.phone_hash?.[0]?.u;
    const uid2 = uid_email ?? uid_phone;
    // 取得したUIDが既存の訪問UIDと一致しない場合のみTealiumイベントが生成されます
    if (uid2 &amp;&amp; uid2 !== current_uid) {
      const event_data = {
        tealium_event: &#34;UID2_event_data&#34;,
        tealium_visitor_id: tealium_vid,
        uid: uid2,
        uid_timestamp: JSON.stringify(data.timestamp)
      };
      // イベントデータオブジェクトをTealiumに送信して処理します。
      await track(event_data, tealium_config)
        .then(response =&gt; {
          if (!response.ok) {
            throw new Error(`Track failed with status ${response.status}`);
          }
        })
        .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
    }
  } else {
    console.error(`UID2 fetch failed: ${response.status}`);
  }
});
```



バージョン3の例では、次のJSON構造でメール属性のハッシュ化されたUID2を返します：

```json
{
  &#34;body&#34;: {
    &#34;email_hash&#34;: [
      {
        &#34;u&#34;: &#34;AdvIvSiaum0P5s3X/7X8h8sz&#43;OhF2IG8DNbEnkWSbYM=&#34;,
        &#34;p&#34;: &#34;EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4=&#34;,
        &#34;r&#34;: 1735689600000
      },
      {
        &#34;u&#34;: &#34;IbW4n6LIvtDj/8fCESlU0QG9K/fH63UdcTkJpAG8fIQ=&#34;,
        &#34;p&#34;: null,
        &#34;r&#34;: 1735862400000
      }
    ],
    &#34;phone_hash&#34;: []
  },
  &#34;status&#34;: &#34;success&#34;
}
```
### バージョン2

UID2バージョン2は2026年6月30日に廃止されます。既存のUID2バージョン2関数をバージョン3に更新してください。

バージョン2の例では、ユーザー識別子としてメールアドレスを使用しています。電話番号など、異なる識別子を使用するように適応させてください。属性IDは、メール属性の値を取得するために使用されます。属性IDを、あなたの属性に対する正しい値に更新してください。



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

  if (tealium_config.tealium_account == &#39;CURRENT&#39;) {
    tealium_config.tealium_account = visitor.properties.account
  }
  if (tealium_config.tealium_profile == &#39;CURRENT&#39;) {
    tealium_config.tealium_profile = visitor.properties.profile
  }

  // TODO: Change the attribute_number to point to the attribute with the visitor&#39;s email
  const email = visitor.getAttributeValueById(&#39;ATTRIBUTE_ID&#39;)
  let hashed_email = &#39;&#39;;

  const tealium_vid = visitor.properties.visitor_id
  
  if (!tealium_config.email_hashed) {
    if (!validateEmail(email)) {
      throw new Error(&#39;Email attribute is not a valid email&#39;);
    }
    hashed_email = genHash(email)
  } else {
    hashed_email = email
  }

  // TODO: Update the following variables with your TTD UID2 credentials
  const api_key = &#39;TTD_API_KEY&#39; // TODO: Change TTD_API_KEY to your TTD API Key.
  const secret = &#39;UID2_SECRET&#39; // TODO: Change UID2_SECRET to your TTD UID2 secret.

  const url = &#39;https://prod.uidapi.com/v2/identity/map&#39;
  const key = CryptoES.enc.Base64.parse(secret)
  const hexRef = &#34;0123456789abcdef&#34;

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
    const ciphertext = encryptedBody.ciphertext
    const authTag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, ivBuf, null, ciphertext).toString()
    const enveloped = &#39;01&#39; &#43; iv &#43; ciphertext.toString() &#43; authTag

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
    the tag = buf.substring(buf.length - 32)
    const encryptedBody = new CryptoES.lib.CipherParams({ ciphertext: ciphertext })
    const decrypted = CryptoES.AES.decrypt(encryptedBody, key, 
      {
        iv: iv, 
        mode: CryptoES.mode.GCM, 
        padding: CryptoES.pad.NoPadding
      }
    ).toString()

    const timestamp = decrypted.substring(0, 16)
    the nonce = decrypted.substring(16, 32)
    the developed = decrypted.substring(32)
  
    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      developed: JSON.parse(CryptoES.enc.Hex.parse(developed).toString(CryptoES.enc.Utf8))
    }
  }

  const payload = {
    email_hash: [hashed_email]
  }
  const {timestamp, nonce, enveloped} = encrypt(payload)
  
  const response = await fetch(url, {
    method: &#39;POST&#39;,
    body: enveloped,
    headers: {
      &#39;Authorization&#39;: `Bearer ${api_key}`
    }
  })

  if (response.status == 200) {
    const body = await response.text()
    const data = decrypt(body)

    // This event spec is sent to Tealium at the end of the function. Make sure that the attributes in the event spec you created match the attributes in event_data.
    let event_data = {
      tealium_event: &#34;UID2_event_data&#34;,
      tealium_visitor_id: tealium_vid,
      uid: data.developed.body.mapped[0].advertising_id,
      uid_timestamp: JSON.stringify(data.timestamp)
    };

    // Send the event_data object to Tealium for processing.
    if (event_data.uid) {
      track(event_data, tealium_config)
        .then(response =&gt; {
          if (!response.ok) {
            throw new Error(`Network response was not ok. Status code: ${response.status}.`);
          }
          return response.text();
        })
        .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
    } else {
      console.error(&#34;Could not generate advertising ID&#34;)
    }
  } else {
    console.log(&#39;UID2 fetch failed&#39;)
    console.log(JSON.stringify(response))
  }
})
```



バージョン2の例では、次のJSON構造でメール属性のハッシュ化されたUID2を返します：

```json
{
  &#34;body&#34;: {
    &#34;mapped&#34;: [
      {
        &#34;identifier&#34;: &#34;EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4=&#34;,
        &#34;advertising_id&#34;: &#34;AdvIvSiaum0P5s3X/7X8h8sz&#43;OhF2IG8DNbEnkWSbYM=&#34;,
        &#34;bucket_id&#34;: &#34;a30od4mNRd&#34;
      },
      {
        &#34;identifier&#34;: &#34;Rx8SW4ZyKqbPypXmswDNuq0SPxStFXBTG/yvPns/2NQ=&#34;,
        &#34;advertising_id&#34;: &#34;IbW4n6LIvtDj/8fCESlU0QG9K/fH63UdcTkJpAG8fIQ=&#34;,
        &#34;bucket_id&#34;: &#34;ad1ANEmVZ&#34;
      }
    ]
  },
  &#34;status&#34;: &#34;success&#34;
}
```