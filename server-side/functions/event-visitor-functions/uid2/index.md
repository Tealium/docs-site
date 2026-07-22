---
title: Generate a UID2 with a visitor function
description: Learn how to use a visitor function to generate a UID2 for a user and save it in the visitor profile.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/uid2/
---
## How UID2 works

Unified ID 2.0 (UID2) is an open source ID framework from [The Trade Desk](https://www.thetradedesk.com/us/about-us/industry-initiatives/unified-id-solution-2-0#technical-documentation). UID2 replaces third-party cookies with a deterministic user identifier based on personally identifiable information (PII), such as an email address or phone number. The identifier is hashed and encrypted to create a UID2, which is returned in response to a UID2 request. For more information, see [The Trade Desk: UID2 documentation](https://unifiedid.com/docs/intro).

A UID2 is supported in [The Trade Desk connector](https://docs.tealium.com/the-trade-desk-first-party-data-connector/) and other outbound connectors.

## Create a visitor function

We recommend that you use a visitor function to generate a UID2 for each visitor who has PII but no UID2. The function creates the UID2, sends it with the `tealium_visitor_id` to Tealium Collect, and updates the visitor’s profile. 

For details about visitor functions, see [About event and visitor functions]().

### Prerequisites

Before you create a visitor function to generate a UID2:

* **Define UID2 event spec**: Create a UID2 event spec with attributes for the data received from The Trade Desk (`uid_identifier`, `uid2`, `uid_timestamp`). The function uses this event spec to send an event to Tealium Collect. For more information, see [Manage event specifications]() and [About enrichments]().  
  ![](https://docs.tealium.com/images/server-side/functions-uid2_event_spec.png)
* **Select PII attributes**: Choose a PII attribute or attributes to identify users. UID2 version 3 supports a phone number, an email address, or both. Version 2 supports either a phone number or an email address.
* **Create UID2 visitor attribute**: Create a visitor attribute to store the UID2. Add an enrichment to update this visitor attribute with the value of the event UID2 attribute. For more information, see [Using Attributes]() and [About enrichments]().
* **Build identified audience**: Create an audience for identified visitors (those with an email address, phone number, or other identifier) who do not have a UID2.  
  ![](https://docs.tealium.com/images/server-side/uid2-function-trigger-example.png)  
  For more information, see [Create an audience](https://docs.tealium.com/manage-audiences/#create-an-audience).

### Configure the visitor function

To configure the visitor function:

1. For the trigger, select **Processed Visitor**.
1. For **Audience**, select the audience created for identified visitors without a UID2.
1. For **Trigger On**, select `Joined Audience`.
1. Replace the default code with the [example code](#example-code).
1. Modify the example code as needed. (`TODO` comments in the code mark required changes.)

## Example code

### Version 3

Version 3 supports multiple identifiers, such as email addresses and phone numbers, in a single request. Update the attribute IDs in the code to match your data. The code prioritizes the email UID, but you can change this as needed. The `track()` method runs only if the returned UID does not match the existing visitor UID.

The Trade Desk configuration attributes (`api_key`, `secret`) and the UID2 attribute ID are grouped in the `ttd_config` object at the start of the script.



```js
import CryptoES from 'crypto-es';

activate(async ({ visitor, visit, helper }) => {
  const genHash = (data) => CryptoES.SHA256(data).toString(CryptoES.enc.Base64);
  const validateEmail = (email) => {
    return String(email).toLowerCase().match(
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    );
  };
  // TODO: Update the following Trade Desk configuration attributes.
  const ttd_config = {
    api_key : 'TTD_API_KEY', // TODO: Change TTD_API_KEY to your TTD API Key.
    secret : 'UID2_SECRET' // TODO: Change UID2_SECRET to your TTD UID2 secret.
  };
  // TODO: Update the following Tealium configuration attributes as needed.
  const tealium_config = {
    tealium_account: 'CURRENT',
    tealium_profile: 'CURRENT',
    tealium_datasource: 'DATA_SOURCE_KEY', // TODO: Change DATA_SOURCE_KEY to your Tealium Data Source key.
    email_hashed: false, // TODO: If your email is already hashed, set this to true.
    phone_hashed: false, // TODO: If your phone is already hashed, set this to true.
    email_attr_id: 'EMAIL_ATTRIBUTE_ID', // TODO: Change to the attribute with the visitor's email.
    phone_attr_id: 'PHONE_ATTRIBUTE_ID', // TODO: Change to the attribute with the visitor's phone.
    current_uid2_attr_id: 'CURRENT_UID2_ATTRIBUTE_ID' // TODO: Change to the attribute with the visitor's UID2.
  };
  if (tealium_config.tealium_account === 'CURRENT') {
    tealium_config.tealium_account = visitor.properties.account;
  }
  if (tealium_config.tealium_profile === 'CURRENT') {
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
        throw new Error('Email is not valid');
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
  if (!email_hash && !phone_hash) {
    throw new Error('Provide at least one identity: email or phone.');
  }
  const url = 'https://prod.uidapi.com/v3/identity/map';
  const key = CryptoES.enc.Base64.parse(ttd_config.secret);
  const hexRef = "0123456789abcdef";
  const randomBytes = (bytes) => {
    let buf = '';
    for (let i = 0; i < bytes * 2; i++)
      buf += hexRef.charAt(Math.floor(Math.random() * hexRef.length));
    return buf;
  };
  const writeBigUint64BE = (num, bytes = 8) => {
    let buf = num.toString(16);
    let padding = '';
    for (let i = 0; i < bytes * 2 - buf.length; i++)
      padding += '0';
    return padding + buf;
  };
  const encrypt = (data) => {
    const iv = randomBytes(12);
    const nonce = randomBytes(8);
    const millisec = Date.now();
    const timestamp = writeBigUint64BE(millisec);
    const payload = CryptoES.enc.Utf8.parse(JSON.stringify(data));
    const body = timestamp + nonce + payload;
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
    const enveloped = '01' + iv + ciphertext.toString() + authTag;
    return {
      timestamp: parseInt(timestamp, 16),
      nonce: parseInt(nonce, 16),
      enveloped: CryptoES.enc.Hex.parse(enveloped).toString(CryptoES.enc.Base64)
    };
  };
  const decrypt = (data) => {
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
    const developed = decrypted.substring(32);
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
    method: 'POST',
    body: enveloped,
    headers: {
      'Authorization': `Bearer ${ttd_config.api_key}`
    }
  });
  if (response.status === 200) {
    const body = await response.text();
    const data = decrypt(body);
    // UID from email takes precedence. Modify as needed.
    const uid_email = data.developed.body?.email_hash?.[0]?.u;
    const uid_phone = data.developed.body?.phone_hash?.[0]?.u;
    const uid2 = uid_email ?? uid_phone;
    // Tealium event is generated only if retrieved UID does not match existing visitor UID
    if (uid2 && uid2 !== current_uid) {
      const event_data = {
        tealium_event: "UID2_event_data",
        tealium_visitor_id: tealium_vid,
        uid: uid2,
        uid_timestamp: JSON.stringify(data.timestamp)
      };
      // Send the event_data object to Tealium for processing.
      await track(event_data, tealium_config)
        .then(response => {
          if (!response.ok) {
            throw new Error(`Track failed with status ${response.status}`);
          }
        })
        .catch(error => console.error('Error:', error.message));
    }
  } else {
    console.error(`UID2 fetch failed: ${response.status}`);
  }
});
```



The version three example returns a hashed UID2 for the email attribute in the following JSON structure:

```json
{
  "body": {
    "email_hash": [
      {
        "u": "AdvIvSiaum0P5s3X/7X8h8sz+OhF2IG8DNbEnkWSbYM=",
        "p": "EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4=",
        "r": 1735689600000
      },
      {
        "u": "IbW4n6LIvtDj/8fCESlU0QG9K/fH63UdcTkJpAG8fIQ=",
        "p": null,
        "r": 1735862400000
      }
    ],
    "phone_hash": []
  },
  "status": "success"
}
```

### Version 2


<blockquote>
UID2 version 2 is deprecated on June 30, 2026. Update any existing UID2 version 2 functions to version 3.
</blockquote>


The version 2 example uses email addresses as the user identifier. Adapt it to use a different identifier, such as a phone number. An attribute ID is used to get the value of the email attribute. Update the attribute ID with the correct value for your attribute.



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

  if (tealium_config.tealium_account == 'CURRENT') {
    tealium_config.tealium_account = visitor.properties.account
  }
  if (tealium_config.tealium_profile == 'CURRENT') {
    tealium_config.tealium_profile = visitor.properties.profile
  }

  // TODO: Change the attribute_number to point to the attribute with the visitor's email
  const email = visitor.getAttributeValueById('ATTRIBUTE_ID')
  let hashed_email = '';

  const tealium_vid = visitor.properties.visitor_id
  
  if (!tealium_config.email_hashed) {
    if (!validateEmail(email)) {
      throw new Error('Email attribute is not a valid email');
    }
    hashed_email = genHash(email)
  } else {
    hashed_email = email
  }

  // TODO: Update the following variables with your TTD UID2 credentials
  const api_key = 'TTD_API_KEY' // TODO: Change TTD_API_KEY to your TTD API Key.
  const secret = 'UID2_SECRET' // TODO: Change UID2_SECRET to your TTD UID2 secret.

  const url = 'https://prod.uidapi.com/v2/identity/map'
  const key = CryptoES.enc.Base64.parse(secret)
  const hexRef = "0123456789abcdef"

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
    const ciphertext = encryptedBody.ciphertext
    const authTag = CryptoES.mode.GCM.mac(CryptoES.algo.AES, key, ivBuf, null, ciphertext).toString()
    const enveloped = '01' + iv + ciphertext.toString() + authTag

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
    const decrypted = CryptoES.AES.decrypt(encryptedBody, key, 
      {
        iv: iv, 
        mode: CryptoES.mode.GCM, 
        padding: CryptoES.pad.NoPadding
      }
    ).toString()

    const timestamp = decrypted.substring(0, 16)
    const nonce = decrypted.substring(16, 32)
    const developed = decrypted.substring(32)
  
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
    method: 'POST',
    body: enveloped,
    headers: {
      'Authorization': `Bearer ${api_key}`
    }
  })

  if (response.status == 200) {
    const body = await response.text()
    const data = decrypt(body)

    // This event spec is sent to Tealium at the end of the function. Make sure that the attributes in the event spec you created match the attributes in event_data.
    let event_data = {
      tealium_event: "UID2_event_data",
      tealium_visitor_id: tealium_vid,
      uid: data.developed.body.mapped[0].advertising_id,
      uid_timestamp: JSON.stringify(data.timestamp)
    };

    // Send the event_data object to Tealium for processing.
    if (event_data.uid) {
      track(event_data, tealium_config)
        .then(response => {
          if (!response.ok) {
            throw new Error(`Network response was not ok. Status code: ${response.status}.`);
          }
          return response.text();
        })
        .catch(error => console.error('Error:', error.message));
    } else {
      console.error("Could not generate advertising ID")
    }
  } else {
    console.log('UID2 fetch failed')
    console.log(JSON.stringify(response))
  }
})
```



The version two example returns a hashed UID2 for the email attribute in the following JSON structure:


```json
{
  "body": {
    "mapped": [
      {
        "identifier": "EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4=",
        "advertising_id": "AdvIvSiaum0P5s3X/7X8h8sz+OhF2IG8DNbEnkWSbYM=",
        "bucket_id": "a30od4mNRd"
      },
      {
        "identifier": "Rx8SW4ZyKqbPypXmswDNuq0SPxStFXBTG/yvPns/2NQ=",
        "advertising_id": "IbW4n6LIvtDj/8fCESlU0QG9K/fH63UdcTkJpAG8fIQ=",
        "bucket_id": "ad1ANEmVZ"
      }
    ]
  },
  "status": "success"
}
```
