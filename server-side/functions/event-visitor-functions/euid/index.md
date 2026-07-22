---
title: Use a function to generate an EUID
description: This article describes how to use a visitor function to generate an EUID for a user and save it in the visitor profile.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/euid/
---
European Unified ID (EUID) is an open source ID framework created by [The Trade Desk](https://euid.eu/docs/intro), which can be used instead of a third-party cookie. EUID is a deterministic user identifier based on a user's Personally Identifiable Information (PII). EUID currently uses only the user's email address as an identifier and is limited to European regions. The identifier is hashed and encrypted to create an EUID that is returned in the response to an EUID request. For more information, see the [European Unified ID Overview](https://euid.eu/docs/intro).

An EUID can be used in [The Trade Desk connector](https://docs.tealium.com/the-trade-desk-first-party-data-connector/) and other supported outbound connectors.

## Generate EUID for a visitor profile

We recommend using a visitor function to generate the EUID. Trigger the function when the visitor has PII but does not have an EUID assigned. For more information about visitor functions, see [About event and visitor functions]().

The visitor function does the following:

* Capture the visitor’s email address and hash it.
* Uses the [EUID endpoint](https://euid.eu/docs/endpoints/post-identity-map) to generate an EUID if the visitor does not have one assigned.
* Sends an event containing the EUID and `tealium_visitor_id` to Tealium Collect.

The visitor attribute is enriched by the event sent from the function.

### Prerequisites

Before you create a visitor function to generate an EUID, do the following:

* Choose a PII visitor attribute to use as an identifier for your users. EUID currently supports an email address identifier.
* Create a visitor attribute to store the EUID. Add an enrichment to enrich this visitor attribute with the value of the event EUID attribute. For more information, see [Using Attributes]() and [About enrichments]().
* Create an audience to identify visitors that have an email address assigned but do not have an EUID assigned. For example:  
![](https://docs.tealium.com/images/server-side/euid-function-trigger-example.png)  
For more information, see [Create an audience](https://docs.tealium.com/manage-audiences/#create-an-audience).

## EUID generator function

When you create your function, do the following:

1. For the trigger, select **Processed Visitor**.
1. For **Audience**, select the audience you created for identified visitors that do not have an EUID assigned. Leave **Trigger On** set to the default value, which is `Joined Audience`.  
Delete the default code for a processed visitor function, then copy and paste the example code to generate an EUID shown in [Example code](#example-code). Modify the example code as needed.

### Example code 


<blockquote>
This example code is only a guide for setting up a function to assign an EUID to visitors and **cannot be used without modification**. Look for comments in the code with `TODO` for the lines that must be modified for your configuration.
</blockquote>


This example uses an email address as the user identifier, but can be adapted to use other user identifiers. An attribute ID is used to get the value of the email attribute. Update the attribute ID with the correct value for the attribute you're using and place your EUID credentials in the appropriate locations (`api_key` and `secret`).

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
    const decrypted = CryptoES.AES.decrypt(encryptedBody,key, 
      {
        iv: iv, 
        mode: CryptoES.mode.GCM, 
        padding: CryptoES.pad.NoPadding
      }
    ).toString()

    const timestamp = decrypted.substring(0, 16)
    const nonce = decrypted.substring(16, 32)
    const developed = decrypted.substring(32)
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